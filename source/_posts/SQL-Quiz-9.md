---
title: SQL-Quiz-9
date: 2020-01-02 22:32:51
tags: ["Oracle"]
categories: ["Develop","Oracle"]
---

SQL Quiz 9

<!-- more -->

### 1. In the employee table, the salary subtotal and sum by department number (DEPTNO) and job (JOB) Print it out like the example below.
{% asset_img 1.PNG %}

~~~
SELECT deptno,
       job,
       SUM(sal) SUM_SAL
  FROM emp
 GROUP BY ROLLUP(deptno, job)
 ORDER BY deptno, job
~~~

### 2. In the employee table, the salary subtotal and sum by department number (DEPTNO) and job (JOB) Print it out like the example below.
{% asset_img 2.PNG %}

~~~
SELECT deptno, job, SUM(sal) sum_sal
  FROM emp
 WHERE deptno IS NOT NULL
 GROUP BY CUBE(deptno, job)
 ORDER BY deptno, job DESC
~~~

### 3. Specify the salary subtotal and total by department name (DNAME) and job (JOB).Print it like an example.
{% asset_img 3.PNG %}

~~~
SELECT CASE
        WHEN dname IS NULL THEN '합계'
        ELSE dname
       END AS dname,
       CASE
        WHEN job IS NULL AND dname <> '합계' THEN '소계'
        ELSE job
       END AS job,
       SUM(sal) sum_sal
  FROM emp
 INNER JOIN dept
    ON emp.deptno = dept.deptno
 WHERE emp.deptno IS NOT NULL
 GROUP BY ROLLUP(dname, job)
 ORDER BY dname
~~~

### 4. Specify the salary subtotal and total by department name (DNAME) and job (JOB).Only the top one is shown and salary is in amount (thousands,) as in the example below Do you print.
{% asset_img 4.PNG %}

~~~
SELECT CASE GROUPING(dname)
        WHEN 1 THEN '합계'
        ELSE (CASE
                WHEN job = FIRST_VALUE(job) OVER()
                THEN dname ELSE NULL
              END)
        END AS dname,
        CASE GROUPING(job)
          WHEN 1 THEN (CASE GROUPING(dname)
          WHEN 1 THEN ''
          WHEN 0 THEN '소계'
        ELSE job
        END)
        ELSE job
        END AS job,
        TO_CHAR( SUM(sal) , '999,999') AS SUM_SAL
  FROM emp
 INNER JOIN dept
    ON emp.deptno = dept.deptno
 GROUP BY ROLLUP(dname, job)
~~~

### 5. Specify the salary subtotal and total by department name (DNAME) and job (JOB).Only the top one is shown and salary is in amount (thousands,) as in the example below Print only the data of salary more than 1000 by department name and occupation?.
{% asset_img 5.PNG %}

~~~
SELECT CASE GROUPING(dname)
          WHEN 1 THEN '합계'
          ELSE (CASE
                  WHEN job = (FIRST_VALUE(job) OVER(PARTITION BY DNAME ORDER BY JOB ROWS UNBOUNDED PRECEDING))
                  THEN dname ELSE NULL
                END)
          END AS dname,
       CASE GROUPING(job)
          WHEN 1 THEN (CASE GROUPING(dname)
                          WHEN 1 THEN ''
                          WHEN 0 THEN '소계'
                          ELSE job
                      END)
          ELSE job
          END AS job,
       TO_CHAR( SUM(sal) , '999,999') AS SUM_SAL
  FROM (SELECT * FROM EMP WHERE sal > 1000) emp
 INNER JOIN dept
    ON emp.deptno = dept.deptno
 GROUP BY ROLLUP(dname, job)
~~~
