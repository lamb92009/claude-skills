---
name: skill-loader
description: Reads the remote skill catalog from GitHub, analyzes project context, recommends relevant skills, and fetches them for the session.
---

# Skill Loader

Load only the skills you need for this session from the central skill repository at `lamb92009/claude-skills`.

## Flags & Modifiers

Before starting, check whether the user invoked skill-loader with any modifiers or constraints:

### `--quick` mode
If the user said `skill-loader --quick`, "quick mode", "skip confirmation", or "just fetch":
- Run Steps 1–3 normally
- **Skip Step 4 confirmation** — proceed directly to Step 5 (fetch) with the auto-generated list
- Still display the token budget and skill list so the user can see what was loaded

### Category filter
If the user specified a category (e.g., "infrastructure skills only", "only web frameworks", "data & ml skills"):
- In Step 3, **only consider skills from the requested category**
- Note the active filter when presenting recommendations

Available categories (match loosely):
- **Language Experts** — javascript-pro, typescript-pro, python-pro, golang-pro, rust-engineer, java-architect, kotlin-specialist, csharp-developer, cpp-pro, php-pro, swift-expert
- **Web Frameworks** — react-expert, react-native-expert, nextjs-developer, vue-expert, vue-expert-js, angular-architect, nestjs-expert, django-expert, fastapi-expert, rails-expert, laravel-specialist, spring-boot-engineer, dotnet-core-expert, wordpress-pro, shopify-expert
- **Data & ML** — sql-pro, postgres-pro, database-optimizer, pandas-pro, ml-pipeline, fine-tuning-expert, rag-architect, spark-engineer
- **Infrastructure & DevOps** — devops-engineer, cloud-architect, kubernetes-specialist, terraform-engineer, monitoring-expert, sre-engineer
- **API & Integration** — api-designer, graphql-architect, websocket-engineer, mcp-developer, atlassian-mcp, salesforce-developer
- **Mobile** — flutter-expert
- **Specialized Domains** — cli-developer, embedded-systems, game-developer, security-reviewer, secure-code-guardian, chaos-engineer, playwright-expert, email-design, content-strategy, prompt-engineer
- **Process & Quality** — architecture-designer, code-reviewer, debugging-wizard, test-master, legacy-modernizer, spec-miner, microservices-architect, fullstack-guardian, feature-forge, code-documenter, the-fool, ui-ux-pro-max

## Step 1 — Fetch the catalog

Run this to get the README:

```bash
bash -c 'source ~/.bashrc && gh api repos/lamb92009/claude-skills/contents/README.md --jq ".content" | base64 -d'
```

Read and understand the full catalog of available skills and their descriptions.

## Step 2 — Collect project context signals

Check each of the following (skip silently if not present):

```bash
# What files exist in the working directory?
ls -la

# Package manager / language signals
cat package.json 2>/dev/null | head -30
cat requirements.txt 2>/dev/null | head -10
cat go.mod 2>/dev/null | head -5
cat Cargo.toml 2>/dev/null | head -5
cat composer.json 2>/dev/null | head -10

# Project instructions
cat CLAUDE.md 2>/dev/null
cat .claude/CLAUDE.md 2>/dev/null

# Infrastructure signals
cat Dockerfile 2>/dev/null | head -20
cat docker-compose.yaml 2>/dev/null | head -20
cat docker-compose.yml 2>/dev/null | head -20
```

Also note:
- What task or goal has the user stated for this session?
- What file extensions dominate the working directory?

## Permanent residents (always available — never fetch, never add to manifest)

These skills are installed locally at all times. Do not recommend fetching them (they're already present) and do not write them to `.session-skills`:

- `lamb-brand-reference`
- `debugging-wizard`
- `prompt-engineer`
- `devops-engineer`
- `skill-loader`
- `skill-cleanup`

## Step 3 — Generate recommendations and estimate token budget

Based on the catalog descriptions, project signals, and any active category filter, select skills that are **directly relevant** to this project and session. For each recommendation, give one sentence of reasoning tied to a specific signal. **Skip any permanent residents listed above.**

**Aim for 3–8 skills.** Be selective — do not recommend everything.

After selecting candidates, fetch file sizes from the GitHub tree to estimate their token cost:

```bash
bash -c 'source ~/.bashrc && gh api "repos/lamb92009/claude-skills/git/trees/main?recursive=1" --jq "[.tree[] | select(.path | endswith(\"/SKILL.md\")) | {skill: (.path | split(\"/\")[0]), bytes: .size}]"'
```

For each recommended skill, find its byte count in the output. Estimate tokens as `bytes ÷ 4`, rounded to the nearest 100. Sum them for the session total.

## Step 4 — Present and confirm

Present in this format:

```
[If category filter active]: Filtering to [Category Name] skills only.

Based on [key signals observed], I recommend fetching these skills:

✓ `skill-name` — reason tied to specific signal   (~800 tokens)
✓ `skill-name` — reason tied to specific signal   (~1,200 tokens)
✓ `skill-name` — reason tied to specific signal   (~600 tokens)

Session token budget: ~2,600 tokens

Also available but not recommended for this project: skill-a, skill-b, skill-c

Confirm this list, adjust it, or add skill names?
```

**In `--quick` mode:** Display the list and token budget, then proceed directly to Step 5 without waiting. Append a note: `(--quick mode: fetching immediately)`

**Otherwise:** Wait for the user to respond before fetching anything.

## Step 5 — Fetch approved skills

For each confirmed skill name, run:

```bash
# Fetch SKILL.md
bash -c 'source ~/.bashrc && \
  SKILL=<skill-name> && \
  mkdir -p ~/.claude/skills/$SKILL && \
  gh api "repos/lamb92009/claude-skills/contents/$SKILL/SKILL.md" --jq ".content" | base64 -d > ~/.claude/skills/$SKILL/SKILL.md && \
  echo "Fetched: $SKILL/SKILL.md"'
```

Then fetch any reference files for that skill:

```bash
bash -c 'source ~/.bashrc && \
  SKILL=<skill-name> && \
  REFS=$(gh api "repos/lamb92009/claude-skills/git/trees/main?recursive=1" --jq ".tree[] | select(.path | startswith(\"$SKILL/references/\")) | .path") && \
  if [ -n "$REFS" ]; then
    mkdir -p ~/.claude/skills/$SKILL/references
    echo "$REFS" | while IFS= read -r path; do
      fname=$(basename "$path")
      gh api "repos/lamb92009/claude-skills/contents/$path" --jq ".content" | base64 -d > ~/.claude/skills/$SKILL/references/$fname
      echo "Fetched: $path"
    done
  fi'
```

Repeat for each skill in the confirmed list.

## Step 6 — Write the session manifest

```bash
cat > ~/.claude/skills/.session-skills << 'MANIFEST'
<skill1>
<skill2>
<skill3>
MANIFEST
```

Write one skill name per line, listing every skill that was fetched in this session.

## Step 7 — Confirm

Report which skills were fetched and are now active. Remind the user:

> When you're done with this session, invoke `skill-cleanup` to remove these skills and keep `~/.claude/skills/` lean.
