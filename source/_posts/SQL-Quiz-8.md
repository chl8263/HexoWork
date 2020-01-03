---
title: SQL-Quiz-8
date: 2020-01-02 22:28:31
tags: ["Oracle"]
categories: ["Develop","Oracle"]
---

SQL Quiz 8

<!-- more -->

### 1. In EMP table, print number of employee and first hire date each job as example in the below.
{% asset_img 1.PNG %}

~~~
SELECT job, COUNT(job), MIN(hiredate)
  FROM emp
 GROUP BY job;
~~~

### 2. In EMP table, print number of employee each hire date as example in the below.
{% asset_img 2.PNG %}

~~~
SELECT TO_CHAR(hiredate, 'YYYY-MM') AS hiredate,
       COUNT(TO_CHAR(hiredate, 'YYYY-MM')) AS CNT
  FROM emp
 GROUP BY TO_CHAR(hiredate, 'YYYY-MM')
~~~

### 3. In EMP table, print number of more than 2 employee by date of employee as example in the below.
{% asset_img 3.PNG %}

~~~
SELECT TO_CHAR(hiredate, 'YYYY-MM') AS HIREDATE,
       COUNT(TO_CHAR(hiredate, 'YYYY-MM')) AS CNT
  FROM emp
 GROUP BY TO_CHAR(hiredate, 'YYYY-MM')
HAVING COUNT(TO_CHAR(hiredate, 'YYYY-MM')) >= 2
~~~

### 4. Print number of employee and sum of salary as example in the below. (Print 'NO DEPT' if employee who has not department)
{% asset_img 4.PNG %}

~~~
SELECT CASE
        WHEN d.dname = '' THEN 'NO DEPT'
        ELSE d.dname
       END AS DANME,
       COUNT(e.deptno) AS CNT,
       SUM(e.sal) AS SAL
  FROM emp e
 INNER JOIN dept d
    ON e.deptno = d. deptno
 GROUP BY d.dname
~~~
