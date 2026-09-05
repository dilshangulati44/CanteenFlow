# CanteenFlow QuickPick

**Individual project — campus food pre-ordering with capacity-controlled pickup slots.**

| Field | Value |
| --- | --- |
| Project name | CanteenFlow QuickPick |
| Student | Dilshan Gulati |
| Student ID | 6605142005 |
| Project owner | Dilshan Gulati (sole owner) |
| Work type | Individual assignment |
| Document date | 2026-09-05 |
| Repository branch | `main` |

---

## 1. What this project is

CanteenFlow QuickPick is a campus food **pre-order website** for students who have short breaks between
classes. A student browses the campus food stalls, picks menu items, reserves a **pickup time slot that has
limited capacity**, submits the order with a name and contact number, and then tracks the order through
**Received → Preparing → Ready**. Vendors get a simple dashboard to move orders along and to switch menu
items on or off.

This repository holds the **documentation deliverables** for the individual assignment. No application code
is included at this stage.

## 2. Relationship to the shared class idea

The class shares a broad concept called **CanteenFlow** — digitising campus canteen ordering. CanteenFlow
QuickPick is an **original individual interpretation** of that shared starting point, not a copy of it and
not a team deliverable.

The individual angle is deliberately narrow:

- The shared idea asks *"how do we let students order food online?"*
- **This project asks a different question: "how do we stop the lunchtime queue from forming in the first
  place?"**

The answer this project commits to is **pickup-slot capacity control**. Every pickup slot has a hard maximum
number of orders. Once a slot is full, or once its cut-off time has passed, no further orders can be placed
into it. Demand is therefore spread across the lunch period instead of arriving in one physical queue at the
counter. Every design decision in this project — the data model, the ordering flow, the vendor dashboard —
is judged against whether it supports that one goal.

See [Design Thinking](Docs/CanteenFlow-QuickPick-Design-Thinking.md#2-empathize) for the reasoning behind
this focus.

## 3. Individual MVP scope

| # | MVP feature |
| --- | --- |
| 1 | Browse campus food stalls |
| 2 | View menu items, prices, images, and availability |
| 3 | Select items and quantities |
| 4 | View pickup slots with remaining capacity |
| 5 | Prevent selection of full or expired pickup slots |
| 6 | Submit an order using a customer name and contact information |
| 7 | Receive an order number and confirmation |
| 8 | Track status as Received, Preparing, or Ready |
| 9 | Vendor dashboard to manage orders and menu availability |

## 4. Explicitly out of scope

This version does **not** include:

- Delivery to buildings, lockers, or desks
- Online payments, wallets, or refunds
- Loyalty points, vouchers, or discount engines
- AI or machine-learning recommendations
- Multi-campus support
- Student accounts, passwords, or social login (orders are identified by order number and contact number)
- Native mobile applications

## 5. Documentation

Start at the [documentation index](Docs/README.md), or go directly to a document:

| Document | Purpose |
| --- | --- |
| [Design Thinking](Docs/CanteenFlow-QuickPick-Design-Thinking.md) | Empathize, Define, Ideate, Prototype, Test |
| [Project Charter](Docs/Project-Charter-CanteenFlow-QuickPick.md) | Objectives, scope, milestones, risks, next steps |
| [Requirements Specification](Docs/Requirements-Specification-CanteenFlow-QuickPick.md) | Numbered functional and non-functional requirements |
| [Acceptance Criteria](Docs/Acceptance-Criteria-CanteenFlow-QuickPick.md) | Given/When/Then criteria for every MVP feature |
| [Database Design](Docs/Database-Design-CanteenFlow-QuickPick.md) | Tables, keys, constraints, Mermaid ER diagram |

## 6. Evidence status

> **Important.** No user interviews, surveys, or usability tests have been carried out yet. Every persona
> detail, quotation, and pain point in this documentation is an explicitly labelled **hypothesis** written to
> guide design, and each one is listed as something to validate. No statistics, research findings, or test
> results are claimed. See the [validation backlog](Docs/CanteenFlow-QuickPick-Design-Thinking.md#63-validation-backlog).

## 7. Repository layout

```text
.
├── .gitattributes
├── README.md                  # This file
└── Docs/
    ├── README.md
    ├── CanteenFlow-QuickPick-Design-Thinking.md
    ├── Project-Charter-CanteenFlow-QuickPick.md
    ├── Requirements-Specification-CanteenFlow-QuickPick.md
    ├── Acceptance-Criteria-CanteenFlow-QuickPick.md
    └── Database-Design-CanteenFlow-QuickPick.md
```
