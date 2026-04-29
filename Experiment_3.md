# SQL Experiment No.3 – Sorting and Filtering Queries

---

### 1. List all employees and jobs in Department 30 in descending order by salary
```sql
SELECT ENAME, JOB, SAL
FROM EMPLOYEE
WHERE DEPTNO = 30
ORDER BY SAL DESC;
```

---

### 2. List job and Department Number of employees whose names are five letters long, begin with A and end with N
```sql
SELECT JOB, DEPTNO
FROM EMPLOYEE
WHERE ENAME LIKE 'A___N';
```

---

### 3. Display employees whose names start with alphabet S
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE ENAME LIKE 'S%';
```

---

### 4. Display employees whose names end with alphabet S
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE ENAME LIKE '%S';
```

---

### 5. Display employees working in department 10, 20, 40 or working as clerk, salesman or analyst
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO IN (10,20,40)
OR JOB IN ('CLERK','SALESMAN','ANALYST');
```

---

### 6. Display employee number and names for employees who earn commission
```sql
SELECT EMPNO, ENAME
FROM EMPLOYEE
WHERE COMM IS NOT NULL
AND COMM > 0;
```

---

### 7. Display employee number and total salary for each employee
```sql
SELECT EMPNO, (SAL + IFNULL(COMM,0)) AS TOTAL_SALARY
FROM EMPLOYEE;
```

---

### 8. Display employee number and annual salary for each employee
```sql
SELECT EMPNO, (SAL * 12) AS ANNUAL_SALARY
FROM EMPLOYEE;
```

---

### 9. Display names of clerks earning salary more than 3000
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB = 'CLERK'
AND SAL > 3000;
```

---

### 10. Display employees working as clerk, salesman or analyst earning salary more than 3000
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB IN ('CLERK','SALESMAN','ANALYST')
AND SAL > 3000;
```

---
