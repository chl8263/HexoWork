---
title: Database Question 3
date: 2019-12-01 22:35:40
tags: ["Oracle"]
categories: ["Develop","Oracle"]
---

Database Question 3

<!-- more -->

### 1. Print each employee grade at EMP table as in the example below.

{% asset_img 1.PNG %}
~~~
SELECT empno, ename, sal, CASE
                            WHEN sal BETWEEN 700 AND 1200 THEN 1
                            WHEN sal BETWEEN 1201 AND 1400 THEN 2
                            WHEN sal BETWEEN 1401 AND 2000 THEN 3
                            WHEN sal BETWEEN 2001 AND 3000 THEN 4
                            WHEN sal BETWEEN 3001 AND 9999 THEN 5
                            END grade
  FROM emp
 ORDER BY grade
~~~

~~~
SELECT empno, ename, sal, grade
  FROM emp
  JOIN salgrade
    ON emp.sal >= salgrade.losal AND emp.sal <= salgrade.hisal
 ORDER BY grade ASC
~~~

### 2.Print employee information which over average SAL at EMP table.

{% asset_img 2.PNG %}

~~~
SELECT empno, ename, job, sal
  FROM EMP
 WHERE sal > (SELECT ROUND(AVG(sal),1)
               FROM emp
             )
 ORDER BY sal DESC
~~~

### 3. Print employee information which over than average SAL in department at EMP table as in the example below.

{% asset_img 3.PNG %}

~~~
SELECT dname, empno, ename, job, sal
  FROM emp e
 INNER JOIN dept
    ON e.deptno = dept.deptno
 WHERE sal > ( SELECT ROUND(AVG(sal),1)
                 FROM emp
                WHERE emp.deptno = e.deptno
             )
 ORDER BY sal DESC
~~~

### 4. Print the number of people by SAL rank for each employee at EMP table as in the example below. (Join SALGRADE table)

{% asset_img 4.PNG %}

~~~

SELECT grade, losal, hisal, COUNT(*) AS cnt
  FROM emp
  JOIN salgrade
    ON emp.sal >= salgrade.losal AND emp.sal <= salgrade.hisal
 GROUP BY grade, losal, hisal
 ORDER BY grade
~~~

### 5. Print employee information which department name is 'RESEARCH' or department location is 'NEW YORK'.

{% asset_img 5.PNG %}

~~~
## 5. Print employee information which department name is 'RESEARCH' or department location is 'NEW YORK'.
~~~
