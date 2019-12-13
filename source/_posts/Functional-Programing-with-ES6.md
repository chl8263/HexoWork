---
title: Functional Programing with ES6
date: 2019-12-11 23:25:32
tags: ["javascript"]
categories: ["Develop","es6"]
---

Functional programming is paradigm for successful programming.

<!-- more -->

## Concepts of functional programming
* Pure functions
* Recursion
* Referential transparency
* Functions are First-Class and can be Higher-Order
* Variables are Immutable

### Pure function
~~~Javascript
function add(a, b){
  return a + b;
}
console.log(5, 10);
~~~

First, the above example is pure function, this is because giving the same arguments returns the same values.

And this function have no side effects.

The example below is not a pure function.
~~~Javascript
let c = 10;
function add2 (a, b){
    return a + b +c;
}

console.log(add2(10, 20));
c = 20;
console.log(add2(10, 20));
~~~

Because this function refer to variable 'c', so this function can change return value when 'c' value changes.
