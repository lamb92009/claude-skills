# Claude Skills Repository

A catalog of 69 reusable Claude Code skills, managed via `skill-loader` for lean, per-session loading.

## How Skill Loading Works

Skills are not all loaded at once. Instead:

1. **At the start of a new project or unfamiliar task**, invoke `skill-loader`.
2. `skill-loader` reads this README to understand what's available, analyzes your project context (CLAUDE.md, package.json, Dockerfile, file types, task description), then suggests a relevant subset.
3. You confirm or adjust the list. Claude fetches only those skills from this repo into `~/.claude/skills/` and records them in `~/.claude/skills/.session-skills`.
4. **At the end of a session**, invoke `skill-cleanup` to remove session-fetched skills, keeping `~/.claude/skills/` lean.

`lamb-brand-reference` is a permanent local skill (private business data — not in this repo).

---

## Skills by Category

### Language Experts

| Skill | Description |
|-------|-------------|
| `javascript-pro` | Use when building JavaScript applications with modern ES2023+ features, async patterns, or Node.js development. Invoke for vanilla JavaScript, browser APIs, performance optimization, module systems. |
| `typescript-pro` | Use when building TypeScript applications requiring advanced type systems, generics, or full-stack type safety. Invoke for type guards, utility types, tRPC integration, monorepo setup. |
| `python-pro` | Use when building Python 3.11+ applications requiring type safety, async programming, or production-grade patterns. Invoke for type hints, pytest, async/await, dataclasses, mypy configuration. |
| `golang-pro` | Use when building Go applications requiring concurrent programming, microservices architecture, or high-performance systems. Invoke for goroutines, channels, Go generics, gRPC integration. |
| `rust-engineer` | Use when building Rust applications requiring memory safety, systems programming, or zero-cost abstractions. Invoke for ownership patterns, lifetimes, traits, async/await with tokio. |
| `java-architect` | Use when building enterprise Java applications with Spring Boot 3.x, microservices, or reactive programming. Invoke for WebFlux, JPA optimization, Spring Security, cloud-native patterns. |
| `kotlin-specialist` | Use when building Kotlin applications requiring coroutines, multiplatform development, or Android with Compose. Invoke for Flow API, KMP projects, Ktor servers, DSL design, sealed classes. |
| `csharp-developer` | Use when building C# applications with .NET 8+, ASP.NET Core APIs, or Blazor web apps. Invoke for Entity Framework Core, minimal APIs, async patterns, CQRS with MediatR. |
| `cpp-pro` | Use when building C++ applications requiring modern C++20/23 features, template metaprogramming, or high-performance systems. Invoke for concepts, ranges, coroutines, SIMD optimization, memory management. |
| `php-pro` | Use when building PHP applications with modern PHP 8.3+ features, Laravel, or Symfony frameworks. Invoke for strict typing, PHPStan level 9, async patterns with Swoole, PSR standards. |
| `swift-expert` | Use when building iOS/macOS applications with Swift 5.9+, SwiftUI, or async/await concurrency. Invoke for protocol-oriented programming, SwiftUI state management, actors, server-side Swift. |

### Web Frameworks

| Skill | Description |
|-------|-------------|
| `react-expert` | Use when building React 18+ applications requiring component architecture, hooks patterns, or state management. Invoke for Server Components, performance optimization, Suspense boundaries, React 19 features. |
| `react-native-expert` | Use when building cross-platform mobile applications with React Native or Expo. Invoke for navigation patterns, platform-specific code, native modules, FlatList optimization. |
| `nextjs-developer` | Use when building Next.js 14+ applications with App Router, server components, or server actions. Invoke for full-stack features, performance optimization, SEO implementation, production deployment. |
| `vue-expert` | Use when building Vue 3 applications with Composition API, Nuxt 3, or Quasar. Invoke for Pinia, TypeScript, PWA, Capacitor mobile apps, Vite configuration. |
| `vue-expert-js` | Use when building Vue 3 applications with JavaScript only (no TypeScript). Invoke for JSDoc typing, vanilla JS composables, .mjs modules. |
| `angular-architect` | Use when building Angular 17+ applications with standalone components or signals. Invoke for enterprise apps, RxJS patterns, NgRx state management, performance optimization, advanced routing. |
| `nestjs-expert` | Use when building NestJS applications requiring modular architecture, dependency injection, or TypeScript backend development. Invoke for modules, controllers, services, DTOs, guards, interceptors, TypeORM/Prisma. |
| `django-expert` | Use when building Django web applications or REST APIs with Django REST Framework. Invoke for Django models, ORM optimization, DRF serializers, viewsets, authentication with JWT. |
| `fastapi-expert` | Use when building high-performance async Python APIs with FastAPI and Pydantic V2. Invoke for async SQLAlchemy, JWT authentication, WebSockets, OpenAPI documentation. |
| `rails-expert` | Use when building Rails 7+ web applications with Hotwire, real-time features, or background job processing. Invoke for Active Record optimization, Turbo Frames/Streams, Action Cable, Sidekiq. |
| `laravel-specialist` | Use when building Laravel 10+ applications requiring Eloquent ORM, API resources, or queue systems. Invoke for Laravel models, Livewire components, Sanctum authentication, Horizon queues. |
| `spring-boot-engineer` | Use when building Spring Boot 3.x applications, microservices, or reactive Java applications. Invoke for Spring Data JPA, Spring Security 6, WebFlux, Spring Cloud integration. |
| `dotnet-core-expert` | Use when building .NET 8 applications with minimal APIs, clean architecture, or cloud-native microservices. Invoke for Entity Framework Core, CQRS with MediatR, JWT authentication, AOT compilation. |
| `wordpress-pro` | Use when developing WordPress themes, plugins, customizing Gutenberg blocks, implementing WooCommerce features, or optimizing WordPress performance and security. |
| `shopify-expert` | Use when building Shopify themes, apps, custom storefronts, or e-commerce solutions. Invoke for Liquid templating, Storefront API, app development, checkout customization, Shopify Plus features. |

