# SQL Reference

SQL concepts and query patterns built for learning, practice, and quick revision.

---

## What is SQL?

**SQL = Structured Query Language**

SQL is a language used to communicate with and manage databases.
It allows us to:
- Store data
- Retrieve data
- Modify data
- Manage data efficiently
> **Database** = A place where data is stored  
> **SQL** = The language used to communicate with the database
---

## What is SQL Mainly Used For?

| Operation | SQL Command |
|---|---|
| Read data | `SELECT` |
| Add data | `INSERT` |
| Update data | `UPDATE` |
| Delete data | `DELETE` |
| Create tables | `CREATE TABLE` |
| Filter data | `WHERE` |
| Sort data | `ORDER BY` |
| Combine tables | `JOIN` |
| Group and calculate data | `GROUP BY`, `COUNT()`, `SUM()` |

---

## Quick Example

```sql
SELECT name, age
FROM students
WHERE age > 18
ORDER BY age;
