
### Employee

| EmpID | EmpName | Gender | DeptID | ManagerID | Salary | HireDate   |
| ----- | ------- | ------ | ------ | --------- | ------ | ---------- |
| 101   | John    | M      | 10     | 105       | 70000  | 2021-01-10 |
| 102   | David   | M      | 10     | 105       | 80000  | 2020-06-15 |
| 103   | Mary    | F      | 20     | 106       | 60000  | 2022-03-20 |
| 104   | Lisa    | F      | 20     | 106       | 90000  | 2019-11-01 |
| 105   | Robert  | M      | 10     | NULL      | 120000 | 2018-05-18 |
| 106   | Nancy   | F      | 20     | NULL      | 115000 | 2017-09-12 |
| 107   | Sam     | M      | 30     | 108       | 50000  | 2023-02-11 |
| 108   | Kevin   | M      | 30     | NULL      | 100000 | 2016-07-07 |
| 109   | Priya   | F      | 40     | 110       | 85000  | 2021-12-22 |
| 110   | Anita   | F      | 40     | NULL      | 130000 | 2015-08-09 |
| 111   | Rahul   | M      | 10     | 105       | 80000  | 2024-01-15 |
| 112   | Sneha   | F      | 20     | 106       | 60000  | 2024-02-20 |

---

# 2. Department Table

### Department

| DeptID | DeptName  | Location  |
| ------ | --------- | --------- |
| 10     | IT        | Bangalore |
| 20     | HR        | Chennai   |
| 30     | Finance   | Hyderabad |
| 40     | Sales     | Mumbai    |
| 50     | Marketing | Delhi     |



---

# 3. Customer Table

### Customer

| CustomerID | CustomerName | City      |
| ---------- | ------------ | --------- |
| 1          | Alice        | Bangalore |
| 2          | Bob          | Mumbai    |
| 3          | Charlie      | Delhi     |
| 4          | Diana        | Chennai   |
| 5          | Ethan        | Hyderabad |

---

# 4. Orders Table

### Orders

| OrderID | CustomerID | Amount | OrderDate  |
| ------- | ---------- | ------ | ---------- |
| 1001    | 1          | 2500   | 2025-01-02 |
| 1002    | 1          | 3200   | 2025-01-05 |
| 1003    | 2          | 5000   | 2025-01-10 |
| 1004    | 4          | 4200   | 2025-01-15 |


---

# 5. Product Table

### Product

| ProductID | ProductName | Category    | Price |
| --------- | ----------- | ----------- | ----- |
| 1         | Laptop      | Electronics | 60000 |
| 2         | Mouse       | Electronics | 800   |
| 3         | Chair       | Furniture   | 5000  |
| 4         | Desk        | Furniture   | 12000 |
| 5         | Keyboard    | Electronics | 1500  |

---

# 6. Sales Table

### Sales

| SaleID | ProductID | SaleDate   | Amount |
| ------ | --------- | ---------- | ------ |
| 1      | 1         | 2025-01-01 | 1000   |
| 2      | 1         | 2025-01-02 | 1500   |
| 3      | 2         | 2025-01-03 | 1200   |
| 4      | 3         | 2025-01-04 | 2000   |
| 5      | 2         | 2025-01-05 | 1800   |
| 6      | 1         | 2025-01-06 | 2200   |

---

# 7. Student Table

### Student

| StudentID | Name  | Email                                     |
| --------- | ----- | ----------------------------------------- |
| 1         | Ravi  | [ravi@gmail.com](mailto:ravi@gmail.com)   |
| 2         | Asha  | [asha@gmail.com](mailto:asha@gmail.com)   |
| 3         | Raj   | [raj@gmail.com](mailto:raj@gmail.com)     |
| 4         | Anil  | [ravi@gmail.com](mailto:ravi@gmail.com)   |
| 5         | Meena | [asha@gmail.com](mailto:asha@gmail.com)   |
| 6         | Kiran | [kiran@gmail.com](mailto:kiran@gmail.com) |

Perfect duplicate example.

---

# 8. Attendance Table

### Attendance

| EmpID | AttendanceDate |
| ----- | -------------- |
| 101   | 2025-01-01     |
| 101   | 2025-01-02     |
| 101   | 2025-01-03     |
| 101   | 2025-01-05     |
| 102   | 2025-01-01     |
| 102   | 2025-01-03     |
| 102   | 2025-01-04     |

---

# Tables for Set Operations

### A

| ID |
| -- |
| 1  |
| 2  |
| 3  |
| 4  |

### B

| ID |
| -- |
| 3  |
| 4  |
| 5  |
| 6  |

Use these to demonstrate:

```sql
UNION
```

Result

```
1
2
3
4
5
6
```

---

```sql
UNION ALL
```

Result

```
1
2
3
4
3
4
5
6
```

---

```sql
INTERSECT
```

Result

```
3
4
```

---

```sql
EXCEPT
```

Result

```
1
2
```
