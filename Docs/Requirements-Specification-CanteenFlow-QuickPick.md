# Requirements Specification — CanteenFlow QuickPick

| Field | Value |
| --- | --- |
| Project | CanteenFlow QuickPick |
| Student | Dilshan Gulati |
| Student ID | 6605142005 |
| Project owner | Dilshan Gulati (sole owner) |
| Work type | Individual assignment |
| Document | Requirements Specification |
| Version | 1.0 |
| Date | 2026-09-05 |

**Related documents:** [Documentation index](./README.md) ·
[Design Thinking](./CanteenFlow-QuickPick-Design-Thinking.md) ·
[Project Charter](./Project-Charter-CanteenFlow-QuickPick.md) ·
[Acceptance Criteria](./Acceptance-Criteria-CanteenFlow-QuickPick.md) ·
[Database Design](./Database-Design-CanteenFlow-QuickPick.md)

---

## Contents

- [1. Purpose](#1-purpose)
- [2. Definitions](#2-definitions)
- [3. Actors](#3-actors)
- [4. Functional requirements](#4-functional-requirements)
- [5. Non-functional requirements](#5-non-functional-requirements)
- [6. Business rules](#6-business-rules)
- [7. Traceability matrix](#7-traceability-matrix)
- [8. Assumptions and exclusions](#8-assumptions-and-exclusions)

---

## 1. Purpose

This document lists the numbered requirements for the individual **CanteenFlow QuickPick** MVP: a campus food
pre-order website whose distinguishing mechanism is **limited-capacity pickup time slots** used to reduce the
physical queue at the canteen counter.

Requirements are identified as **FR-nn** (functional) and **NFR-nn** (non-functional). Every functional
requirement traces to an MVP feature and to an acceptance criterion in the
[Acceptance Criteria](./Acceptance-Criteria-CanteenFlow-QuickPick.md) document.

Priority values: **Must** (required for MVP), **Should** (valuable, may be deferred), **Could** (optional).
All MVP requirements below are **Must** unless stated otherwise.

## 2. Definitions

| Term | Meaning |
| --- | --- |
| **Stall** | A campus food vendor with its own menu and its own pickup slots |
| **Menu item** | A single dish or drink sold by one stall, with a price, an image, and an availability flag |
| **Pickup slot** | A time interval published by a stall, with a maximum number of orders (capacity) and an ordering cut-off time |
| **Capacity** | The maximum number of orders a stall will accept for one pickup slot |
| **Remaining capacity** | Capacity minus the number of active orders already placed in that slot |
| **Cut-off time** | The moment after which a slot can no longer be selected, even if capacity remains |
| **Expired slot** | A slot whose cut-off time has passed |
| **Full slot** | A slot whose remaining capacity is zero |
| **Order** | One student's request for items from one stall, for one pickup slot |
| **Order number** | The short, human-readable reference a student gives at the counter |
| **Order status** | One of `Received`, `Preparing`, or `Ready` |

## 3. Actors

| Actor | Description | Authentication |
| --- | --- | --- |
| **Student (guest customer)** | Places and tracks an order | None — identified by order number and contact number |
| **Vendor** | Manages one stall's orders and menu availability | Signs in; sees only that stall's data |
| **System** | Evaluates slot capacity and cut-off times, and generates order numbers | — |

## 4. Functional requirements

### 4.1 Stalls and menu (MVP 1, 2, and 3)

| ID | Requirement | Priority | MVP |
| --- | --- | --- | --- |
| **FR-01** | The system shall display a list of all campus food stalls, showing for each stall its name, image, short description, and open or closed state. | Must | 1 |
| **FR-02** | The system shall let a student open a single stall to view that stall's menu. | Must | 1 |
| **FR-03** | The system shall clearly mark a closed stall and shall not allow an order to be started for it. | Must | 1 |
| **FR-04** | The system shall display, for each menu item, its name, description, price, and image. | Must | 2 |
| **FR-05** | The system shall display an availability state for each menu item, distinguishing available from unavailable. | Must | 2 |
| **FR-06** | The system shall prevent an unavailable menu item from being added to an order. | Must | 2 |
| **FR-07** | The system shall let a student add an available menu item to the order and set a whole-number quantity of at least 1. | Must | 3 |
| **FR-08** | The system shall show the selected items, their quantities, each line total, and the order total before the order is submitted, and shall let the student change a quantity or remove an item. | Must | 3 |

### 4.2 Pickup slots (MVP 4 and 5)

| ID | Requirement | Priority | MVP |
| --- | --- | --- | --- |
| **FR-09** | The system shall display the pickup slots published by the selected stall for the current service day, showing for each slot its start time, end time, and remaining capacity. | Must | 4 |
| **FR-10** | The system shall display a slot with zero remaining capacity as **Full** and shall make it non-selectable. | Must | 5 |
| **FR-11** | The system shall display a slot whose cut-off time has passed as **Closed** and shall make it non-selectable. | Must | 5 |
| **FR-12** | The system shall evaluate remaining capacity and cut-off time on the server at the moment of submission, and shall reject an order for a slot that has become full or expired since the slot list was displayed. | Must | 5 |

### 4.3 Ordering (MVP 6 and 7)

| ID | Requirement | Priority | MVP |
| --- | --- | --- | --- |
| **FR-13** | The system shall require a customer name and a contact number before an order can be submitted, and shall not require account registration. | Must | 6 |
| **FR-14** | The system shall validate that the customer name is not blank and that the contact number matches an accepted phone-number format, and shall show a field-level message for each invalid entry. | Must | 6 |
| **FR-15** | The system shall create an order only when all items are still available, the chosen slot is still selectable, and the customer details are valid; otherwise no order is created and the student is returned to the step that must be corrected. | Must | 6 |
| **FR-16** | The system shall generate a unique order number for every created order and shall consume one place of that slot's capacity at the moment the order is created. | Must | 7 |
| **FR-17** | The system shall display a confirmation showing the order number, the stall name, the pickup slot time range, the ordered items with quantities, and the order total. | Must | 7 |

### 4.4 Order tracking (MVP 8)

| ID | Requirement | Priority | MVP |
| --- | --- | --- | --- |
| **FR-18** | The system shall set every new order to the status `Received`. | Must | 8 |
| **FR-19** | The system shall let a student retrieve an order and see its current status of `Received`, `Preparing`, or `Ready`, using the order number together with the contact number given on the order. | Must | 8 |
| **FR-20** | The system shall show the pickup slot time and the stall name alongside the status on the tracking view. | Must | 8 |

### 4.5 Vendor dashboard (MVP 9)

| ID | Requirement | Priority | MVP |
| --- | --- | --- | --- |
| **FR-21** | The system shall require a vendor to sign in before the dashboard is shown. | Must | 9 |
| **FR-22** | The system shall show a signed-in vendor only the orders belonging to that vendor's own stall. | Must | 9 |
| **FR-23** | The system shall list a stall's orders grouped by pickup slot and ordered by slot start time, showing for each order its order number, customer name, items with quantities, and current status. | Must | 9 |
| **FR-24** | The system shall let a vendor advance an order from `Received` to `Preparing` and from `Preparing` to `Ready`, each in a single action. | Must | 9 |
| **FR-25** | The system shall let a vendor toggle any of that stall's menu items between available and unavailable, and shall apply the change to new orders immediately. | Must | 9 |
| **FR-26** | The system shall let a vendor view the capacity and remaining capacity of each of that stall's pickup slots. | Must | 9 |
| **FR-27** | The system should let a vendor mark an order as `Collected` after handover. | Should | Post-MVP |
| **FR-28** | The system should let a vendor edit the capacity of a future pickup slot. | Should | Post-MVP |

## 5. Non-functional requirements

### 5.1 Usability

| ID | Requirement |
| --- | --- |
| **NFR-01** | The website shall be usable on a mobile phone screen 360 px wide without horizontal scrolling. |
| **NFR-02** | Every interactive control shall have a touch target of at least 44 × 44 px. |
| **NFR-03** | A student shall be able to complete an order from the stall list to the confirmation screen in no more than six screens, with no account registration at any point. |
| **NFR-04** | A vendor shall be able to advance an order status or toggle item availability in a single tap from the dashboard. |
| **NFR-05** | Slot states (**Available**, **Full**, **Closed**) shall be distinguishable by text label as well as by colour. |

### 5.2 Reliability and data integrity

| ID | Requirement |
| --- | --- |
| **NFR-06** | The number of active orders in a pickup slot shall never exceed that slot's capacity, including when two orders are submitted simultaneously. |
| **NFR-07** | An order shall be created as a single atomic transaction covering the order, its line items, and the capacity check; a partial order shall never be stored. |
| **NFR-08** | Deleting or archiving a stall shall not orphan its menu items, slots, or orders; referential integrity shall be enforced by the database. |

### 5.3 Security and privacy

| ID | Requirement |
| --- | --- |
| **NFR-09** | Vendor dashboard access shall be authenticated, and every dashboard query shall be scoped to the signed-in vendor's own stall. |
| **NFR-10** | The system shall collect only a customer name and a contact number, and shall collect no payment details of any kind. |
| **NFR-11** | Order tracking shall require both the order number and the contact number on that order, so an order number alone does not expose personal data. |
| **NFR-12** | All traffic shall be served over HTTPS. |
| **NFR-13** | No credentials, API keys, or connection strings shall be stored in the repository; configuration shall come from environment variables. |
| **NFR-14** | All user input shall be validated and escaped on the server to prevent injection and cross-site scripting. |

### 5.4 Performance

| ID | Requirement |
| --- | --- |
| **NFR-15** | The stall list, a stall menu, and the slot list shall each render within 3 seconds on a typical campus mobile connection. |
| **NFR-16** | An order submission shall return a confirmation or a clear rejection within 3 seconds. |
| **NFR-17** | Remaining capacity shown to a student shall be no more than 30 seconds stale, and shall always be re-verified at submission. |

### 5.5 Maintainability and portability

| ID | Requirement |
| --- | --- |
| **NFR-18** | The website shall run in current versions of Chrome, Firefox, Safari, and Edge. |
| **NFR-19** | Slot capacity, slot duration, and cut-off offset shall be configurable data values, not hard-coded constants. |
| **NFR-20** | The database schema shall match the [Database Design](./Database-Design-CanteenFlow-QuickPick.md) document, and any change shall be reflected there. |

### 5.6 Accessibility

| ID | Requirement |
| --- | --- |
| **NFR-21** | Text shall meet a contrast ratio of at least 4.5:1 against its background. |
| **NFR-22** | Every menu item image shall have descriptive alternative text. |
| **NFR-23** | The ordering flow shall be completable using a keyboard alone. |

## 6. Business rules

| ID | Rule |
| --- | --- |
| **BR-01** | One order belongs to exactly one stall. Items from two stalls require two separate orders. |
| **BR-02** | One order occupies exactly one pickup slot and consumes exactly one place of that slot's capacity, regardless of how many items it contains. |
| **BR-03** | A slot is selectable only when the current time is before its cut-off time **and** its remaining capacity is greater than zero **and** its stall is open. |
| **BR-04** | The cut-off time of a slot is on or before that slot's start time. |
| **BR-05** | Order status advances in one direction only: `Received` → `Preparing` → `Ready`. |
| **BR-06** | An order number is unique across the whole system and is safe to read aloud at a counter. |
| **BR-07** | Menu item availability is controlled by the owning vendor and applies only to new orders; orders already placed are unaffected. |
| **BR-08** | Payment is taken at the counter on collection and is never handled by the system. |
| **BR-09** | Cancelled orders release their slot place back to remaining capacity; cancellation itself is post-MVP ([X-9](./Project-Charter-CanteenFlow-QuickPick.md#42-out-of-scope)). |

## 7. Traceability matrix

| MVP feature | Functional requirements | Acceptance criterion | Primary tables |
| --- | --- | --- | --- |
| 1. Browse campus food stalls | FR-01, FR-02, FR-03 | [AC-01](./Acceptance-Criteria-CanteenFlow-QuickPick.md#3-ac-01--browse-campus-food-stalls) | `stalls` |
| 2. View menu items, prices, images, availability | FR-04, FR-05, FR-06 | [AC-02](./Acceptance-Criteria-CanteenFlow-QuickPick.md#4-ac-02--view-menu-items-prices-images-and-availability) | `menu_items` |
| 3. Select items and quantities | FR-07, FR-08 | [AC-03](./Acceptance-Criteria-CanteenFlow-QuickPick.md#5-ac-03--select-items-and-quantities) | `menu_items`, `order_items` |
| 4. View pickup slots with remaining capacity | FR-09 | [AC-04](./Acceptance-Criteria-CanteenFlow-QuickPick.md#6-ac-04--view-pickup-slots-with-remaining-capacity) | `pickup_slots` |
| 5. Prevent selection of full or expired slots | FR-10, FR-11, FR-12 | [AC-05](./Acceptance-Criteria-CanteenFlow-QuickPick.md#7-ac-05--prevent-selection-of-full-or-expired-pickup-slots) | `pickup_slots`, `orders` |
| 6. Submit an order with name and contact | FR-13, FR-14, FR-15 | [AC-06](./Acceptance-Criteria-CanteenFlow-QuickPick.md#8-ac-06--submit-an-order-using-a-customer-name-and-contact-information) | `orders`, `order_items` |
| 7. Receive an order number and confirmation | FR-16, FR-17 | [AC-07](./Acceptance-Criteria-CanteenFlow-QuickPick.md#9-ac-07--receive-an-order-number-and-confirmation) | `orders` |
| 8. Track Received / Preparing / Ready | FR-18, FR-19, FR-20 | [AC-08](./Acceptance-Criteria-CanteenFlow-QuickPick.md#10-ac-08--track-status-as-received-preparing-or-ready) | `orders` |
| 9. Vendor dashboard | FR-21 – FR-26 | [AC-09](./Acceptance-Criteria-CanteenFlow-QuickPick.md#11-ac-09--vendor-dashboard-for-orders-and-menu-availability) | `stalls`, `menu_items`, `orders`, `pickup_slots` |

## 8. Assumptions and exclusions

Assumptions behind these requirements are recorded in the
[Project Charter, section 8](./Project-Charter-CanteenFlow-QuickPick.md#8-assumptions). Assumptions about user
behaviour are labelled as hypotheses in the
[Design Thinking document](./CanteenFlow-QuickPick-Design-Thinking.md#63-validation-backlog) and have not been
validated with real users.

The following are explicitly **not** requirements of this version: delivery, online payments, loyalty points,
AI recommendations, multi-campus support, student accounts, native mobile apps, and vendor analytics. See
[Project Charter, section 4.2](./Project-Charter-CanteenFlow-QuickPick.md#42-out-of-scope).
