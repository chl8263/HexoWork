---
title: SQL Quiz 6
date: 2019-12-18 19:01:12
tags: ["Oracle"]
categories: ["Develop","Oracle"]
---

SQL Quiz 6

<!-- more -->

### 1. In emp table, print 
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
  FROM emp
~~~
