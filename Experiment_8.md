# SQL Experiment No.8 – Joins and Self Joins

### 1. Display all employees with their department name
```sql
SELECT E.EMPNO, E.ENAME, D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D
ON E.DEPTNO = D.DEPTNO;
```

**Alternative Query**
```sql
SELECT E.ENAME, D.DNAME
FROM EMPLOYEE E, DEPARTMENT D
WHERE E.DEPTNO = D.DEPTNO;
```

---

### 2. Display employees whose manager is JONES
```sql
SELECT 
    E.ENAME AS EMPLOYEE,
    M.ENAME AS MANAGER
FROM EMPLOYEE E
JOIN EMPLOYEE M
ON E.MGR = M.EMPNO
WHERE M.ENAME = 'JONES';
```

---

### 3. Display employee name, job, department, manager and grade
```sql
CREATE TABLE SALGRADE (
    GRADE CHAR(1),
    LOSAL INT,
    HISAL INT
);
```

```sql
INSERT INTO SALGRADE VALUES
('A', 700, 1200),
('B', 1201, 1400),
('C', 1401, 2000),
('D', 2001, 3000),
('E', 3001, 9999);
```

```sql
SELECT e.ENAME, e.JOB, d.DNAME, m.ENAME AS MANAGER, s.GRADE
FROM EMPLOYEE e
JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO
LEFT JOIN EMPLOYEE m ON e.MGR = m.EMPNO
JOIN SALGRADE s ON e.SAL BETWEEN s.LOSAL AND s.HISAL
ORDER BY d.DNAME;
```

---

### 4. Display employees except clerks sorted by highest salary
```sql
SELECT e.ENAME, e.JOB, e.SAL, s.GRADE, d.DNAME
FROM EMPLOYEE e
JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO
JOIN SALGRADE s ON e.SAL BETWEEN s.LOSAL AND s.HISAL
WHERE e.JOB <> 'CLERK'
ORDER BY e.SAL DESC;
```

---

### 5. Display employee name, job and manager including employees without manager
```sql
SELECT e.ENAME, e.JOB, m.ENAME AS MANAGER
FROM EMPLOYEE e
LEFT JOIN EMPLOYEE m ON e.MGR = m.EMPNO;
```

---

### 6. Employees earning 36000 annually or not clerks
```sql
SELECT e.ENAME, e.JOB, (e.SAL * 12) AS ANNUAL_SAL,
       e.DEPTNO, d.DNAME, s.GRADE
FROM EMPLOYEE e
JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO
JOIN SALGRADE s ON e.SAL BETWEEN s.LOSAL AND s.HISAL
WHERE (e.SAL * 12) >= 36000
   OR e.JOB <> 'CLERK';
```

---

### 7. Employees earning 30000 annually and not clerks
```sql
SELECT e.ENAME, e.JOB, (e.SAL * 12) AS ANNUAL_SAL,
       e.DEPTNO, d.DNAME, s.GRADE
FROM EMPLOYEE e
JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO
JOIN SALGRADE s ON e.SAL BETWEEN s.LOSAL AND s.HISAL
WHERE (e.SAL * 12) = 30000
  AND e.JOB <> 'CLERK';
```

---

### 8. Display employees with manager name and number
```sql
SELECT e.EMPNO, e.ENAME,
       COALESCE(CAST(m.EMPNO AS CHAR), 'No Manager') AS MGR_NO,
       COALESCE(m.ENAME, 'No Manager') AS MGR_NAME
FROM EMPLOYEE e
LEFT JOIN EMPLOYEE m ON e.MGR = m.EMPNO;
```

---

### 9. Display department name, department number and total salary
```sql
SELECT d.DEPTNO, d.DNAME, SUM(e.SAL) AS TOTAL_SAL
FROM EMPLOYEE e
JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO
GROUP BY d.DEPTNO, d.DNAME;
```

---

### 10. Display employee number, name and department location
```sql
ALTER TABLE DEPARTMENT
ADD LOCATION VARCHAR(20);
```

```sql
UPDATE DEPARTMENT SET LOCATION = 'MUMBAI' WHERE DEPTNO = 10;
UPDATE DEPARTMENT SET LOCATION = 'CHENNAI' WHERE DEPTNO = 20;
UPDATE DEPARTMENT SET LOCATION = 'HYDERABAD' WHERE DEPTNO = 30;
UPDATE DEPARTMENT SET LOCATION = 'DELHI' WHERE DEPTNO = 40;
```

```sql
SELECT e.EMPNO, e.ENAME, d.LOCATION
FROM EMPLOYEE e
JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO;
```

---

### 11. Display employee name and department name
```sql
SELECT e.ENAME, d.DNAME
FROM EMPLOYEE e
JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO;
```

---

