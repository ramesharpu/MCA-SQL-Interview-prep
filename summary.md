# 2-Hour SQL Interview Masterclass

## Agenda (120 Minutes)

| Time   | Topic                         | Style               |
| ------ | ----------------------------- | ------------------- |
| 10 min | How interviewers evaluate SQL | Interactive         |
| 20 min | Execution Order + Joins       | Live coding         |
| 20 min | GROUP BY & Aggregations       | Interview questions |
| 20 min | Subqueries & CTEs             | Medium problems     |
| 20 min | Window Functions              | Advanced problems   |
| 15 min | Database Design & Theory      | Discussion          |
| 10 min | Performance & Indexes         | Optimization        |
| 5 min  | Rapid Fire Round              | Fun                 |

---

# Start with this Question

Instead of introducing yourself...

Show this.

## Question 1

Employee

| EmpID | Name  | DeptID | Salary |
| ----- | ----- | ------ | ------ |
| 1     | John  | 10     | 70000  |
| 2     | David | 10     | 80000  |
| 3     | Mary  | 20     | 60000  |
| 4     | Lisa  | NULL   | 90000  |

Department

| DeptID | DeptName |
| ------ | -------- |
| 10     | IT       |
| 20     | HR       |
| 30     | Finance  |

Ask

> Which join returns Lisa?

Most students immediately say

> LEFT JOIN

Correct.

Now ask

> Which join returns Finance?

Many students fail.

Answer:

RIGHT JOIN
FULL JOIN

Now ask

> Which join returns only unmatched records?

Answer

LEFT JOIN + WHERE dept IS NULL

This immediately warms them up.

---

# Interview Trick #1

## SQL Execution Order

Ask

```sql
SELECT name
FROM Employee
WHERE salary > AVG(salary);
```

Everyone says

Valid.

Wrong.

Because

WHERE executes before AVG.

Correct

```sql
SELECT *
FROM Employee
WHERE salary >
(
SELECT AVG(salary)
FROM Employee
);
```

Teach

FROM

↓

WHERE

↓

GROUP BY

↓

HAVING

↓

SELECT

↓

ORDER BY

↓

LIMIT

This alone answers many interviews.

---

# Challenge 1

Find employees earning more than department average.

Students usually write

```sql
SELECT *
FROM Employee
WHERE salary >
AVG(salary);
```

Wrong.

Expected

```sql
SELECT e.*
FROM Employee e
JOIN
(
SELECT DeptID,
AVG(Salary) AvgSalary
FROM Employee
GROUP BY DeptID
) d
ON e.DeptID=d.DeptID
WHERE e.Salary>d.AvgSalary;
```

Then show CTE version

```sql
WITH DeptAvg AS
(
SELECT DeptID,
AVG(Salary) AvgSalary
FROM Employee
GROUP BY DeptID
)

SELECT *
FROM Employee e
JOIN DeptAvg d
ON e.DeptID=d.DeptID
WHERE e.Salary>d.AvgSalary;
```

---

# Challenge 2

Highest salary in every department

Expected

```sql
SELECT DeptID,
MAX(Salary)
FROM Employee
GROUP BY DeptID;
```

Now ask

Return employee names too.

Most students write

```sql
SELECT Name,
MAX(Salary)
```

Wrong.

Correct answer

Window function

```sql
SELECT *
FROM
(
SELECT *,
ROW_NUMBER() OVER
(
PARTITION BY DeptID
ORDER BY Salary DESC
) rn
FROM Employee
)t
WHERE rn=1;
```

Perfect interview question.

---

# Challenge 3

Second Highest Salary

Three different solutions

## Method 1

```sql
SELECT MAX(Salary)
FROM Employee
WHERE Salary <
(
SELECT MAX(Salary)
FROM Employee
);
```

Simple.

---

Method 2

Using DENSE_RANK

```sql
SELECT *
FROM
(
SELECT *,
DENSE_RANK()
OVER
(
ORDER BY Salary DESC
) r
FROM Employee
)t
WHERE r=2;
```

---

Method 3

OFFSET

```sql
SELECT DISTINCT Salary
FROM Employee
ORDER BY Salary DESC
OFFSET 1 ROW
FETCH NEXT 1 ROW ONLY;
```

Ask

Which one works with duplicates?

Expected

DENSE_RANK()

---

# Challenge 4

Find duplicate emails.

```sql
SELECT Email,
COUNT(*)
FROM Customer
GROUP BY Email
HAVING COUNT(*)>1;
```

Then ask

Delete duplicates while keeping first row.

