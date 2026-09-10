---
title: On-Call and Incident Response
category: it
doc_type: procedure
version: "2.3"
effective_date: 2026-02-01
owner: IT Operations
---

# On-Call and Incident Response

How Northwind Ltd runs its production on-call rotas, classifies incidents,
escalates them, and closes them out. Applies to all engineering teams operating
a service in production, and to the IT Operations platform team.

## 1. Scope

Every service in the production catalogue has a named owning team and a
published rota. A service without a published rota may not be promoted to
production; the release process checks this at the promotion gate.

The rota covers the service, not the individual. Where a team owns several
services, one rota covers all of them unless the department head has approved a
split.

## 2. Rota structure

Rotas run in PagerDuty on a weekly cycle, handing over at **10:00 local time on
Wednesday**. Wednesday handover is deliberate: it avoids a Monday handover
colliding with the weekly release window and avoids a Friday handover leaving a
new responder alone over a weekend.

Each rota has two levels:

- **Primary.** Acknowledges pages and leads the response.
- **Secondary.** Pages if the primary has not acknowledged within 10 minutes,
  and acts as a second pair of hands on any SEV1.

A rota must have at least **five engineers** in the primary rotation. A rota that
falls below five is suspended by IT Operations and its services are absorbed into
the platform team rota until the owning team is staffed again. No engineer may be
primary for more than one week in any four.

Escalation beyond secondary goes to the engineering manager for the owning team,
then to the department head. The escalation chain is configured in PagerDuty and
is reviewed monthly by IT Operations. An engineer who cannot take a shift
arranges a swap in PagerDuty and tells their manager; unfilled shifts are covered
by the engineering manager by default.

## 3. Joining a rota

An engineer joins a rota only when all three of the following are true. The
engineering manager confirms them in the rota record before the engineer is added
to PagerDuty.

1. The engineer has completed **90 days of service** at Northwind.
2. The engineer has completed **two shadow shifts** on the rota they are joining,
   during which they receive every page alongside the primary but hold no
   responsibility for the response.
3. The engineer holds the production access required by the runbooks for every
   service on the rota, provisioned under the Access Control policy.

Shadow shifts do not attract an on-call allowance. An engineer returning to a
rota after more than 6 months away repeats one shadow shift but not the service
qualification.

**Compensation.** Standby and callout rates, the treatment of a full week on
rota, and the delayed-start entitlement after an overnight page are set out in
the Benefits reference document. This procedure governs eligibility and duty; the
Benefits reference governs the amount.

## 4. Severity classification

The responder classifies an incident at the point of acknowledgement. The
classification may be revised in either direction as the picture changes, and the
revision is recorded in the incident timeline.

| Severity | Definition | Acknowledge | Update cadence |
|---|---|---|---|
| SEV1 | Complete loss of a customer-facing service, or any confirmed exposure of customer data | 5 minutes | Every 30 minutes |
| SEV2 | Severe degradation of a customer-facing service, or loss of an internal service that blocks a function | 15 minutes | Every 60 minutes |
| SEV3 | Partial degradation with a workaround available | 4 working hours | Daily |
| SEV4 | Minor defect, no customer impact | Next working day | On closure |

When in doubt between two severities, the responder takes the higher one.
Downgrading later costs nothing; discovering late that a SEV2 was a SEV1 costs
the notification clock.

## 5. Running a SEV1

A SEV1 has three named roles, held by three different people:

- **Incident lead.** Runs the response and makes the calls. Usually the primary.
- **Communications lead.** Owns updates to stakeholders and the status page. Held
  by the engineering manager unless delegated explicitly.
- **Scribe.** Maintains the timeline in the incident channel.

The incident lead does not debug. The moment the lead is head-down in a terminal,
the response has lost its coordinator and a second person takes the lead role.

A dedicated Slack channel is opened for every SEV1 and SEV2, named
`inc-YYYYMMDD-short-description`. All decisions are recorded in that channel, not
in direct messages, because the channel is the evidence base for the review.

Customer communication is issued by the communications lead only. Engineers do
not contact customers directly during an incident, however well intentioned.

## 6. Incidents involving personal data

Any incident where customer or employee personal data may have been exposed,
altered or lost is classified **SEV1 from the outset**, regardless of the number
of records involved and regardless of whether exposure is confirmed.

The responder must additionally:

1. Notify the Data Protection Officer within **1 hour** of the incident being
   raised, through the Service Desk major incident line, not by email
2. Preserve all logs relevant to the incident and suspend any automated deletion
   affecting them
3. Record in the timeline the categories of data involved and the earliest known
   time of exposure

**The notification obligations that follow — who must be told outside Northwind,
and within what period — are set out in the Data Retention and Protection
policy.** The responder's duty under this procedure is to raise, classify and
notify internally; the external clock is governed by that policy.

No engineer may decide independently that a suspected data incident does not
require notification. That decision belongs to the Data Protection Officer.

## 7. Runbooks

Every service carries a runbook covering the alerts on its rota. A runbook that
has not been reviewed in 12 months is flagged in the service catalogue and
blocks the next release of that service.

A runbook entry states the alert, what it means, the first three things to check,
and the escalation contact. Runbooks are written for a responder who did not
build the service and is reading at 03:00.

## 8. Closing an incident

An incident is closed when the service is restored and the responder has recorded
the resolution in the timeline. Restoration is not resolution: a workaround
closes the incident but opens a follow-up ticket with the owning team.

SEV1 and SEV2 incidents require a written review within **5 working days**,
attended by the incident lead, the owning team and IT Operations. Reviews are
blameless. The review produces actions with named owners and dates; actions
without an owner are not recorded as actions.

Follow-up actions from a SEV1 are tracked to completion by IT Operations and
reported to the department head monthly until closed.

## 9. Maintenance windows and change freezes

Planned maintenance runs in the weekly window, Wednesday 20:00 to 23:00 local
time, and is announced at least 3 working days in advance. Changes made in the
window still page if they break something; the rota is not suspended during
maintenance.

A change freeze applies from 20 December to 2 January and for the 5 working days
before any announced customer event. Releases during a freeze require department
head approval.

## 10. Questions

Questions about rotas, escalation and severity go to IT Operations through the
Northwind Service Desk.
