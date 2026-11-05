# SharedExpenseTracker AI Context — Design

**Date:** 2026-11-05  
**Status:** Approved (conversational); awaiting written-spec review before scaffold  
**Parent path:** `/Users/bs1100/Documents/SharedExpense Tracker All/`  
**Repo name:** `SharedExpenseTracker-ai-context`

## Goal

Create a lean AI development workspace (same role as `evolvme-ai-context`) for the Trip Discovery & Shared Expense Management Platform. Context and standards first; backend and Flutter repos later.

## Decisions locked in

| Decision | Choice |
|----------|--------|
| Fidelity | Lean EVOLV-shaped workspace (no full `.specsmd` AI-DLC port) |
| Sibling repos | Register `shared-expense-api` and `shared-expense-mobile` (not scaffolded yet) |
| Roadmap encoding | One roadmap standard doc; empty `intents/` and `bolts/` until work starts |
| Language | **Node.js + JavaScript** (not TypeScript) |
| Approach | Mirror top-level conventions of `evolvme-ai-context`; seed standards from the 8-week PDF |

## Layout

```
SharedExpense Tracker All/
└── SharedExpenseTracker-ai-context/   ← open this in Cursor
    ├── README.md
    ├── CLAUDE.md
    ├── .gitignore
    ├── .cursorignore
    ├── shared-expense-siblings.code-workspace
    ├── .cursor/rules/cross-repo-access.mdc
    ├── docs/superpowers/specs/        ← this design doc lives here
    └── memory-bank/
        ├── project.yaml
        ├── maintenance-log.md
        ├── story-index.md             # stub
        ├── standards/
        │   ├── tech-stack.md
        │   ├── system-architecture.md
        │   ├── domain-model.md
        │   ├── product-scope.md
        │   ├── learning-roadmap.md
        │   ├── coding-standards.md
        │   ├── decision-index.md
        │   └── backend-index.md       # stub endpoint registry
        ├── intents/                   # empty (.gitkeep)
        └── bolts/                     # empty (.gitkeep)
```

Future siblings (registered only):

- `../shared-expense-api` — Node.js + Express modular monolith (+ worker)
- `../shared-expense-mobile` — Flutter (after API contracts stabilize)

## Memory-bank standards (content sources)

Derived from *Trip Discovery & Shared Expense Project — 8-Week Backend Learning Roadmap*:

### `tech-stack.md`

| Area | Choice |
|------|--------|
| Runtime / language | Node.js + **JavaScript** |
| HTTP | Express.js |
| DB / ORM | PostgreSQL + Sequelize |
| Validation / docs | Zod + OpenAPI / Swagger UI |
| Auth | Password hashing + access/refresh tokens |
| Cache / rate limit | Redis |
| Jobs | BullMQ + Redis; scheduled jobs |
| Files | S3-compatible object storage |
| Containers | Docker + Docker Compose |
| Manual API checks | Postman |
| Mobile | Flutter after contracts stabilize |

### `system-architecture.md`

Modular monolith: one API deployment with clear feature modules; separate worker process shares domain services.

Suggested modules: `auth`, `users`, `trips`, `memberships`, `expenses`, `settlements`, `notifications`, `uploads`.  
Infrastructure: `database`, `redis`, `queue`, `storage`.

### `domain-model.md`

Entities: User, Trip, TripMember, JoinRequest, Expense, ExpenseParticipant, ExpenseAdjustment, SettlementSnapshot, Settlement, SettlementPayment, Notification, FileAsset.

Financial rules:

- Money in integer minor units (poisha for BDT); never floating-point.
- Do not store a mutable current balance as the only truth.
- Derive balances from expense/adjustment records; versioned settlement snapshot on finalize.
- Invariants: participant shares sum to expense amount; trip balances sum to zero.

### `product-scope.md`

**In scope:** accounts/profiles; public/private trips; discovery; join requests; organizer approval; capacity; invitations; lifecycle/cancellation; announcements/notifications; equal shared expenses + personal expenses; auditable adjustments; balances; optimized settlement suggestions; payment mark + receiver confirm; receipt/profile uploads.

**Out of scope (8-week):** real-money / MFS integration; live location; full chat; complex matching; microservices/K8s/event streaming; advanced multi-currency; complex custom split rules.

### `learning-roadmap.md`

Eight weeks (10–12h/week): data modelling → transactions → Express modules → authz/rate limits → expense ledger/settlement → Redis cache → storage/jobs/Docker → docs/deploy/Flutter E2E. Include weekly habits and definition of success from the PDF.

### `coding-standards.md`

REST conventions; Zod on params/query/body; centralized errors; consistent response shapes; service/data-access boundaries; transactions for membership capacity and expense writes; resource-level authorization; cache not source of truth for balances; idempotent jobs.

### `decision-index.md` (initial ADRs)

1. Lean AI context workspace (no full specsmd port at start).
2. Modular monolith + separate worker.
3. JavaScript (not TypeScript) for the learning backend.
4. PostgreSQL + Sequelize; explicit join models (`TripMember`, `ExpenseParticipant`).
5. BDT minor units (poisha) for money.
6. Access + refresh token auth.
7. Redis for rate limits and selected read caches; balances stay DB-backed.
8. Sibling repo names: `shared-expense-api`, `shared-expense-mobile`.

### `backend-index.md`

Empty/stub registry to fill as endpoints ship.

## Agent / repo policy

- `CLAUDE.md` + `.cursor/rules/cross-repo-access.mdc`: siblings listed above; no secrets; ask once per session before sibling writes; ask every time before git ops; no `Co-Authored-By` on commits.
- `.cursorignore`: block sibling `.env` / secret-like paths.
- `shared-expense-siblings.code-workspace`: context + both future siblings.
- Git init for the context repo; no remote and no first commit unless requested.

## Explicitly out of this scaffold

- Creating `shared-expense-api` or `shared-expense-mobile`
- Porting `.specsmd` agents / slash-command machinery
- Pre-seeding week or domain intents
- Any application source code

## Success criteria

- Context repo exists at the path above and is usable as the Cursor open root.
- An agent reading `memory-bank/standards/` can explain product scope, domain, stack (JS), architecture, and the 8-week plan.
- Cross-repo rules are ready for when the API sibling is created.
- Empty intents/bolts ready for Week 1 inception when backend work starts.

## Next step after written-spec approval

Scaffold the files listed in Layout (implementation), then stop; backend development is a later session.
