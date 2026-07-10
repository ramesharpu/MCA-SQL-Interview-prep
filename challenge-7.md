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

## Reason

Window functions don't collapse rows.

Huge interview point.

