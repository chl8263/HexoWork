---
title: Conditional statement
date: 2019-11-18 20:48:06
tags: ["javascript"]
categories: ["Develop","javascript"]
---

Conditional statement makes application behave different according to given condition.
<!-- more -->

## if

~~~javaScript
if(true){
  console.warn("hello");
}
~~~

The example above result appear "hello" at console.
Because there is "true" in the if statement.

It is always executed if there is "true" in the if statement.

~~~javaScript
if(false){
  console.warn("hello");
}
~~~

The example above don't executed, Because there is "false" in the if statement.

As you saw the example, "true" have meaning always executed and "false" have meaning always don't executed.

## else

"else" is used when you need process more complex case.

~~~javaScript
var a = 1;

if(a == 1){
  console.warn("hello");
}else {
  console.warn("No hello");
}
~~~

The result is "hello" at console, because a's value is 1.

~~~javaScript
var a = 2;

if(a == 1){
  console.warn("hello");
}else {
  console.warn("No hello");
}
~~~

The result is "No hello" at console, because a's value is 2.

## else if

You can make more various case if use "else if"

~~~javaScript
var a = 2;

if(a == 1){
  console.warn("hello");
}else if(a == 2) {
  console.warn("No hello");
}else{
  console.warn("Not hello");
}
~~~

The example above result is No hello, Because true in the else if statement.
