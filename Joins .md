Joins are used to combine data from two or more tables based on a related column.
## Topics
33.`Relationships` — Understand how tables are connected
34. `INNER JOIN` — Return matching rows from both tables
35. `LEFT JOIN` — Return all rows from the left table and matching rows from the right table
36. `RIGHT JOIN` — Return all rows from the right table and matching rows from the left table
37. `FULL OUTER JOIN` — Return matching and non-matching rows from both tables
38. `Self Join` — Join a table with itself
39.` Multiple-table Joins` — Join more than two tables
-------------------------------------------------------------------------------------------------------------

## Tables Used

We will use the following tables for all examples.

### Employees Table

| employee_id | first_name | department_id | manager_id |
|---:|---|---:|---:|
| 1 | John | 10 | NULL |
| 2 | Priya | 20 | 1 |
| 3 | Rahul | 10 | 1 |
| 4 | Anita | 30 | 2 |
| 5 | David | 40 | 1 |
| 6 | Sarah | NULL | 2 |

### Departments Table

| department_id | department_name |
|---:|---|
| 10 | IT |
| 20 | HR |
| 30 | Finance |
| 50 | Marketing |

### Projects Table

| project_id | project_name | employee_id |
|---:|---|---:|
| 101 | Website | 1 |
| 102 | Database | 3 |
| 103 | Payroll | 4 |
| 104 | Mobile App | 7 |

**Note:** These tables intentionally contain unmatched values so you can understand how different joins work.

----------------------------------------------------------------------------------------------------------------

## 33. What Is a Relationship?

**Explanation:** A relationship connects two tables through a related column.

For example, the `department_id` column connects the `employees` table with the `departments` table.

### Example

```sql
SELECT employees.first_name, departments.department_name
FROM employees
INNER JOIN departments
ON employees.department_id = departments.department_id;
```
**Remember:** The related columns do not need to have the same column name, but their values and data types must be compatible for the intended match.
----------------------------------------------------------------------------------------------------------------
## 34. INNER JOIN

**Explanation:** Returns only rows that have matching values in both tables.

### Example: Employees with their departments

```sql
SELECT employees.first_name, departments.department_name
FROM employees
INNER JOIN departments
ON employees.department_id = departments.department_id;
```

**Expected Output**

| first_name | department_name |
|---|---|
| John | IT |
| Priya | HR |
| Rahul | IT |
| Anita | Finance |
**Remember:** `INNER JOIN` returns only matching rows.
----------------------------------------------------------------------------------------------------------------
## 35. LEFT JOIN

**Explanation:** Returns all rows from the left table and matching rows from the right table. If there is no match, the right table's columns contain `NULL`.

### Example: Show all employees and their departments

```sql
SELECT employees.first_name, departments.department_name
FROM employees
LEFT JOIN departments
ON employees.department_id = departments.department_id;
```

**Expected Output**

| first_name | department_name |
|---|---|
| John | IT |
| Priya | HR |
| Rahul | IT |
| Anita | Finance |
| David | NULL |
| Sarah | NULL |

**Remember:** The left table is the table written before `LEFT JOIN`.
----------------------------------------------------------------------------------------------------------------
## 36. RIGHT JOIN

**Explanation:** Returns all rows from the right table and matching rows from the left table. If there is no match, the left table's columns contain `NULL`.

### Example: Show all departments and their employees

```sql
SELECT employees.first_name, departments.department_name
FROM employees
RIGHT JOIN departments
ON employees.department_id = departments.department_id;
```

**Expected Output**

| first_name | department_name |
|---|---|
| John | IT |
| Rahul | IT |
| Priya | HR |
| Anita | Finance |
| NULL | Marketing |

**Remember:** The right table is the table written after `RIGHT JOIN`.
----------------------------------------------------------------------------------------------------------------
## 37. FULL OUTER JOIN

**Explanation:** Returns all matching rows and all non-matching rows from both tables.

### Example: Show all employees and all departments

```sql
SELECT employees.first_name, departments.department_name
FROM employees
FULL OUTER JOIN departments
ON employees.department_id = departments.department_id;
```

**Expected Output**

| first_name | department_name |
|---|---|
| John | IT |
| Priya | HR |
| Rahul | IT |
| Anita | Finance |
| David | NULL |
| Sarah | NULL |
| NULL | Marketing |

**Remember:** MySQL does not directly support `FULL OUTER JOIN`. In MySQL, you can combine a `LEFT JOIN` with a `RIGHT JOIN` using `UNION` to achieve similar results.
----------------------------------------------------------------------------------------------------------------
## 38. Self Join

**Explanation:** A self join joins a table with itself. It is useful when rows in the same table are related, such as employees and their managers.

### Example: Show employees and their managers

```sql
SELECT
    e.first_name AS employee,
    m.first_name AS manager
FROM employees e
LEFT JOIN employees m
ON e.manager_id = m.employee_id;
```

**Expected Output**

| employee | manager |
|---|---|
| John | NULL |
| Priya | John |
| Rahul | John |
| Anita | Priya |
| David | John |
| Sarah | Priya |

**Remember:** A self join uses aliases to distinguish between two roles played by the same table.
----------------------------------------------------------------------------------------------------------------
## 39. Multiple-Table Joins

**Explanation:** Multiple-table joins combine data from three or more tables.

### Example: Show employees, their departments, and their projects

```sql
SELECT
    e.first_name,
    d.department_name,
    p.project_name
FROM employees e
LEFT JOIN departments d
ON e.department_id = d.department_id
LEFT JOIN projects p
ON e.employee_id = p.employee_id;
```

**Expected Output**

| first_name | department_name | project_name |
|---|---|---|
| John | IT | Website |
| Priya | HR | NULL |
| Rahul | IT | Database |
| Anita | Finance | Payroll |
| David | NULL | NULL |
| Sarah | NULL | NULL |

**Remember:** Each join needs an appropriate `ON` condition to connect the tables.
----------------------------------------------------------------------------------------------------------------
## Quick Revision
| SQL concept | Meaning |
|---|---|
| Relationship | Connects related data between tables |
| `INNER JOIN` | Returns matching rows only |
| `LEFT JOIN` | Returns all left-table rows and matches |
| `RIGHT JOIN` | Returns all right-table rows and matches |
| `FULL OUTER JOIN` | Returns all rows from both tables |
| Self Join | Joins a table with itself |
| Multiple-table Joins | Joins three or more tables |
----------------------------------------------------------------------------------------------------------------
