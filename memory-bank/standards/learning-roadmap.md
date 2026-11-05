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
