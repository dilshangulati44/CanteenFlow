# Acceptance Criteria — CanteenFlow QuickPick

| Field | Value |
| --- | --- |
| Project | CanteenFlow QuickPick |
| Student | Dilshan Gulati |
| Student ID | 6605142005 |
| Project owner | Dilshan Gulati (sole owner) |
| Work type | Individual assignment |
| Document | Acceptance Criteria (Given / When / Then) |
| Version | 1.0 |
| Date | 2026-09-05 |

**Related documents:** [Documentation index](./README.md) ·
[Design Thinking](./CanteenFlow-QuickPick-Design-Thinking.md) ·
[Project Charter](./Project-Charter-CanteenFlow-QuickPick.md) ·
[Requirements](./Requirements-Specification-CanteenFlow-QuickPick.md) ·
[Database Design](./Database-Design-CanteenFlow-QuickPick.md)

---

## Contents

- [1. Purpose and conventions](#1-purpose-and-conventions)
- [2. Test data used in the examples](#2-test-data-used-in-the-examples)
- [3. AC-01 — Browse campus food stalls](#3-ac-01--browse-campus-food-stalls)
- [4. AC-02 — View menu items, prices, images, and availability](#4-ac-02--view-menu-items-prices-images-and-availability)
- [5. AC-03 — Select items and quantities](#5-ac-03--select-items-and-quantities)
- [6. AC-04 — View pickup slots with remaining capacity](#6-ac-04--view-pickup-slots-with-remaining-capacity)
- [7. AC-05 — Prevent selection of full or expired pickup slots](#7-ac-05--prevent-selection-of-full-or-expired-pickup-slots)
- [8. AC-06 — Submit an order using a customer name and contact information](#8-ac-06--submit-an-order-using-a-customer-name-and-contact-information)
- [9. AC-07 — Receive an order number and confirmation](#9-ac-07--receive-an-order-number-and-confirmation)
- [10. AC-08 — Track status as Received, Preparing, or Ready](#10-ac-08--track-status-as-received-preparing-or-ready)
- [11. AC-09 — Vendor dashboard for orders and menu availability](#11-ac-09--vendor-dashboard-for-orders-and-menu-availability)
- [12. Cross-cutting criteria](#12-cross-cutting-criteria)
- [13. Coverage summary](#13-coverage-summary)

---

## 1. Purpose and conventions

This document defines, in **Given / When / Then** form, the conditions under which each MVP feature of
CanteenFlow QuickPick is considered complete. Each criterion traces back to numbered requirements in the
[Requirements Specification](./Requirements-Specification-CanteenFlow-QuickPick.md).

- One **AC-nn** covers one MVP feature and contains numbered scenarios (`AC-nn.n`).
- Scenarios cover the successful path, the boundary, and the failure path.
- These are specifications to be tested, **not** results. **No test has been executed and no outcome is
  reported anywhere in this document.**

## 2. Test data used in the examples

The following is invented sample data used purely to make the scenarios concrete. It does not describe any
real stall, person, or price.

| Stall | State | Items | Pickup slots (sample day) |
| --- | --- | --- | --- |
| Stall A — "Rice & Noodles" | Open | Chicken Rice (THB 45, available), Beef Noodles (THB 55, unavailable) | 12:00–12:15 capacity 10, 12:15–12:30 capacity 10, 12:30–12:45 capacity 10 |
| Stall B — "Drinks Corner" | Closed | Iced Tea (THB 25, available) | none published |

Sample customer: name "Nara", contact number `0800000000`. Slot cut-off is the slot start time.

---

## 3. AC-01 — Browse campus food stalls

**MVP feature 1** · Requirements [FR-01, FR-02, FR-03](./Requirements-Specification-CanteenFlow-QuickPick.md#41-stalls-and-menu-mvp-1-2-and-3)

### AC-01.1 — The stall list is shown

> **Given** a student opens the CanteenFlow QuickPick home page
> **And** Stall A and Stall B exist in the system
> **When** the page finishes loading
> **Then** both stalls are listed
> **And** each stall shows its name, image, short description, and open or closed state.

### AC-01.2 — Opening a stall shows its menu

> **Given** the stall list is displayed
> **And** Stall A is open
> **When** the student selects Stall A
> **Then** the menu of Stall A is displayed
> **And** no items belonging to any other stall are shown.

### AC-01.3 — A closed stall cannot be ordered from

> **Given** Stall B is marked closed
> **When** the student views the stall list
> **Then** Stall B is displayed with a visible "Closed" label
> **And** no control that would start an order from Stall B is available.

### AC-01.4 — No stalls exist

> **Given** no stalls have been added to the system
> **When** the student opens the home page
> **Then** an empty-state message explaining that no stalls are available is shown
> **And** no error is displayed.

---

## 4. AC-02 — View menu items, prices, images, and availability

**MVP feature 2** · Requirements [FR-04, FR-05, FR-06](./Requirements-Specification-CanteenFlow-QuickPick.md#41-stalls-and-menu-mvp-1-2-and-3)

### AC-02.1 — Item details are shown

> **Given** the student is viewing the menu of Stall A
> **When** the menu is displayed
> **Then** Chicken Rice is shown with its name, description, price of THB 45, and image
> **And** every other item of Stall A is shown with the same four details.

### AC-02.2 — Availability is visible

> **Given** Chicken Rice is marked available and Beef Noodles is marked unavailable
> **When** the student views the menu of Stall A
> **Then** Chicken Rice is shown as available
> **And** Beef Noodles is shown with a clearly visible "Unavailable" label.

### AC-02.3 — An unavailable item cannot be added

> **Given** Beef Noodles is marked unavailable
> **When** the student attempts to add Beef Noodles to the order
> **Then** the item is not added
> **And** the add control for that item is disabled.

### AC-02.4 — An image is missing

> **Given** a menu item has no image recorded
> **When** the student views the menu
> **Then** a placeholder image is shown in its place
> **And** the item name, description, price, and availability are still displayed.

---

## 5. AC-03 — Select items and quantities

**MVP feature 3** · Requirements [FR-07, FR-08](./Requirements-Specification-CanteenFlow-QuickPick.md#41-stalls-and-menu-mvp-1-2-and-3)

### AC-03.1 — An available item is added with a quantity

> **Given** the student is viewing the menu of Stall A
> **And** Chicken Rice is available
> **When** the student adds Chicken Rice with a quantity of 2
> **Then** the order contains one line for Chicken Rice with a quantity of 2
> **And** the line total is shown as THB 90.

### AC-03.2 — The order total is calculated

> **Given** the order contains Chicken Rice at a quantity of 2, priced at THB 45 each
> **When** the student opens the order review screen
> **Then** each line shows its quantity and line total
> **And** the order total is shown as THB 90.

### AC-03.3 — A quantity can be changed

> **Given** the order contains Chicken Rice with a quantity of 2
> **When** the student changes the quantity to 3
> **Then** the line total updates to THB 135
> **And** the order total updates to THB 135.

### AC-03.4 — An item can be removed

> **Given** the order contains one line for Chicken Rice
> **When** the student removes that line
> **Then** the line no longer appears in the order
> **And** the order total updates accordingly.

### AC-03.5 — Quantity boundary

> **Given** the order contains Chicken Rice with a quantity of 1
> **When** the student attempts to set the quantity to 0 or to a negative or non-whole number
> **Then** the quantity is not accepted
> **And** a message states that the quantity must be a whole number of at least 1.

### AC-03.6 — The order cannot proceed while empty

> **Given** the order contains no items
> **When** the student attempts to continue to the pickup slot screen
> **Then** the student is not allowed to continue
> **And** a message states that at least one item must be selected.

---

## 6. AC-04 — View pickup slots with remaining capacity

**MVP feature 4** · Requirement [FR-09](./Requirements-Specification-CanteenFlow-QuickPick.md#42-pickup-slots-mvp-4-and-5)

### AC-04.1 — Slots are listed with remaining capacity

> **Given** Stall A has published the slots 12:00–12:15, 12:15–12:30, and 12:30–12:45, each with a capacity of 10
> **And** the current time is 11:30
> **When** the student opens the pickup slot screen for Stall A
> **Then** all three slots are listed in ascending order of start time
> **And** each slot shows its start time, its end time, and its remaining capacity.

### AC-04.2 — Remaining capacity reflects existing orders

> **Given** the slot 12:15–12:30 has a capacity of 10
> **And** 4 active orders already exist for that slot
> **When** the student views the pickup slot screen
> **Then** the slot 12:15–12:30 shows a remaining capacity of 6.

### AC-04.3 — Only the selected stall's slots are shown

> **Given** the student is ordering from Stall A
> **When** the pickup slot screen is displayed
> **Then** only slots published by Stall A are listed.

### AC-04.4 — No slots are published

> **Given** Stall A has published no slots for the current service day
> **When** the student opens the pickup slot screen
> **Then** a message states that no pickup times are available
> **And** the order cannot be submitted.

---

## 7. AC-05 — Prevent selection of full or expired pickup slots

**MVP feature 5** · Requirements [FR-10, FR-11, FR-12](./Requirements-Specification-CanteenFlow-QuickPick.md#42-pickup-slots-mvp-4-and-5)

This is the core queue-control criterion of the project.

### AC-05.1 — A full slot cannot be selected

> **Given** the slot 12:15–12:30 has a capacity of 10
> **And** 10 active orders already exist for that slot
> **When** the student views the pickup slot screen
> **Then** the slot 12:15–12:30 is displayed with the label "Full"
> **And** its remaining capacity is shown as 0
> **And** it cannot be selected.

### AC-05.2 — An expired slot cannot be selected

> **Given** the slot 12:00–12:15 has a cut-off time of 12:00
> **And** the current time is 12:05
> **When** the student views the pickup slot screen
> **Then** the slot 12:00–12:15 is displayed with the label "Closed"
> **And** it cannot be selected
> **And** the slot 12:15–12:30 remains selectable if it has remaining capacity.

### AC-05.3 — The last remaining place is selectable

> **Given** the slot 12:30–12:45 has a capacity of 10 and 9 active orders
> **And** the current time is before its cut-off
> **When** the student views the pickup slot screen
> **Then** the slot shows a remaining capacity of 1
> **And** it is selectable.

### AC-05.4 — A slot that fills after the page was loaded is rejected at submission

> **Given** the student loaded the slot screen while 12:15–12:30 showed a remaining capacity of 1
> **And** another order has since taken that last place
> **When** the student submits the order for the slot 12:15–12:30
> **Then** the order is not created
> **And** a message states that the slot is now full
> **And** the student is returned to the slot screen showing that slot as "Full".

### AC-05.5 — A slot whose cut-off passes before submission is rejected

> **Given** the student loaded the slot screen at 11:58 with 12:00–12:15 selectable
> **And** the current time is now 12:01, past that slot's cut-off
> **When** the student submits the order for the slot 12:00–12:15
> **Then** the order is not created
> **And** a message states that the pickup time has closed
> **And** the student is returned to the slot screen to choose another slot.

### AC-05.6 — Capacity is never exceeded under simultaneous submission

> **Given** the slot 12:30–12:45 has exactly 1 remaining place
> **When** two students submit an order for that slot at the same moment
> **Then** exactly one order is created
> **And** the other submission is rejected with a message that the slot is full
> **And** the number of active orders in that slot equals its capacity and never exceeds it.

---

## 8. AC-06 — Submit an order using a customer name and contact information

**MVP feature 6** · Requirements [FR-13, FR-14, FR-15](./Requirements-Specification-CanteenFlow-QuickPick.md#43-ordering-mvp-6-and-7)

### AC-06.1 — An order is submitted with valid details

> **Given** the order contains Chicken Rice with a quantity of 2
> **And** the selectable slot 12:15–12:30 has been chosen
> **When** the student enters the name "Nara" and the contact number `0800000000` and submits
> **Then** the order is created against Stall A and the slot 12:15–12:30
> **And** the confirmation screen is displayed.

### AC-06.2 — No account is required

> **Given** the student has never used the site before
> **When** the student completes the ordering flow
> **Then** at no point is a sign-up, password, or login required
> **And** only a name and a contact number are requested.

### AC-06.3 — A blank name is rejected

> **Given** the student has chosen a selectable slot
> **When** the student leaves the name field blank and submits
> **Then** the order is not created
> **And** a field-level message states that a name is required.

### AC-06.4 — An invalid contact number is rejected

> **Given** the student has entered the name "Nara"
> **When** the student enters a contact number that does not match the accepted phone-number format and submits
> **Then** the order is not created
> **And** a field-level message states that a valid contact number is required.

### AC-06.5 — An item that became unavailable is rejected

> **Given** the order contains Chicken Rice
> **And** the vendor has marked Chicken Rice unavailable since the item was added
> **When** the student submits the order
> **Then** the order is not created
> **And** a message identifies Chicken Rice as no longer available
> **And** the student is returned to the menu to amend the order.

### AC-06.6 — A rejected submission stores nothing

> **Given** any submission is rejected under AC-05.4, AC-05.5, AC-06.3, AC-06.4, or AC-06.5
> **When** the rejection is shown
> **Then** no order record and no order line record exist for that submission
> **And** no slot capacity has been consumed.

---

## 9. AC-07 — Receive an order number and confirmation

**MVP feature 7** · Requirements [FR-16, FR-17](./Requirements-Specification-CanteenFlow-QuickPick.md#43-ordering-mvp-6-and-7)

### AC-07.1 — An order number is issued

> **Given** an order has been created successfully
> **When** the confirmation screen is displayed
> **Then** an order number is shown prominently
> **And** that order number is not already in use by any other order.

### AC-07.2 — The confirmation shows the order details

> **Given** the confirmation screen is displayed for the order placed in AC-06.1
> **When** the student reads the screen
> **Then** it shows the order number, the stall name "Stall A", the pickup slot 12:15–12:30, the line
> "Chicken Rice × 2", and the order total THB 90.

### AC-07.3 — Capacity is consumed at creation

> **Given** the slot 12:15–12:30 showed a remaining capacity of 6 before submission
> **When** the order is created
> **Then** the slot shows a remaining capacity of 5 on the next view of the slot screen.

### AC-07.4 — The confirmation leads to tracking

> **Given** the confirmation screen is displayed
> **When** the student selects the tracking link
> **Then** the tracking view for that order number is opened.

---

## 10. AC-08 — Track status as Received, Preparing, or Ready

**MVP feature 8** · Requirements [FR-18, FR-19, FR-20](./Requirements-Specification-CanteenFlow-QuickPick.md#44-order-tracking-mvp-8)

### AC-08.1 — A new order starts as Received

> **Given** an order has just been created
> **When** the student opens the tracking view for that order
> **Then** the status is shown as "Received".

### AC-08.2 — Status changes are visible to the student

> **Given** the student is tracking an order whose status is "Received"
> **And** the vendor advances it to "Preparing"
> **When** the student refreshes the tracking view
> **Then** the status is shown as "Preparing".

### AC-08.3 — Ready is shown on completion

> **Given** the vendor has advanced the order to "Ready"
> **When** the student views the tracking view
> **Then** the status is shown as "Ready"
> **And** the student is told to collect the order at the stall using the order number.

### AC-08.4 — Context is shown alongside the status

> **Given** the student is on the tracking view
> **When** the view is displayed
> **Then** it shows the order number, the stall name, and the pickup slot time range in addition to the status.

### AC-08.5 — Tracking requires the matching contact number

> **Given** a valid order number is entered
> **When** the contact number entered does not match the one recorded on that order
> **Then** the order details are not shown
> **And** a message states that the order number and contact number do not match.

### AC-08.6 — An unknown order number

> **Given** an order number that does not exist is entered
> **When** the student submits the tracking form
> **Then** a message states that no matching order was found
> **And** no order details are displayed.

---

## 11. AC-09 — Vendor dashboard for orders and menu availability

**MVP feature 9** · Requirements [FR-21 – FR-26](./Requirements-Specification-CanteenFlow-QuickPick.md#45-vendor-dashboard-mvp-9)

### AC-09.1 — The dashboard requires sign-in

> **Given** a person is not signed in as a vendor
> **When** they open the vendor dashboard URL
> **Then** the dashboard is not shown
> **And** they are asked to sign in.

### AC-09.2 — A vendor sees only their own stall

> **Given** the vendor of Stall A is signed in
> **And** orders exist for both Stall A and another stall
> **When** the dashboard is displayed
> **Then** only orders belonging to Stall A are listed
> **And** no data belonging to any other stall is shown.

### AC-09.3 — Orders are grouped by pickup slot

> **Given** Stall A has orders in the slots 12:00–12:15 and 12:15–12:30
> **When** the vendor views the dashboard
> **Then** the orders are grouped under their pickup slot
> **And** the groups are ordered by slot start time
> **And** each order shows its order number, customer name, items with quantities, and current status.

### AC-09.4 — An order is advanced to Preparing

> **Given** an order of Stall A has the status "Received"
> **When** the vendor selects the action to start preparing it
> **Then** the status becomes "Preparing" in a single action
> **And** the change is visible to the student on the tracking view.

### AC-09.5 — An order is advanced to Ready

> **Given** an order of Stall A has the status "Preparing"
> **When** the vendor selects the action to mark it ready
> **Then** the status becomes "Ready" in a single action.

### AC-09.6 — Status cannot move backwards

> **Given** an order has the status "Ready"
> **When** the vendor views that order
> **Then** no control is offered that would return it to "Preparing" or "Received".

### AC-09.7 — An item is marked unavailable

> **Given** Chicken Rice is marked available
> **When** the vendor toggles Chicken Rice to unavailable
> **Then** the item is saved as unavailable in a single action
> **And** a student opening the menu of Stall A afterwards sees Chicken Rice labelled "Unavailable" and cannot add it.

### AC-09.8 — An item is marked available again

> **Given** Beef Noodles is marked unavailable
> **When** the vendor toggles Beef Noodles to available
> **Then** a student opening the menu of Stall A afterwards can add Beef Noodles to an order.

### AC-09.9 — Availability does not affect placed orders

> **Given** an existing order contains Chicken Rice
> **When** the vendor marks Chicken Rice unavailable
> **Then** the existing order still shows Chicken Rice with its original quantity and price.

### AC-09.10 — Slot capacity is visible to the vendor

> **Given** the vendor of Stall A is signed in
> **When** the vendor views the stall's pickup slots
> **Then** each slot shows its capacity and its remaining capacity.

---

## 12. Cross-cutting criteria

### AC-X1 — Mobile layout

> **Given** the site is opened on a screen 360 px wide
> **When** any screen in the ordering flow is displayed
> **Then** the content fits the width without horizontal scrolling
> **And** every interactive control has a touch target of at least 44 × 44 px.
>
> Traces to [NFR-01, NFR-02](./Requirements-Specification-CanteenFlow-QuickPick.md#51-usability).

### AC-X2 — Slot state is not conveyed by colour alone

> **Given** the pickup slot screen is displayed
> **When** a slot is full or closed
> **Then** its state is stated in text as well as indicated by colour.
>
> Traces to [NFR-05](./Requirements-Specification-CanteenFlow-QuickPick.md#51-usability).

### AC-X3 — Order creation is atomic

> **Given** an order submission fails partway through
> **When** the database is inspected
> **Then** neither the order nor any of its line items exists
> **And** no slot capacity has been consumed.
>
> Traces to [NFR-07](./Requirements-Specification-CanteenFlow-QuickPick.md#52-reliability-and-data-integrity).

### AC-X4 — No payment data is collected

> **Given** a student completes the entire ordering flow
> **When** every screen and every stored record is inspected
> **Then** no card number, wallet identifier, or other payment detail has been requested or stored.
>
> Traces to [NFR-10](./Requirements-Specification-CanteenFlow-QuickPick.md#53-security-and-privacy).

---

## 13. Coverage summary

| MVP feature | Acceptance criterion | Scenarios | Requirements covered |
| --- | --- | --- | --- |
| 1. Browse campus food stalls | [AC-01](#3-ac-01--browse-campus-food-stalls) | 4 | FR-01, FR-02, FR-03 |
| 2. View menu items, prices, images, availability | [AC-02](#4-ac-02--view-menu-items-prices-images-and-availability) | 4 | FR-04, FR-05, FR-06 |
| 3. Select items and quantities | [AC-03](#5-ac-03--select-items-and-quantities) | 6 | FR-07, FR-08 |
| 4. View pickup slots with remaining capacity | [AC-04](#6-ac-04--view-pickup-slots-with-remaining-capacity) | 4 | FR-09 |
| 5. Prevent selection of full or expired slots | [AC-05](#7-ac-05--prevent-selection-of-full-or-expired-pickup-slots) | 6 | FR-10, FR-11, FR-12 |
| 6. Submit an order with name and contact | [AC-06](#8-ac-06--submit-an-order-using-a-customer-name-and-contact-information) | 6 | FR-13, FR-14, FR-15 |
| 7. Receive an order number and confirmation | [AC-07](#9-ac-07--receive-an-order-number-and-confirmation) | 4 | FR-16, FR-17 |
| 8. Track Received / Preparing / Ready | [AC-08](#10-ac-08--track-status-as-received-preparing-or-ready) | 6 | FR-18, FR-19, FR-20 |
| 9. Vendor dashboard | [AC-09](#11-ac-09--vendor-dashboard-for-orders-and-menu-availability) | 10 | FR-21 – FR-26 |
| Cross-cutting | [AC-X1 – AC-X4](#12-cross-cutting-criteria) | 4 | NFR-01, NFR-02, NFR-05, NFR-07, NFR-10 |

> **Status.** These criteria have not been executed. No pass, fail, or partial result is claimed for any
> scenario in this document.
