# CanteenFlow QuickPick — Documentation Index

| Field | Value |
| --- | --- |
| Project | CanteenFlow QuickPick |
| Student | Dilshan Gulati |
| Student ID | 6605142005 |
| Project owner | Dilshan Gulati (sole owner) |
| Work type | Individual assignment |
| Last updated | 2026-09-05 |

This folder contains the complete documentation set for the individual **CanteenFlow QuickPick** project.
The project takes the shared class concept *CanteenFlow* as a starting point and develops an original
individual interpretation centred on **limited-capacity pickup time slots as a queue-reduction mechanism**.

---

## 1. Documents

| # | Document | What it answers |
| --- | --- | --- |
| 1 | [Design Thinking](./CanteenFlow-QuickPick-Design-Thinking.md) | Who is this for, what problem is being solved, and how was the solution reached? Covers Empathize, Define, Ideate, Prototype, and Test. |
| 2 | [Project Charter](./Project-Charter-CanteenFlow-QuickPick.md) | What is being built, by when, within what boundaries, and at what risk? |
| 3 | [Requirements Specification](./Requirements-Specification-CanteenFlow-QuickPick.md) | Numbered functional (FR) and non-functional (NFR) requirements. |
| 4 | [Acceptance Criteria](./Acceptance-Criteria-CanteenFlow-QuickPick.md) | Given/When/Then criteria proving each MVP feature is done. |
| 5 | [Database Design](./Database-Design-CanteenFlow-QuickPick.md) | Tables, columns, keys, constraints, and the Mermaid ER diagram. |

## 2. Suggested reading order

1. Start with the [Design Thinking](./CanteenFlow-QuickPick-Design-Thinking.md) document to understand the
   student problem and why pickup-slot capacity was chosen as the core mechanism.
2. Read the [Project Charter](./Project-Charter-CanteenFlow-QuickPick.md) for scope boundaries, milestones,
   and risks.
3. Read the [Requirements Specification](./Requirements-Specification-CanteenFlow-QuickPick.md) for the
   numbered requirements the build must satisfy.
4. Read the [Acceptance Criteria](./Acceptance-Criteria-CanteenFlow-QuickPick.md) to see how each requirement
   will be judged complete.
5. Finish with the [Database Design](./Database-Design-CanteenFlow-QuickPick.md), which shows how the slot
   capacity rule is enforced in data.

## 3. Traceability

The documents are linked in one chain, so any MVP feature can be followed end to end:

```text
MVP feature  →  FR / NFR number  →  Acceptance criterion (AC)  →  Database table
```

For example, "prevent selection of full or expired pickup slots" is MVP feature 5, which is
[FR-09 and FR-10](./Requirements-Specification-CanteenFlow-QuickPick.md#42-pickup-slots-mvp-4-and-5),
verified by [AC-05](./Acceptance-Criteria-CanteenFlow-QuickPick.md#7-ac-05--prevent-selection-of-full-or-expired-pickup-slots),
and enforced by the `pickup_slots` table described in the
[Database Design](./Database-Design-CanteenFlow-QuickPick.md#53-pickup_slots).

## 4. Evidence and honesty statement

> No interviews, surveys, observations, or usability tests have been conducted for this project so far.
>
> All personas, quotations, empathy-map entries, and pain points are labelled **HYPOTHESIS** and exist only
> to direct design decisions. They are assumptions to be tested, not findings. No statistics, percentages,
> or test results are reported anywhere in this documentation. Items awaiting evidence are collected in the
> [validation backlog](./CanteenFlow-QuickPick-Design-Thinking.md#63-validation-backlog).

## 5. Document conventions

- **HYPOTHESIS** — an unverified assumption written by the project owner; must be validated before it is
  treated as fact.
- **FR-nn** — numbered functional requirement.
- **NFR-nn** — numbered non-functional requirement.
- **AC-nn** — acceptance criterion, written in Given/When/Then form.
- Times are campus local time in 24-hour format. Currency is shown as THB.
