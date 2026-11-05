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
