---
title: Device and Endpoint Standard
category: it
doc_type: policy
version: "1.3"
effective_date: 2025-08-01
owner: IT Operations
---

# Device and Endpoint Standard

The devices Northwind Ltd issues, how they are configured and maintained, and
what employees may and may not do with them.

## 1. The standard build

Every employee is issued one laptop. There are two standard builds, selected by
role family rather than by preference:

| Build | Specification | Issued to |
|---|---|---|
| **Standard** | 14-inch laptop, 16 GB memory, 512 GB storage | All roles outside engineering and design |
| **Engineering** | 16-inch laptop, 32 GB memory, 1 TB storage | Engineering, data and design roles |

Both builds ship with full-disk encryption enabled, the Northwind management
agent, the endpoint detection agent, and the approved software baseline. A device
that cannot report to the management agent is blocked from Northwind systems
within 24 hours.

Monitors, keyboards, mice and headsets are ordered against the same request as
the laptop. One monitor is standard; a second requires manager approval.

## 2. Requesting a device

Device requests are raised in the Northwind Service Desk. For a new joiner the
request is raised by the hiring manager on offer acceptance, and the hiring
manager is the approver for a standard build — the timing of that request and of
issue on day one is set out in the Onboarding procedure.

**Non-standard requests** — any specification outside the two builds above, or a
second laptop, or a device running an operating system other than the two
supported — require:

- A written technical justification from the requester
- Approval from the department head
- Confirmation from IT Operations that the device can be managed and monitored

Non-standard devices are not held in stock. Lead time is 10 to 15 working days,
which is why non-standard requests for new joiners must be raised at least
10 working days before the start date.

## 3. Refresh and return

Laptops are refreshed on a **36-month** cycle. IT Operations contacts the
employee 30 days before the refresh date to arrange the swap. A refresh is not
an opportunity to change build; a change of build follows the non-standard
request route.

A device that fails outside the refresh cycle is replaced within 2 working days
in Manchester and 5 working days in Bengaluru and Austin. Loan devices are
available from the Service Desk for the interval.

Devices are returned on the final working day, or within 5 working days for
leavers who were working remotely, using the prepaid return packaging issued by
IT Operations. A device not returned within 30 days of the final working day is
reported to Finance Operations and its value recovered.

## 4. Acceptable use

Northwind devices are provided for work. Incidental personal use is permitted
and expected; the following are not:

- Installing software outside the approved catalogue, which is governed by the
  Software Request procedure
- Disabling, delaying or attempting to remove the management or endpoint agents
- Allowing family members or any other person to use the device
- Storing Northwind data on personal cloud storage or personal email
- Connecting the device to an unsecured public network without the VPN

Personal equipment may not be used to access Northwind systems. The single
exception is the Okta Verify application on a personal phone, which is permitted
and is the default second factor.

## 5. Patching

Operating system updates are deployed automatically and may be deferred by the
employee for no more than **7 days**. Critical security patches may be deferred
for **24 hours**. A device more than 14 days behind on patching loses access to
internal systems until it is compliant.

Employees on extended leave return to a device that will patch on first
connection; that first connection should be made at a point where the device can
remain on and connected for at least an hour.

## 6. Loss, theft and damage

Loss or theft is reported to the Service Desk **within 4 hours** of being
discovered, regardless of location or time of day. IT Operations issues a remote
wipe on report. Reporting promptly never attracts a penalty; delaying a report
does.

Accidental damage is repaired or replaced at Northwind's cost. Repeated damage
arising from a failure to take reasonable care is referred to the employee's
manager.

## 7. Mobile phones

Mobile phones are issued only to roles that carry an on-call obligation or that
require a phone for customer contact. Where a phone is issued, it is enrolled in
management and subject to the same standards as a laptop. Employees who are on
call and are not issued a phone use Okta Verify on their personal device to
receive pages, and claim the on-call allowance set out in the Benefits reference
document.

## 8. Questions

Device questions go to IT Operations through the Northwind Service Desk.
