---
title: Kotlin Enum
date: 2020-02-24 23:56:33
tags: ["Kotlin"]
categories: ["Develop","Kotlin"]
---
Summarize of Kotlin Enum

<!-- more -->

## 6. Enum

#### 1. Initialization
Enum classes as any other classes can have a constructor and be initialized
~~~Kotlin
enum class Color (val rgb: Int){
    RED(0xFF000),
    GREEN(0x00FF00),
    BLUE(0x0000FF)
}
~~~

#### 2. Simple Enum

~~~Kotlin
enum class Color2{
    RED, GREEN, BLUE
}
~~~
Each enum constant is an object. Enum constants are separated with commas.

#### 3. Mutability
Enums can be mutable, this is another way to obtain a singleton behavior:

~~~Kotlin
enum class Color3(var x : Int = 0){
    EARTH(7 * 10000),
    MARS();

    override fun toString(): String = "$name [x = $x]"
}
~~~

~~~Kotlin
var c = Color3.MARS
println(c)
c.x = 1234
println(c)
~~~
