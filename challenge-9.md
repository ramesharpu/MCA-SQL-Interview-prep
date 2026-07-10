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

