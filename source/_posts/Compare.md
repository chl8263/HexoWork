---
title: Compare
date: 2019-11-17 15:55:32
tags: ["javascript"]
categories: ["Develop","javascript"]
---

In programming, comparison refer to distinguising whether given values are equal, different, large, or small.
<!-- more -->

In this case, The comparison operator is used. The result of comparison operator is either true or false.

True is meaning to result of comparison operator is true.

Flase is meaning to result of comparison operator is false.

'true' and 'false' is called boolean that is type of data in JavaScript.

## 1. ==

This meaning is equal operator.
Compare left and right identity, and true if they have same values, false if they have different values.

~~~javaScript
alert(1 == 2);  // false
alert(1 == 1);  // false
alert("one" == "two");  //false
alert("one" == "one");  //true
~~~

## 2. ===

It is match operator.
The result is true if true when comparison left, right identity exactly the same.

~~~javaScript
console.warn(1 == '1');   //true
console.warn(1 === '1');   //false

console.warn(1 == true);   //true
console.warn(1 === true);   //false
~~~

JavaScript is strongly recommended to use the === operator instead of the == operator.

Because more accuate data comparison is possible.
