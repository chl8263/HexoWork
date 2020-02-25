---
title: Kotlin Basic grammar
date: 2020-02-24 23:51:23
tags: ["Kotlin"]
categories: ["Develop","Kotlin"]
---
Summarize of Kotlin basic grammar.

<!-- more -->

## 2.1 Basic Example

#### 1. Unit
The __Unit__ return type declaration is optional for functions. The following code are equivalent.

~~~Kotlin
fun printHello(name : String?) : Unit{
        if(name != null){
            println("Hello $name")
        }
    }
~~~
~~~Kotlin
fun printHello(name : String?){
    if(name != null){
        println("Hello $name")
    }
}
~~~

#### 2. Single-Expression function
When a function returns a single expression, curly braces can be omitted and the body is specified after = symbol.

~~~Kotlin
fun double (x : Int) : Int = x *2
~~~

And declaring the return type is optional when this can be inferred by compiler.

~~~Kotlin
fun double (x : Int) = x * 2
~~~

#### 3. NULL hold
In Kotlin, the type system distinguishes between references that can hold null and those that can not.
If use nullable value, should use `?`.
~~~Kotlin
var a : String = "123"
a = null    // compile error
~~~

~~~Kotlin
var a : String? = "123"
a = null    // working
~~~

#### 4. Comparison
In Kotlin, Actually check for equality of values.  By convention, an expression like a == b is translated to

~~~Kotlin
a?.equals(b) ?: (b === null)
~~~
