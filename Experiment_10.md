# SQL Experiment No.10 – Advanced Subqueries using ANY and ALL

---

### 1. Employees from department 10 with salary greater than ANY employee in other departments
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = 10
AND SAL > ANY (
    SELECT SAL
    FROM EMPLOYEE
    WHERE DEPTNO <> 10
);
```

---

### 2. Employees from department 10 with salary greater than ALL employees in other departments
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = 10
AND SAL > ALL (
    SELECT SAL
    FROM EMPLOYEE
    WHERE DEPTNO <> 10
);
```

---

### 3. Display employees in SALES department with grade C
```sql
SELECT E.*
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE D.DNAME = 'SALES'
AND S.GRADE = 'C';
```

---

### 4. Display employees who are not managers but manage someone
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB <> 'MANAGER'
AND EMPNO IN (
    SELECT MGR
    FROM EMPLOYEE
    WHERE MGR IS NOT NULL
);
```

---

### 5. Display employees whose manager is JONES
```sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE M.ENAME = 'JONES';
```

---

### 6. Display employees working in SALES department
```sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE D.DNAME = 'SALES';
```

---

### 7. Display employee name, department, salary and commission for salary between 2000–5000 in Mumbai
```sql
SELECT E.ENAME, D.DNAME, E.SAL, E.COMM
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE E.SAL BETWEEN 2000 AND 5000
AND D.LOCATION = 'MUMBAI';
```

---

### 8. Display employees whose salary is greater than manager salary
```sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL > M.SAL;
```

---

### 9. Display employees working in same department as manager
```sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.DEPTNO = M.DEPTNO;
```

---

### 10. Display employee name and grade for dept 10 or 30, grade not D, joined before 31-Dec-1982
```sql
SELECT E.ENAME, S.GRADE
FROM EMPLOYEE E
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.DEPTNO IN (10, 30)
AND S.GRADE <> 'D'
AND E.HIREDATE < '1982-12-31';
```

---
