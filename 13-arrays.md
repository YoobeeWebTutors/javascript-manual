---
title: 13 – Arrays
layout: page
---

Sometimes we need to store a list of values. Who's coming to dinner? What were the team's scores for the season?

```js
var guests = ["Alice", "Charles", "Dave", "Bob"];
var scores = [10, 15, 12, 17, 3, 11, 23];
var bananas = [true, 0, "Today"]; // Yes! We Have No Bananas
```

Here we use square brackets to denote an Array literal. There are other ways to create arrays, but this is the most useful.

## Array Elements

If we try to output an array, we'll see the contents of the array as a string:

```js
console.log(guests); // "Alice,Charles,Dave,Bob"
console.log(scores); // "10,15,12,17,3,11,23"
```

Note how the order of the elements is kept intact; no sorting takes place.

We can access elements of an array by index:

```js
guests[0]; // "Alice"
guests[2]; // "Dave"
```

We can find out how many elements are in an array with the `length` property:

```js
scores.length; // 7
for (var i = 0; i < scores.length; i += 1) {
  console.log(i + ": " + scores[i]);
}
```

## Creating an Array from a String

We can create an array from a string with the `split` method:

`String.split( delimiter )`

```js
var guests = "Alice,Charles,Dave,Bob".split(',');
var scores = "9 15 12 17 3 11 23".split(' ');
guests.length; // 4
scores.length; // 7
```

## Creating a string from an array

Usually, when an array is output, it will be coerced into a string:
```js
alert(guests); // "Alice,Charles,Dave,Bob"
alert(scores); // "9,15,12,17,3,11,23"
```
However, when using `console.log` or the like, the console panel will often show you the array in literal form.

We get more control over converting an array to a string using the `join` method:

`Array.join( separator = ',' )`

It coerces each element's value to a string, and concatenates them, separating each element string with the separator, which defaults to `,`.

```js
scores.join(); // "9,15,12,17,3,11,23"
scores.join(" "); // "9 15 12 17 3 11 23"
guests.join(', '); // "Alice, Charles, Dave, Bob"
guests.join(' & '); // "Alice & Charles & Dave & Bob"
```

## Modifing an Array

We can modify an element in an array:

```js
guests[2] = "Steve";
guests; // "Alice,Charles,Steve,Bob"
scores[0] = 9;
scores; // "9,15,12,17,3,11,23"
```

We can add elements onto the end of an array with the `push` method.:

```js
scores.push(11);
scores; // "9,15,12,17,3,11,23,11"
scores.length; // 8

guests.push("Elaine", "Frodo");
guests; // "Alice,Charles,Steve,Bob,Elaine,Frodo"
guests.length; // 6
```

JavaScript can also take elements off the end of an array with `pop`:

```js
var lastGuest = guests.pop();
guests; // "Alice,Charles,Steve,Bob,Elaine"
guests.length; // 5
lastGuest; // "Frodo"
```

We can also add and remove elements from the start of an array with `unshift` and `shift`:

```js
guests.unshift("Gollum", "Samwise", "Merry", "Pippin");
guests; // "Gollum,Samwise,Merry,Pippen,Alice,Charles,Steve,Bob,Elaine"
guests.length; // 9
var unableToAttend = guests.shift();
unableToAttend; // "Gollum"
```

Deleting and adding elements into an array is possible with `splice`

`Array.splice( start, deleteCount [, item1 [, item2...]] )`

```js
guests.splice(5, 2);
guests; // "Samwise,Merry,Pippen,Alice,Charles,Elaine"
guests.splice(3,0,"Frodo");
guests; // "Samwise,Merry,Pippen,Frodo,Alice,Charles,Elaine"
guests.splice(1,0,"Bilbo","Gandalf");
guests; // "Samwise,Bilbo,Gandalf,Merry,Pippen,Frodo,Alice,Charles,Elaine"
```

### The modify functions
<!-- font must be Menlo -->
```
    unshift      shift
          │      ▲
          │      │
       ┌──▼──────┴─┐
      0│   Frodo   │
       ├───────────┤
      1│    Sam    │ ───▶
       ├───────────┤      splice
      2│   Merry   │ ◀───
       ├───────────┤
      3│  Pippin   │
       └─▲───────┬─┘
         │       │
         │       ▼
      push       pop
```

