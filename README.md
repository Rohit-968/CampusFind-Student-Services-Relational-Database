<div align="center">

<img src="https://img.shields.io/badge/SQL-PostgreSQL-003B57?style=for-the-badge&logo=postgresql&logoColor=white"/>
<img src="https://img.shields.io/badge/Schema-3NF%20Normalized-0078D4?style=for-the-badge&logo=databricks&logoColor=white"/>
<img src="https://img.shields.io/badge/Design-ER%20Modeling-6A0DAD?style=for-the-badge"/>
<img src="https://img.shields.io/badge/Queries-Search%20%7C%20Filter%20%7C%20Aggregate-FF6B35?style=for-the-badge"/>
<img src="https://img.shields.io/badge/License-MIT-brightgreen?style=for-the-badge"/>

# 🎓 CampusFind — Student Services Relational Database

**A fully normalized relational database system that lets students discover, filter, and retrieve local services — from cafeterias to gyms — through structured SQL on a production-grade schema designed from first principles.**

[**Schema Diagrams**](#-schema-diagrams) · [**Queries**](#-queries-implemented) · [**Project Report**](report.pdf) · [**Roadmap**](#-roadmap)

---

</div>

## 📌 The Problem

Students navigating a new campus or city face a fragmented, unstructured landscape of services. Finding a nearby gym open after 6PM, or comparing food outlets by student rating, typically means scattered Google searches and word-of-mouth — not structured, reliable data.

**CampusFind solves that** with a fully relational backend: a normalized schema, typed constraints, and expressive SQL queries that return ranked, filtered, and aggregated service results in milliseconds.

---

## 🏗️ System Architecture

```
Conceptual Design (ER Model)
        │
        ▼
┌─────────────────────────┐
│  Relational Schema      │  ← 3NF normalization · referential integrity
│  (schema.sql)           │    primary keys · foreign keys · constraints
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────────┐
│  Data Population        │  ← Seed data across 4 service categories
│                         │    Students, locations, ratings, access logs
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────────┐
│  Query Layer            │  ← Search · Filter · Aggregation
│  (queries.sql)          │    Ranked recommendations per student profile
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────────┐
│  Reporting & Outputs    │  ← Documented results · business interpretation
│  (report.pdf)           │    Schema diagrams · sample query screenshots
└─────────────────────────┘
```

---

## 🗃️ Database Design

### Entity-Relationship Model

Four core entities, carefully modeled before a single line of SQL was written:

| Entity | Key Attributes |
|---|---|
| `Student` | student_id, name, department, year, campus_zone |
| `Service` | service_id, name, category_id, location_id, rating, hours |
| `Category` | category_id, category_name, description |
| `Location` | location_id, area_name, coordinates, distance_from_campus |

Relationships capture which students access which services, under what category and location context — with junction tables handling many-to-many access history.

### Normalization

The schema is normalized to **Third Normal Form (3NF)**:
- **1NF** — All attributes are atomic; no repeating groups
- **2NF** — No partial dependencies on composite keys
- **3NF** — No transitive dependencies; every non-key attribute depends only on the primary key

This eliminates data redundancy, enforces referential integrity, and ensures clean aggregation across all service types.

### Service Categories

| Category | Examples |
|---|---|
| 🍽️ Food Outlets | Cafeterias, restaurants, food delivery counters |
| 🛍️ Shopping | Malls, bookstores, convenience stores |
| 🏋️ Sports Facilities | Gyms, courts, swimming pools, recreation centers |
| 🏥 General Services | Libraries, health centers, transport hubs |

---

## 📐 Schema Diagrams

**Entity-Relationship Diagram**
<img width="975" height="689" alt="ER Diagram" src="https://github.com/user-attachments/assets/c1be4e4d-466b-4de3-aadb-797bdccfbdbe"/>

**Relational Schema**
<img width="975" height="784" alt="Relational Schema" src="https://github.com/user-attachments/assets/21dfa663-47dc-422d-a7e1-f590f5905519"/>

**Query Output Sample**
<img width="975" height="586" alt="Query Output" src="https://github.com/user-attachments/assets/19845720-b1e1-4b9c-90c9-bca9bf316946"/>

---

## 🔍 Queries Implemented

| Query Type | Description | SQL Feature Used |
|---|---|---|
| **Search by Category** | Retrieve all services under Food / Sports / Shopping | `WHERE` + `JOIN` |
| **Filter by Rating** | Return services above a minimum rating threshold | `WHERE rating >= ?` |
| **Filter by Proximity** | Narrow results by distance from campus zone | `ORDER BY distance` |
| **Availability Filter** | Show only services open within a given time window | `BETWEEN` on hours |
| **Aggregation — Count** | Number of services per category | `GROUP BY` + `COUNT` |
| **Aggregation — Average** | Mean rating per location area | `GROUP BY` + `AVG` |
| **Ranked Recommendations** | Top-rated services most accessed by similar students | `JOIN` + `ORDER BY` + `LIMIT` |
| **Student Access History** | Services a specific student has visited, with frequency | Self-join on access log |

Full SQL with annotated sample outputs is documented in [`report.pdf`](report.pdf) and [`queries.sql`](queries.sql).

---

## 🚀 Quickstart

```bash
# 1. Clone the repository
git clone https://github.com/your-username/campusfind.git
cd campusfind

# 2. Set up the database (PostgreSQL or SQLite)
psql -U your_user -d your_db -f schema.sql

# 3. Seed with sample data
psql -U your_user -d your_db -f seed_data.sql

# 4. Run queries
psql -U your_user -d your_db -f queries.sql

# 5. View documented outputs
open report.pdf
```

> Compatible with PostgreSQL 14+ and SQLite 3.x. For SQLite, minor syntax adjustments apply — see comments in `schema.sql`.

---

## 📁 Repository Structure

```
campusfind/
│
├── schema.sql              # Table definitions, constraints, foreign keys
├── seed_data.sql           # Sample data population across all entities
├── queries.sql             # All search, filter, aggregation, and recommendation queries
│
├── diagrams/
│   ├── er_diagram.png      # Entity-Relationship conceptual model
│   └── relational_schema.png  # Final mapped relational schema
│
├── sample_outputs/         # Screenshots of executed query results
│   ├── search_query.png
│   ├── aggregation_query.png
│   └── recommendation_query.png
│
├── report.pdf              # Full project report: design decisions, outputs, interpretation
└── README.md
```

---

## 💡 Design Decisions

**Why 3NF over denormalization?**
At this scale, query performance is not a bottleneck. 3NF was chosen to demonstrate correct database engineering practice — every design choice maps to a real-world justification, not just passing requirements.

**Why separate `Location` as its own entity?**
Multiple services share the same physical area. Embedding location inside `Service` would create update anomalies — if an area is renamed, every service row would need updating. The normalized design fixes this with a single update to the `Location` table.

**Why a junction table for student-service access?**
A student can access many services; a service is accessed by many students. Many-to-many relationships require an associative entity — `StudentServiceAccess` — to avoid data duplication and enable access history queries.

---

## 🔭 Roadmap

- [ ] Web front-end (Flask / Django) for non-SQL users to query through a UI
- [ ] Stored procedures for automated rating recalculation on new reviews
- [ ] Triggers to log service access events automatically
- [ ] Integration with live location APIs for real-time proximity filtering
- [ ] Role-based access control — admin vs. student query permissions

---

## 📄 License

MIT — see [LICENSE](LICENSE) for details.

---

<div align="center">

**Built to demonstrate that clean database design is a foundation skill — not an afterthought.**

⭐ Star this repo if it helped you think more clearly about relational modeling.

</div>







