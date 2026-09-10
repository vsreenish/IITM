---
title: Access Control Policy
category: it
doc_type: policy
version: "1.5"
effective_date: 2025-11-01
owner: IT Operations
---

# Access Control Policy

How identities are created, granted access, reviewed and removed at Northwind
Ltd. Applies to every system that holds Northwind or customer data, whether
hosted by Northwind or by a supplier.

## 1. Identity

Every person who accesses a Northwind system holds exactly one identity in Okta.
Shared accounts are not permitted under any circumstance, including for testing,
for demonstrations and for automation. Where automation requires access, a
service account is created and owned by a named engineer.

Multi-factor authentication is mandatory for all identities, with no exemption by
role or seniority. The permitted second factors are the Okta Verify application
and hardware security keys. SMS is not an accepted second factor.

## 2. Role-based provisioning

Access is granted against a **role profile**, not system by system. When a joiner
is provisioned, IT Operations reads the access section of the role profile
attached to the requisition and grants the standard set for that role.

Requests for access beyond the role profile require a business justification and
approval from the system owner. Standing exceptions are reviewed at each
recertification and lapse if the justification is no longer recorded.

## 3. Joiners, movers and leavers

**Joiners.** Access is provisioned on the equipment request raised by the hiring
manager on offer acceptance, and is active on day one. Access is never granted
before the employment start date.

**Movers.** On an internal move, access for the new role is provisioned against
the new role profile, and access attached to the previous role is removed within
**5 working days**. Accumulated access from a sequence of internal moves is the
single largest source of over-privilege at Northwind, and the removal step is not
optional.

**Leavers.** All access is revoked on the final working day, at the end of the
working day in the employee's home office. Where a departure is not amicable,
the department head may request revocation at the point notice is given; the
employee remains employed and paid through their notice period. Notice periods
themselves are set out in the Leave Policy.

Mailbox contents are retained under the schedule in the Data Retention and
Protection policy and are accessible to the leaver's manager on request through
the Service Desk.

## 4. Non-employees

Agency contractors, interns, auditors and supplier staff do not hold employee
identities. They are provisioned **sponsored accounts**, which differ in four
ways:

1. Every sponsored account has a named **sponsor** who must be a Northwind
   employee at manager grade or above. The sponsor is accountable for the access,
   not the contracting agency.
2. A sponsored account has a **maximum lifetime of 90 days**. It expires
   automatically on that date and is not extended silently. An extension is a
   fresh request from the sponsor, approved again, for a further period of up to
   90 days.
3. Sponsored accounts are excluded from role-based provisioning. Access is
   granted explicitly, item by item, and defaults to read-only where a read-only
   variant exists.
4. Sponsored accounts may not hold privileged access, may not be granted access
   to production customer data, and may not be used to approve a change.

The sponsor is notified 14 days and 3 days before expiry. Where a sponsor leaves
Northwind, every account they sponsor is suspended within 24 hours and must be
re-sponsored to be reinstated.

Contractors are not covered by Northwind employment policies, and their leave and
working arrangements are administered by their agency, as set out in the Leave
Policy. This does not reduce the sponsor's accountability for what the account
can reach.

## 5. Privileged access

Privileged access — administrator rights, production database access, and the
ability to change access for others — is granted just in time. An engineer
requests elevation in Okta, states a reason, and the elevation expires
automatically after **4 hours**.

Standing privileged access exists for a small number of break-glass accounts held
by IT Operations. Use of a break-glass account raises a SEV3 incident
automatically, which is closed once the use has been explained.

## 6. Recertification

System owners recertify access **quarterly**. A recertification that is not
completed within 15 working days of being issued results in the removal of all
access flagged in it, not in a reminder.

Sponsored accounts are recertified at every expiry rather than quarterly.

## 7. Reporting

Suspected credential compromise, a lost second factor, or a device loss is
reported to the Service Desk within **4 hours**. Reporting a suspected compromise
never attracts a penalty, including where the cause was the employee's own error.

## 8. Questions

Questions about access go to IT Operations through the Northwind Service Desk.
