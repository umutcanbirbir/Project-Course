---
project_outline: "[[01-project-outline]]"
title: "Smart Parking Garage Management System"
text-scale: 140%
---

<!-- 5xl -->
<!-- @set-scale 100% -->
# Smart Parking Garage Management System

Author: **Umut Can Birbir**  
Neptun: **DUJ3ZD**  
Supervisor: **Anett LENART**  
Project ID: **2026-LA-04**

---

<!-- 2xl -->
<!-- @set-scale 100% -->
## Problem

- Customers can request the same space at the same time.
- Reservations must remain consistent with occupation and maintenance.
- Entry, exit, subscriptions, and tariffs must produce a reproducible fee.
- The database must enforce these rules during concurrent operations.

---

<!-- 2xl -->
<!-- @set-scale 100% -->
## Project goal

A relational parking-garage system with database-enforced rules and a small web interface.

- Customers search, reserve, cancel, and view their own reservations.
- Operators register entry/exit and monitor occupancy.
- Transactions prevent conflicting allocations.
- SQL measurements support the final design decisions.

---

<!-- 2xl -->
<!-- @set-scale 100% -->
## Target users

| User | Main needs |
| --- | --- |
| Customer | Available spaces and personal reservations |
| Operator | Entry/exit, occupancy, maintenance, and conflicts |
| Administrator | Accounts, garages, spaces, and pricing versions |

---

<!-- 2xl -->
<!-- @set-scale 100% -->
## Planned scope

- Garages, floors, spaces, and physical state history
- Customers, vehicles, and reservations
- Actual visits, tariffs, subscriptions, and demonstration payments
- Maintenance and basic operational reports
- Concurrency tests and SQL performance evaluation

---

<!-- 2xl -->
<!-- @set-scale 100% -->
## Initial user journey: reservation

1. Select a garage and a future interval.
2. Search and choose a suitable space.
3. Select a registered vehicle and confirm.
4. View the reservation or an availability conflict.
5. Cancel before the start if plans change.

The database rechecks availability when creating the reservation.

---

<!-- 2xl -->
<!-- @set-scale 100% -->
## Initial user journey: parking visit

1. The operator finds the confirmed reservation.
2. The database validates the entry window and physical space.
3. Entry opens a visit and marks the space occupied.
4. Exit closes the visit, calculates the fee, and releases the space.
5. The operator records a demonstration payment separately.

---

<!-- 2xl -->
<!-- @set-scale 100% -->
## Initial operating policies

- Reservation required, with a 15-minute arrival window.
- Customer cancellation before the reservation starts.
- Conflicting maintenance requests are rejected.
- Overstays block physical entry for the next vehicle.
- Fees use the entry-time tariff and actual duration.

These are proposed policies for supervisor review.

---

<!-- 2xl -->
<!-- @set-scale 100% -->
## Database study and evaluation

- Compare row locking with guarded SERIALIZABLE transactions.
- Both candidates use shared resources and atomic validation.
- Generate at least 100,000 reservations and 100,000 parking events.
- Create at least ten complex SQL queries.
- Measure at least five queries before and after optimization.

<!-- @note -->
> The guarded alternative updates common resource rows before checking availability and retries the entire transaction on serialization failure. Bare SERIALIZABLE plus an overlap query is insufficient. This is a proposed design to test, not a completed benchmark. Reference: [Oracle concurrency documentation](https://docs.oracle.com/en/database/oracle/oracle-database/19/cncpt/data-concurrency-and-consistency.html).

---

<!-- 2xl -->
<!-- @set-scale 100% -->
## Initial architecture

- Browser pages support customer and operator workflows.
- A FastAPI service verifies identity and manages transactions.
- Oracle PL/SQL validates rules, changes state, and calculates fees.
- Constraints, views, and audit records support consistency.

Oracle and FastAPI are the proposed technology direction.

---

<!-- 2xl -->
<!-- @set-scale 100% -->
## First MVP and scope boundaries

The first milestone covers availability search, safe reservation creation/cancellation, and a personal reservation page.

Later required milestones add entry/exit, fees, subscriptions, payments, maintenance, operator reports, and large-scale evaluation.

Mobile apps, real payments, recognition hardware, charging, dynamic pricing, and 3D visualization remain outside scope.

---

<!-- 2xl -->
<!-- @set-scale 100% -->
## Next steps

1. Review the proposed policies with the supervisor.
2. Register the repository and planning board.
3. Validate the Oracle environment and driver.
4. Design the attribute-level ERD and normalize the schema.
5. Build the first database and web MVP.

Related documents: [Outline](./01-project-outline.md) and [Specification](./02-specification.md).
