---
title: SQL-Quiz-7
date: 2020-01-02 22:26:35
tags: ["Oracle"]
categories: ["Develop","Oracle"]
---
SQL Quiz 7

<!-- more -->

### 1. In EMP table, print update sentence whose employees with a job of 'SALESMAN' to 400.

~~~
UPDATE EMP_BAK_TABLE
   SET sal = sal + 400
 WHERE job = 'SALESMAN'
~~~

### 2. In EMP table, print update sentence that adds a year as employees whose salary higher than their average salary

~~~
UPDATE EMP_BAK_TABLE
   SET hiredate = hiredate + (INTERVAL '1' YEAR)
 WHERE sal > (SELECT AVG(sal) FROM emp)
~~~

### 3. In EMP table, print update sentence that adds 100 in COMM column and multiply 2 times for employee whose job of 'CLERK' and multiply 3 times for employee whose job of 'MANAGER' and multiply 4 times for employee whose have another job.

~~~
UPDATE EMP_BAK_TABLE
   SET COMM = COMM + 100,
       SAL = CASE
  WHEN job = 'CLERK' THEN sal * 2
  WHEN job = 'MANAGER' THEN sal * 3
  ELSE sal * 4
END
~~~

### 4. In EMP table, print delete sentence that employee whose name start with 'M'.

~~~
DELETE FROM EMP_BAK_TABLE
 WHERE ename LIKE 'M%'
~~~

### 5. In EMP table, print delete sentence that employee whose salary higher than another average salary.

~~~
DELETE FROM EMP_BAK_TABLE
 WHERE sal > (SELECT AVG(sal) FROM EMP_BAK_TABLE);
~~~
