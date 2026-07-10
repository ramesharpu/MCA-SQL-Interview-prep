# Database Design Round


## Question

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

## Question:

Without index?

Linear search.

With index?

B-Tree lookup.

## Next Question

Why not create index on every column?

Students usually fail.

Answer

INSERT

UPDATE

DELETE become slower.

---

# ACID

Instead of definitions

# Example
UPI payment

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

