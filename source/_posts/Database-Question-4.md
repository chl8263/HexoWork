---
title: Database Question 4
date: 2019-12-05 23:50:47
tags: ["Oracle"]
categories: ["Develop","Oracle"]
---

Database Question 4

<!-- more -->

### 1. Print number of 5 employee in high order of SAL at EMP table in the example below.

{% asset_img 1.PNG %}
~~~
SELECT *
  FROM (SELECT *
          FROM emp
         ORDER BY sal DESC
        )
 WHERE ROWNUM <= 5
~~~

### 2. When each employee ranks in the SAL order in the EMP table, print the ranks 6th to 10th as in the example below.

{% asset_img 2.PNG %}
~~~
SELECT *
  FROM ( SELECT empno, ename, job, mgr, hiredate, sal, comm, deptno, RANK() OVER(ORDER BY sal DESC) AS rn
           FROM emp         
        )
 WHERE RN >=6 AND RN <= 10
~~~

### 3. Explain why the result which in the example below is 0 matches.
~~~
SELECT ROWNUM, A.*
  FROM EMP A
 WHERE ROWNUM > 5
~~~

>> Rownum keyword execute after 'where' execute finished.


### 4. Print example which in the vertical example to horizontal example below.

{% asset_img 4.PNG %}

### 5. First, make SALGRADE_TEMP table as example below, Print example which in the horizontal example to vertical example below.

{% asset_img 5.PNG %}
