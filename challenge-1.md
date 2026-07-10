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

Expected Answer

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

CTE version

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

