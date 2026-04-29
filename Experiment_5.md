# SQL Experiment No.5 – Aggregate and String Functions

### 1. Display total number of employees working in the company
```sql
SELECT COUNT(*) AS TOTAL_EMPLOYEES
FROM EMPLOYEE;
```

---

### 2. Display total salary being paid to all employees
```sql
SELECT SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE;
```

---

### 3. Display maximum salary
```sql
SELECT MAX(SAL) AS MAX_SALARY
FROM EMPLOYEE;
```

---

### 4. Display minimum salary
```sql
SELECT MIN(SAL) AS MIN_SALARY
FROM EMPLOYEE;
```

---

### 5. Display average salary
```sql
SELECT AVG(SAL) AS AVERAGE_SALARY
FROM EMPLOYEE;
```

---

### 6. Display maximum salary paid to clerk
```sql
SELECT MAX(SAL) AS MAX_CLERK_SALARY
FROM EMPLOYEE
WHERE JOB = 'CLERK';
```

---

### 7. Display maximum salary in department 20
```sql
SELECT MAX(SAL) AS MAX_SALARY_DEPT20
FROM EMPLOYEE
WHERE DEPTNO = 20;
```

---

### 8. Display minimum salary paid to salesman
```sql
SELECT MIN(SAL) AS MIN_SALESMAN_SALARY
FROM EMPLOYEE
WHERE JOB = 'SALESMAN';
```

---

### 9. Display average salary of managers
```sql
SELECT AVG(SAL) AS AVG_MANAGER_SALARY
FROM EMPLOYEE
WHERE JOB = 'MANAGER';
```

---

### 10. Display total salary of analyst in department 40
```sql
SELECT SUM(SAL) AS TOTAL_ANALYST_SALARY
FROM EMPLOYEE
WHERE JOB = 'ANALYST'
AND DEPTNO = 40;
```

---

### 11. Display employee names in uppercase
```sql
SELECT UPPER(ENAME) AS EMPLOYEE_NAME
FROM EMPLOYEE;
```

---

### 12. Display employee names in lowercase
```sql
SELECT LOWER(ENAME) AS EMPLOYEE_NAME
FROM EMPLOYEE;
```

---

### 13. Display employee names in proper case
```sql
SELECT CONCAT(
       UPPER(LEFT(ENAME,1)),
       LOWER(SUBSTRING(ENAME,2))
) AS EMPLOYEE_NAME
FROM EMPLOYEE;
```

---

### 14. Display length of your name
```sql
SELECT LENGTH('SANDEEP') AS NAME_LENGTH;
```

> Replace `'SANDEEP'` with your own name if needed.

---

### 15. Display length of all employee names
```sql
SELECT ENAME, LENGTH(ENAME) AS NAME_LENGTH
FROM EMPLOYEE;
```
