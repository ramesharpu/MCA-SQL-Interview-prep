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

## Next Question

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

