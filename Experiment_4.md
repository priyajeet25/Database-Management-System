# SQL Experiment No.4 – Functions and Salary Operations


### 1. Display employees who joined before 30-Jun-1980 or after 31-Dec-1981
```sql
SELECT *
FROM EMPLOYEE
WHERE HIREDATE < '1980-06-30'
   OR HIREDATE > '1981-12-31';
```

**Alternative Query**
```sql
SELECT *
FROM EMPLOYEE
WHERE HIREDATE NOT BETWEEN '1980-06-30' AND '1981-12-31';
```

---

### 2. Display employees whose second alphabet is A
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE ENAME LIKE '_A%';
```

---

### 3. Display employees whose names are exactly 5 characters
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE ENAME LIKE '_____';
```

---

### 4. Display employees whose second alphabet is A
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE ENAME LIKE '_A%';
```

---

### 5. Display employees not working as salesman, clerk or analyst
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB NOT IN ('SALESMAN', 'CLERK', 'ANALYST');
```

---

### 6. Display employee annual salary with highest first
```sql
SELECT ENAME, (SAL * 12) AS ANNUAL_SALARY
FROM EMPLOYEE
ORDER BY ANNUAL_SALARY DESC;
```

---

### 7. Display name, salary, HRA, DA, PF and total salary
```sql
SELECT
    ENAME,
    SAL,
    SAL * 0.15 AS HRA,
    SAL * 0.10 AS DA,
    SAL * 0.05 AS PF,
    (SAL + (SAL * 0.15) + (SAL * 0.10) - (SAL * 0.05)) AS TOTALSAL
FROM EMPLOYEE
ORDER BY TOTALSAL, HRA, DA, PF;
```

---

### 8. Update salary by 10% for employees without commission
```sql
UPDATE EMPLOYEE
SET SAL = SAL + (SAL * 0.10)
WHERE COMM IS NULL;
```

---

### 9. Display employees whose salary is more than 3000 after 20% increment
```sql
SELECT ENAME, SAL, (SAL * 1.20) AS INCREMENTED_SAL
FROM EMPLOYEE
WHERE (SAL * 1.20) > 3000;
```

---

### 10. Display employees whose salary contains at least 3 digits
```sql
SELECT ENAME, SAL
FROM EMPLOYEE
WHERE SAL >= 100;
```

---
