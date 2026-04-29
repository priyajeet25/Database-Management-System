# SQL Experiment No.7 – Group By, Date Functions and Formatting

---

### 1. Compute number of days remaining in current year
```sql
SELECT 
DATEDIFF(
    MAKEDATE(YEAR(CURDATE()) + 1, 1),
    CURDATE()
) AS DAYS_REMAINING;
```

**Alternative Query**
```sql
SELECT DATEDIFF(
    CONCAT(YEAR(CURDATE()), '-12-31'),
    CURDATE()
) AS DAYS_LEFT;
```

---

### 2. Find highest salary, lowest salary and difference
```sql
SELECT 
MAX(SAL) AS HIGHEST_SALARY,
MIN(SAL) AS LOWEST_SALARY,
MAX(SAL) - MIN(SAL) AS DIFFERENCE
FROM EMPLOYEE;
```

---

### 3. Employees whose commission is greater than 25% of salary
```sql
SELECT ENAME, SAL, COMM
FROM EMPLOYEE
WHERE COMM > (SAL * 0.25);
```

**Alternative with NULL handling**
```sql
SELECT ENAME, SAL, COMM
FROM EMPLOYEE
WHERE IFNULL(COMM,0) > SAL * 0.25;
```

---

### 4. Display salary in dollar format
```sql
SELECT ENAME,
CONCAT('$', FORMAT(SAL, 2)) AS SALARY_IN_DOLLAR
FROM EMPLOYEE;
```

**Salary conversion example (₹ to $ at rate 83)**
```sql
SELECT 
ENAME,
CONCAT('$ ', FORMAT(SAL / 83, 2)) AS SALARY_IN_DOLLAR
FROM EMPLOYEE;
```

---

### 5. Matrix query: salary by job and department
```sql
SELECT 
JOB,
SUM(CASE WHEN DEPTNO = 10 THEN SAL ELSE 0 END) AS DEPT10,
SUM(CASE WHEN DEPTNO = 20 THEN SAL ELSE 0 END) AS DEPT20,
SUM(CASE WHEN DEPTNO = 30 THEN SAL ELSE 0 END) AS DEPT30,
SUM(CASE WHEN DEPTNO = 40 THEN SAL ELSE 0 END) AS DEPT40,
SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE
GROUP BY JOB;
```

---

### 6. Display employees hired in 1980, 1981, 1982 and 1983
```sql
SELECT
COUNT(*) AS TOTAL_EMPLOYEES,
SUM(CASE WHEN YEAR(HIREDATE) = 1980 THEN 1 ELSE 0 END) AS HIRED_1980,
SUM(CASE WHEN YEAR(HIREDATE) = 1981 THEN 1 ELSE 0 END) AS HIRED_1981,
SUM(CASE WHEN YEAR(HIREDATE) = 1982 THEN 1 ELSE 0 END) AS HIRED_1982,
SUM(CASE WHEN YEAR(HIREDATE) = 1983 THEN 1 ELSE 0 END) AS HIRED_1983
FROM EMPLOYEE;
```

---

### 7. Get last Sunday of any month
```sql
SELECT 
DATE_SUB(
    LAST_DAY('2026-02-01'),
    INTERVAL (WEEKDAY(LAST_DAY('2026-02-01')) + 1) DAY
) AS LAST_SUNDAY;
```

---

### 8. Display department numbers and total employees
```sql
SELECT DEPTNO, COUNT(*) AS TOTAL_EMPLOYEES
FROM EMPLOYEE
GROUP BY DEPTNO;
```

---

### 9. Display jobs and employee count in each job group
```sql
SELECT JOB, COUNT(*) AS TOTAL_EMPLOYEES
FROM EMPLOYEE
GROUP BY JOB;
```

---

### 10. Display department numbers and total salary
```sql
SELECT DEPTNO, SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE
GROUP BY DEPTNO;
```

