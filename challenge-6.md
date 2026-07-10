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

## Next Question

Can this be generalized?
