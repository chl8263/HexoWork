---
title: '[Algorithm]Seattle Hackers December'
date: 2019-12-17 23:29:46
tags: ["Algorithm"]
categories: ["Develop","Algorithm"]
---

This content is what i did in 'SeattleJS Hackers Code Katas[Theme: Recursion]'
<!-- more -->

### 1.
Given the triangle of consecutive odd numbers:
~~~
            1
         3     5
      7     9    11
  13    15    17    19
21    23    25    27    29
...
~~~

Calculate the row sums of this triangle from the row index (starting at index 1) e.g.:

~~~
rowSumOddNumbers(1); // 1
rowSumOddNumbers(2); // 3 + 5 = 8
~~~

Solution
~~~Javascript
const sumNested = (arr) => {
  let total = 0
  for (let i = 0; i < arr.length; i++) {
    if (typeof arr[i] === 'number') {
      total+=arr[i]
    } else if (arr[i] instanceof Array) {
      total += sumNested(arr[i])
    }
  }
  return total
~~~

### 2.
Implement a function to calculate the sum of the numerical values in a nested list. For example :

Example
~~~
sumNested([1, [2, [3, [4]]]]) => 10
~~~

Solution
~~~Javascript
const sumNested = arr => {
let sum = 0;
  for (let i = 0; i < arr.length; i++){
    if (Array.isArray(arr[i])){
      sum += sumNested(arr[i])
     }
   else if (typeof arr[i] === 'number'){
    sum += arr[i];
    }
  }
  return sum;

~~~


### 3.
In this kata, you must create a digital root function.

A digital root is the recursive sum of all the digits in a number. Given n, take the sum of the digits of n. If that value has more than one digit, continue reducing in this way until a single-digit number is produced. This is only applicable to the natural numbers.

Here's how it works:

Example
~~~
digital_root(16)
=> 1 + 6
=> 7

digital_root(942)
=> 9 + 4 + 2
=> 15 ...
=> 1 + 5
=> 6

digital_root(132189)
=> 1 + 3 + 2 + 1 + 8 + 9
=> 24 ...
=> 2 + 4
=> 6

digital_root(493193)
=> 4 + 9 + 3 + 1 + 9 + 3
=> 29 ...
=> 2 + 9
=> 11 ...
=> 1 + 1
=> 2
~~~

Solution
~~~Javascript
function digital_root(n) {
  let result = 0;
  let coptResult = n.toString().length;

  while(n != 0){
    result += Math.floor(n % 10);
    n /= 10;
  }
    if (coptResult <= 2) return result;
  return digital_root(result);
}
~~~

### 4.
The new "Avengers" movie has just been released! There are a lot of people at the cinema box office standing in a huge line. Each of them has a single 100, 50 or 25 dollar bill. An "Avengers" ticket costs 25 dollars.

Vasya is currently working as a clerk. He wants to sell a ticket to every single person in this line.

Can Vasya sell a ticket to every person and give change if he initially has no money and sells the tickets strictly in the order people queue?

Return YES, if Vasya can sell a ticket to every person and give change with the bills he has at hand at that moment. Otherwise return NO.

Example
~~~
tickets([25, 25, 50]) // => YES
tickets([25, 100]) // => NO. Vasya will not have enough money to give change to 100 dollars
tickets([25, 25, 50, 50, 100]) // => NO. Vasya will not have the right bills to give 75 dollars of change (you can't make two bills of 25 from one of 50)
~~~

Solution
~~~Javascript
function tickets(peopleInLine){
  // ...
  let twenty5 = 0;
  let fifty = 0;
  for (const item of peopleInLine){
    switch(item){
      case 25 :
        twenty5++;
        break;
      case 50 :
        fifty++;
        twenty5--;
        if(twenty5 < 0) return "NO";
        break;
      case 100 :
        if(twenty5 > 0){
          twenty5--;
          if(fifty > 0){
            fifty--;
          }else if( fifty <= 0 && twenty5 >= 2){
            twenty5 -= 2;
          }else return "NO";
        }else return "NO";
        break;
    }
  };
  return "YES";
}
~~~
