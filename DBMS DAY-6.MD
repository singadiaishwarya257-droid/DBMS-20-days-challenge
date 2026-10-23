# 📘 DBMS — DAY 6

## Sorting, Removing Duplicates and Limiting Results with `ORDER BY`, `DISTINCT` and `LIMIT`

**Challenge:** 20-Day DBMS Interview Challenge  
**Progress:** Day 6 of 20 — Days 1–5 completed  
**Study time:** 1.5 hours  
**Practical:** MySQL  
**Focus:** Sort query results, return unique values and limit the number of rows.

## 🎯 Today's goal

Learn how to sort query results, remove duplicate values from output and control how many rows MySQL returns. These are common SQL interview topics.

The examples use the `day4_students` table:

| student_id | name | marks |
|---:|---|---:|
| 101 | Aishwarya | 85 |
| 102 | Priya | 90 |
| 103 | Sneha | 75 |
| 104 | Riya | 60 |
| 105 | Rahul | 90 |

## 1. `ORDER BY` — Sort records

`ORDER BY` sorts the rows returned by a query by one or more columns.

### Ascending order — `ASC`

```sql
SELECT *
FROM day4_students
ORDER BY marks ASC;
```

This sorts marks from lowest to highest. `ASC` is the default direction when no direction is specified.

### Descending order — `DESC`

```sql
SELECT *
FROM day4_students
ORDER BY marks DESC;
```

This sorts marks from highest to lowest.

### Sort by multiple columns

```sql
SELECT *
FROM day4_students
ORDER BY marks DESC, name ASC;
```

Rows are sorted by marks from highest to lowest. For students with the same marks, names are sorted alphabetically.

### 🎤 Interview question

**Q: What is the difference between `ASC` and `DESC`?**

**A:** `ASC` sorts values in ascending order, while `DESC` sorts them in descending order.

**Follow-up: What happens if the sorting direction is omitted?**  
`ASC` is assumed by default.

## 2. `DISTINCT` — Remove duplicate values from results

`DISTINCT` returns unique rows in the query output. It does not delete or modify data in the table.

Suppose a `students` table contains:

| name | course |
|---|---|
| Aishwarya | BCA |
| Priya | BCA |
| Sneha | BBA |
| Riya | BCA |

This query returns each course once:

```sql
SELECT DISTINCT course
FROM students;
```

Result:

| course |
|---|
| BCA |
| BBA |

### `DISTINCT` on multiple columns

```sql
SELECT DISTINCT course, marks
FROM students;
```

This returns unique **course-and-marks combinations**. A course can appear more than once if it is paired with different marks.

### 🎤 Interview question

**Q: What is the difference between `DISTINCT` and `UNIQUE`?**

**A:** `DISTINCT` is used in a `SELECT` query to eliminate duplicate result rows. `UNIQUE` is a database constraint that prevents duplicate values in a column or column combination.

**Follow-up: Does `DISTINCT` delete duplicate records from the table?**  
No. It changes only the query output; the original data remains unchanged.

## 3. `LIMIT` — Restrict the number of rows

`LIMIT` specifies the maximum number of rows returned by a MySQL query.

### Get the top three students by marks

```sql
SELECT *
FROM day4_students
ORDER BY marks DESC
LIMIT 3;
```

This returns at most three rows, beginning with the highest marks. Use `ORDER BY` with `LIMIT` when selecting top or bottom results; without an explicit ordering, which rows are returned is not guaranteed.

### Skip rows with `OFFSET`

```sql
SELECT *
FROM day4_students
ORDER BY student_id
LIMIT 2 OFFSET 2;
```

This skips the first two rows in student ID order and returns the next two, if available.

MySQL also supports the equivalent `LIMIT offset, row_count` syntax:

```sql
SELECT *
FROM day4_students
ORDER BY student_id
LIMIT 2, 2;
```

Here, the first number is the offset and the second is the maximum number of rows.

### 🎤 Interview question

**Q: How do you find the top five highest-scoring students?**

**A:**

```sql
SELECT *
FROM day4_students
ORDER BY marks DESC
LIMIT 5;
```

