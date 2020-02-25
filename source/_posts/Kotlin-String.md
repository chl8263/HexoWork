---
title: Kotlin String
date: 2020-02-24 23:54:30
tags: ["Kotlin"]
categories: ["Develop","Kotlin"]
---
Summarize of Kotlin String.

<!-- more -->
## 3. String

#### 1. String Equality
String are compared with == operator with check for their structural equality.

~~~Kotlin
val str1 = "Hello, World"
val str2 = "Hello," + " World"
println(str1 == st2)    // print true
~~~

Referential equality is checked with `===` operator.

~~~Kotlin
val str1 = """
 |Hello, World!
 """.trimMargin()
val str2 = """
 #Hello, World!
 """.trimMargin("#")
val str3 = str1

println(str1 == str2) // Prints true
println(str1 === str2) // Prints false
println(str1 === str3) // Prints true
~~~

#### 2. String Literals
Kotlin has two types of string literals:
* Escaped string
* Raw string

__Escaped string__ handles special characters by escaping them. The following escape sequences are supported: `\t, \b, \n, \r, \', \", \\ \$`, also use Unicode `\uFF00`.

~~~Kotlin
val a = "Hello \n Hello"
val b = "Hello \t Hello"
val c = "Hello \b Hello"
val d = "Hello \r Hello"
val e = "Hello \' Hello"
val f = "Hello \" Hello"
val g = "Hello \\ Hello"
val h = "Hello \$ Hello"
~~~

The result is like below.

~~~
Hello
 Hello
Hello 	 Hello
Hello Hello
 Hello
Hello ' Hello
Hello " Hello
Hello \ Hello
Hello $ Hello
~~~

__Raw string__ delimited by `""""`.

~~~Kotlin
val text = """
 for (c in "foo")
 print(c)
"""
~~~

Leading whitespace can be removed with trimMargin() function.

~~~Kotlin
val text = """
 |Tell me and I forget.
 |Teach me and I remember.
 |Involve me and I learn.
 |(Benjamin Franklin)
 """.trimMargin()
~~~

#### 3. Elements of String

Element of String are characters that can be accessed by the indexing operation string[index].

~~~Kotlin
val str = "Hello, World!"
println(str[1])
~~~

String elements can be iterated with a for loop.

~~~Kotlin
for(x in str){
    println(x)
}
~~~

#### 4. String Templates

String template starts with a dollar sign $ and consists of either a variable name:
Or an arbitrary expression in curly braces:
~~~Kotlin
val i = 10
val s = "i = $i"

val a = "abc"
val str = "$a.length is ${a.length}" // "abc.length is 3"
~~~
