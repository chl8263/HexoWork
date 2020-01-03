---
title: SQL Quiz 6
date: 2019-12-18 19:01:12
tags: ["Oracle"]
categories: ["Develop","Oracle"]
---

SQL Quiz 6

<!-- more -->

### 1. In EMP table, print SAL value as the cumulate in the EMPNO ascending sort order as example in the below.
{% asset_img 1.PNG %}



### 2. In EMP table, print lowest salary among 'SALESMAN' employee ranks in order as example in the below.
{% asset_img 2.PNG %}

~~~
SELECT job,
       ename,
       sal,
       ROW_NUMBER() OVER(ORDER BY SAL) AS rank
  FROM emp
 WHERE job = 'SALESMAN'
~~~

### 3. In EMP table, print lowest salary among 'SALESMAN' employee ranks in order as example in the below.
{% asset_img 3.PNG %}
~~~
SELECT job,
       ename,
       sal,
       RANK() OVER(ORDER BY SAL) AS rank
  FROM emp
 WHERE job = 'SALESMAN'
~~~

### 4. In EMP table, print lowest salary among 'SALESMAN' employee ranks in order as example in the below.
{% asset_img 4.PNG %}

~~~
SELECT job,
       ename,
       sal,
       DENSE_RANK() OVER(ORDER BY SAL) AS rank
  FROM emp
 WHERE job = 'SALESMAN'
~~~

### 5. Print SQL to clone EMP table which for backup. (Table name is 'EMP_BAK_TABLE)
~~~
CREATE TABLE EMP_BAK_TABLE
        AS SELECT * FROM emp;
~~~
