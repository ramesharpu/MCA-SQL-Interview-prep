# Rapid Fire

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

