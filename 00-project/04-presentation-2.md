---
project_outline: "[[01-project-outline]]"
title: "Smart Parking Garage Management System — Presentation 2"
text-scale: 100%
table-scale: 90%
---

<!-- @set-align center -->
<!-- @set-scale 100% -->
# Smart Parking Garage Management System

Specification and implementation plan

Author: **Umut Can Birbir**  
Neptun: **DUJ3ZD**  
Supervisor: **Anett LENART**  
Project ID: **2026-LA-04**

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Specification summary

- A database system with a small web interface.
- First MVP: search, reserve, view and cancel.
- Later work includes visits, fees and operator tools.
- Current stage: planning before implementation.

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Main user journeys

1. The customer selects a garage and time interval.
2. The system searches for available spaces.
3. The customer chooses a vehicle and confirms.
4. The customer views or cancels an eligible booking.

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Main requirements

- Customers can access only their own records.
- Operators record vehicle entry and exit.
- The database calculates fees from the actual stay.
- Occupied spaces and maintenance block conflicting use.

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Initial technical proposal

- Oracle Database with SQL and PL/SQL.
- Python and FastAPI for the application layer.
- python-oracledb for database access.
- Simple HTML pages with CSS and Jinja2.

<!-- Sources: ./02-specification.md; https://python-oracledb.readthedocs.io/en/latest/user_guide/installation.html; https://fastapi.tiangolo.com/advanced/templates/ -->

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Architecture and responsibilities

| Layer | Responsibility |
| --- | --- |
| Web pages | Forms, results and feedback |
| FastAPI | User identity and database calls |
| Oracle / PL/SQL | Rules, transactions and stored data |

<!-- Source: ./02-specification.md, section 8 -->

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Data model proposal

- 19 related tables in the initial proposal.
- Garages contain floors and parking spaces.
- Vehicles link customers to reservations and visits.
- Keys and constraints protect data relationships.

<!-- Source: ./02-specification.md, section 8.3 -->

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Planned screens

- Search: garage, dates and available spaces.
- Confirmation: selected space, vehicle and booking.
- My reservations: details and cancellation.
- Operator: occupancy, entry/exit and reports.

<!-- Source: ./02-specification.md, section 5 -->

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Reservation safety

- Lock the selected space during booking.
- Recheck availability before saving.
- Save the whole operation or undo it.
- Compare two transaction approaches in tests.

<!-- Source: ./02-specification.md, section 8.4 -->

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Testing and evaluation plan

- Test workflows, permissions and failed operations.
- Check conflicting bookings from parallel clients.
- Generate 100,000+ reservations and 100,000+ events.
- Prepare 12 queries and measure 5 optimizations.

<!-- Source: ./02-specification.md, sections 6 and 8 -->

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Semester-2 implementation plan

- **Weeks 1–2:** Verify Oracle and the Python connection.
- **Weeks 3–4:** Complete the ERD and schema scripts.
- **Weeks 5–6:** Build and test the reservation MVP.

<!-- @scale 85% -->
Proposed schedule, subject to course dates and feedback.

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Later milestones

- **Weeks 7–8:** Entry/exit and fee calculation.
- **Weeks 9–10:** Subscriptions, payments and maintenance.
- **Weeks 11–12:** Reports, test data and benchmarks.
- **Weeks 13–14:** Improvements, fixes and documentation.

---

<!-- @set-align left -->
<!-- @set-scale 100% -->
## Open risks and next steps

- Verify Oracle access and driver compatibility.
- Confirm entry and pricing policies with the supervisor.
- Review the design and refine the schedule.
- Set up GitHub Projects and begin the first milestone.

<!-- Sources: ./01-project-outline.md; ./02-specification.md -->
