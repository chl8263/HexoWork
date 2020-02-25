---
title: Kotlin Arrays
date: 2020-02-24 23:52:21
tags: ["Kotlin"]
categories: ["Develop","Kotlin"]
---
Summarize of Kotlin Arrays.

<!-- more -->

## 4. Arrays

#### 1. Generic Arrays

Generic arrays in Kotlin are represented by `Array<T>`

To create an empty array, use `emptyArray<T>()` factory function.

~~~Kotlin
val empty = emptyArray<String>()
~~~

Can use like below situation.

~~~Kotlin
return someInputArray?.filterNotNull() ?: emptyArray()
~~~

To create an array with given size and initial values, use the constructor.

~~~Kotlin
var arr = Array<String>(size = 5, init = {index -> "Item #$index"})
println(Arrays.toString(arr))
println(arr.size)
~~~

~~~Kotlin
emptyArr.set(1, "A")
emptyArr.set(2, "B")
// or
emptyArr[1] = "A"
emptyArr[2] = "B"
~~~

#### 2. Arrays of Primitives
Those types do not inherit from Array<T> to avoid boxing, however, they have same attributes and method.

|Kotlin type|Factory function|JVM type|
|------|---|---|
|BooleanArray| booleanArrayOf(true, false)|boolean[ ]|
|ByteArray|byteArrayOf(1, 2, 3)|byte[ ]|
|CharArray|charArrayOf('a', 'b', 'c')|char[ ]|
|DoubleArray|doubleArrayOf(1.2, 5.0)|double[ ]|
|FloatArray|floatArrayOf(1.2, 5.0)|float[ ]|
|IntArray|intArrayOf(1, 2, 3)|int[ ]|
|LongArray|longArrayOf(1, 2, 3)|long[ ]|
|ShortArray|shortArrayOf(1, 2, 3)|short[ ]|

#### 3. Create an array
Can create array as factory method.

~~~Kotlin
val a = arrayOf(1,2,3) // create an Array<Int> of size 3 containing [1, 2, 3]
~~~

#### 4. Create an array using a closure

~~~Kotlin
val a = Array(3){ i -> i * 2 }  // create an Array<Int> of size 3 containing [0, 2, 4]
~~~

#### 5. Create an uninitialized array

~~~Kotlin
val a = arrayOfNulls<Int>(3)  // creates an Array<int>? of [null, null, null]
~~~
