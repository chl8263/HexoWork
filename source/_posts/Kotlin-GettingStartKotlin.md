---
title: Kotlin GettingStartKotlin
date: 2020-02-24 23:44:24
tags: ["Kotlin"]
categories: ["Develop","Kotlin"]
---
Summarize about Kotlin.

<!-- more -->

## 1.1 Hello World

All Kotlin programs start at the main function.

When targeting the JVM, the function will be compiled as a static method in a class with a name derived from the
filename. In the above example, the main class to run would be my.program.MainKt.

~~~Kotlin
package my.program
fun main(args: Array<String>){
    println("Hello Kotlin")
}
~~~

### 1.2. With companion object
Similar to using an Object Declaration, can define at Class lke this.

~~~Kotlin
class Hello {
    companion object{
        @JvmStatic fun main(args: Array<String>){
            println("hello")
        }
    }
}
~~~

The advantage to this method is more self-evident and any other functions you add are scope into the class App.

### 1.3. With Object Declaration

Can alternatively use an Object Declaration what contains the main function.

~~~Kotlin
object App {
    @JvmStatic fun main(args: Array<String>){
        println("hello with object");
    }
}
~~~

The advantage to this method is super self-evident and also have singleton instance of App.

### 1.4. Compile and Run Kotlin Code

As java provide two different commands to compile and run Java code. Same as Kotlin also provide you different
commands.
javac to compile java files. java to run java files.
Same as kotlinc to compile kotlin files kotlin to run kotlin file.
