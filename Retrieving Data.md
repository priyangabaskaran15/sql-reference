This level covers SQL commands used to retrieve, filter, sort, and limit data 
# Sample Table
All queries in this level use an `employees` table.
```sql
CREATE TABLE employees (
    employee_id INT,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    department VARCHAR(50),
    job_title VARCHAR(50),
    salary INT,
    age INT,
    city VARCHAR(50),
    manager_id INT
);
```

Example data:

| ID | Name    | Department | Salary | Age | City      | Manager |
| -: | ------- | ---------- | -----: | --: | --------- | ------: |
|  1 | John    | IT         |  60000 |  25 | Chennai   |       5 |
|  2 | Priya   | HR         |  45000 |  28 | Bangalore |       6 |
|  3 | Rahul   | IT         |  70000 |  30 | Chennai   |       5 |
|  4 | Anita   | Finance    |  55000 |  32 | Mumbai    |       7 |
|  5 | David   | IT         |  90000 |  40 | Chennai   |    NULL |
|  6 | Sarah   | HR         |  85000 |  38 | Bangalore |    NULL |
|  7 | Michael | Finance    |  88000 |  42 | Mumbai    |    NULL |
|  8 | Arun    | Marketing  |  50000 |  27 | Delhi     |       9 |
|  9 | Emma    | Marketing  |  80000 |  36 | Delhi     |    NULL |
| 10 | Kiran   | IT         |  58000 |  26 | Chennai   |       5 |

---

# 13. WHERE

## Explanation

`WHERE` is used to **filter rows**.

It tells SQL:

> "Give me only the rows that satisfy this condition."

## Syntax

```sql
SELECT columns
FROM table
WHERE condition;
```

## Example

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

This returns only employees from the IT department.

--------------------------------------------------------------------------------------------------------------

# 14. Comparison Operators

Comparison operators allow us to compare values.

| Operator | Meaning                  |
| -------- | ------------------------ |
| `=`      | Equal to                 |
| `<>`     | Not equal to             |
| `>`      | Greater than             |
| `<`      | Less than                |
| `>=`     | Greater than or equal to |
| `<=`     | Less than or equal to    |

## Examples

### Equal to

```sql
SELECT *
FROM employees
WHERE department = 'HR';
```

### Greater than

```sql
SELECT *
FROM employees
WHERE salary > 60000;
```

### Less than

```sql
SELECT *
FROM employees
WHERE salary < 60000;
```

### Greater than or equal to

```sql
SELECT *
FROM employees
WHERE salary >= 60000;
```

### Less than or equal to

```sql
SELECT *
FROM employees
WHERE salary <= 60000;
```

### Not equal to

```sql
SELECT *
FROM employees
WHERE department <> 'IT';
```

-----------------------------------------------------------------------------------------------------------------

# 15. AND

## Explanation

`AND` means **all conditions must be true**.

## Example

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 60000;
```

This means:

> Find employees who work in IT **and** earn more than 60,000.

Both conditions must be true.

---

# 16. OR

## Explanation

`OR` means **at least one condition must be true**.

## Example

```sql
SELECT *
FROM employees
WHERE department = 'IT'
OR department = 'HR';
```

This returns employees who work in either IT or HR.
-----------------------------------------------------------------------------------------------------------------
# 17. NOT

## Explanation

`NOT` reverses a condition.

## Example

```sql
SELECT *
FROM employees
WHERE NOT department = 'IT';
```

This means:

> Find employees who are not in IT.

The following is another way to write it:

```sql
SELECT *
FROM employees
WHERE department <> 'IT';
```
-----------------------------------------------------------------------------------------------------------------
# 18. IN

## Explanation

`IN` is used when checking against **multiple possible values.**

Instead of:

```sql
WHERE department = 'IT'
OR department = 'HR'
OR department = 'Finance'
```

we can write:

```sql
WHERE department IN ('IT', 'HR', 'Finance')
```

## Example

```sql
SELECT *
FROM employees
WHERE department IN ('IT', 'HR', 'Finance');
```

This returns employees from IT, HR, or Finance.

## NOT IN

```sql
SELECT *
FROM employees
WHERE department NOT IN ('IT', 'HR');
```

This returns employees who are not in IT or HR.
-----------------------------------------------------------------------------------------------------------------
# 19. BETWEEN

## Explanation

`BETWEEN` checks whether a value falls within a **range**.

## Example

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 50000 AND 70000;
```

This finds employees earning between 50,000 and 70,000.

`BETWEEN` includes **both boundary values**.

So:

```sql
salary BETWEEN 50000 AND 70000
```

means:

```sql
salary >= 50000
AND salary <= 70000
```

## Another example

```sql
SELECT *
FROM employees
WHERE age BETWEEN 25 AND 30;
```
-----------------------------------------------------------------------------------------------------------------
# 20. LIKE

## Explanation

`LIKE` is used to search for patterns in text.

There are two important wildcards:

| Wildcard | Meaning                 |
| -------- | ----------------------- |
| `%`      | Zero or more characters |
| `_`      | Exactly one character   |

## Starts with A

```sql
SELECT *
FROM employees
WHERE first_name LIKE 'A%';
```

Finds names starting with A.

Example:

```text
Anita
Arun
```

## Ends with A

```sql
SELECT *
FROM employees
WHERE first_name LIKE '%a';
```

Finds names ending with A.

## Contains "an"

```sql
SELECT *
FROM employees
WHERE first_name LIKE '%an%';
```

Finds names containing `an`.

## Exactly 4 characters

```sql
SELECT *
FROM employees
WHERE first_name LIKE '____';
```

