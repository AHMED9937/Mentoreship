# Task 1 — Vacation Tracking System (VTS)

A domain analysis of a **Vacation Tracking System**: the problem, requirements,
constraints, and the supporting diagrams.

## Vision

A Vacation Tracking System (VTS) gives individual employees the capability to
manage their own vacation time, sick leave, and personal time off — **without
having to be an expert in company policy or the local facility's leave policies**.

The goal is to streamline the Human Resources (HR) department, minimise non-core
management activity, and give employees a sense of empowerment and ownership over
this aspect of their employment agreement. HR personnel remain responsible for
entering and updating employee vacation data, but they are **no longer a link in
the chain** for requesting and validating each individual time request — that work
is replaced by a rules-based validation system. The potential saving in time and
money falls mostly on HR.

## Functional requirements

| # | Requirement |
|---|-------------|
| F1 | Enables manager approval (optional). |
| F2 | Provides access to requests for the previous calendar year, and allows requests to be made up to a year and a half into the future. |
| F3 | Uses e-mail notification to request manager approval and to notify employees of request status changes. |
| F4 | Uses existing hardware and middleware. |
| F5 | Is implemented as an extension to the existing intranet portal system, and uses the portal's single-sign-on (SSO) mechanism for all authentication. |
| F6 | Keeps activity logs for all transactions. |
| F7 | Enables HR and system-administration personnel to override all actions restricted by rules, with logging of those overrides. |
| F8 | Allows managers to directly award personal leave time (within system-set limits). |
| F9 | Provides a Web-service interface for other internal systems to query any given employee's vacation-request summary. |
| F10 | Interfaces with the HR department's legacy systems to retrieve required employee information and changes. |

## Non-functional requirements

- **NFR1 — Flexible rules engine.** Implements a flexible, rules-based system for
  validating and verifying leave-time requests.
- **NFR2 — Usability.** The system must be easy to use, intuitive, and
  intelligent.
- **NFR3 — Reuse of infrastructure.** Runs on existing hardware, middleware, and
  the intranet portal (see F4/F5).
- **NFR4 — Auditability.** All transactions and all rule overrides are logged
  (see F6/F7).

## Constraints

- The system must be **easy to use, intuitive, and intelligent**.
- **HR personnel remain responsible** for entering and updating employee vacation
  data in the system; however, they are no longer a link in the chain for
  requesting and validating each individual time request.

## Domain — define the problem

> **The employee wishes to submit a new request for vacation time.**

This is the core journey the system exists to serve. An employee submits a leave
request; the rules engine validates it against company and facility policy; a
manager optionally approves it; and all parties are notified by e-mail while every
transaction is logged.

## Diagrams

The diagrams live in Lucidchart; each file under [`docs/diagrams/`](docs/diagrams/)
links to its source.

| # | Diagram | File | Link |
|---|---------|------|------|
| 1 | Flowchart | [`docs/diagrams/01-flowchart.md`](docs/diagrams/01-flowchart.md) | [Lucid](https://lucid.app/lucidchart/8b88e3e0-78ac-4eeb-a3b5-63b824c1d8e3/edit) |
| 2 | Sequence diagram | [`docs/diagrams/02-sequence-diagram.md`](docs/diagrams/02-sequence-diagram.md) | [Lucid](https://lucid.app/lucidchart/d45b8374-fe33-4ad1-95e8-91574aae2253/edit) |
| 3 | Data model (ERD) | [`docs/diagrams/03-data-model-erd.md`](docs/diagrams/03-data-model-erd.md) | [Lucid](https://lucid.app/lucidchart/d8e7b2e5-89a3-411d-9695-0f945f7aff0f/edit) |
