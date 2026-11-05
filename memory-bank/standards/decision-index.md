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
