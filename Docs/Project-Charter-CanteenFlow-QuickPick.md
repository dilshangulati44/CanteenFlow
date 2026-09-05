# Project Charter — CanteenFlow QuickPick

| Field | Value |
| --- | --- |
| Project | CanteenFlow QuickPick |
| Student | Dilshan Gulati |
| Student ID | 6605142005 |
| Project owner | Dilshan Gulati (sole owner) |
| Work type | Individual assignment |
| Document | Project Charter |
| Version | 1.0 |
| Date | 2026-09-05 |
| Status | Draft for review |

**Related documents:** [Documentation index](./README.md) ·
[Design Thinking](./CanteenFlow-QuickPick-Design-Thinking.md) ·
[Requirements](./Requirements-Specification-CanteenFlow-QuickPick.md) ·
[Acceptance Criteria](./Acceptance-Criteria-CanteenFlow-QuickPick.md) ·
[Database Design](./Database-Design-CanteenFlow-QuickPick.md)

---

## Contents

- [1. Purpose](#1-purpose)
- [2. Background and relationship to the shared class idea](#2-background-and-relationship-to-the-shared-class-idea)
- [3. Objectives](#3-objectives)
- [4. Scope](#4-scope)
- [5. Stakeholders and roles](#5-stakeholders-and-roles)
- [6. Deliverables](#6-deliverables)
- [7. Milestones](#7-milestones)
- [8. Assumptions](#8-assumptions)
- [9. Constraints](#9-constraints)
- [10. Risks](#10-risks)
- [11. Success criteria](#11-success-criteria)
- [12. Next steps](#12-next-steps)

---

## 1. Purpose

CanteenFlow QuickPick is a campus food pre-order website for students with short breaks between classes. Its
distinguishing purpose is **queue reduction through limited-capacity pickup time slots**: a student reserves
not only food but a specific pickup interval, and each interval accepts only a fixed number of orders.

This charter defines what the individual project will and will not deliver, who owns it, and how completion
will be judged.

## 2. Background and relationship to the shared class idea

The class works from a shared concept called **CanteenFlow** — moving campus canteen ordering online.
CanteenFlow QuickPick is my **own individual interpretation** of that concept. It is not a group deliverable,
and it is owned solely by me.

The interpretation narrows the shared idea to one question and one mechanism:

| | Shared CanteenFlow concept | CanteenFlow QuickPick |
| --- | --- | --- |
| Question asked | How do we let students order food online? | How do we prevent the lunchtime queue from forming? |
| Mechanism | Digital ordering | Capacity-limited pickup slots with a cut-off time |
| What is reserved | Food | Food **and a pickup interval** |

Ordering ahead by itself only relocates the queue: if everyone collects at the same moment, the crowd at the
counter is unchanged. Capping the number of orders per interval is what changes the shape of demand. The
full reasoning is in the [Design Thinking document](./CanteenFlow-QuickPick-Design-Thinking.md#13-why-the-narrow-focus).

## 3. Objectives

| # | Objective | How it will be judged |
| --- | --- | --- |
| O-1 | Let a student place a campus food order before arriving at the canteen | End-to-end flow passes [AC-01 to AC-07](./Acceptance-Criteria-CanteenFlow-QuickPick.md) |
| O-2 | Make the pickup slot a capacity-controlled resource | Full and expired slots cannot be selected — [AC-05](./Acceptance-Criteria-CanteenFlow-QuickPick.md#7-ac-05--prevent-selection-of-full-or-expired-pickup-slots) |
| O-3 | Remove uncertainty about waiting by showing a fixed pickup time and a live order status | [AC-04](./Acceptance-Criteria-CanteenFlow-QuickPick.md#6-ac-04--view-pickup-slots-with-remaining-capacity) and [AC-08](./Acceptance-Criteria-CanteenFlow-QuickPick.md#10-ac-08--track-status-as-received-preparing-or-ready) pass |
| O-4 | Give vendors a level workload and simple controls | [AC-09](./Acceptance-Criteria-CanteenFlow-QuickPick.md#11-ac-09--vendor-dashboard-for-orders-and-menu-availability) passes |
| O-5 | Keep the ordering task short enough to complete between classes | No account creation; the flow is [NFR-03](./Requirements-Specification-CanteenFlow-QuickPick.md#51-usability) compliant |
| O-6 | Produce a complete, honest documentation set with no invented research | Every assumption carries a HYPOTHESIS label and appears in the [validation backlog](./CanteenFlow-QuickPick-Design-Thinking.md#63-validation-backlog) |

## 4. Scope

### 4.1 In scope — the individual MVP

| # | MVP feature | Requirements |
| --- | --- | --- |
| 1 | Browse campus food stalls | [FR-01–FR-03](./Requirements-Specification-CanteenFlow-QuickPick.md#41-stalls-and-menu-mvp-1-2-and-3) |
| 2 | View menu items, prices, images, and availability | [FR-04–FR-06](./Requirements-Specification-CanteenFlow-QuickPick.md#41-stalls-and-menu-mvp-1-2-and-3) |
| 3 | Select items and quantities | [FR-07–FR-08](./Requirements-Specification-CanteenFlow-QuickPick.md#41-stalls-and-menu-mvp-1-2-and-3) |
| 4 | View pickup slots with remaining capacity | [FR-09](./Requirements-Specification-CanteenFlow-QuickPick.md#42-pickup-slots-mvp-4-and-5) |
| 5 | Prevent selection of full or expired pickup slots | [FR-10–FR-12](./Requirements-Specification-CanteenFlow-QuickPick.md#42-pickup-slots-mvp-4-and-5) |
| 6 | Submit an order using a customer name and contact information | [FR-13–FR-15](./Requirements-Specification-CanteenFlow-QuickPick.md#43-ordering-mvp-6-and-7) |
| 7 | Receive an order number and confirmation | [FR-16–FR-17](./Requirements-Specification-CanteenFlow-QuickPick.md#43-ordering-mvp-6-and-7) |
| 8 | Track status as Received, Preparing, or Ready | [FR-18–FR-20](./Requirements-Specification-CanteenFlow-QuickPick.md#44-order-tracking-mvp-8) |
| 9 | Vendor dashboard for orders and menu availability | [FR-21–FR-26](./Requirements-Specification-CanteenFlow-QuickPick.md#45-vendor-dashboard-mvp-9) |

### 4.2 Out of scope

| # | Excluded | Reason |
| --- | --- | --- |
| X-1 | Delivery to buildings, lockers, or desks | Does not reduce the counter queue; adds logistics the project cannot support |
| X-2 | Online payments, wallets, refunds | Payment handling and its compliance burden are outside an individual coursework scope; payment stays at the counter |
| X-3 | Loyalty points, vouchers, discounts | Marketing features unrelated to queue reduction |
| X-4 | AI or machine-learning recommendations | Adds complexity without shortening a queue |
| X-5 | Multi-campus support | One campus is enough to prove the slot mechanism |
| X-6 | Student accounts, passwords, social login | Registration friction defeats the short-break use case |
| X-7 | Native iOS or Android apps | The deliverable is a website |
| X-8 | Vendor sales analytics and reporting | Not required by any MVP feature |
| X-9 | Order cancellation and refunds by students | Deferred to a later version; a cancelled slot place would need to be returned to capacity |

### 4.3 Scope change control

Any change to sections [4.1](#41-in-scope--the-individual-mvp) or [4.2](#42-out-of-scope) is decided by the
project owner, recorded in this charter, and reflected in the requirements and acceptance criteria documents
before implementation begins.

## 5. Stakeholders and roles

This is an individual assignment. There is no project team.

| Role | Held by | Responsibility |
| --- | --- | --- |
| Project owner | Dilshan Gulati (6605142005) | All analysis, design, documentation, implementation, and testing |
| Primary user | Campus students with short breaks | Places orders and collects food |
| Secondary user | Campus food stall vendors | Manages orders and menu availability |
| Assessor | Course instructor | Reviews the deliverables |

## 6. Deliverables

| # | Deliverable | Location | Status |
| --- | --- | --- | --- |
| D-1 | Project overview | [`README.md`](../README.md) | Delivered |
| D-2 | Documentation index | [`Docs/README.md`](./README.md) | Delivered |
| D-3 | Design Thinking document | [`Docs/CanteenFlow-QuickPick-Design-Thinking.md`](./CanteenFlow-QuickPick-Design-Thinking.md) | Delivered |
| D-4 | Project Charter | This document | Delivered |
| D-5 | Requirements Specification | [`Docs/Requirements-Specification-CanteenFlow-QuickPick.md`](./Requirements-Specification-CanteenFlow-QuickPick.md) | Delivered |
| D-6 | Acceptance Criteria | [`Docs/Acceptance-Criteria-CanteenFlow-QuickPick.md`](./Acceptance-Criteria-CanteenFlow-QuickPick.md) | Delivered |
| D-7 | Database Design with ER diagram | [`Docs/Database-Design-CanteenFlow-QuickPick.md`](./Database-Design-CanteenFlow-QuickPick.md) | Delivered |
| D-8 | Click-through prototype (screens S-1 to S-9) | Not started | Planned |
| D-9 | MVP web application | Not started | Planned |
| D-10 | Usability test notes | Not started | Planned |

## 7. Milestones

Milestones are expressed as ordered phases with dependencies rather than fixed calendar dates, so the plan
stays valid as the course schedule is confirmed.

| # | Milestone | Exit condition | Depends on |
| --- | --- | --- | --- |
| M-1 | Concept defined | Individual interpretation and queue-reduction focus agreed | — |
| M-2 | Documentation set complete | D-1 to D-7 published in this repository | M-1 |
| M-3 | Prototype built | Screens S-1 to S-9 clickable end to end | M-2 |
| M-4 | Prototype tested | Test plan in [section 6](./CanteenFlow-QuickPick-Design-Thinking.md#6-test) executed; hypotheses resolved | M-3 |
| M-5 | Database implemented | Schema created and seeded with sample stalls, items, and slots | M-2 |
| M-6 | MVP features 1–8 built | Student flow passes AC-01 to AC-08 | M-5 |
| M-7 | MVP feature 9 built | Vendor dashboard passes AC-09 | M-6 |
| M-8 | Final verification and submission | All acceptance criteria pass; documentation updated to match the build | M-7 |

## 8. Assumptions

| # | Assumption | If it proves false |
| --- | --- | --- |
| A-1 | Vendors will publish and maintain pickup slots for their service period | Slot capacity must be generated automatically from stall opening hours |
| A-2 | Vendors will keep item availability current during service | Sold-out items would reach students, requiring vendor-side order rejection |
| A-3 | Payment at the counter on collection is acceptable to vendors | Payments would have to be reconsidered, which is currently out of scope |
| A-4 | An order number plus a contact number is enough to identify a student at collection | A stronger identifier such as a QR code would be needed |
| A-5 | Students use a phone browser on campus Wi-Fi | Offline or low-bandwidth handling would become a priority |
| A-6 | The prototype can be tested with real students and vendors during the course | The hypotheses stay unvalidated and must be reported as such |

## 9. Constraints

| # | Constraint |
| --- | --- |
| C-1 | Individual work — all effort comes from one person, with no team capacity |
| C-2 | Delivered as a website; no native mobile applications |
| C-3 | No payment processing, so no cardholder data is ever handled |
| C-4 | Single campus only |
| C-5 | Coursework timeframe limits the build to the nine MVP features |
| C-6 | No secrets, credentials, or API keys may be committed to the repository |
| C-7 | Any personal data is limited to a customer name and contact number, kept only as long as the order needs it |

## 10. Risks

| # | Risk | Likelihood | Impact | Response |
| --- | --- | --- | --- | --- |
| R-1 | Two students take the last place in a slot at the same time, overbooking it | Medium | High | Enforce capacity in the database at insert time, not only in the interface — see [capacity enforcement](./Database-Design-CanteenFlow-QuickPick.md#7-capacity-enforcement) |
| R-2 | Students book a slot and never collect, wasting capacity | Medium | Medium | Record no-shows against the order; consider releasing capacity after the slot ends in a later version |
| R-3 | Vendors do not update availability, so students order sold-out food | Medium | Medium | Make the toggle a single tap; show the last-updated time on the vendor menu screen |
| R-4 | Slot capacity is set too high and the queue returns | Medium | High | Let the vendor edit capacity per slot; review after the first service period |
| R-5 | Slot capacity is set too low and students cannot order | Low | Medium | Same control as R-4; show the next available slot when one is full |
| R-6 | Hypotheses turn out to be wrong once real users are asked | Medium | Medium | Every assumption is labelled and listed in the [validation backlog](./CanteenFlow-QuickPick-Design-Thinking.md#63-validation-backlog) before it is relied upon |
| R-7 | No participants can be recruited within the course timeframe | Medium | Medium | Report the hypotheses as unvalidated rather than inventing findings |
| R-8 | Scope creep from the excluded features in [section 4.2](#42-out-of-scope) | Medium | High | Charter change control in [section 4.3](#43-scope-change-control) |
| R-9 | Individual workload exceeds available time | Medium | High | MVP features are ordered by milestone so features 1–8 ship before feature 9 is extended |
| R-10 | Contact numbers are exposed to the wrong vendor | Low | High | Scope vendor dashboard queries to that vendor's own stall only — [NFR-08](./Requirements-Specification-CanteenFlow-QuickPick.md#53-security-and-privacy) |
| R-11 | Clock differences make a slot look open on one device and closed on another | Low | Medium | Evaluate cut-off times on the server, never in the browser — [FR-12](./Requirements-Specification-CanteenFlow-QuickPick.md#42-pickup-slots-mvp-4-and-5) |

## 11. Success criteria

The project is successful when all of the following hold:

1. Every MVP feature in [section 4.1](#41-in-scope--the-individual-mvp) is implemented.
2. Every criterion in the [Acceptance Criteria](./Acceptance-Criteria-CanteenFlow-QuickPick.md) document passes.
3. A slot can never be overbooked beyond its capacity, and a slot past its cut-off can never be selected.
4. A student can complete an order without creating an account.
5. A vendor can advance an order to Ready and mark an item unavailable, each in a single action.
6. The documentation matches the built system, and no unvalidated assumption is presented as a finding.

## 12. Next steps

| # | Next step | Owner | Depends on |
| --- | --- | --- | --- |
| 1 | Publish this documentation set to the repository | Dilshan Gulati | — |
| 2 | Build the click-through prototype (D-8) | Dilshan Gulati | M-2 |
| 3 | Recruit participants and run the planned usability sessions | Dilshan Gulati | M-3 |
| 4 | Resolve or revise every hypothesis in the validation backlog | Dilshan Gulati | M-4 |
| 5 | Implement the database schema (M-5) | Dilshan Gulati | M-2 |
| 6 | Build MVP features 1–9 (M-6, M-7) | Dilshan Gulati | M-5 |
| 7 | Verify against the acceptance criteria and submit (M-8) | Dilshan Gulati | M-7 |
