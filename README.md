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
