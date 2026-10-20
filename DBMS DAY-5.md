# 📘 DBMS — DAY 5

## Filtering Data with `WHERE`, Operators, `LIKE`, `IN`, `BETWEEN` and `NULL`

**Challenge:** 20-Day DBMS Interview Challenge  
**Progress:** Day 5 of 20 — Days 1–4 completed  
**Study time:** 1.5 hours  
**Practical:** MySQL  
**Focus:** Filter records correctly, write practical queries and explain your answers in interviews.

## 🎯 Today's goal

Learn how to filter rows using conditions in SQL. These concepts are essential for solving SQL coding-round problems and building backend applications.

The examples below use the `day4_students` table from Day 4:

| student_id | name | marks |
|---:|---|---:|
| 101 | Aishwarya | 85 |
| 102 | Priya | 90 |
| 103 | Sneha | 75 |
| 104 | Riya | 60 |
| 105 | Rahul | 90 |

Your table may contain different records if you have already completed the Day 4 update and delete exercises.

## 1. `WHERE` — Filter rows

The `WHERE` clause returns only rows that satisfy a condition.

```sql
SELECT *
FROM day4_students
WHERE marks > 80;
```

With the sample data above, this returns Aishwarya, Priya and Rahul.

### 🎤 Interview question

**Q: What is the purpose of the `WHERE` clause?**

**A:** It filters rows based on a specified condition.

## 2. Comparison operators

Comparison operators compare values in a condition.

| Operator | Meaning | Example |
|---|---|---|
| `=` | Equal to | `marks = 90` |
| `!=` or `<>` | Not equal to | `marks != 90` |
| `>` | Greater than | `marks > 80` |
| `<` | Less than | `marks < 80` |
| `>=` | Greater than or equal to | `marks >= 80` |
| `<=` | Less than or equal to | `marks <= 60` |

For example, this returns students who scored at least 90:

```sql
SELECT *
FROM day4_students
WHERE marks >= 90;
```

### 🎤 Interview question

**Q: What is the difference between `=` and `LIKE`?**

**A:** `=` checks whether a value matches exactly. `LIKE` checks whether text matches a pattern.

## 3. Logical operators — `AND`, `OR` and `NOT`

### `AND`

Both conditions must be true. This query returns students with marks from 80 to 90, inclusive:

```sql
SELECT *
FROM day4_students
WHERE marks >= 80 AND marks <= 90;
```

### `OR`

At least one condition must be true. This query returns students who scored either 75 or 90:

```sql
SELECT *
FROM day4_students
WHERE marks = 75 OR marks = 90;
```

### `NOT`

`NOT` reverses a condition. This query returns students whose marks are not 90:

```sql
SELECT *
FROM day4_students
WHERE NOT marks = 90;
```

### 🎤 Interview question

**Q: What is the difference between `AND` and `OR`?**

**A:** `AND` requires every condition to be true; `OR` requires at least one condition to be true.

## 4. `LIKE` — Match text patterns ⭐

`LIKE` searches text using wildcard characters:

| Wildcard | Meaning |
|---|---|
| `%` | Matches zero or more characters |
| `_` | Matches exactly one character |

### Names starting with `A`

```sql
SELECT *
FROM day4_students
WHERE name LIKE 'A%';
```

### Names ending with `a`

```sql
SELECT *
FROM day4_students
WHERE name LIKE '%a';
```

With the sample data, this matches Priya, Sneha and Riya.

### Names containing `iy`

```sql
SELECT *
FROM day4_students
WHERE name LIKE '%iy%';
```

With the sample data, this matches Priya and Riya.

### Names with exactly four characters

```sql
SELECT *
FROM day4_students
WHERE name LIKE '____';
```

With the sample data, this matches Riya.

### 🎤 Interview question

**Q: What is the difference between `%` and `_` in a `LIKE` pattern?**

**A:** `%` matches zero or more characters; `_` matches exactly one character.

## 5. `IN` — Match values in a list

`IN` checks whether a value matches any value in a list.

```sql
SELECT *
FROM day4_students
WHERE marks IN (75, 90);
```

This is equivalent to:

```sql
WHERE marks = 75 OR marks = 90;
```

Use `NOT IN` to exclude values:

```sql
SELECT *
FROM day4_students
WHERE marks NOT IN (75, 90);
```

`IN` can make a query with several possible values easier to read than multiple `OR` conditions.

> **Important:** `NOT IN` can produce unexpected results if its list or subquery contains `NULL`. This is especially important when using subqueries.

### 🎤 Interview question

**Q: Why use `IN` instead of several `OR` conditions?**

**A:** `IN` makes queries that match against several values more concise and readable.

## 6. `BETWEEN` — Match a range

`BETWEEN` checks whether a value falls within a range. Both endpoints are included.

```sql
SELECT *
FROM day4_students
WHERE marks BETWEEN 75 AND 90;
```

This is equivalent to:

```sql
WHERE marks >= 75 AND marks <= 90;
```

Use `NOT BETWEEN` to exclude the range:

