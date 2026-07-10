# Challenge 2

Highest salary in every department

Expected

```sql
SELECT DeptID,
MAX(Salary)
FROM Employee
GROUP BY DeptID;
```

## Next Question - Return employee names too.

Most students write

```sql
SELECT Name,
MAX(Salary)
```

Wrong.

## Correct answer

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

