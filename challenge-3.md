
# Challenge 3

Second Highest Salary

## Three different solutions

## Method 1 
Using Sub-Query

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

## Next Question

Which one works with duplicates?

Expected

DENSE_RANK()

