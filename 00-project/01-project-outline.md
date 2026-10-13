---
name: "Umut Can Birbir"
neptun: "DUJ3ZD"
id: 2026-LA-04
github: "https://github.com/umutcanbirbir/Project-Course"
trello: "https://trello.com/b/oCicOEBk"
---

# Smart Parking Garage Management System

A parking garage must coordinate spaces, customers, vehicles, reservations, entries and exits, tariffs, subscriptions, maintenance, and payments. Concurrent requests can produce double booking or inconsistent records unless the database enforces the relevant rules. This project will design and implement a relational database with a small customer/operator web interface. Database design, PL/SQL business logic, transaction management, concurrent access, and measured SQL performance form the main thesis contribution.

## Objectives

- **Primary objective:** Deliver a documented, reproducible system supporting the core operation of one or more parking garages.
- **Database objective:** Design at least twelve related tables in at least third normal form, with keys, referential integrity, uniqueness constraints, and database-enforced business rules.
- **Concurrency objective:** Prevent overlapping reservations and inconsistent entry, exit, cancellation, or maintenance changes under parallel access.
- **Research objective:** Compare explicit row locking with guarded serializable transactions, then justify the choice using consistency, latency, and throughput measurements.
- **Performance objective:** Generate at least 100,000 reservations and at least 100,000 parking-event records reproducibly; develop at least ten complex queries and measure at least five before and after optimization.
- **Target users / stakeholders:** Customers, parking-garage operators, administrators, and the organization operating the garages.
- **Measurable success criteria:**
  - Customers can search by garage/interval, create and cancel eligible reservations, and view only their own reservations.
  - Conflicting parallel requests produce no overlapping committed blocking allocations.
  - Database procedures perform entry/exit atomically, and database fee functions pass the documented examples.
  - Operators see occupancy, operational conflicts, and basic statistics.
  - Seeded test generation reaches the stated volume and passes integrity checks.
  - Query optimization and concurrency comparisons have reproducible measurements and interpreted plans.
- **Technical direction:** Oracle Database with SQL and PL/SQL is the proposed platform. A small FastAPI service and server-rendered interface will call database routines. The exact deployment version will be recorded after the environment prototype.
- **Constraints:** Critical rules remain in the database, the web scope stays limited, and credentials/secrets are excluded from version control.

## Scope

### In scope

- Garages, floors, space types, spaces, physical states, and state history.
- Customer accounts, operator/administrator roles, and registered vehicles.
- Availability search and concurrency-safe reservation creation/cancellation.
- Reservation-based entry/exit, parking events, and overstay conflict reporting.
- Versioned tariffs, deterministic fees, subscription plans and subscriptions.
- Recording demonstration payments without a live payment provider.
- Maintenance scheduling with database-enforced conflict checks.
- Customer reservation/history pages and a basic operator occupancy/reporting interface.
- Seeded data generation, complex reports, plan analysis, indexing, and benchmarks.
- Version-controlled source, setup instructions, tests, and documented limitations.

### Semester-2 MVP

The first working milestone includes the core schema, account/vehicle fixtures, availability search, safe reservation creation/cancellation, ownership checks, a minimal customer interface, and a two-session conflict test. Its acceptance condition is one complete search–reserve–view–cancel workflow with safe rejection of a competing reservation. Entry/exit, fees, payments, subscriptions, maintenance, operator reporting, and large-scale evaluation remain required later milestones before final thesis completion.

### Out of scope

- Walk-ins and automatic reassignment of conflicting reservations.
- Native mobile applications and detailed graphical/3D visualization.
- Real payment-provider integration, refunds, and accounting services.
- Automatic number-plate recognition and physical gate control.
- Charging-process management and demand-based dynamic pricing.

## Notes

The initial policies and test tariffs in the [specification](./02-specification.md) are proposed assumptions, not an assertion of supervisor approval or commercial pricing. Physical state is distinct from availability for a requested interval. Both concurrency candidates use common resource guards; bare SERIALIZABLE plus an overlap query is not sufficient protection. The service owns commit/rollback boundaries while PL/SQL owns validation and state changes.

Project documents live under `00-project/`. The first presentation introduces the problem, users, scope, and journeys. Implementation and measurement results will be produced in later milestones.
