# SharedExpenseTracker AI Context Scaffold — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Scaffold a lean AI context workspace at `SharedExpenseTracker-ai-context` with standards seeded from the 8-week Trip/Shared Expense roadmap PDF (JavaScript stack).

**Architecture:** Mirror `evolvme-ai-context` top-level conventions (README, CLAUDE.md, Cursor cross-repo rules, memory-bank standards) without porting `.specsmd`. Empty `intents/` and `bolts/`. Register sibling repos `shared-expense-api` and `shared-expense-mobile` without creating them.

**Tech Stack:** Markdown memory-bank; Cursor rules; git repo init; no application runtime.

## Global Constraints

- Root: `/Users/bs1100/Documents/SharedExpense Tracker All/SharedExpenseTracker-ai-context/`
- Language for future API: **Node.js + JavaScript** (not TypeScript)
- Sibling folder names: `shared-expense-api`, `shared-expense-mobile`
- Do not create sibling code repos in this plan
- Do not port `.specsmd`
- Do not commit unless the user explicitly asks
- Never add `Co-Authored-By` attribution to commits
- Money: integer minor units (poisha for BDT); balances derived from ledger records

## File map

| Path | Responsibility |
|------|----------------|
| `README.md` | Workspace purpose, setup, workflow |
| `CLAUDE.md` | Agent git + cross-repo policy |
| `.gitignore` | Ignore IDE/OS/node junk; keep memory-bank |
| `.cursorignore` | Block sibling secrets |
| `.cursor/rules/cross-repo-access.mdc` | Always-on sibling access rule |
| `shared-expense-siblings.code-workspace` | Multi-root workspace |
| `memory-bank/project.yaml` | Repo registry |
| `memory-bank/maintenance-log.md` | Init entry |
| `memory-bank/story-index.md` | Stub |
| `memory-bank/standards/*.md` | Product/tech standards from PDF |
| `memory-bank/intents/.gitkeep` | Placeholder |
| `memory-bank/bolts/.gitkeep` | Placeholder |
| `.git/` | Local git init only |

---

### Task 1: Repo root policy files + git init

**Files:**
- Create: `README.md`
- Create: `CLAUDE.md`
- Create: `.gitignore`
- Create: `.cursorignore`
- Create: `.cursor/rules/cross-repo-access.mdc`
- Create: `shared-expense-siblings.code-workspace`

**Interfaces:**
- Consumes: Design spec at `docs/superpowers/specs/2026-11-05-shared-expense-tracker-ai-context-design.md`
- Produces: Cross-repo sibling names `shared-expense-api`, `shared-expense-mobile` used by later tasks

- [ ] **Step 1: Write `README.md`**

```markdown
# Shared Expense Tracker — AI Development Workspace

Shared AI workspace for the **Trip Discovery & Shared Expense Management Platform**. Open this repo as the editor root. It holds project standards, roadmap context, and (later) feature planning artifacts shared by sibling code repos.

> Context first. Backend and Flutter come next in sibling folders.

---

## What is this repo?

| Folder | Purpose |
|--------|---------|
| `memory-bank/` | Project brain — standards, intents, bolt artifacts |
| `docs/superpowers/` | Design specs and implementation plans |
| `.cursor/rules/` | Always-on agent policies |

**Rule:** Application code goes in sibling repos (`../shared-expense-api/`, `../shared-expense-mobile/`). Planning and standards live here.

---

## Platform repos

| Repo | Stack | Local path | Status |
|------|-------|------------|--------|
| shared-expense-api | Node.js, JavaScript, Express, PostgreSQL, Sequelize | `../shared-expense-api/` | Not scaffolded yet |
| shared-expense-mobile | Flutter | `../shared-expense-mobile/` | After API contracts stabilize |

---

## First-time setup

1. Open `SharedExpenseTracker-ai-context/` in Cursor (or open `shared-expense-siblings.code-workspace`).
2. Read `memory-bank/standards/` — start with `product-scope.md`, `domain-model.md`, `tech-stack.md`, `learning-roadmap.md`.
3. When ready for Week 1 backend work, create `../shared-expense-api/` and an intent under `memory-bank/intents/`.

Expected layout:

```
SharedExpense Tracker All/
├── SharedExpenseTracker-ai-context/   ← open THIS
├── shared-expense-api/                ← later
└── shared-expense-mobile/             ← later
```

---

## Daily workflow

```bash
git pull
# edit memory-bank/ standards or intents
git add memory-bank/
git commit -m "docs: describe change"
```

Push `memory-bank/` when an intent or bolt stage is ready for reuse.

---

## Learning roadmap pointer

See `memory-bank/standards/learning-roadmap.md` for the 8-week backend plan (10–12 hours/week).
```