```sql
SELECT *
FROM day4_students
WHERE marks NOT BETWEEN 75 AND 90;
```

### 🎤 Interview question

**Q: Is `BETWEEN 75 AND 90` inclusive?**

**A:** Yes. It includes both 75 and 90.

## 7. `NULL` and `IS NULL` ⭐⭐⭐

`NULL` represents missing or unknown data. It is not the same as zero or an empty string.

Use `IS NULL` to find rows without a marks value:

```sql
SELECT *
FROM day4_students
WHERE marks IS NULL;
```

Use `IS NOT NULL` to find rows with a known marks value:

```sql
SELECT *
FROM day4_students
WHERE marks IS NOT NULL;
```

Do not use `marks = NULL` to check for missing values. Comparisons with `NULL` do not work like ordinary equality comparisons.

SQL uses three-valued logic: a condition can be `TRUE`, `FALSE` or `UNKNOWN`. A comparison with `NULL` usually evaluates to `UNKNOWN`, and `WHERE` returns only rows for which the condition is `TRUE`.

### 🎤 Interview question

**Q: Why can't we use `= NULL`?**

**A:** `NULL` represents an unknown or missing value, so ordinary equality comparisons cannot test for it correctly. Use `IS NULL` or `IS NOT NULL`.

## 8. Hands-on MySQL practical

Use the `day4_students` table created on Day 4. The following queries assume it contains the sample records shown above.

### Task 1 — Find students scoring above 80

```sql
SELECT *
FROM day4_students
WHERE marks > 80;
```

### Task 2 — Find students scoring between 70 and 90

```sql
SELECT *
FROM day4_students
WHERE marks BETWEEN 70 AND 90;
```

### Task 3 — Find names starting with `S`

```sql
SELECT *
FROM day4_students
WHERE name LIKE 'S%';
```

### Task 4 — Find students scoring 75 or 95

```sql
SELECT *
FROM day4_students
WHERE marks IN (75, 95);
```

### Task 5 — Find students scoring at least 80 whose names start with `A`

```sql
SELECT *
FROM day4_students
WHERE marks >= 80
  AND name LIKE 'A%';
```

### Task 6 — Find students whose marks are `NULL`

```sql
SELECT *
FROM day4_students
WHERE marks IS NULL;
```

The current table may not contain a `NULL` marks value. To add a separate practice record:

```sql
INSERT INTO day4_students (student_id, name, marks)
VALUES (106, 'Kiran', NULL);
```

Then rerun Task 6.

## 9. Check your interview understanding

Choose one answer for each question.

### 1. Which condition finds marks from 60 to 80, including both endpoints?

- A. `marks > 60 AND marks < 80`
- B. `marks BETWEEN 60 AND 80`
- C. `marks IN (60, 80)`
- D. `marks = 60 OR marks < 80`

### 2. What does `LIKE 'A_'` match?

- A. Any name starting with `A`
- B. `A` followed by exactly one character
- C. Any name ending with `A`
- D. Only the single letter `A`

### 3. Which condition correctly checks for missing marks?

- A. `marks = NULL`
- B. `marks == NULL`
- C. `marks IS NULL`
- D. `marks <> NULL`

### 4. What does `WHERE marks = 75 OR marks = 90` return?

- A. Only students with both marks
- B. Students with either 75 or 90 marks
- C. All students below 90
- D. No rows

### 5. Which pattern finds names ending in `a`?

- A. `LIKE 'a%'`
- B. `LIKE '%a'`
- C. `LIKE '_a_'`
- D. `LIKE '%a%'`

### 6. What does `WHERE marks = NULL` usually evaluate to?

- A. `TRUE`
- B. `FALSE` in every context
- C. `UNKNOWN`
- D. A syntax error in every database

<details>
<summary>Answer key</summary>

1. B — `BETWEEN` includes both endpoints.
2. B — `_` matches exactly one character.
3. C — Use `IS NULL` to test for a missing value.
4. B — `OR` matches either condition.
5. B — `%a` matches text ending in `a`.
6. C — A comparison with `NULL` usually evaluates to `UNKNOWN`.

</details>

## ⏱️ Suggested 90-minute schedule

| Time | Activity |
|---:|---|
| 20 min | Study `WHERE`, comparison operators and logical operators |
| 20 min | Practice `LIKE`, `IN` and `BETWEEN` |
| 15 min | Review `NULL` and `IS NULL` |
| 25 min | Write and run the six practical queries |
| 10 min | Answer the MCQs and explain your answers aloud |

## ✅ Day 5 completion checklist

- [ ] I can combine conditions with `AND`, `OR` and `NOT`.
- [ ] I understand the difference between `%` and `_`.
- [ ] I know that `BETWEEN` includes both endpoints.
- [ ] I can use `IN` and `NOT IN`.
- [ ] I know why `IS NULL` is correct and `= NULL` is not.

## ➡️ Next: Day 6

**Topics:** `ORDER BY`, `DISTINCT`, `LIMIT` and sorting/filtering interview problems.