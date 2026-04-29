# SQL Experiment No.12 – Nested Queries and Delete Operations

---

### 1. Display employees whose salary is less than manager but greater than any manager salary
```sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL < M.SAL
AND E.SAL > ANY (
    SELECT SAL
    FROM EMPLOYEE
    WHERE JOB = 'MANAGER'
);
```

---

### 2. Count employees whose salary is greater than manager salary
```sql
SELECT COUNT(*) AS TOTAL
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL > M.SAL;
```

---

### 3. Display managers working under another manager but not under president
```sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.JOB = 'MANAGER'
AND M.JOB <> 'PRESIDENT';
```

---

### 4. Delete departments with no employees
```sql
DELETE FROM DEPARTMENT
WHERE DEPTNO NOT IN (
    SELECT DISTINCT DEPTNO
    FROM EMPLOYEE
);
```

---

### 5. Delete employees whose department does not exist
```sql
DELETE FROM EMPLOYEE
WHERE DEPTNO NOT IN (
    SELECT DEPTNO
    FROM DEPARTMENT
);
```

---

### 6. Display employees whose salary is outside salary grade range
```sql
SELECT ENAME, SAL
FROM EMPLOYEE
WHERE SAL NOT BETWEEN 
    (SELECT MIN(LOSAL) FROM SALGRADE)
AND
    (SELECT MAX(HISAL) FROM SALGRADE);
```

---

### 7. Display employees whose net pay is greater than any salary in company
```sql
SELECT ENAME, SAL, COMM,
       (SAL + IFNULL(COMM,0)) AS NET_PAY
FROM EMPLOYEE
WHERE (SAL + IFNULL(COMM,0)) >= ANY (
    SELECT SAL
    FROM EMPLOYEE
);
```

---

### 8. Display employees working in SALES or RESEARCH
```sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE D.DNAME IN ('SALES', 'RESEARCH');
```

---

### 9. Display grade of JONES
```sql
SELECT S.GRADE
FROM EMPLOYEE E
JOIN SALGRADE S
ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.ENAME = 'JONES';
```

---

### 10. Display department names whose length equals employee count of any department
```sql
SELECT D.DNAME
FROM DEPARTMENT D
WHERE LENGTH(D.DNAME) IN (
    SELECT COUNT(*)
    FROM EMPLOYEE
    GROUP BY DEPTNO
);
```