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

How can make functional programming of above example?

~~~Javascript
const obj = {
  number : 10
}

function add (obj, something){
  return obj.number + something;
}

console.log(add(obj, 3));
~~~

In the above example, function 'add' return value using 'obj' reference.
This example doesn't change directly other value, just reference object.

### Functions are First-Class

First-class function are treated as first-class variable.
Thr first class variables can be passed to function as parameter, can be returned from function return value.

If execute example below.
~~~Javascript
const f1 = function(a){ return a * a;}
console.log(f1);
~~~

Result as below.

~~~Javascript
ƒ (a){ return a * a;}
~~~

The important point here is some value can has function as value.

The example which in below show how can use to function in parameter.

~~~Javascript
function fun(parameter){
  return parameter();
}

console.log( fun(function () {return 10;}) );
~~~

### Variables are Immutable
 In functional programming, we can’t modify a variable after it’s been initialized. We can create new variables – but we can’t modify existing variables, and this really helps to maintain state throughout the runtime of a program. Once we create a variable and set its value, we can have full confidence knowing that the value of that variable will never change.

### Advantages and Disadvantages of Functional programming

* Advantages
1. Pure functions are easier to understand because they don’t change any states and depend only on the input given to them. Whatever output they produce is the return value they give. Their function signature gives all the information about them i.e. their return type and their arguments.
2. The ability of functional programming languages to treat functions as values and pass them to functions as parameters make the code more readable and easily understandable.
Testing and debugging is easier. Since pure functions take only arguments and produce output, they don’t produce any changes don’t take input or produce some hidden output. They use immutable values, so it becomes easier to check some problems in programs written uses pure functions.
3. It is used to implement concurrency/parallelism because pure functions don’t change variables or any other data outside of it.
It adopts lazy evaluation which avoids repeated evaluation because the value is evaluated and stored only when it is needed.

* Disadvantages
1. Sometimes writing pure functions can reduce the readability of code.
Writing programs in recursive style instead of using loops can be bit intimidating.
2. Writing pure functions are easy but combining them with rest of application and I/O operations is the difficult task.
Immutable values and recursion can lead to decrease in performance.







>>
