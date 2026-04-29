# SQL Experiment No.6 – Date Functions and CASE Statements

---

### 1. Display empno, ename and department name instead of department number
```sql
SELECT 
    EMPNO,
    ENAME,
    CASE DEPTNO
        WHEN 10 THEN 'RESEARCH'
        WHEN 20 THEN 'ACCOUNTING'
        WHEN 30 THEN 'SALES'
        WHEN 40 THEN 'OPERATIONS'
    END AS DNAME
FROM EMPLOYEE;
```

---

### 2. Display your age in days
```sql
SELECT DATEDIFF(CURDATE(), '2000-01-01') AS AGE_IN_DAYS;
```

---

### 3. Display your age in months
```sql
SELECT TIMESTAMPDIFF(MONTH, '2000-01-01', CURDATE()) AS AGE_IN_MONTHS;
```

---

### 4. Display current date in formatted style
```sql
SELECT DATE_FORMAT(CURDATE(), '%D %M %W %Y') AS CURRENT_DATE;
```

---

### 5. Display joining information of SCOTT
```sql
SELECT 
CONCAT(
    ENAME,
    ' has joined the company on ',
    DATE_FORMAT(HIREDATE, '%W %D %M %Y')
) AS DETAILS
FROM EMPLOYEE
WHERE ENAME = 'SCOTT';
```

---

### 7. Find nearest Saturday after current date
```sql
SELECT DATE_ADD(
    CURDATE(),
    INTERVAL MOD(5 - WEEKDAY(CURDATE()) + 7, 7) DAY
) AS NEXT_SATURDAY;
```

---

### 8. Display current time
```sql
SELECT CURTIME() AS CURRENT_TIME;
```

---

### 9. Display date three months before current date
```sql
SELECT DATE_SUB(CURDATE(), INTERVAL 3 MONTH) AS DATE_BEFORE_3_MONTHS;
```

---

### 10. Display employees who joined in December
```sql
SELECT ENAME, HIREDATE
FROM EMPLOYEE
WHERE MONTH(HIREDATE) = 12;
```

---

### 11. Display employees whose first 2 digits of joining year match last 2 digits of salary
```sql
SELECT ENAME, HIREDATE, SAL
FROM EMPLOYEE
WHERE LEFT(DATE_FORMAT(HIREDATE,'%y'),2) = RIGHT(SAL,2);
```

---

### 12. Display employees whose 10% salary equals joining year
```sql
SELECT ENAME, SAL, HIREDATE
FROM EMPLOYEE
WHERE (SAL * 0.10) = YEAR(HIREDATE);
```

---

### 13. Display employees who joined before 15th of month
```sql
SELECT ENAME, HIREDATE
FROM EMPLOYEE
WHERE DAY(HIREDATE) < 15;
```

---

### 14. Display employees who joined after 15th of month
```sql
SELECT ENAME, HIREDATE
FROM EMPLOYEE
WHERE DAY(HIREDATE) > 15;
```

---

### 15. Display employees having joining date and department number
```sql
SELECT ENAME, HIREDATE, DEPTNO
FROM EMPLOYEE
WHERE HIREDATE IS NOT NULL
AND DEPTNO IS NOT NULL;
```

---

## Additional Examples

### Add 7 days
```sql
SELECT DATE_ADD('2025-01-01', INTERVAL 7 DAY);
```

### Subtract 3 hours
```sql
SELECT DATE_SUB('2025-01-01 12:00:00', INTERVAL 3 HOUR);
```

---
