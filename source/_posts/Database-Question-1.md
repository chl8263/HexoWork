---
title: Database Question 1
date: 2019-11-29 23:34:53
tags: ["Oracle"]
categories: ["Develop","Oracle"]
---

Oracle Database practice question 1.
<!-- more -->

This Database practice question using the 'SCOTT' in oracle.

### 1. Print EMPNO,ENAME with EMPNO number 7369,7698
~~~
SELECT EMPNO, ENAME
  FROM EMP
 WHERE EMPNO IN ('7369','7698')
~~~

### 2. Print EMPNO, ENAME without EMPNO number 7369,7698
~~~
SELECT EMPNO, ENAME
  FROM EMP
 WHERE EMPNO NOT IN ('7369','7698')
~~~

### 3. Print all EMP table information with SAL between 3000 and 5000.
~~~
SELECT *
  FROM EMP
 WHERE SAL BETWEEN 3000 AND 5000
~~~

### 4. Print all EMP table information with HIREDATE greater than 12-1-1981.
~~~
SELECT *
  FROM emp
 WHERE hiredate > '01-DEC-81'
~~~

### 5. Print max value EMPNO with job SALESMAN in EMP table.
~~~
SELECT max(empno)
  FROM emp
 WHERE job IN 'SALESMAN'
~~~
