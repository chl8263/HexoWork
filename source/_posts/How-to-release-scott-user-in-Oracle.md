---
title: How to release 'scott'user in Oracle
date: 2019-11-27 22:12:21
tags: ["Oracle"]
categories: ["Develop","Oracle"]
---

This document is how to release 'scott' user in oracle for test.
<!-- more -->

If you install oracle first, 'SCOTT' user is locking basically.

If you want use 'SCOTT' user for test, you can release command below.

__Fitst of all, you have to connect oracle as DBA.__

Command for release 'SCOTT' user.
~~~
ALTER USER scott IDENTIFIED By tiger ACCOUNT UNLOCK;
~~~

Connect using 'SCOTT'
~~~
CONNECT scott/tiger
~~~

If you don't have 'SCOTT' user,
create user to name 'scott'
and create table, data.

1. CREATE 'SCOTT' user after connect as DBA authority.

~~~
CRAETE USER scott IDENTIFIED BY tiger
DEFAULT TABLESPACE users
TEMPORARY TABLESPACE temp;
~~~

2. Authorization
~~~
GRANT connect, resource TO scott;
~~~

3. Execute script to connect using scott user
~~~
CONNECT scott/tiger
@$ORACLE_HOME/sqlplus/demo/demlbld.sql
~~~

The path of demobld.sql is defferent each other,
you should correct your own path or execute script after download script.

__demobld.sql download__
http://www.gurubee.net/files/sql/demobld.sql

__demobld.sql Script Sample__
~~~
DROP TABLE EMP;

DROP TABLE DEPT;

DROP TABLE BONUS;

DROP TABLE SALGRADE;

DROP TABLE DUMMY;



CREATE TABLE EMP

       (EMPNO NUMBER(4) NOT NULL,

        ENAME VARCHAR2(10),

        JOB VARCHAR2(9),

        MGR NUMBER(4),

        HIREDATE DATE,

        SAL NUMBER(7, 2),

        COMM NUMBER(7, 2),

        DEPTNO NUMBER(2));



INSERT INTO EMP VALUES

        (7369, 'SMITH',  'CLERK',     7902,

        sysdate,  800, NULL, 20);



INSERT INTO EMP VALUES

        (7499, 'ALLEN',  'SALESMAN',  7698,

        sysdate, 1600,  300, 30);



INSERT INTO EMP VALUES

        (7521, 'WARD',   'SALESMAN',  7698,

        sysdate, 1250,  500, 30);



INSERT INTO EMP VALUES

        (7566, 'JONES',  'MANAGER',   7839,

        sysdate,  2975, NULL, 20);



INSERT INTO EMP VALUES

        (7654, 'MARTIN', 'SALESMAN',  7698,

        sysdate, 1250, 1400, 30);



INSERT INTO EMP VALUES

        (7698, 'BLAKE',  'MANAGER',   7839,

        sysdate,  2850, NULL, 30);



INSERT INTO EMP VALUES

        (7782, 'CLARK',  'MANAGER',   7839,

        sysdate,  2450, NULL, 10);

INSERT INTO EMP VALUES

        (7788, 'SCOTT',  'ANALYST',   7566,

        sysdate, 3000, NULL, 20);



INSERT INTO EMP VALUES

        (7839, 'KING',   'PRESIDENT', NULL,

        sysdate, 5000, NULL, 10);



INSERT INTO EMP VALUES

        (7844, 'TURNER', 'SALESMAN',  7698,

        sysdate,  1500,    0, 30);



INSERT INTO EMP VALUES

        (7876, 'ADAMS',  'CLERK',     7788,

        sysdate, 1100, NULL, 20);



INSERT INTO EMP VALUES

        (7900, 'JAMES',  'CLERK',     7698,

        sysdate,   950, NULL, 30);



INSERT INTO EMP VALUES

        (7902, 'FORD',   'ANALYST',   7566,

        sysdate,  3000, NULL, 20);



INSERT INTO EMP VALUES

        (7934, 'MILLER', 'CLERK',     7782,

        sysdate, 1300, NULL, 10);



CREATE TABLE DEPT

       (DEPTNO NUMBER(2),

        DNAME VARCHAR2(14),

        LOC VARCHAR2(13) );



INSERT INTO DEPT VALUES (10, 'ACCOUNTING', 'NEW YORK');

INSERT INTO DEPT VALUES (20, 'RESEARCH',   'DALLAS');

INSERT INTO DEPT VALUES (30, 'SALES',      'CHICAGO');

INSERT INTO DEPT VALUES (40, 'OPERATIONS', 'BOSTON');



CREATE TABLE BONUS

        (ENAME VARCHAR2(10),

         JOB   VARCHAR2(9),

         SAL   NUMBER,

         COMM  NUMBER);



CREATE TABLE SALGRADE

        (GRADE NUMBER,

         LOSAL NUMBER,

         HISAL NUMBER);



INSERT INTO SALGRADE VALUES (1,  700, 1200);

INSERT INTO SALGRADE VALUES (2, 1201, 1400);

INSERT INTO SALGRADE VALUES (3, 1401, 2000);

INSERT INTO SALGRADE VALUES (4, 2001, 3000);

INSERT INTO SALGRADE VALUES (5, 3001, 9999);



CREATE TABLE DUMMY

        (DUMMY NUMBER);



INSERT INTO DUMMY VALUES (0);



COMMIT;
~~~
