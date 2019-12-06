---
title: Database Question 2
date: 2019-12-01 13:07:45
tags: ["Oracle"]
categories: ["Develop","Oracle"]
---

Database Question 2

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

### 2. Print DNAME, EMPNO, ENAME for each employee from EMP table as in the example below. (Print employee without department when joining tables)

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

### 4. Print max SAL value in the department as in the example below. (Do not print employee without department)

{% asset_img 4.PNG %}
~~~
SELECT deptno, MAX(sal) as SAL
  FROM emp
 GROUP BY deptno
~~~

### 5. Print employee information receiving the max SAL value in the department as the example below. (Except employee without department)
{% asset_img 5.PNG %}
~~~
SELECT deptno, sal ,empno , ename, job
  FROM emp
 WHERE (deptno, sal) IN (SELECT deptno, MAX(sal)
                           FROM emp
                          WHERE deptno IS NOT NULL
                          GROUP BY deptno
                        )
 ORDER BY deptno
~~~
