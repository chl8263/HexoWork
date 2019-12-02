---
title: Database Question 2
date: 2019-12-01 13:07:45
tags: ["Oracle"]
categories: ["Develop","Oracle"]
---

<!-- more -->

### 1. Print DNAME, EMPNO, ENAME for each employee from EMP table as in the example below. (Do not print employee without department when joining tables)

{% asset_img 1.PNG %}
~~~
SELECT DNAME, EMPNO,ENAME
  FROM emp
 INNER JOIN dept
    ON emp.deptno = dept.deptno
 WHERE emp.deptno IS NOT NULL
 ORDER BY DNAME
~~~

### 2. Print DNAME, EMPNO, ENAME for eaxh employee from EMP table as in the example below. (Print employee without department when joining tables)

{% asset_img 2.PNG %}
~~~
SELECT DNAME, EMPNO,ENAME
  FROM emp
 INNER JOIN dept
    ON emp.deptno = dept.deptno
 ORDER BY DNAME
~~~

### 3. Print employee information in the department location 'DALLAS', 'CHICAGO' as in the example below.

{% asset_img 3.PNG %}
~~~
SELECT dept.loc, emp.deptno, emp.ename
  FROM emp
 INNER JOIN dept
    ON emp.deptno = dept.deptno
 WHERE dept.loc IN ('DALLAS', 'CHICAGO')
 ORDER By dept.loc
~~~

### 4. 
