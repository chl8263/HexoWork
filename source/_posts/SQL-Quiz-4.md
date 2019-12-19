---
title: SQL Quiz 4
date: 2019-12-05 23:50:47
tags: ["Oracle"]
categories: ["Develop","Oracle"]
---

SQL Quiz 4

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

~~~
SELECT MAX(CASE grade
        WHEN 1
        THEN 700 ||'~'|| 1200
        END
        ) AS GRADE_1
        ,
        MAX(CASE grade
        WHEN 2
        THEN 1201 ||'~'|| 1400
        END
        ) AS GRADE_2
        ,
        MAX(CASE grade
        WHEN 3
        THEN 1401 ||'~'|| 2000
        END
        ) AS GRADE_3
        ,
        MAX(CASE grade
        WHEN 4
        THEN 2001 ||'~'|| 3000
        END
        ) AS GRADE_4
        ,
        MAX(CASE grade
        WHEN 5
        THEN 3001 ||'~'|| 9999
        END
        ) AS GRADE_5
  FROM salgrade
~~~

### 5. First, make SALGRADE_TEMP table as example below, Print example which in the horizontal example to vertical example below.

{% asset_img 5.PNG %}

~~~
CREATE TABLE HORIZONAL_SALGRADE(
    GRADE_1 VARCHAR2(30),
    GRADE_2 VARCHAR2(30),
    GRADE_3 VARCHAR2(30),
    GRADE_4 VARCHAR2(30),
    GRADE_5 VARCHAR2(30)
)

INSERT INTO horizonal_salgrade(
    grade_1,grade_2,grade_3,grade_4,grade_5
)
VALUES (
    '700~1200','1201~1400','1401~2000','2001~3000','3001~9999'
)
~~~

~~~

~~~
