# SQL — Level 1: Absolute Basics

## 1. What is a Database?

A **database** is an organized collection of data that allows us to store, manage, and retrieve information efficiently.

For example, a school may have a database containing information about:

* Students
* Teachers
* Courses
* Marks

A database can contain multiple tables.

---

## 2. Database vs Table

### Database

A **database** is a container that holds related data and tables.

Example:

```text
School Database
│
├── students
├── teachers
├── courses
└── marks
```

### Table

A **table** stores data in the form of **rows and columns**.

Example:

```text
students

+----+-------+-----+
| id | name  | age |
+----+-------+-----+
|  1 | Arun  |  20 |
|  2 | Priya |  21 |
|  3 | Ravi  |  19 |
+----+-------+-----+
```

**Simple difference:**

> Database = Collection/container of related tables
> Table = Structure that stores the actual data

---

## 3. Rows and Columns

A table consists of **rows and columns**.

### Column

A **column** represents a specific type of information.

Example:

```text
id
name
age
```

Each column has a name and usually a specific data type.

### Row

A **row** represents one complete record.

Example:

```text
1 | Arun | 20
```

This is one student's record.

### Example

```text
+----+-------+-----+
| id | name  | age |
+----+-------+-----+
|  1 | Arun  |  20 |  ← Row
|  2 | Priya |  21 |  ← Row
+----+-------+-----+
   ↑
 Columns
```

**Remember:**

> Column = Type of information
> Row = One record

---

## 4. Primary Key

A **primary key** is a column (or combination of columns) that uniquely identifies each row in a table.

Example:

```sql
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT
);
```

Here, `id` is the primary key.

Example data:

```text
+----+-------+-----+
| id | name  | age |
+----+-------+-----+
|  1 | Arun  |  20 |
|  2 | Priya |  21 |
|  3 | Ravi  |  19 |
+----+-------+-----+
```

Each student has a unique `id`.

### Important rules

A primary key:

* Must be unique
* Cannot contain `NULL`
* Identifies a row uniquely
* A table can have one primary key constraint

**Example:**

```text
Student ID = 101
```

No other student should have the same ID.

---

## 5. Foreign Key

A **foreign key** is a column that creates a relationship between two tables.

For example, suppose we have two tables:

### Students

```text
+----+-------+
| id | name  |
+----+-------+
|  1 | Arun  |
|  2 | Priya |
+----+-------+
```

### Orders

```text
+----------+------------+
| order_id | student_id |
+----------+------------+
|    101   |     1      |
|    102   |     2      |
+----------+------------+
```

Here, `student_id` in the `orders` table can be a foreign key referencing `students.id`.

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    student_id INT,
    FOREIGN KEY (student_id) REFERENCES students(id)
);
```

### Simple difference

> Primary Key → Identifies a record in its own table
> Foreign Key → Connects one table to another table

---

## 6. Data Types

A **data type** defines what kind of data a column can store.

Common SQL data types include:

| Data Type  | Used For              | Example                   |
| ---------- | --------------------- | ------------------------- |
| `INT`      | Whole numbers         | `25`                      |
| `DECIMAL`  | Decimal numbers       | `99.50`                   |
| `VARCHAR`  | Variable-length text  | `'Arun'`                  |
| `CHAR`     | Fixed-length text     | `'IN'`                    |
| `TEXT`     | Large amounts of text | `'This is a description'` |
| `DATE`     | Date                  | `'2026-10-08'`            |
| `DATETIME` | Date and time         | `'2026-10-08 10:30:00'`   |
| `BOOLEAN`  | True/False            | `TRUE`                    |

Example:

```sql
CREATE TABLE students (
    id INT,
    name VARCHAR(100),
    age INT,
    fees DECIMAL(10,2),
    date_of_birth DATE
);
```

---

# 7. CREATE DATABASE

`CREATE DATABASE` is used to create a new database.

### Syntax

```sql
CREATE DATABASE database_name;
```

### Example

```sql
CREATE DATABASE school;
```

Now a database named `school` is created.

To use the database:

```sql
USE school;
```

> Note: `USE` syntax is supported by systems such as MySQL. Other database systems may handle database selection differently.

---

# 8. CREATE TABLE

`CREATE TABLE` is used to create a new table inside a database.

### Syntax

```sql
CREATE TABLE table_name (
    column1 data_type,
    column2 data_type,
    column3 data_type
);
```

### Example

```sql
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT
);
```

This creates a `students` table with three columns:

```text
id
name
age
```

---

# 9. INSERT

`INSERT` is used to add new records to a table.

### Syntax

```sql
INSERT INTO table_name (column1, column2)
VALUES (value1, value2);
```

### Example

```sql
INSERT INTO students (id, name, age)
VALUES (1, 'Arun', 20);
```

Insert multiple records:

```sql
INSERT INTO students (id, name, age)
VALUES
    (1, 'Arun', 20),
    (2, 'Priya', 21),
    (3, 'Ravi', 19);
