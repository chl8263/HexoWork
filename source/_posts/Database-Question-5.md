---
title: Database Question 5
date: 2019-12-09 00:25:02
tags: ["Oracle"]
categories: ["Develop","Oracle"]
---

Database Question 5

<!-- more -->

### 1. In EMP table, assume three columns, EMPNO, MGR and SAL with just numeric meaning, print max value, minimum value of three value as in the example below. (If EMPNO, MGR, SAL value are null, change them to 0)
{% asset_img 1.PNG %}

~~~
SELECT empno,
       mgr,
       sal,
       GREATEST(NVL(empno,0),
       NVL(mgr,0),
       NVL(sal,0)) AS MAX_VALUE,
       LEAST(NVL(empno,0),
       NVL(mgr,0),
       NVL(sal,0)) AS MIN_VALUE
  from emp
~~~

### 2. In DEPT table, if column length is over 6 digit, show them 5 digit and add '..' to the back.
{% asset_img 2.PNG %}

~~~
SELECT dname,
       CASE WHEN LENGTH(dname) > 5
            THEN CONCAT(SUBSTR(dname,1,5),'..')
            ELSE dname
       END AS DATA
  FROM DEPT
~~~

### 3. In EMP table, print last day of HIREDATE month and WORK_DAY from HIREDATE to 2006/08/05 as in example below.
{% asset_img 3.PNG %}

~~~
SELECT empno,
       hiredate,
       LAST_DAY(hiredate),
       TO_DATE('20060805', 'YYYYMMDD') - TRUNC(hiredate) AS WORK_DAY
  FROM emp
 ORDER BY WORK_DAY DESC
~~~

### 4. Print the person with the highest workdays in solution number 3.
{% asset_img 4.PNG %}
~~~

~~~

### 4. Print the person with highest person and lowest person each in solution number 3.
{% asset_img 5.PNG %}

~~~

~~~
