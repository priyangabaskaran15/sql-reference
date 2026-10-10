#Aggregation is used to summarize data in SQL.

| employee_id | first_name | department | salary |
|---:|---|---|---:|
| 1 | John | IT | 60000 |
| 2 | Priya | HR | 45000 |
| 3 | Rahul | IT | 70000 |
| 4 | Anita | Finance | 55000 |
| 5 | David | IT | 90000 |
| 6 | Sarah | HR | 85000 |
| 7 | Michael | Finance | 88000 |
| 8 | Arun | Marketing | 50000 |
| 9 | Emma | Marketing | 80000 |
| 10 | Kiran | IT | 58000 |
-----------------------------------------------------------------------------
## 26. COUNT()

**Explanation:** Counts rows or non-NULL values.

### Example 1: Count all employees

```sql
SELECT COUNT(*) AS total_employees
FROM employees;
```
**Meaning:** Counts every employee in the table.

### Example 2: Count IT employees

```sql
SELECT COUNT(*) AS it_employees
FROM employees
WHERE department = 'IT';
```
**Meaning:** Counts employees who work in IT.

**Remember:**

- `COUNT(*)` counts all rows.
- `COUNT(column_name)` counts non-NULL values in that column.
--------------------------------------------------------------------------------
## 27. SUM()

**Explanation:** Adds numeric values together.

### Example 1: Total salary

```sql
SELECT SUM(salary) AS total_salary
FROM employees;
```
**Meaning:** Adds the salaries of all employees.

### Example 2: Total IT salary

```sql
SELECT SUM(salary) AS it_total_salary
FROM employees
WHERE department = 'IT';
```
**Meaning:** Adds salaries only for IT employees.
--------------------------------------------------------------------------------
## 28. AVG()

**Explanation:** Calculates the average of numeric values.

### Example 1: Average salary

```sql
SELECT AVG(salary) AS average_salary
FROM employees;
```
**Meaning:** Calculates the average salary of all employees.

### Example 2: Average salary in IT

```sql
SELECT AVG(salary) AS it_average_salary
FROM employees
WHERE department = 'IT';
```

**Meaning:** Calculates the average salary of IT employees.

**Remember:** `AVG()` ignores NULL values.
--------------------------------------------------------------------------------
## 29. MIN()

**Explanation:** Finds the smallest value.

### Example 1: Lowest salary

```sql
SELECT MIN(salary) AS lowest_salary
FROM employees;
```
**Meaning:** Finds the lowest salary in the company.

### Example 2: Lowest salary in IT

```sql
SELECT MIN(salary) AS lowest_it_salary
FROM employees
WHERE department = 'IT';
```

**Meaning:** Finds the lowest salary among IT employees.
--------------------------------------------------------------------------------
## 30. MAX()

**Explanation:** Finds the largest value.

### Example 1: Highest salary

```sql
SELECT MAX(salary) AS highest_salary
FROM employees;
```
**Meaning:** Finds the highest salary in the company.

### Example 2: Highest salary in IT

```sql
SELECT MAX(salary) AS highest_it_salary
FROM employees
WHERE department = 'IT';
```
**Meaning:** Finds the highest salary among IT employees.
--------------------------------------------------------------------------------
## 31. GROUP BY

**Explanation:** Groups rows with the same value so that aggregate functions can calculate results for each group.

### Example 1: Count employees by department

```sql
SELECT department, COUNT(*) AS total_employees
FROM employees
GROUP BY department;
```
**Meaning:** Counts how many employees work in each department.

### Example 2: Total salary by department

```sql
SELECT department, SUM(salary) AS total_salary
FROM employees
GROUP BY department;
```

**Meaning:** Calculates the total salary for each department.

### Example 3: Average salary by department

```sql
SELECT department, AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

**Meaning:** Calculates the average salary for each department.

**Remember:** `GROUP BY` lets you calculate separate results for each group instead of one result for the whole table.
--------------------------------------------------------------------------------
## 32. HAVING

**Explanation:** Filters groups after `GROUP BY`.

### Example 1: Departments with more than 2 employees

```sql
SELECT department, COUNT(*) AS total_employees
FROM employees
GROUP BY department
HAVING COUNT(*) > 2;
```
**Meaning:** Shows only departments that have more than two employees.

### Example 2: Departments with total salary above 140000

```sql
SELECT department, SUM(salary) AS total_salary
FROM employees
GROUP BY department
HAVING SUM(salary) > 140000;
```
**Meaning:** Shows departments whose combined salaries exceed 140000.
--------------------------------------------------------------------------------
## WHERE vs HAVING

`WHERE` filters individual rows before grouping.

`HAVING` filters groups after grouping.

### Example

```sql
SELECT department, AVG(salary) AS average_salary
FROM employees
WHERE salary >= 50000
GROUP BY department
HAVING AVG(salary) > 65000;
```
**How it works:**

1. `WHERE` selects employees earning at least 50000.
2. `GROUP BY` groups the remaining employees by department.
3. `AVG()` calculates the average salary for each department.
4. `HAVING` keeps departments whose average salary exceeds 65000.
--------------------------------------------------------------------------------

## Quick Revision
| SQL | Meaning |
|---|---|
| `COUNT(*)` | Count rows |
| `SUM(salary)` | Add salaries |
| `AVG(salary)` | Calculate average salary |
| `MIN(salary)` | Find lowest salary |
| `MAX(salary)` | Find highest salary |
| `GROUP BY department` | Calculate results for each department |
| `HAVING COUNT(*) > 2` | Keep groups with more than 2 rows |
--------------------------------------------------------------------------------