# Sorting an array

The `sort` method is a very interesting one. It sorts an array's elements into order.

`Array.sort( [ compareFunction ]);`

```js
var fruit = ['apple', 'banana', 'Cherry'];
fruit.sort();
fruit; // "Cherry,apple,banana" <-- not sorted alphabetically

var ages = [15, 20, 2, 11, 9, 10];
ages.sort();
ages; // "10,11,15,2,20,9" <-- not sorted numerically
```

But as you can see, it doesn't really work the way you want. `sort` coerces each element into a string, then sorts the strings according to Unicode code point order. In Unicode, Number characters are before the letters, and capital letters are before the lower case letters. At least the numbers and letters are in numeric and alphabetical order.

So `sort` is case sensitive to a tee, and prefers numbers to letters. However, we can teach `sort` in many different ways, by providing it a compare function. This function accepts two parameters, often called `a` and `b`, and returns `-1` if `a < b`, or `1` if `a > b`, or `0` if they are equal.

```js
function compare(a, b) {
  console.log(a + " vs " + b);
  if (a < b) {
    return -1;
  }
  if (a > b) {
    return 1;
  }
  // by elimination, a must be equal to b.
  return 0;
}
```

Of course, the above compare function does exactly the same thing as `sort` by itself, except it does not coerce elements to strings.

```js
fruit.sort(compare); // ["Cherry", "apple", "banana"]
console.log('---');
ages.sort(compare); // [2, 9, 10, 11, 15, 20] <-- numerically ascending!
```

Output:
```
Cherry vs apple
apple vs banana
---
20 vs 15
20 vs 11
15 vs 11
20 vs 10
15 vs 10
11 vs 10
20 vs 9
15 vs 9
11 vs 9
10 vs 9
20 vs 2
15 vs 2
11 vs 2
10 vs 2
9 vs 2
```

Please note that we're *not calling* `compare` when we pass it to `sort`. `sort` will call `compare` each time it needs to compare two elements.

```js
// WRONG:
fruit.sort(compare());
// CORRECT:
fruit.sort(compare);
```

***Aside***: Functions in JavaScript are fully fledged values. You can put them in variables and pass them as arguments and even have a function return a function. In computer programming, this is called an *[anonymous function](http://en.wikipedia.org/wiki/Anonymous_function)*

### Sorting Arrays of Numbers

The above function is a good explaination, but if we wish to sort numerically, this `compareNumbers` function is much better.

```js
function compareNumbersAscending(a, b) {
  return a - b;
}
function compareNumbersDescending(a, b) {
  return b - a;
}

var ages = [15, 20, 2, 11, 9, 10];
ages.sort(compareNumbersAscending); // [2, 9, 10, 11, 15, 20]
ages.sort(compareNumbersDescending); // [20, 15, 11, 10, 9, 2]
```
The `compareNumbersAscending` still returns a positive or negative number, or zero. `compareNumbersDescending` does the same thing, only larger numbers come first.

### Sorting Arrays of Strings Alphabetically

Here are some compare functions for sorting arrays of strings, case insensitively:

```js
function compareStringsAscending(a, b) {
  return a.toLowerCase() - b.toLowerCase();
}

var fruit = ["apple", "banana", "Cherry", "dates"];
fruit.sort(compareStringsAscending);

```

### Notes about Sorting

Sorting is one of the more processor-intensive things you can ask a computer to do, and the more elements to sort, the longer it takes. While sorting ~100 things shouldn't take a lot of time on today's computers, doing that sort unnecessarily could slow the program down.

JavaScript should use an appropriately efficient sorting algorithm (which is these days is Quick Sort), and we just need to provide the compare function.

* [https://www.youtube.com/watch?v=kgBjXUE_Nwc](Computerphile: Getting Sorted) - How computer sorts work on paper.
* [Sorting Algorithms](http://www.sorting-algorithms.com/) - animations on how different computer sort methods work.
* [Fisher–Yates Shuffle](http://bost.ocks.org/mike/shuffle/) - an explanation on how to de-sort or *shuffle* an array efficiently in JavaScript.

# Exercises
* Write a function that will convert an array of names to a proper english sentence: "Alice, Bob, and Charles". Every name is separated with a comma, except the last one which also includes 'and'
*
