---
project_outline: "[[01-project-outline]]"
title: "Smart Parking Garage Management System"
text-scale: 100%
table-scale: 90%
---

<!-- @set-align center -->
<!-- @set-scale 100% -->
# Smart Parking Garage Management System

Author: **Umut Can Birbir**  
Neptun: **DUJ3ZD**  
Supervisor: **Anett LENART**  
Project ID: **2026-LA-04**

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Problem

- Concurrent requests can double-book a space.
- Reservations can conflict with occupancy or maintenance.
- Tariffs and subscriptions affect the final parking fee.

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Project goal

A relational parking system with a small web interface.

- Customers search, reserve, cancel and view their bookings.
- Operators manage entry, exit and occupancy.
- Database transactions prevent conflicting allocations.
- SQL measurements guide performance decisions.

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Target users

| User | Main needs |
| --- | --- |
| Customer | Availability and own reservations |
| Operator | Entry/exit, occupancy, maintenance, conflicts |
| Administrator | Accounts, garages, spaces, tariff versions |

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Planned scope

- Garages, floors, spaces and state history
- Customers, vehicles and reservations
- Visits, tariffs, subscriptions and demo payments
- Maintenance and operator reports
- Concurrency tests and SQL performance evaluation

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Reservation journey

1. Select a garage and a future interval.
2. Search for a suitable space.
3. Choose a registered vehicle and confirm.
4. See the booking or an availability conflict.
5. Cancel before the start if needed.

<!-- @scale 85% -->
The database rechecks availability when saving.

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Parking visit journey

1. The operator finds the confirmed booking.
2. The database checks entry time and space status.
3. Entry opens a visit and marks the space occupied.
4. Exit closes the visit, calculates the fee and releases the space.
5. The operator records a demo payment separately.

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Proposed operating policies

- Entry within 15 minutes of start and before reservation end.
- Customers can cancel before the reservation starts.
- An overstay blocks entry for the next vehicle.
- Fees use the entry-time tariff and actual duration.

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## MVP and scope boundaries

- **First MVP:** Search, reserve, view and cancel safely.
- **Later required:** Entry/exit, fees, subscriptions, demo payments, maintenance, reports and evaluation.
- **Out of scope:** Mobile apps, real payments, recognition hardware, charging, dynamic pricing and 3D.

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Next steps

1. Set up GitHub Projects and confirm course registration.
2. Validate Oracle and its application driver.
3. Design the ERD and normalize the schema.
4. Build and test the first MVP.

<!-- @note -->
> Related documents: [Outline](./01-project-outline.md) and [Specification](./02-specification.md).
