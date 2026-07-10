
# Challenge 4

Find duplicate emails.

```sql
SELECT Email,
COUNT(*)
FROM Customer
GROUP BY Email
HAVING COUNT(*)>1;
```

## Next Question

Delete duplicates while keeping first row.

Window Function.
