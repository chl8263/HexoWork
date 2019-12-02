---
title: Database Question 2
date: 2019-12-01 13:07:45
tags: ["Oracle"]
categories: ["Develop","Oracle"]
---

Oracle Database practice question 2.
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

### 2.
