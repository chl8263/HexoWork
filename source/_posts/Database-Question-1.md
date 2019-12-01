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