Each `_` represents exactly one character.
-----------------------------------------------------------------------------------------------------------------
# 21. IS NULL

## Explanation

`NULL` represents a missing or unknown value.

For example:

```text
manager_id = NULL
```

means there is no manager value recorded.

Do **not** use:

```sql
WHERE manager_id = NULL;
```

Use:

```sql
WHERE manager_id IS NULL;
```

## Example

```sql
SELECT *
FROM employees
WHERE manager_id IS NULL;
```

This finds employees who don't have a manager.

## IS NOT NULL

```sql
SELECT *
FROM employees
WHERE manager_id IS NOT NULL;
```

This finds employees who have a manager.
-----------------------------------------------------------------------------------------------------------------
# 22. ORDER BY

## Explanation

`ORDER BY` sorts the results.

### ASC

Ascending order:

```sql
SELECT *
FROM employees
ORDER BY salary ASC;
```

Lowest salary → highest salary.

### DESC

Descending order:

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

Highest salary → lowest salary.

## Example

```sql
SELECT first_name, salary
FROM employees
ORDER BY salary DESC;
```
This shows the highest-paid employees first.
-----------------------------------------------------------------------------------------------------------------
# 23. LIMIT

## Explanation

`LIMIT` controls how many rows SQL returns.

## Example

```sql
SELECT *
FROM employees
LIMIT 5;
```
Returns only 5 rows.

## Very useful combination

Find the 3 highest-paid employees:

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 3;
```
The process is:

```text
1. Sort salary from highest to lowest
2. Take only the first 3 rows
```
-----------------------------------------------------------------------------------------------------------------
# 24. DISTINCT

## Explanation

`DISTINCT` removes duplicate values from the result.

## Example

```sql
SELECT DISTINCT department
FROM employees;
```

Possible result:

```text
IT
HR
Finance
Marketing
```
Each department appears only once.

## Another example

```sql
SELECT DISTINCT city
FROM employees;
```

Returns the unique cities.
-----------------------------------------------------------------------------------------------------------------
# 25. Aliases

## Explanation

An alias gives a temporary name to a column or table.

The keyword used is `AS`.

## Column Alias

```sql
SELECT salary AS annual_salary
FROM employees;
```

The result column will be called `annual_salary`.

The actual database column is still called `salary`.

## Multiple aliases

```sql
SELECT
    first_name AS first_name,
    last_name AS last_name,
    salary AS annual_salary
FROM employees;
```
## Table Alias

```sql
SELECT e.first_name, e.salary
FROM employees AS e;
```

Here:

```text
employees → e
```

So:

```sql
e.first_name
```

means:

```sql
employees.first_name
```

Table aliases become especially useful when learning `JOIN`.
-----------------------------------------------------------------------------------------------------------------
# Combining Concepts

The real power of SQL comes from combining multiple commands.

## Example 1 — Highest-paid IT employees

```sql
SELECT first_name, salary
FROM employees
WHERE department = 'IT'
ORDER BY salary DESC
LIMIT 3;
```

Meaning:

> Find IT employees → sort by highest salary → show only 3.
-----------------------------------------------------------------------------------------------------------------
## Example 2 — Employees from specific cities

```sql
SELECT first_name, city, salary
FROM employees
WHERE city IN ('Chennai', 'Bangalore')
AND salary BETWEEN 50000 AND 90000
ORDER BY salary DESC;
```
Concepts used:

* `IN`
* `AND`
* `BETWEEN`
* `ORDER BY`
-----------------------------------------------------------------------------------------------------------------
## Example 3 — Names starting with A

```sql
SELECT *
FROM employees
WHERE first_name LIKE 'A%'
AND department <> 'IT';
```
Concepts used:

* `LIKE`
* `AND`
* `<>`
-----------------------------------------------------------------------------------------------------------------
## Example 4 — Unique cities

```sql
SELECT DISTINCT city
FROM employees
WHERE salary > 60000;
```
Concepts used:
* `DISTINCT`
* `WHERE`
* `>`

---

# SQL Query Order

Remember this basic structure:

```sql
SELECT columns
FROM table
WHERE condition
ORDER BY column
LIMIT number;
```

Example:

```sql
SELECT first_name, salary
FROM employees
WHERE department = 'IT'
AND salary > 55000
ORDER BY salary DESC
LIMIT 3;
```

Read it as:

> Select first name and salary
> from employees
> where department is IT
> and salary is greater than 55,000
> order by salary from highest to lowest
> and show only 3 rows.
-----------------------------------------------------------------------------------------------------------------
# Quick Revision

|  # | Topic                | Main Purpose                   |
| -: | -------------------- | ------------------------------ |
| 13 | `WHERE`              | Filter rows                    |
| 14 | Comparison operators | Compare values                 |
| 15 | `AND`                | All conditions must be true    |
| 16 | `OR`                 | At least one condition is true |
| 17 | `NOT`                | Reverse a condition            |
| 18 | `IN`                 | Match multiple values          |
| 19 | `BETWEEN`            | Search within a range          |
| 20 | `LIKE`               | Search text patterns           |
| 21 | `IS NULL`            | Find missing values            |
| 22 | `ORDER BY`           | Sort results                   |
| 23 | `LIMIT`              | Limit number of rows           |
| 24 | `DISTINCT`           | Remove duplicates              |
| 25 | `AS`                 | Create aliases                 |
-----------------------------------------------------------------------------------------------------------------
14. Find the 3 highest-paid IT employees.
15. Find employees from Chennai earning between 50,000 and 90,000, sorted by salary.

Try these first, then compare your answers with the SQL file.
