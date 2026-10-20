# 📘 DBMS — DAY 3

## Relational Model, Keys, Constraints and Relationships

**Challenge:** 20-Day DBMS Interview Challenge  
**Study time:** 1.5 hours  
**Focus:** Understand how relational databases structure data, identify records, enforce valid data and connect tables.

## 🎯 Today's goal

Learn how tables organize relational data, how keys identify records and connect tables, and how constraints help maintain valid data.

## 1. The relational model

The **relational model** stores data in tables. Rows represent records, and columns represent attributes.

### Example: `STUDENTS`

| student_id | name | course |
|---:|---|---|
| 101 | Aishwarya | BCA |
| 102 | Priya | BCA |
| 103 | Sneha | BCA |

### Important terms

| Term | Meaning |
|---|---|
| Relation | A table |
| Tuple | A row or record |
| Attribute | A column |
| Domain | The set of valid values for an attribute |
| Schema | The structure or design of the database |
| Instance | The actual data stored at a particular time |

### 🎤 Interview question

**Q: What is the relational model?**

**A:** The relational model represents data using tables consisting of rows and columns. Keys can establish relationships between tables.

**Follow-up: What is a tuple?**  
A tuple is a single row or record in a relational table.

## 2. Keys

Keys help uniquely identify records and connect tables. They are a core DBMS interview topic.

### 2.1 Super key

A **super key** is one or more attributes that can uniquely identify a record.

If `student_id` is unique, each of these is a super key:

- `student_id`
- `student_id` + `name`
- `student_id` + `course`

The additional attributes are not needed for uniqueness, but the combinations still uniquely identify records.

**Interview question: What is a super key?**  
A super key is a set of one or more attributes that uniquely identifies a record in a table.

### 2.2 Candidate key

A **candidate key** is a minimal super key: it uniquely identifies a record, and no attribute can be removed while preserving that uniqueness.

Suppose both `student_id` and `email` are unique:

- `student_id` is a candidate key.
- `email` is a candidate key.
- `student_id` + `name` is not a candidate key because `name` is unnecessary.

> **Remember:** Candidate key = minimal super key.

**Interview question: What is a candidate key?**  
A candidate key is a minimal super key that can uniquely identify a record.

### 2.3 Primary key

One candidate key is selected as the **primary key**.

```sql
student_id INT PRIMARY KEY
```

A primary key:

- Uniquely identifies each record.
- Cannot contain `NULL`.
- Cannot contain duplicate values.
- Is defined as one primary key constraint per table. That constraint may consist of multiple columns.

**Interview question: Can a table have multiple primary keys?**  
A table can have only one primary key constraint, but that primary key can contain multiple columns.

### 2.4 Alternate key

Candidate keys not selected as the primary key are called **alternate keys**.

If `student_id` and `email` are candidate keys and `student_id` is selected as the primary key, then `email` is an alternate key.

```text
Candidate keys → one selected as the primary key
               → remaining candidate keys are alternate keys
```

### 2.5 Composite key

A **composite key** is formed from two or more columns that together uniquely identify a record.

For example, an `ENROLLMENT` table could use `(student_id, subject_id)` as its key:

| student_id | subject_id |
|---:|---:|
| 101 | 1 |
| 101 | 2 |
| 102 | 1 |

Neither column alone needs to be unique; the pair must be unique.

**Interview question: What is a composite key?**  
A composite key is a key formed using two or more columns together to uniquely identify a record.

### 2.6 Foreign key

A **foreign key** connects tables by referring to a key in another table.

**Departments**

| department_id | department_name |
|---:|---|
| 1 | BCA |
| 2 | BBA |

**Students**

| student_id | name | department_id |
|---:|---|---:|
| 101 | Aishwarya | 1 |
| 102 | Priya | 1 |

Here, `Students.department_id` is a foreign key referencing `Departments.department_id`.

**Interview question: Why do we use a foreign key?**  
A foreign key establishes a relationship between tables and helps maintain referential integrity.

## 3. Constraints

Constraints are rules applied to table columns to help maintain valid and consistent data.

| Constraint | Purpose | Example |
|---|---|---|
| `NOT NULL` | Requires a value | `name VARCHAR(100) NOT NULL` |
| `UNIQUE` | Prevents duplicate values | `email VARCHAR(100) UNIQUE` |
| `PRIMARY KEY` | Uniquely identifies each row and disallows `NULL` | `student_id INT PRIMARY KEY` |
| `FOREIGN KEY` | Requires referenced values to exist in the related table | `FOREIGN KEY (department_id) REFERENCES departments(department_id)` |
| `CHECK` | Requires a condition to be true | `CHECK (marks >= 0 AND marks <= 100)` |
| `DEFAULT` | Supplies a value when none is provided | `status VARCHAR(20) DEFAULT 'Active'` |