Window Function.

---

# Challenge 5

Customers without orders

Tables

Customer

Orders

Expected

```sql
SELECT c.*
FROM Customer c
LEFT JOIN Orders o
ON c.id=o.customerid
WHERE o.customerid IS NULL;
```

Now ask

Can NOT EXISTS solve it?

Yes.

```sql
SELECT *
FROM Customer c
WHERE NOT EXISTS
(
SELECT 1
FROM Orders o
WHERE o.CustomerID=c.CustomerID
);
```

Discuss why `NOT EXISTS` is often preferred over `NOT IN` when `NULL` values are present.

---

# Challenge 6

Nth Highest Salary

```sql
SELECT *
FROM
(
SELECT *,
DENSE_RANK()
OVER
(
ORDER BY Salary DESC
) r
FROM Employee
)t
WHERE r=5;
```

Ask

Can this be generalized?

---

# Challenge 7

Running Total

Sales

| Day | Sales |
| --- | ----- |
| 1   | 100   |
| 2   | 200   |
| 3   | 400   |

Expected

```sql
SUM(Sales)
OVER
(
ORDER BY Day
)
```

Explain

Window functions don't collapse rows.

Huge interview point.

---

# Challenge 8

Difference between

ROW_NUMBER

RANK

DENSE_RANK

Show

Salary

100

100

90

80

Result

ROW_NUMBER

1

2

3

4

RANK

1

1

3

4

DENSE_RANK

1

1

2

3

Students remember forever.

---

# Challenge 9

Top 3 Salaries in each Department

```sql
SELECT *
FROM
(
SELECT *,
DENSE_RANK()
OVER
(
PARTITION BY DeptID
ORDER BY Salary DESC
) r
FROM Employee
)t
WHERE r<=3;
```

Very common Amazon/TCS/Infosys question.

---

# Challenge 10

Find consecutive login days.

Use

```sql
LAG()

LEAD()
```

Excellent advanced question.

---

# Database Design Round

Instead of definitions

Ask

> Why shouldn't student marks be stored repeatedly in multiple tables?

Students answer

Redundancy.

Then explain

1NF

↓

2NF

↓

3NF

↓

BCNF

using one running example.

---

# Indexing

Show

Table

10 million rows

Query

```sql
SELECT *
FROM Employee
WHERE Email='abc@gmail.com';
```

Ask

Without index?

Linear search.

With index?

B-Tree lookup.

Then ask

Why not create index on every column?

Students usually fail.

Answer

INSERT

UPDATE

DELETE become slower.

---

# ACID

Instead of definitions

Use UPI payment.

Debit

↓

Network fails

↓

Credit doesn't happen

Why?

Atomicity.

Consistency

Balance always correct.

Isolation

Two users booking same seat.

Durability

Power failure after commit.

This sticks.

---

# Rapid Fire (Last 10 Minutes)

Display one question every 30 seconds.

1.

Difference between WHERE and HAVING?

---

2.

COUNT(*)

COUNT(column)

COUNT(DISTINCT)

---

3.

NULL=NULL?

(False in SQL; comparisons with `NULL` yield unknown. Use `IS NULL`.)

---

4.

DELETE

TRUNCATE

DROP

---

5.

UNION

UNION ALL

---

6.

CHAR

VARCHAR

---

7.

EXISTS

IN

---

8.

PRIMARY KEY

UNIQUE KEY

---

9.

Clustered

Non-clustered Index

---

10.

Which is faster?

JOIN

Subquery

(Answer: neither inherently; it depends on the optimizer and execution plan.)

---

# Fun Puzzle

```
A

1
2
3

B

2
3
4
```

Ask students to write SQL for:

✔ Common values

✔ Values only in A

✔ Values only in B

✔ All values

✔ All values removing duplicates

This covers

INTERSECT

EXCEPT

UNION

UNION ALL

---

# Final Slide: The 15 SQL Questions Every Placement Candidate Should Master

1. Second highest salary.
2. Nth highest salary.
3. Highest salary per department.
4. Employees above department average.
5. Duplicate records.
6. Remove duplicates.
7. Customers without orders.
8. Top N per group.
9. Running total.
10. Previous/next row (`LAG`/`LEAD`).
11. Difference between `WHERE` and `HAVING`.
12. `INNER` vs `LEFT` vs `RIGHT` vs `FULL` JOIN.
13. `ROW_NUMBER` vs `RANK` vs `DENSE_RANK`.
14. `UNION` vs `UNION ALL`.
15. Indexes, normalization, and ACID.


