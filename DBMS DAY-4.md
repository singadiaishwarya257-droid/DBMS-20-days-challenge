# 📘 DBMS — DAY 4

## SQL Fundamentals: `SELECT`, `INSERT`, `UPDATE` and `DELETE`

**Challenge:** 20-Day DBMS Interview Challenge  
**Progress:** Day 4 of 20 — Days 1–3 completed  
**Study time:** 1.5 hours  
**Practical:** MySQL  
**Focus:** Understand the commands, write queries and explain your answers in interviews.

## 🎯 Today's goal

Learn how to retrieve, insert, modify and delete data using SQL. These commands are essential for backend and full-stack development.

For example, in a Student Results Management System, SQL lets you retrieve students' marks, add students, update marks and delete records.

## 1. What is SQL?

**SQL (Structured Query Language)** is used to communicate with relational databases such as MySQL.

## 2. `SELECT` — Retrieve data

`SELECT` fetches data from a table. Suppose the `students` table contains:

| student_id | name | marks |
|---:|---|---:|
| 101 | Aishwarya | 85 |
| 102 | Priya | 90 |
| 103 | Sneha | 75 |

### Retrieve all columns

```sql
SELECT *
FROM students;
```

The `*` means all columns.

### Retrieve specific columns

```sql
SELECT name, marks
FROM students;
```

### 🎤 Interview question

**Q: What is the difference between `SELECT *` and `SELECT name, marks`?**

**A:** `SELECT *` retrieves every column, while `SELECT name, marks` retrieves only the specified columns.

**Follow-up: Why might selecting specific columns be better?**  
It avoids fetching unnecessary data and can reduce data transfer.

## 3. `INSERT` — Add data

`INSERT` adds new records to a table.

```sql
INSERT INTO students (student_id, name, marks)
VALUES (104, 'Riya', 88);
```

This adds a record for Riya.

### 🎤 Interview question

**Q: What happens if you insert a duplicate primary key?**

**A:** The database rejects the insertion because a primary key must be unique.

## 4. `UPDATE` — Modify existing data

`UPDATE` changes existing records.

```sql
UPDATE students
SET marks = 95
WHERE student_id = 101;
```

This changes Aishwarya's marks to 95.

### ⚠️ Important: Use `WHERE` carefully

When you intend to update only specific records, include a `WHERE` clause:

```sql
UPDATE students
SET marks = 95;
```

Without `WHERE`, this statement updates the `marks` value for every row in the table.

### 🎤 Interview question

**Q: What happens if you execute an `UPDATE` statement without `WHERE`?**

**A:** All rows may be updated, unless another condition or limitation applies.

## 5. `DELETE` — Remove records

`DELETE` removes rows from a table.

```sql
DELETE FROM students
WHERE student_id = 104;
```

This removes Riya's record.

Without `WHERE`, all rows are removed, but the table structure remains:

```sql
DELETE FROM students;
```

### 🎤 Interview question

**Q: Does `DELETE` remove the table structure?**

**A:** No. `DELETE` removes rows, not the table itself.

## 6. Command comparison

| Command | Purpose |
|---|---|
| `SELECT` | Retrieve records |
| `INSERT` | Add new records |
| `UPDATE` | Modify existing records |
| `DELETE` | Remove records |

These four are foundational SQL commands. Filtering and more advanced queries are covered on later days.

## 7. Hands-on MySQL practical

Use your existing `college_db`. Create a separate practice table so earlier tables are not changed.

### Step 1 — Create the table

```sql
USE college_db;

CREATE TABLE day4_students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    marks INT
);
```

### Step 2 — Insert records

```sql
INSERT INTO day4_students (student_id, name, marks)
VALUES
    (101, 'Aishwarya', 85),
    (102, 'Priya', 90),
    (103, 'Sneha', 75);
```

### Step 3 — Retrieve records

```sql
SELECT *
FROM day4_students;

SELECT name, marks
FROM day4_students;
```

### Step 4 — Update a record

```sql
UPDATE day4_students
SET marks = 95
WHERE student_id = 101;
```

### Step 5 — Delete a record

```sql
DELETE FROM day4_students
WHERE student_id = 103;
```

### Step 6 — Verify the result

```sql
SELECT *
FROM day4_students;
```

You should see Aishwarya with 95 marks and Priya with 90 marks.

## 8. Check your interview understanding

Choose one answer for each question.

### 1. Which SQL command retrieves data?

- A. `INSERT`
- B. `SELECT`
- C. `UPDATE`
- D. `DELETE`

### 2. Which command changes existing records?

- A. `INSERT`
- B. `CREATE`
- C. `UPDATE`
- D. `SELECT`

### 3. What happens when `UPDATE` has no `WHERE` clause?

- A. Only the first row changes
- B. All rows may be updated
- C. The table is deleted
- D. The query always fails

### 4. Which command removes rows but preserves the table structure?

- A. `DROP`
- B. `DELETE`
- C. `REMOVE TABLE`
- D. `ALTER`

### 5. What happens if an `INSERT` uses an existing primary key?

- A. The old row is replaced automatically
- B. Both rows are stored
- C. The insertion is rejected
- D. The primary key becomes `NULL`

### 6. Which query retrieves only names?

- A. `SELECT * FROM students`
- B. `SELECT name FROM students`
- C. `INSERT name FROM students`
- D. `UPDATE students SET name`

<details>
<summary>Answer key</summary>

1. B — `SELECT`
2. C — `UPDATE`
3. B — All rows may be updated
4. B — `DELETE`
5. C — The insertion is rejected
6. B — `SELECT name FROM students`

</details>

## ⏱️ Suggested 90-minute schedule

| Time | Activity |
|---:|---|
| 20 min | Understand `SELECT` and `INSERT` |
| 20 min | Understand `UPDATE` and `DELETE` |
| 25 min | Execute the MySQL practical |
| 15 min | Answer the interview questions aloud |
| 10 min | Revise and answer the MCQs |

## ✅ Day 4 completion checklist

- [ ] I can explain `SELECT`, `INSERT`, `UPDATE` and `DELETE`.
- [ ] I can write each command without copying.
- [ ] I understand why `WHERE` matters.
- [ ] I can answer the interview questions.

## ➡️ Next: Day 5

**Topics:** `WHERE` clause, comparison operators, logical operators, `LIKE`, `IN`, `BETWEEN` and `NULL`.

These topics will help you solve practical SQL interview problems.

## More practice

- Create sample queries to update multiple students' marks safely.
- Try inserting a duplicate primary key and observe the error.
- Compare how `DELETE` with and without `WHERE` affects table data.