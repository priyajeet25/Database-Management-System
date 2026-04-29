# SQL Experiment No.9 – Subqueries

---

### 1. Display employee name who earns highest salary
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE);
```

---

### 2. Display clerk earning highest salary among clerks
```sql
SELECT EMPNO, ENAME
FROM EMPLOYEE
WHERE JOB = 'CLERK'
AND SAL = (
    SELECT MAX(SAL)
    FROM EMPLOYEE
    WHERE JOB = 'CLERK'
);
```

---

### 3. Display salesmen earning more than highest paid clerk
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB = 'SALESMAN'
AND SAL > (
    SELECT MAX(SAL)
    FROM EMPLOYEE
    WHERE JOB = 'CLERK'
);
```

---

### 4. Display clerks earning more than JAMES but less than SCOTT
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB = 'CLERK'
AND SAL > (
    SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES'
)
AND SAL < (
    SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT'
);
```

---

### 5. Display employees earning more than JAMES or SCOTT
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE SAL > (
    SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES'
)
OR SAL > (
    SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT'
);
```

---

### 6. Display employees earning highest salary in each department
```sql
SELECT ENAME, DEPTNO, SAL
FROM EMPLOYEE E
WHERE SAL = (
    SELECT MAX(SAL)
    FROM EMPLOYEE
    WHERE DEPTNO = E.DEPTNO
);
```

---

### 7. Display employees earning highest salary in each job group
```sql
SELECT ENAME, JOB, SAL
FROM EMPLOYEE E
WHERE SAL = (
    SELECT MAX(SAL)
    FROM EMPLOYEE
    WHERE JOB = E.JOB
);
```

---

### 8. Display employees working in ACCOUNTING department
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = (
    SELECT DEPTNO
    FROM DEPARTMENT
    WHERE DNAME = 'ACCOUNTING'
);
```

---

### 9. Display employees working in MUMBAI
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = (
    SELECT DEPTNO
    FROM DEPARTMENT
    WHERE LOCATION = 'MUMBAI'
);
```

---

### 10. Display job groups with total salary greater than max manager salary
```sql
SELECT JOB, SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE
GROUP BY JOB
HAVING SUM(SAL) > (
    SELECT MAX(SAL)
    FROM EMPLOYEE
    WHERE JOB = 'MANAGER'
);
```