```

---

# 10. SELECT

`SELECT` is used to retrieve data from a table.

### Select all columns

```sql
SELECT * FROM students;
```

`*` means **all columns**.

### Select specific columns

```sql
SELECT name, age
FROM students;
```

This returns only the `name` and `age` columns.

Example result:

```text
+-------+-----+
| name  | age |
+-------+-----+
| Arun  |  20 |
| Priya |  21 |
| Ravi  |  19 |
+-------+-----+
```

---

# 11. UPDATE

`UPDATE` is used to modify existing records.

### Syntax

```sql
UPDATE table_name
SET column_name = new_value
WHERE condition;
```

### Example

```sql
UPDATE students
SET age = 21
WHERE id = 1;
```

This changes Arun's age from `20` to `21`.

### ⚠️ Important

Always be careful with the `WHERE` clause.

Without `WHERE`:

```sql
UPDATE students
SET age = 21;
```

This changes the age of **every student** to `21`.

---

# 12. DELETE

`DELETE` is used to remove records from a table.

### Syntax

```sql
DELETE FROM table_name
WHERE condition;
```

### Example

```sql
DELETE FROM students
WHERE id = 3;
```

This deletes the student whose `id` is `3`.

### ⚠️ Important

Be careful with `DELETE`.

Without `WHERE`:

```sql
DELETE FROM students;
```

This deletes **all rows** from the table.

---

# Quick Revision

| Command           | Purpose               |
| ----------------- | --------------------- |
| `CREATE DATABASE` | Creates a database    |
| `CREATE TABLE`    | Creates a table       |
| `INSERT`          | Adds data             |
| `SELECT`          | Reads data            |
| `UPDATE`          | Changes existing data |
| `DELETE`          | Removes data          |

## Key Concepts

| Concept     | Meaning                                   |
| ----------- | ----------------------------------------- |
| Database    | Collection/container for related data     |
| Table       | Stores data in rows and columns           |
| Row         | One record                                |
| Column      | One type/field of information             |
| Primary Key | Uniquely identifies a row                 |
| Foreign Key | Creates a relationship between tables     |
| Data Type   | Defines what kind of data a column stores |

---

# Complete Example

```sql
CREATE DATABASE school;

USE school;

CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT
);

INSERT INTO students (id, name, age)
VALUES
    (1, 'Arun', 20),
    (2, 'Priya', 21),
    (3, 'Ravi', 19);

SELECT * FROM students;

UPDATE students
SET age = 21
WHERE id = 1;

DELETE FROM students
WHERE id = 3;
```

## Level 1 Goal

After completing Level 1, you should understand:

* What a database is
* What a table is
* Rows and columns
* Primary keys
* Foreign keys
* Basic data types
* How to create databases and tables
* How to insert data
* How to retrieve data
* How to update data
* How to delete data

**Next → Level 2: Filtering, Sorting, and Basic Queries**