### Data & ML

| Skill | Description |
|-------|-------------|
| `sql-pro` | Use when optimizing SQL queries, designing database schemas, or tuning database performance. Invoke for complex queries, window functions, CTEs, indexing strategies, query plan analysis. |
| `postgres-pro` | Use when optimizing PostgreSQL queries, configuring replication, or implementing advanced database features. Invoke for EXPLAIN analysis, JSONB operations, extension usage, VACUUM tuning, performance monitoring. |
| `database-optimizer` | Use when investigating slow queries, analyzing execution plans, or optimizing database performance. Invoke for index design, query rewrites, configuration tuning, partitioning strategies, lock contention resolution. |
| `pandas-pro` | Use when working with pandas DataFrames, data cleaning, aggregation, merging, or time series analysis. Invoke for data manipulation, missing value handling, groupby operations, or performance optimization. |
| `ml-pipeline` | Use when building ML pipelines, orchestrating training workflows, automating model lifecycle, implementing feature stores, or managing experiment tracking systems. |
| `fine-tuning-expert` | Use when fine-tuning LLMs, training custom models, or optimizing model performance for specific tasks. Invoke for parameter-efficient methods, dataset preparation, or model adaptation. |
| `rag-architect` | Use when building RAG systems, vector databases, or knowledge-grounded AI applications requiring semantic search, document retrieval, or context augmentation. |
| `spark-engineer` | Use when building Apache Spark applications, distributed data processing pipelines, or optimizing big data workloads. Invoke for DataFrame API, Spark SQL, RDD operations, performance tuning, streaming analytics. |

### Infrastructure & DevOps

| Skill | Description |
|-------|-------------|
| `devops-engineer` | Use when setting up CI/CD pipelines, containerizing applications, or managing infrastructure as code. Invoke for pipelines, Docker, Kubernetes, cloud platforms, GitOps. |
| `cloud-architect` | Use when designing cloud architectures, planning migrations, or optimizing multi-cloud deployments. Invoke for Well-Architected Framework, cost optimization, disaster recovery, landing zones, security architecture, serverless design. |
| `kubernetes-specialist` | Use when deploying or managing Kubernetes workloads requiring cluster configuration, security hardening, or troubleshooting. Invoke for Helm charts, RBAC policies, NetworkPolicies, storage configuration, performance optimization. |
| `terraform-engineer` | Use when implementing infrastructure as code with Terraform across AWS, Azure, or GCP. Invoke for module development, state management, provider configuration, multi-environment workflows, infrastructure testing. |
| `monitoring-expert` | Use when setting up monitoring systems, logging, metrics, tracing, or alerting. Invoke for dashboards, Prometheus/Grafana, load testing, profiling, capacity planning. |
| `sre-engineer` | Use when defining SLIs/SLOs, managing error budgets, or building reliable systems at scale. Invoke for incident management, chaos engineering, toil reduction, capacity planning. |

### API & Integration

| Skill | Description |
|-------|-------------|
| `api-designer` | Use when designing REST or GraphQL APIs, creating OpenAPI specifications, or planning API architecture. Invoke for resource modeling, versioning strategies, pagination patterns, error handling standards. |
| `graphql-architect` | Use when designing GraphQL schemas, implementing Apollo Federation, or building real-time subscriptions. Invoke for schema design, resolvers with DataLoader, query optimization, federation directives. |
| `websocket-engineer` | Use when building real-time communication systems with WebSockets or Socket.IO. Invoke for bidirectional messaging, horizontal scaling with Redis, presence tracking, room management. |
| `mcp-developer` | Use when building MCP servers or clients that connect AI systems with external tools and data sources. Invoke for MCP protocol compliance, TypeScript/Python SDKs, resource providers, tool functions. |
| `atlassian-mcp` | Use when querying Jira issues, searching Confluence pages, creating tickets, updating documentation, or integrating Atlassian tools via MCP protocol. |
| `salesforce-developer` | Use when developing Salesforce applications, Apex code, Lightning Web Components, SOQL queries, triggers, integrations, or CRM customizations. Invoke for governor limits, bulk processing, platform events, Salesforce DX. |

### Mobile

