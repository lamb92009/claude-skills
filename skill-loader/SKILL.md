---
name: skill-loader
description: Reads the remote skill catalog from GitHub, analyzes project context, recommends relevant skills, and fetches them for the session.
---

# Skill Loader

Load only the skills you need for this session from the central skill repository at `lamb92009/claude-skills`.

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

## Step 3 — Generate recommendations

Based on the catalog descriptions and project signals, select skills that are **directly relevant** to this project and session. For each recommendation, give one sentence of reasoning tied to a specific signal. **Skip any permanent residents listed above — they are always available without fetching.**

**Aim for 3–8 skills.** Be selective — do not recommend everything. Skills you don't recommend are still available if asked.

## Step 4 — Present and confirm

Present in this format:

```
Based on [key signals observed], I recommend fetching these skills:

✓ `skill-name` — reason tied to specific signal
✓ `skill-name` — reason tied to specific signal
...

Also available but not recommended for this project: skill-a, skill-b, skill-c

Confirm this list, adjust it, or add skill names?
```

**Wait for the user to respond before fetching anything.**

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