**Follow-up: What if multiple students tie for the fifth-highest score?**  
This query returns at most five rows, so it may exclude some students tied at that score. To include everyone tied at fifth place, use a ranking function or a score-threshold query.

## 4. Combine `ORDER BY`, `DISTINCT` and `LIMIT`

### Task 1 — Sort marks from highest to lowest

```sql
SELECT *
FROM day4_students
ORDER BY marks DESC;
```

### Task 2 — Display unique marks

```sql
SELECT DISTINCT marks
FROM day4_students;
```

### Task 3 — Find the three lowest-scoring students

```sql
SELECT *
FROM day4_students
ORDER BY marks ASC
LIMIT 3;
```

### Task 4 — Display unique marks in descending order

```sql
SELECT DISTINCT marks
FROM day4_students
ORDER BY marks DESC;
```

### Task 5 — Find the second-highest distinct mark

```sql
SELECT DISTINCT marks
FROM day4_students
WHERE marks IS NOT NULL
ORDER BY marks DESC
LIMIT 1 OFFSET 1;
```

Why this works:

1. `WHERE marks IS NOT NULL` excludes rows without a marks value.
2. `DISTINCT` removes duplicate marks from the result.
3. `ORDER BY marks DESC` sorts the unique marks from highest to lowest.
4. `LIMIT 1 OFFSET 1` skips the highest value and returns the next one.

This finds the second-highest **distinct marks value**, not necessarily the second row. If there is no second distinct non-`NULL` mark, the query returns no rows.

## 5. Check your interview understanding

Choose one answer for each question.

### 1. Which clause sorts query results?

- A. `GROUP BY`
- B. `ORDER BY`
- C. `WHERE`
- D. `DISTINCT`

### 2. What is the default `ORDER BY` direction?

- A. `DESC`
- B. `Random`
- C. `ASC`
- D. None

### 3. Does `DISTINCT` delete duplicates from the table?

- A. Yes
- B. No
- C. Only `NULL` values
- D. Only numbers

### 4. What does `LIMIT 3` return?

- A. Exactly 3 rows always
- B. At most 3 rows
- C. 3 columns
- D. 3 tables

### 5. After sorting in descending order, what does `LIMIT 1 OFFSET 1` return?

- A. The highest value
- B. The second row
- C. The last row
- D. All tied values

### 6. How do you return the highest marks first?

- A. `ORDER BY marks ASC`
- B. `ORDER BY marks DESC`
- C. `LIMIT marks DESC`
- D. `DISTINCT marks`

<details>
<summary>Answer key</summary>

1. B — `ORDER BY`
2. C — `ASC`
3. B — `DISTINCT` affects query output only
4. B — At most 3 rows
5. B — The second row in the sorted result (assuming the query has an appropriate `ORDER BY`)
6. B — `ORDER BY marks DESC`

</details>

## ⏱️ Suggested 90-minute study schedule

| Time | Activity |
|---:|---|
| 20 min | Learn `ORDER BY`, `ASC` and `DESC` |
| 15 min | Learn `DISTINCT` |
| 15 min | Learn `LIMIT` and `OFFSET` |
| 25 min | Write and run the practical queries |
| 15 min | Answer the MCQs and explain your answers aloud |

## ✅ Day 6 completion checklist

- [ ] I can sort data using `ORDER BY`.
- [ ] I understand `ASC` and `DESC`.
- [ ] I can retrieve unique values using `DISTINCT`.
- [ ] I can use `LIMIT` and `OFFSET`.
- [ ] I can find the top three rows and the second-highest distinct value.

## ➡️ Next: Day 7

**Topics:** Aggregate functions and `GROUP BY` — `COUNT`, `SUM`, `AVG`, `MIN` and `MAX`.

These are essential for SQL interview problem-solving.

## More practice

- Write a query to find the third-highest distinct mark.
- Practise paginating student records with `LIMIT` and `OFFSET`.
- Try queries that combine `WHERE`, `DISTINCT`, `ORDER BY` and `LIMIT`.