| Skill | Description |
|-------|-------------|
| `flutter-expert` | Use when building cross-platform applications with Flutter 3+ and Dart. Invoke for widget development, Riverpod/Bloc state management, GoRouter navigation, platform-specific implementations, performance optimization. |

### Specialized Domains

| Skill | Description |
|-------|-------------|
| `cli-developer` | Use when building CLI tools, implementing argument parsing, or adding interactive prompts. Invoke for CLI design, argument parsing, interactive prompts, progress indicators, shell completions. |
| `embedded-systems` | Use when developing firmware for microcontrollers, implementing RTOS applications, or optimizing power consumption. Invoke for STM32, ESP32, FreeRTOS, bare-metal, power optimization, real-time systems. |
| `game-developer` | Use when building game systems, implementing Unity/Unreal features, or optimizing game performance. Invoke for Unity, Unreal, game patterns, ECS, physics, networking, performance optimization. |
| `security-reviewer` | Use when conducting security audits, reviewing code for vulnerabilities, or analyzing infrastructure security. Invoke for SAST scans, penetration testing, DevSecOps practices, cloud security reviews. |
| `secure-code-guardian` | Use when implementing authentication/authorization, securing user input, or preventing OWASP Top 10 vulnerabilities. Invoke for authentication, authorization, input validation, encryption, OWASP Top 10 prevention. |
| `chaos-engineer` | Use when designing chaos experiments, implementing failure injection frameworks, or conducting game day exercises. Invoke for chaos experiments, resilience testing, blast radius control, game days, antifragile systems. |
| `playwright-expert` | Use when writing E2E tests with Playwright, setting up test infrastructure, or debugging flaky browser tests. Invoke for browser automation, E2E tests, Page Object Model, test flakiness, visual testing. |
| `email-design` | Email marketing design with layout patterns, subject line formulas, and deliverability rules. Covers welcome sequences, promotional emails, transactional templates, and mobile optimization. |
| `content-strategy` | When the user wants to plan a content strategy, decide what content to create, or figure out what topics to cover. Also use when the user mentions "content strategy," "what should I write about," "content ideas," "blog strategy," "topic clusters," or "content planning." |
| `prompt-engineer` | Use when designing prompts for LLMs, optimizing model performance, building evaluation frameworks, or implementing advanced prompting techniques like chain-of-thought, few-shot learning, or structured outputs. |

### Process & Quality

| Skill | Description |
|-------|-------------|
| `architecture-designer` | Use when designing new system architecture, reviewing existing designs, or making architectural decisions. Invoke for system design, architecture review, design patterns, ADRs, scalability planning. |
| `code-reviewer` | Use when reviewing pull requests, conducting code quality audits, or identifying security vulnerabilities. Invoke for PR reviews, code quality checks, refactoring suggestions. |
| `debugging-wizard` | Use when investigating errors, analyzing stack traces, or finding root causes of unexpected behavior. Invoke for error investigation, troubleshooting, log analysis, root cause analysis. |
| `test-master` | Use when writing tests, creating test strategies, or building automation frameworks. Invoke for unit tests, integration tests, E2E, coverage analysis, performance testing, security testing. |
| `legacy-modernizer` | Use when modernizing legacy systems, implementing incremental migration strategies, or reducing technical debt. Invoke for strangler fig pattern, monolith decomposition, framework upgrades. |
| `spec-miner` | Use when understanding legacy or undocumented systems, creating documentation for existing code, or extracting specifications from implementations. Invoke for legacy analysis, code archaeology, undocumented features. |
| `microservices-architect` | Use when designing distributed systems, decomposing monoliths, or implementing microservices patterns. Invoke for service boundaries, DDD, saga patterns, event sourcing, service mesh, distributed tracing. |
| `fullstack-guardian` | Use when implementing features across frontend and backend, building APIs with UI, or creating end-to-end data flows. Invoke for feature implementation, API development, UI building, cross-stack work. |
| `feature-forge` | Use when defining new features, gathering requirements, or writing specifications. Invoke for feature definition, requirements gathering, user stories, EARS format specs. |
| `code-documenter` | Use when adding docstrings, creating API documentation, or building documentation sites. Invoke for OpenAPI/Swagger specs, JSDoc, doc portals, tutorials, user guides. |
| `the-fool` | Use when challenging ideas, plans, decisions, or proposals using structured critical reasoning. Invoke to play devil's advocate, run a pre-mortem, red team, or audit evidence and assumptions. |
| `ui-ux-pro-max` | UI/UX design intelligence. 67 styles, 96 palettes, 57 font pairings, 25 charts, 13 stacks (React, Next.js, Vue, Svelte, SwiftUI, React Native, Flutter, Tailwind, shadcn/ui). Actions: plan, build, create, design, implement, review, fix, improve, optimize, enhance, refactor, check UI/UX code. |

---

## Skill Management Skills (always local, not in catalog)

These two skills live permanently in `~/.claude/skills/` and are never fetched from this repo:

| Skill | Description |
|-------|-------------|
| `skill-loader` | Reads this README, analyzes project context, recommends and fetches relevant skills for the session |
| `skill-cleanup` | Removes session-fetched skills from `~/.claude/skills/` using the `.session-skills` manifest |
