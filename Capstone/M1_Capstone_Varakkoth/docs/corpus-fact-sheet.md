# Northwind Ltd — Canonical Fact Sheet

Not part of the corpus. This is the authoring reference: every fact below must
appear identically wherever it is repeated across the sixteen documents. A fact
that drifts between documents makes the golden set unfalsifiable.

## The organisation

| | |
|---|---|
| Legal entity | Northwind Ltd |
| Headcount | 1,240 employees, 85 agency contractors |
| Head office | Manchester, United Kingdom |
| Other offices | Bengaluru (India), Austin (United States) |
| Functions | Engineering, Product, Commercial, People Operations, Finance Operations, IT Operations |
| Currency | GBP for all policy figures |
| Leave year | 1 April – 31 March |
| Financial year | 1 April – 31 March |

## Grade structure

L1–L7. **Director level means L6 and above.** Any policy that varies by
seniority uses this boundary.

## Systems named in the corpus

| System | Used for |
|---|---|
| Workday | Leave requests, personal details, performance reviews |
| Northwind Service Desk | IT requests, access requests, incident tickets |
| Okta | Single sign-on and multi-factor authentication |
| Coupa | Purchase requisitions and supplier onboarding |
| Northwind Expenses | Expense claims and mileage |
| PagerDuty | On-call rota and paging |

## Document owners

| Cluster | Owner |
|---|---|
| `hr-*` | People Operations |
| `it-*` | IT Operations |
| `ops-*` | Finance Operations (facilities: Workplace Services) |

## Shared numeric facts

These appear in more than one document and must match exactly.

| Fact | Value | Authoritative document |
|---|---|---|
| Resignation notice, below director | 30 calendar days | `hr-leave-policy.md` |
| Resignation notice, director and above | 90 calendar days | `hr-leave-policy.md` |
| Expense claim window | 30 calendar days from expense date | `ops-expenses.md` |
| Continuous service for parental leave | 12 months | `hr-leave-policy.md` |
| Probation period | 6 months | `hr-onboarding.md` |
| Contractor sponsored account maximum | 90 days | `it-access-control.md` |
| On-call eligibility service | 90 days | `it-oncall.md` |
| Standard device refresh | 36 months | `it-device-endpoint.md` |

## Deliberate absences

Nothing in the corpus may state a position on these. They are the anchors for
the refusal questions.

- **Sabbaticals** — `hr-leave-policy.md` §6 states no scheme exists.
- **Cryptocurrency payments** — no document mentions crypto in any form.
- **Leave appeals** — no document describes an appeal route for a refused leave
  request. This is the escalation question: the correct behaviour is to say the
  corpus does not cover it and route the employee to People Operations.

## Deliberate collisions

- **"30 days"** means resignation notice in `hr-leave-policy.md` and the expense
  claim window in `ops-expenses.md`. Both are correct; neither is the other.
- **"90 days"** means director notice period, contractor account expiry, and
  on-call eligibility. Three different things, three documents.

## Vocabulary rule

The corpus says **"remote working arrangements"** and **"hybrid working
pattern"**. It never says "work from home", "WFH", or "telecommuting". Golden-set
questions use the informal terms.