- [ ] **Step 2: Write `CLAUDE.md`**

```markdown
# Project Instructions

## Git Commits

- Never add a `Co-Authored-By` trailer (or any Claude/Anthropic attribution) to commit messages in this repository.

## Cross-Repo Access (Sibling Repos)

From this repo, an AI agent may access these sibling repos (located alongside this one under `SharedExpense Tracker All/`): `shared-expense-api`, `shared-expense-mobile`.

- **Read**: allowed in the repos listed above, EXCEPT `.env` files or any other files containing sensitive data (secrets, credentials, keys, tokens). Do not access files outside these listed repos.
- **Write**: ask the user for permission once per session before writing any file/folder in a given sibling repo (e.g., ask once before the first write to `shared-expense-api`; subsequent writes in that repo within the same session don't need to ask again).
- **Before writing anything to any repo**: first read that repo's own context/rules file (`CLAUDE.md`, `.cursorrules`, `.cursor/rules/*`, or equivalent) if one exists, and follow it.
- **Git operations**: always ask the user for permission before any git operation (commit, push, branch, etc.) in any of these sibling repos, every time.

This policy applies to every AI agent operating from this repo. The same rule is mirrored in `.cursor/rules/cross-repo-access.mdc`.

**Cursor complement:** this repo’s `.cursorignore` (plus each sibling’s own `.cursorignore` when present) keeps sibling `.env`/secrets out of Agent indexing and file tools.
```

- [ ] **Step 3: Write `.gitignore`**

```gitignore
# AI tool temps
tmpclaude-*
.claude-cache/
.claude/settings.local.json
.copilot/
cursor-*/
.ai-cache/
ai-temp-*

# IDE
.idea/
*.iml
.vscode/
.history/

# OS
.DS_Store
.AppleDouble
.LSOverride
Thumbs.db

# Node (if any local tooling appears)
node_modules/
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Secrets / env
.env
.env.*
!.env.example

# Logs / temp
*.log
*.tmp
*.temp
*.bak
*.swp
*.cache
```

- [ ] **Step 4: Write `.cursorignore`**

```gitignore
# Cross-repo access — block secrets in sibling repos
# See CLAUDE.md and .cursor/rules/cross-repo-access.mdc

../shared-expense-api/**/.env*
../shared-expense-api/**/*secret*
../shared-expense-api/**/*credentials*
../shared-expense-api/**/*.pem
../shared-expense-api/**/*.key

../shared-expense-mobile/**/.env*
../shared-expense-mobile/**/*secret*
../shared-expense-mobile/**/*credentials*
../shared-expense-mobile/**/*.pem
../shared-expense-mobile/**/*.key
```

- [ ] **Step 5: Write `.cursor/rules/cross-repo-access.mdc`**

```markdown
---
description: Global cross-repo access policy — applies to every AI agent working from this repo (Claude, Cursor, or any other)
globs:
  - "**/*"
alwaysApply: true
---

# Cross-Repo Access (Sibling Repos)

From this repo, an AI agent may access these sibling repos (located alongside this one under `SharedExpense Tracker All/`): `shared-expense-api`, `shared-expense-mobile`.

