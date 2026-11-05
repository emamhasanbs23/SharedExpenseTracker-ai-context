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
