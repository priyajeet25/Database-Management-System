# SQL Experiment No.11 – Advanced Queries, Delete Operations and Ranking
---

### 1. Delete employees joined before 31-Dec-1982 from New York or Chicago departments
```sql
DELETE FROM EMPLOYEE
WHERE HIREDATE < '1982-12-31'
AND DEPTNO IN (
    SELECT DEPTNO
    FROM DEPARTMENT
    WHERE LOCATION IN ('NEW YORK', 'CHICAGO')
);
```

---

### 2. Display managers with department name and location
```sql
SELECT 
    E.ENAME,
    E.JOB,
    D.DNAME,
    D.LOCATION
FROM EMPLOYEE E
JOIN DEPARTMENT D 
ON E.DEPTNO = D.DEPTNO
WHERE E.JOB = 'MANAGER';
```

---

### 3. Display FORD salary if equal to highest salary in his grade
```sql
SELECT E.ENAME, E.SAL
FROM EMPLOYEE E
JOIN SALGRADE S 
ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.ENAME = 'FORD'
AND E.SAL = (
    SELECT MAX(E2.SAL)
    FROM EMPLOYEE E2
    JOIN SALGRADE S2 
    ON E2.SAL BETWEEN S2.LOSAL AND S2.HISAL
    WHERE S2.GRADE = S.GRADE
);
```

---

### 4. Find top 5 earners of company
```sql
SELECT ENAME, SAL
FROM EMPLOYEE
ORDER BY SAL DESC
LIMIT 5;
```

---

### 5. Display employees getting highest salary
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE);
```

---

### 6. Display employees whose salary equals average of max and min salary
```sql
SELECT ENAME, SAL
FROM EMPLOYEE
WHERE SAL = (
    (SELECT MAX(SAL) FROM EMPLOYEE) +
    (SELECT MIN(SAL) FROM EMPLOYEE)
) / 2;
```

---

### 7. Display department names where at least 3 employees work
```sql
SELECT D.DNAME
FROM DEPARTMENT D
JOIN EMPLOYEE E ON D.DEPTNO = E.DEPTNO
GROUP BY D.DNAME
HAVING COUNT(*) >= 3;
```

---

### 8. Display managers earning more than company average salary
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB = 'MANAGER'
AND SAL > (SELECT AVG(SAL) FROM EMPLOYEE);
```

---

### 9. Display managers earning more than average salary of their employees
```sql
SELECT M.ENAME
FROM EMPLOYEE M
WHERE M.JOB = 'MANAGER'
AND M.SAL > (
    SELECT AVG(E.SAL)
    FROM EMPLOYEE E
    WHERE E.MGR = M.EMPNO
);
```

---

### 10. Display employees whose net pay is greater than or equal to any employee salary
```sql
SELECT ENAME, SAL, COMM,
       (SAL + IFNULL(COMM,0)) AS NET_PAY
FROM EMPLOYEE
WHERE (SAL + IFNULL(COMM,0)) >= ANY (
    SELECT SAL FROM EMPLOYEE
);
```