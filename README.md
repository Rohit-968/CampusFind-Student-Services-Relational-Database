# Student Service Database Application

**Relational database system that enables students to discover, filter, and retrieve local services — food outlets, shopping, and sports facilities — through structured SQL queries on a fully normalized schema.**

[![SQL](https://img.shields.io/badge/SQL-Relational%20DB-003B57?style=flat-square&logo=postgresql&logoColor=white)]()
[![Design](https://img.shields.io/badge/Design-ER%20Modeling-0078D4?style=flat-square)]()
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

---

## What it does

Students query a structured local services database — searching by category, filtering by proximity or rating, and receiving ranked recommendations — without navigating unstructured data. The system demonstrates the full database engineering lifecycle from conceptual model to executed query output.

---

## Database design

**Entity-Relationship model**
Core entities: `Student`, `Service`, `Category`, `Location`. Relationships capture which students access which services, under what category and location context.

**Relational schema**
Normalized to 3NF — eliminates redundancy, enforces referential integrity, and ensures clean aggregation across service types.

**Service categories covered**

| Category | Examples |
|---|---|
| Food outlets | Cafeterias, restaurants, delivery |
| Shopping | Malls, convenience stores |
| Sports facilities | Gyms, courts, recreation centers |
| General services | Libraries, health centers, transport |

---

## Queries implemented

| Query type | Purpose |
|---|---|
| Search | Retrieve services by name, category, or location |
| Filter | Narrow results by rating, distance, or availability |
| Aggregation | Count services per category, average ratings by area |
| Recommendation | Surface top-rated or most-accessed services per student profile |

Full query listing with sample outputs is in the [project report](report.pdf).


## Schema Diagrams

<img width="975" height="689" alt="image" src="https://github.com/user-attachments/assets/c1be4e4d-466b-4de3-aadb-797bdccfbdbe" />
<img width="975" height="784" alt="image" src="https://github.com/user-attachments/assets/21dfa663-47dc-422d-a7e1-f590f5905519" />
<img width="975" height="586" alt="image" src="https://github.com/user-attachments/assets/19845720-b1e1-4b9c-90c9-bca9bf316946" />

---

## Repository structure

```
student-service-db/
├── schema.sql          # Table definitions, constraints, foreign keys
├── queries.sql         # All implemented search, filter, and aggregation queries
├── er_diagram.png      # Entity-Relationship diagram
├── report.pdf          # Full project report with schema, outputs, and interpretation
└── sample_outputs/     # Screenshots of executed query results
```

---

## Key deliverables

- Normalized relational schema designed from first principles via ER modeling
- SQL queries covering search, aggregation, and ranked recommendations
- Documented query outputs with interpretation of results
- End-to-end database lifecycle: conceptual design → schema → query → reporting

---

## Roadmap

- [ ] Web front-end (Flask / Django) for non-SQL query access
- [ ] Stored procedures and triggers for automated service updates
- [ ] Integration with live location APIs for real-time proximity filtering

---

## License

MIT — see [LICENSE](LICENSE) for details.







