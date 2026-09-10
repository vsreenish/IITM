---
title: Software Request Procedure
category: it
doc_type: procedure
version: "1.0"
effective_date: 2025-05-01
owner: IT Operations
---

# Software Request Procedure

How employees obtain software that is not part of the standard build, and how new
suppliers are assessed before their software reaches a Northwind device.

## 1. The approved catalogue

The approved catalogue lists every application cleared for use at Northwind,
together with the roles entitled to it. Catalogue applications install on demand
from the self-service portal on the device, with no ticket and no approval where
the employee's role is already entitled.

Where an employee's role is not entitled to a catalogue application, the request
goes to the Service Desk and is approved by the direct manager. Approval is
usually same-day; licence cost is charged to the requesting team's budget.

## 2. Software outside the catalogue

A request for an application that is not in the catalogue is a **new supplier
request**, even where the software is free, open source or browser-based. Three
checks run in parallel:

1. **Security review** by IT Operations, covering authentication, data location
   and the supplier's own security posture. Target: 10 working days.
2. **Data protection review** by the Data Protection Officer, required wherever
   the application will process personal data. Target: 10 working days.
3. **Commercial review** by Finance Operations, covering contract terms, renewal
   and exit. This runs through the Procurement procedure, and the approval
   thresholds set out there apply to the annual licence cost.

An application may not be used, trialled or piloted with real Northwind data
before all applicable reviews have completed. Trials on synthetic data are
permitted with IT Operations approval.

## 3. Browser extensions

Browser extensions are software and follow this procedure. Extensions are blocked
by default and enabled per extension, not per employee. Extensions that request
permission to read page contents on all sites are refused unless there is no
alternative and the department head accepts the risk in writing.

## 4. Artificial intelligence tools

Applications that transmit Northwind content to a third-party model provider
require the full three-way review in Section 2 regardless of cost, including
where the tool is free. The security review additionally confirms that the
supplier does not train on Northwind content and that data is not retained beyond
the session.

Employees may not paste customer data, source code or unpublished commercial
information into a tool that has not completed this review.

## 5. Personal licences

Northwind does not reimburse software an employee has bought personally, and
personally licensed software may not be installed on a Northwind device. Where an
employee already holds a personal licence for an application they need for work,
the correct route is a catalogue request; the personal licence is irrelevant to
the decision.

Professional membership and subscription fees that are not software are handled
under the Benefits reference document.

## 6. Renewals and removal

Licences are reviewed annually against actual use. An application with fewer than
five active users in a 90-day period is a candidate for removal, and the
requesting team is asked to justify renewal.

Employees who no longer need an application release the licence through the
self-service portal. Licences attached to leavers are released automatically on
the final working day.

## 7. Unapproved software already in use

Where an employee discovers they are using an application that has not been
through this procedure, they raise it with IT Operations. No disciplinary action
follows a request made voluntarily; the application is assessed on its merits and
either brought into the catalogue or withdrawn with a migration period of up to
30 days.

The same treatment does not apply to unapproved software discovered by the
endpoint agent rather than declared. In that case the application is removed
immediately and the employee's manager is informed.

Teams migrating away from a withdrawn application may request an export of their
data from the supplier through IT Operations, which is arranged before access is
withdrawn rather than afterwards.

## 8. Accounts held with a personal email address

Applications signed up for with a personal email address are outside Northwind's
control: access cannot be revoked when the employee leaves, and the data cannot
be recovered. Any work-related account must use a Northwind identity through
Okta. An existing account held on a personal address is transferred to a
Northwind identity on discovery, or closed where transfer is not possible.

## 9. Questions

Software questions go to IT Operations through the Northwind Service Desk.
Questions about contracts and thresholds go to Finance Operations.
