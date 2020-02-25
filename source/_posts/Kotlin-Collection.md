---
title: Kotlin Collection
date: 2020-02-24 23:55:24
tags: ["Kotlin"]
categories: ["Develop","Kotlin"]
---
Summarize of Kotlin Collection
<!-- more -->
## 5. Collections

Unlike many language, Kotlin distinguishes between mutable and immutable collections.
Precise control over exactly when collections can be edited is useful for eliminating bugs, and designing good APIs.

#### 1. Using list
~~~Kotlin
//Create a new read-only List<String>
val list = listOf("Item1", "Item2", "Item3")
list.add("Item4")   // compile error

//Create a new editable List<String>
val list2 = mutableListOf("Item1", "Item2", "Item3")
list2.add("Item4")
~~~

#### 2. Using map
~~~Kotlin
//Read-only
val map = mapOf(Pair(1, "Item1"), Pair(2, "Item2"), Pair(3, "Item3"))

//Editable
val map2 = mutableMapOf(Pair(1, "Item1"), Pair(2, "Item2"), Pair(3, "Item3"))
~~~

#### 3. Using set
~~~Kotlin
//Read-only
val set = setOf(1, 3, 5)

//Editable
val set2 = mutableSetOf(1, 3, 5)
~~~
.

<!-- more -->

## 5. Collections

Unlike many language, Kotlin distinguishes between mutable and immutable collections.
Precise control over exactly when collections can be edited is useful for eliminating bugs, and designing good APIs.

#### 1. Using list
~~~Kotlin
//Create a new read-only List<String>
val list = listOf("Item1", "Item2", "Item3")
list.add("Item4")   // compile error

//Create a new editable List<String>
val list2 = mutableListOf("Item1", "Item2", "Item3")
list2.add("Item4")
~~~

#### 2. Using map
~~~Kotlin
//Read-only
val map = mapOf(Pair(1, "Item1"), Pair(2, "Item2"), Pair(3, "Item3"))

//Editable
val map2 = mutableMapOf(Pair(1, "Item1"), Pair(2, "Item2"), Pair(3, "Item3"))
~~~

#### 3. Using set
~~~Kotlin
//Read-only
val set = setOf(1, 3, 5)

//Editable
val set2 = mutableSetOf(1, 3, 5)
~~~