- **Read**: allowed in the repos listed above, EXCEPT `.env` files or any other files containing sensitive data (secrets, credentials, keys, tokens). Do not access files outside these listed repos.
- **Write**: ask the user for permission once per session before writing any file/folder in a given sibling repo (e.g., ask once before the first write to `shared-expense-api`; subsequent writes in that repo within the same session don't need to ask again).
- **Before writing anything to any repo**: first read that repo's own context/rules file (`CLAUDE.md`, `.cursorrules`, `.cursor/rules/*`, or equivalent) if one exists, and follow it.
- **Git operations**: always ask the user for permission before any git operation (commit, push, branch, etc.) in any of these sibling repos, every time.

This is a global policy for this repo and applies to every AI agent, regardless of tool (Claude, Cursor, etc.). The same rule is mirrored in `CLAUDE.md`.
```

- [ ] **Step 6: Write `shared-expense-siblings.code-workspace`**

```json
{
  "folders": [
    {
      "name": "SharedExpenseTracker-ai-context",
      "path": "."
    },
    {
      "name": "shared-expense-api",
      "path": "../shared-expense-api"
    },
    {
      "name": "shared-expense-mobile",
      "path": "../shared-expense-mobile"
    }
  ],
  "settings": {}
}
```

- [ ] **Step 7: Init git (no commit)**

Run from the context repo root:

```bash
cd "/Users/bs1100/Documents/SharedExpense Tracker All/SharedExpenseTracker-ai-context"
git init
```

Expected: creates `.git/`; do **not** commit unless the user asks.

- [ ] **Step 8: Verify root files**

```bash
test -f README.md && test -f CLAUDE.md && test -f .gitignore && test -f .cursorignore \
  && test -f .cursor/rules/cross-repo-access.mdc \
  && test -f shared-expense-siblings.code-workspace \
  && test -d .git && echo OK
```

Expected: `OK`

---

### Task 2: Memory-bank skeleton + project registry

**Files:**
- Create: `memory-bank/project.yaml`
- Create: `memory-bank/maintenance-log.md`
- Create: `memory-bank/story-index.md`
- Create: `memory-bank/intents/.gitkeep`
- Create: `memory-bank/bolts/.gitkeep`

**Interfaces:**
- Consumes: Sibling names from Task 1
- Produces: `project.yaml` repo registry for standards docs

- [ ] **Step 1: Write `memory-bank/project.yaml`**

```yaml
# Project Configuration

project_type: full-stack-mobile-backend
initialized_at: 2026-11-05T00:00:00Z

repos:
  - name: shared-expense-api
    path: ../shared-expense-api
    type: backend-api
    stack: Node.js, JavaScript, Express, Sequelize, PostgreSQL, Redis, BullMQ
    status: planned
  - name: shared-expense-mobile
    path: ../shared-expense-mobile
    type: mobile
    stack: Flutter
    status: planned
    notes: Integrate after API contracts stabilize (Week 8)
```

- [ ] **Step 2: Write `memory-bank/maintenance-log.md`**

```markdown
# Maintenance Log

## 2026-11-05 — Context workspace initialized

- Created lean AI context repo modeled on evolvme-ai-context (no full specsmd port).
- Seeded standards from the 8-week Trip Discovery & Shared Expense backend roadmap.
- Stack language decision: Node.js + JavaScript (not TypeScript).
- Registered planned siblings: `shared-expense-api`, `shared-expense-mobile`.
- Intents and bolts left empty until Week 1 backend work starts.
```

- [ ] **Step 3: Write `memory-bank/story-index.md`**

```markdown
# Story Index

No stories yet. Create an intent under `memory-bank/intents/` when Week 1 backend work begins, then list stories here.
```

- [ ] **Step 4: Create empty intent/bolt placeholders**

```bash
mkdir -p memory-bank/intents memory-bank/bolts
touch memory-bank/intents/.gitkeep memory-bank/bolts/.gitkeep
```

- [ ] **Step 5: Verify**

```bash
test -f memory-bank/project.yaml && test -f memory-bank/maintenance-log.md \
  && test -f memory-bank/story-index.md \
  && test -f memory-bank/intents/.gitkeep \
  && test -f memory-bank/bolts/.gitkeep && echo OK
```

Expected: `OK`

---

### Task 3: Standards — stack, architecture, domain, product, roadmap

**Files:**
- Create: `memory-bank/standards/tech-stack.md`
- Create: `memory-bank/standards/system-architecture.md`
- Create: `memory-bank/standards/domain-model.md`
- Create: `memory-bank/standards/product-scope.md`
- Create: `memory-bank/standards/learning-roadmap.md`

**Interfaces:**
- Consumes: PDF roadmap content summarized in the design spec
- Produces: Canonical product/tech truth for agents

- [ ] **Step 1: Write `tech-stack.md`**

```markdown
# Tech Stack

## Backend (`shared-expense-api`)

| Area | Choice |
|------|--------|
| Runtime / language | Node.js + **JavaScript** |
| HTTP framework | Express.js |
| Database / ORM | PostgreSQL + Sequelize |
| Validation / API docs | Zod + OpenAPI / Swagger UI |
| Authentication | Password hashing + access/refresh token flow |
| Cache / rate limiting | Redis |
| Background processing | BullMQ + Redis; scheduled jobs |
| File storage | S3-compatible object storage |
| Containerization | Docker + Docker Compose |
| Manual API verification | Postman collections and environments |

## Mobile (`shared-expense-mobile`)

| Area | Choice |
|------|--------|
| Client | Flutter — integrate after API contracts stabilize |

## Local tooling

- DB client: pgAdmin or DBeaver
- Money: integer minor units (poisha for BDT); never floating-point
```

- [ ] **Step 2: Write `system-architecture.md`**

```markdown
# System Architecture

## Overview

Trip Discovery & Shared Expense Management Platform. Users discover trips, request to join, organizers manage membership, members record shared expenses, and the system calculates balances and tracks settlement.

**Pattern:** Modular monolith (one API deployment) + separate worker process sharing domain services.

## Containers

| Container | Repo | Type | Stack |
|-----------|------|------|-------|
| REST API | shared-expense-api | Backend | Node.js, JavaScript, Express, Sequelize |
| Worker | shared-expense-api (`worker`) | Background | BullMQ consumers + schedulers |
| Database | — | Data | PostgreSQL |
| Cache / queues | — | Infra | Redis |
| Object storage | — | Infra | S3-compatible |
| Mobile app | shared-expense-mobile | Mobile | Flutter (later) |

## Suggested module layout

```
src/
  config/
  common/
  modules/
    auth/
    users/
    trips/
    memberships/
    expenses/
    settlements/
    notifications/
    uploads/
  infrastructure/
    database/
    redis/
    queue/
    storage/
  app.js
  server.js
  worker.js
```

## Dependency direction

Route → validation (Zod) → controller → service → Sequelize/data-access. Infrastructure adapters sit behind services. Worker reuses domain services; do not duplicate business rules in job handlers.

## Auth sketch

```
Client → POST /auth/login → API validates → { accessToken, refreshToken }
Client sends Bearer access token
Refresh rotates/revokes per Week 4 design
```

## Caching rule

Cache public trip discovery and stable reference data with short TTLs and explicit invalidation. **Financial balances and settlement calculations stay database-backed** — cache is never the source of truth for money.
```

- [ ] **Step 3: Write `domain-model.md`**

```markdown
# Domain Model

## Entities

| Entity | Role |
|--------|------|
| User | Identity and profile |
| Trip | Organizer, visibility, origin/destination, dates, capacity, budget, lifecycle status |
| TripMember | Membership, role, status, joined/left timestamps (explicit join model) |
| JoinRequest | Requester, trip, status, optional message, decision metadata |
| Expense | Trip, creator, payer, amount (minor units), category, type, description, status |
| ExpenseParticipant | Selected member + allocated share for an expense |
| ExpenseAdjustment | Refund/correction linked to an original expense, with reason and creator |
| SettlementSnapshot | Finalized balances for a trip (versioned) |
| Settlement | Suggested/agreed transfer from one member to another |
| SettlementPayment | Actual/partial payments and receiver confirmation |
| Notification | In-app notification and delivery state |
| FileAsset | Object key, owner, related entity, content type, access metadata |

## Financial invariants

1. Store money as **integer minor units** (poisha for BDT). Never use floating-point for money.
2. Do **not** store a mutable current balance as the only financial truth.
3. Derive balances from expense and adjustment records.
4. Create a versioned **SettlementSnapshot** when finalizing a trip settlement.
5. Participant shares for an expense must sum to the expense amount.
6. All trip member balances must sum to zero (after deriving from the ledger).
7. Corrections/refunds are **ExpenseAdjustment** records — never silent overwrites.

## Membership rules (summary)

- Explicit `TripMember` for role/status/joinedAt/leftAt.
- Unique membership and duplicate pending join-request constraints.
- Capacity / last-slot approval must be transactional (no overbooking).

## Expense rules (summary)

- Shared expenses split equally among **selected** participants; personal expenses supported.
- Remainder distribution in minor units must be deterministic.
- Net balance = total paid − total share (positive = receive, negative = owe).
```

- [ ] **Step 4: Write `product-scope.md`**

```markdown
# Product Scope (8-week first release)

## In scope

- Accounts and profiles
- Public/private trip visibility; trip creation and discovery
- Join requests, organizer approval, member capacity, invitations
- Trip lifecycle and cancellation
- Trip announcements and notifications
- Basic itinerary only if time remains
- Shared expenses split equally among selected participants
- Personal expenses
- Corrections/refunds as auditable adjustments (not silent overwrites)
- Trip balances, optimized settlement suggestions
- Payment marking and receiver confirmation
- Receipt/profile image attachments via object storage

## Out of scope

- Real-money or mobile financial service integration
- Live location tracking
- Full real-time chat
- Complex matching algorithms
- Microservices, Kubernetes, event streaming, multi-region infrastructure
- Advanced multi-currency accounting
- Complex custom split rules
```

- [ ] **Step 5: Write `learning-roadmap.md`**

```markdown
# 8-Week Backend Learning Roadmap

**Duration:** 8 weeks  
**Weekly commitment:** 10–12 hours  
**Suggested split:** ~3h learning, 6–7h implementation, 1–2h manual testing/review/notes  
**Primary outcome:** Backend ownership (design, implement, secure, operate, explain)

## Principle

Build to learn, not just to finish. For every feature: understand the problem, sketch data model and request flow, implement, test failures, explain trade-offs. Use AI as a helper; independently understand design, code, queries, and debugging.

## Weekly habits

- Start each week by explaining the concept in your own words and drawing the request/data flow.
- Implement one vertical slice at a time: route → validation → service → Sequelize → response.
- Use Postman for happy paths, invalid input, unauthorized access, not-found, and boundaries.
- Inspect generated SQL when ORM behavior is unclear.
- Keep an engineering log: learned / broke / why / how verified.
- Do not add Redis, queues, or storage before understanding the problem they solve.

## Weeks

### Week 1 — Database theory, modelling & Sequelize foundations

**Build:** Node.js + JavaScript + Express + PostgreSQL via Sequelize. Models: User, Trip, TripMember, JoinRequest, Expense, ExpenseParticipant, Settlement, SettlementPayment. Migrations + seeders.  
**Deliverable:** Running API connected to PostgreSQL with models, migrations, seed data.

### Week 2 — Transactions & data integrity

**Build:** Trip creation and join approval with safe transactions; prevent overbooking; atomic expense + participants; DB constraints; integer minor units.  
**Deliverable:** Reliable membership and expense creation with constraints.

### Week 3 — Express architecture & REST APIs

**Build:** Modules for auth, users, trips, memberships, expenses, settlements. Profile + trip CRUD/discovery with filters/pagination. Zod validation. Centralized errors.  
**Deliverable:** Modular Express API with profile and trip endpoints.

### Week 4 — Auth, authorization, rate limiting & security

**Build:** Signup/login/refresh/logout; organizer-only and member-only authorization; Redis rate limits; security headers/CORS/payload limits.  
**Deliverable:** Protected API with resource-level authz and Redis-backed limits.

### Week 5 — Expense ledger & settlement

**Build:** Shared/personal expenses; deterministic share allocation; settlement suggestions; mark payment / confirm or dispute; adjustments; finalize snapshot.  
**Deliverable:** End-to-end expense and settlement workflow with edge cases verified.

### Week 6 — Redis caching & performance

**Build:** Cache public trip discovery (filters/pagination in keys); invalidate on trip changes; cache stable reference data; keep balances DB-backed.  
**Deliverable:** Measured caching layer with documented invalidation rules.

### Week 7 — Object storage, jobs, schedulers & Docker

**Build:** Receipt/profile uploads; BullMQ workers; departure reminders / stale join-request expiry; Docker Compose for API, Postgres, Redis, worker.  
**Deliverable:** Dockerized local env with worker, storage, and at least one recurring job.

### Week 8 — Docs, deployment & production readiness

**Build:** Swagger UI; complete Postman collections; deploy; health checks; connect Flutter to stable contracts for one E2E journey.  
**Deliverable:** Documented, deployable backend with register → trip → join → expenses → settlement path.

## Definition of success

- Design relational models with Sequelize migrations and PostgreSQL constraints.
- Maintainable Node.js + JavaScript + Express API with validation and consistent errors.
- Authentication plus resource-level authorization.
- Transactions/concurrency for capacity and financial workflows.
- Accurate expense splitting and settlement with auditable corrections.
- Caching with invalidation rules; rate limits and practical security.
- Safe file storage; background jobs/schedulers; Docker Compose; deploy + debug with logs/health checks.
```

- [ ] **Step 6: Verify key phrases**

```bash
rg -n "JavaScript" memory-bank/standards/tech-stack.md
rg -n "poisha|minor units" memory-bank/standards/domain-model.md
rg -n "Out of scope" memory-bank/standards/product-scope.md
rg -n "Week 1" memory-bank/standards/learning-roadmap.md
```

Expected: matches in each file.

---

### Task 4: Standards — coding, decisions, backend index

**Files:**
- Create: `memory-bank/standards/coding-standards.md`
- Create: `memory-bank/standards/decision-index.md`
- Create: `memory-bank/standards/backend-index.md`

**Interfaces:**
- Consumes: Stack/domain from Task 3
- Produces: ADRs and coding rules agents must follow when building the API later

- [ ] **Step 1: Write `coding-standards.md`**

```markdown
# Coding Standards

## Language

- Backend is **JavaScript** (Node.js). Prefer clear modules over clever abstractions.
- Use `async`/`await`; propagate errors to centralized Express error handling.

## API shape

- REST conventions; meaningful HTTP status codes.
- Consistent success and error response envelopes (define once in Week 3 and keep stable).
- Validate params, query, and body with **Zod** at the edge.
- Paginate list endpoints; avoid over-fetching (select attributes intentionally).

## Layering

- Routers → controllers → services → Sequelize models/repositories.
- Keep business rules in services; keep HTTP concerns in controllers/middleware.
- Worker jobs call the same services (or thin wrappers) — no duplicated ledger logic.

## Data & money

- Integer **minor units** only for money fields.
- Use DB constraints (unique membership, positive amounts, FKs) plus application checks.
- Wrap membership capacity changes and expense+participant writes in **transactions**.
- Never silently overwrite financial history; use adjustments.

## Security

- Hash passwords (bcrypt or Argon2); never store plaintext.
- Access + refresh tokens with expiry, rotation/revocation, logout.
- Resource-level authorization: organizer-only vs member-only vs public discovery.
- Changing a path/body ID must not bypass ownership checks (BOLA awareness).
- Redis-backed rate limits on auth and write-heavy endpoints.
- No secrets in git; use env validation in `config/`.

## Caching & jobs

- Document cache keys and invalidation with every cached endpoint.
- Jobs must be idempotent under retry.
- Do not cache balances as source of truth.

## Verification

- Postman: happy path, validation failure, 401/403, 404, pagination boundaries.
- For financial logic: manually verify 2–6 member examples, selective participants, refunds, partial payments, zero-sum balances.
```

- [ ] **Step 2: Write `decision-index.md`**

```markdown
# Decision Index

## ADRs (accepted)

### ADR-001 — Lean AI context workspace
Use an evolvme-style context repo for standards and later intents/bolts. Do **not** port full `.specsmd` AI-DLC machinery at project start.

### ADR-002 — Modular monolith + worker
Ship one API codebase with clear feature modules and a separate worker process sharing domain services. No microservices in the 8-week scope.

### ADR-003 — JavaScript instead of TypeScript
Backend language is **Node.js + JavaScript** to reduce toolchain overhead for this learning project. Types may be revisited later; not required for Week 1–8.

### ADR-004 — PostgreSQL + Sequelize with explicit join models
Use Sequelize migrations/seeders. Model membership and expense participation as explicit tables (`TripMember`, `ExpenseParticipant`), not opaque many-to-many sugar that hides columns.

### ADR-005 — BDT minor units (poisha)
Store all money as integers in the smallest currency unit. Never use floating-point for money.

### ADR-006 — Access + refresh token authentication
Password hashing plus access/refresh token flow with logout and revocation/rotation (Week 4).

### ADR-007 — Cache is not financial truth
Redis may cache discovery and reference data. Balances and settlement math remain database/ledger derived.

### ADR-008 — Sibling repo names
Code siblings are `shared-expense-api` and `shared-expense-mobile`, living next to this context repo under `SharedExpense Tracker All/`.

## PDRs (open)

None yet. Record open product/technical decisions here as they appear during build weeks.
```

- [ ] **Step 3: Write `backend-index.md`**

```markdown
# Backend Endpoint Index

Stub registry. Fill rows as `shared-expense-api` endpoints ship.

| Method | Path | Module | Auth | Status | Notes |
|--------|------|--------|------|--------|-------|
| — | — | — | — | planned | No endpoints until Week 1+ |

## Modules (planned)

- auth
- users
- trips
- memberships
- expenses
- settlements
- notifications
- uploads
```

- [ ] **Step 4: Verify standards directory**

```bash
ls memory-bank/standards | sort
```

Expected listing includes:

```
backend-index.md
coding-standards.md
decision-index.md
domain-model.md
learning-roadmap.md
product-scope.md
system-architecture.md
tech-stack.md
```

- [ ] **Step 5: Final tree check**

```bash
cd "/Users/bs1100/Documents/SharedExpense Tracker All/SharedExpenseTracker-ai-context"
find . -type f -not -path './.git/*' -not -path './docs/superpowers/*' | sort
```

Expected: root policy files + all memory-bank files from Tasks 1–4. Spec/plan under `docs/superpowers/` may also appear (already created).

- [ ] **Step 6: Commit only if user asks**

Do not run `git commit` unless the user explicitly requests it. If they do, stage all scaffold files and use a message such as:

```bash
git add -A
git commit -m "$(cat <<'EOF'
docs: scaffold SharedExpenseTracker AI context workspace

EOF
)"
```

---

## Spec coverage checklist

| Spec item | Task |
|-----------|------|
| README / CLAUDE / cursor rules / cursorignore / workspace | Task 1 |
| Git init, no remote/commit by default | Task 1 |
| project.yaml + empty intents/bolts + maintenance/story stubs | Task 2 |
| tech-stack (JS), architecture, domain, product, roadmap | Task 3 |
| coding standards, ADRs, backend-index stub | Task 4 |
| No sibling code repos / no specsmd | Global constraints |

## Plan self-review

- No TBD/TODO placeholders in steps.
- JavaScript called out consistently (ADR-003 + tech-stack).
- Sibling names consistent: `shared-expense-api`, `shared-expense-mobile`.
- Verification steps are filesystem/content checks (appropriate for a docs scaffold).