**Note:** MySQL enforces `CHECK` constraints in MySQL 8.0.16 and later. Confirm your server version if a check-constraint test does not behave as expected.

## 4. Relationships

### One-to-one (1:1)

One person has one passport.

```text
Person 1 ───── 1 Passport
```

### One-to-many (1:M)

One department can have many students.

```text
Department 1 ─────── Many Students
```

### Many-to-many (M:M)

Many students can take many subjects, and each subject can have many students.

```text
Students  ←────→  Subjects
```

In a relational database, represent a many-to-many relationship with a **junction table** containing foreign keys to both tables:

```text
student_subject
---------------
student_id
subject_id
```

## 5. Hands-on MySQL practical

Use your existing `college_db`. This exercise creates separate `departments` and `students3` tables.

### Step 1 — Select the database and create `departments`

```sql
USE college_db;

CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(50) UNIQUE NOT NULL
);
```

### Step 2 — Insert departments

```sql
INSERT INTO departments (department_id, department_name)
VALUES
    (1, 'BCA'),
    (2, 'BBA');
```

### Step 3 — Create `students3` with constraints

```sql
CREATE TABLE students3 (
    student_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    marks INT CHECK (marks >= 0 AND marks <= 100),
    status VARCHAR(20) DEFAULT 'Active',
    department_id INT,
    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

### Step 4 — Insert valid students

```sql
INSERT INTO students3
    (student_id, name, email, marks, department_id)
VALUES
    (101, 'Aishwarya', 'aishwarya@gmail.com', 85, 1),
    (102, 'Priya', 'priya@gmail.com', 90, 1);
```

`status` is omitted, so it uses the default value `Active`.

### Step 5 — View the records

```sql
SELECT *
FROM students3;
```

## 6. Test the constraints

Run these statements individually after the valid data has been inserted. Each is expected to fail because it violates a constraint.

### Test 1 — Duplicate primary key

```sql
INSERT INTO students3
VALUES (101, 'Sneha', 'sneha@gmail.com', 80, 'Active', 1);
```

**Expected:** Rejected because `student_id` 101 already exists.

### Test 2 — Marks outside the allowed range

```sql
INSERT INTO students3
VALUES (103, 'Sneha', 'sneha@gmail.com', 110, 'Active', 1);
```

**Expected:** Rejected by the `CHECK` constraint when supported and enforced by the MySQL version in use.

### Test 3 — Department does not exist

```sql
INSERT INTO students3
VALUES (104, 'Riya', 'riya@gmail.com', 85, 'Active', 99);
```

**Expected:** Rejected because department 99 does not exist in `departments`.

These tests demonstrate how constraints validate data rather than merely defining table structure.

## 7. Interview questions

### Q1. What is the difference between a super key and a candidate key?

A super key may contain unnecessary attributes, while a candidate key is a minimal super key.

### Q2. What is the difference between a candidate key and a primary key?

Candidate keys are all possible minimal keys that uniquely identify rows. One is selected as the primary key.

### Q3. Can a foreign key contain `NULL`?

Yes. A foreign key can contain `NULL` unless its column is also defined with `NOT NULL`.

### Q4. Can a table have multiple candidate keys?

Yes. A table can have multiple candidate keys, but only one primary key constraint.

### Q5. What is the purpose of a foreign key?

It establishes relationships between tables and helps maintain referential integrity.

### Q6. Why do we use constraints?

Constraints enforce rules on data and help maintain data accuracy and integrity.

### Q7. How do you represent a many-to-many relationship?

Use an intermediate junction table with foreign keys referencing both related tables.

## ⏱️ Suggested 90-minute plan

| Time | Activity |
|---:|---|
| 25 min | Relational model and terminology |
| 30 min | Keys |
| 15 min | Constraints and relationships |
| 15 min | MySQL practical |
| 5 min | Recall the interview answers |

## ⭐ Day 3 must-master

Understand this progression:

```text
Super Key → Candidate Key → Primary Key
```

And remember:

```text
Foreign Key → connects tables
```

## ✅ Day 3 completion checklist

- [ ] I can explain the relational model and its terminology.
- [ ] I can distinguish super, candidate, primary, alternate, composite and foreign keys.
- [ ] I can explain common constraints and table relationships.
- [ ] I can create the practice tables and test their constraints.
- [ ] I can answer the interview questions aloud.

**Day 3 syllabus is fixed.**