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
