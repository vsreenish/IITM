---
title: Data Retention and Protection Policy
category: it
doc_type: policy
version: "2.0"
effective_date: 2026-01-01
owner: IT Operations
---

# Data Retention and Protection Policy

How long Northwind Ltd keeps data, how it is classified and protected, and what
must happen when personal data is exposed. Applies to all Northwind systems and
to supplier systems processing Northwind data.

## 1. Classification

Every piece of data carries one of four classifications. Where data of different
classifications is combined, the combined set takes the highest classification
present.

| Class | Definition | Examples |
|---|---|---|
| **Public** | Cleared for publication | Marketing material, published pricing |
| **Internal** | Default for Northwind material | Runbooks, team plans, this policy |
| **Confidential** | Restricted to those with a need | Contracts, salary bands, roadmaps |
| **Restricted** | Personal data and customer content | Employee records, customer databases |

Restricted data may not be copied to a personal device, a personal cloud account
or an unapproved application, and may not be used in a non-production
environment. Where realistic data is needed for testing, it is synthesised or
irreversibly anonymised; masking that can be reversed is not anonymisation.

## 2. Retention schedule

Data is deleted at the end of its retention period unless a legal hold applies.
Retention runs from the trigger stated in the third column.

| Record | Retention | Runs from |
|---|---|---|
| Employee personnel record | 6 years | End of employment |
| Payroll and pension records | 7 years | End of financial year |
| Recruitment records for unsuccessful candidates | 12 months | Decision date |
| Recruitment records for hires | Merged into personnel record | Start date |
| Performance reviews and calibration notes | 6 years | End of employment |
| Expense claims and receipts | 7 years | End of financial year |
| Customer contracts | 7 years | Contract end |
| Customer support correspondence | 3 years | Case closure |
| Leaver mailbox contents | 12 months | Final working day |
| Application and access logs | 13 months | Log date |
| CCTV in Northwind offices | 30 days | Recording date |
| Incident timelines and reviews | 6 years | Incident closure |

Deletion is automated. A team that needs an exception raises it with the Data
Protection Officer before the retention period expires, not after.

## 3. Legal hold

A legal hold suspends deletion for a defined set of records. Holds are issued by
the Data Protection Officer, are recorded with a scope and a reason, and are
reviewed every 6 months. While a hold is in force, automated deletion is
suspended for the records in scope and no employee may delete them manually.

An engineer responding to an incident that may involve personal data suspends
automated deletion of the relevant logs as part of the response, as set out in
the On-Call and Incident Response procedure.

## 4. Personal data incidents

Classification, internal notification and the responder's duties during an
incident are set out in the On-Call and Incident Response procedure. This section
governs what follows.

The Data Protection Officer assesses every reported incident and decides whether
it is notifiable. Where the incident is notifiable:

- The **supervisory authority must be notified within 72 hours** of Northwind
  becoming aware of the incident. Awareness runs from the moment the incident was
  raised internally, not from the moment the assessment concluded.
- Where the incident is likely to result in a high risk to the individuals
  concerned, **those individuals are notified without undue delay**, in plain
  language, describing what happened, what data was involved and what they should
  do.
- Where the 72-hour deadline cannot be met with complete information, a partial
  notification is made within the deadline and completed afterwards. The deadline
  is not extended by incomplete information.

Every incident involving personal data is recorded in the breach register,
including those assessed as not notifiable, together with the reasoning for that
assessment. The register is retained for 6 years.

Suppliers processing Northwind personal data are contractually required to notify
Northwind **within 24 hours** of becoming aware of an incident, so that Northwind
can meet its own 72-hour obligation.

## 5. Subject access requests

A request from an individual for the personal data Northwind holds about them is
acknowledged within 2 working days and answered within **1 calendar month**. The
period may be extended by a further 2 months for complex requests, provided the
individual is told within the first month.

Requests are routed to the Data Protection Officer through the Service Desk.
Managers who receive a request directly forward it the same day and do not
respond themselves. Interview scorecards and performance records are disclosable
to the individual concerned.

## 6. Data transfers

Northwind operates in the United Kingdom, India and the United States, and
personal data moves between them. Transfers rely on the safeguards recorded in
the transfer register maintained by the Data Protection Officer. A new
cross-border flow, including one created by adopting a new supplier, requires an
assessment before it begins — the review that runs as part of the Software
Request procedure.

## 7. Roles

The **Data Protection Officer** owns this policy, the breach register, the
transfer register and legal holds. **IT Operations** implements retention and
deletion. **System owners** confirm at quarterly recertification that the
retention configured in their system matches the schedule above.

## 8. Questions

Questions about retention, classification and subject access requests go to the
Data Protection Officer through the Northwind Service Desk.
