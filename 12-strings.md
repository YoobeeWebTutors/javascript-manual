---
title: 12 – Strings
layout: page
---

A string value are made out of sequence of characters.

```js
"Hello, world!"
'Another string'
"中文 español English русский 日本語"
```

These characters are numbers, letters, symbols, punctation, and really any character in Unicode.

# `length` Property

Strings in JavaScript have a property called `length` which tells us how many characters are in the string.

```js
console.log("Cave".length) // 4
var name = "Chell";
console.log(name.length); // 5
```

We can use this in conditions, like checking a minimum length for a name:

```js
do {
  var name = prompt("What's your name?");
  if (name.length < 2) {
    alert("Names are two or more characters long. Try again.");
  }
} while (name.length < 2);
```

## About Properties and Methods

The `.` operator used here is called the 'member' operator. It lets us access properties (and shortly, methods) that are attached to values.

We've seen this operator in use: `console.log()`. `console` is an object: a collection of properties. `log` is a property of `console`. Because the `log` property contains a function we can call with `()`, we refer to `log` as a *method*; a function that is a property of an object is called a method..

Strings have properties and methods. Strings only have the one property: `length`. Strings do have a lot of methods. We'll go over the most useful ones here.

# Transform Methods
* `String.toLowerCase()`
* `String.toUpperCase()`
* `String.trim()`

## `toLowerCase()` and `toUpperCase()`

These two methods work on the existing string and return it changed to lowercase or uppercase letters. They don't change the existing string.

```js
var message = 'Bob said to James, \"What\'s happening?\"';
console.log(message.toLowerCase()); // 'bob said to james, "what's happening?"'
console.log(message.toUpperCase()); // 'BOB SAID TO JAMES, "WHAT'S HAPPENING?"'
console.log(message); // 'Bob said to James, "What's happening?"'
```

## `trim()`

This method removes any white space from the start or end of the string.

```js
var spaceMovies = "   Star Trek, Star Wars, Galaxy Quest,     Spaceballs       ";
console.log(spaceMovies.trim()); // "Star Trek, Star Wars, Galaxy Quest,     Spaceballs"
```

While `trim()` works in all modern browsers, it is a relatively new addition. Most noticably, `trim()` doesn't work in Internet Explorer 8 and below.

# Character Methods

* `String.charAt()`
* `String.charCodeAt()`
* `String.substr()`
* `String.substring()`
* `String.slice()`

## `charAt( index )`

`charAt` accepts an integer representing the position in the string, and will return a string of one character long containing the character at that index in the string.

Each character in a string has an index: it's position in the string. The first character is at position 0. A string with a length of 5 will have its last character at index 4.

```js
var fruit = "Plums";
console.log(fruit.length); // 5
console.log(fruit.charAt(0)); // "P"
console.log(fruit.charAt(1)); // "l"
console.log(fruit.charAt(2)); // "u"
console.log(fruit.charAt(3)); // "m"
console.log(fruit.charAt(4)); // "s"

// Don't repeat yourself! Here's a better version:
for (var i = 0; i < fruit.length; i += 1) {
  console.log(fruit.charAt(i));
}

console.log(fruit.charAt(-1)); // "" (empty string)
console.log(fruit.charAt(5)); // "" (empty string)
```

## `charCodeAt( index )`

`charCodeAt` accepts an integer representing the position in the string, and returns the [numeric Unicode value of the character](http://unicode-table.com/en/) at that index in the string. If the index is below zero or above the length of the string, `NaN` is returned.

```js
var fruit = "Bananas";
for (var i = 0; i < fruit.length; i += 1) {
  console.log(fruit.charAt(i) + ": " + fruit.charCodeAt(i));
}
```

Output:

```
B: 66
a: 97
n: 110
a: 97
n: 110
a: 97
s: 115
```

## `substr( startIndex [, length ] )`

`substr` returns a substring - a segment of a string, starting at the `startIndex`, and returning all the characters from that point, or up to `length` characters.

```js
var name = "Wheatley";
name.substr(0, 5); // "Wheat"
name.substr(5); // "ley"
name.substr(2,3); // "eat"
name.substr(-3); // "ley"
name.substr(-3, 2); // "le"
name.substr(5, 10); // "ley"
```

Note that we can provide a negative startIndex. This will count back from the end of the string.

We can use in a loop to do something pretty neat:

```js
var name = "Aperture";
for (var i = 0; i < name.length; i += 1) {
  console.log(name.substr(i, 3));
}
```

Output:

```
Ape
per
ert
rtu
tur
ure
re
e
```
Here we loop over the string to get each character in turn, along with the next two characters.

# Exercise
In the program above, how can we change the program to not show the last two lines, where three letters are not being output?

## `substring( indexA [, indexB ] )`

`substring` is very similar to `substr` but its second parameter is not the length, but the index of the first character not to be included.

```js
var name = "Caroline";
name.substring(0, 5); // "Carol"
name.substring(5); // "ine"
name.substring(2, 3); // "r"
name.substring(-3); // "Caroline"
name.substring(-3, 2); // "Ca"
name.substring(5, 10); // "ine"
```

if indexA is bigger than indexB, `substring` will use them swapped.

```js
name.substring(5, 3); // "rol"
```

`substring` also does not support negative startIndex, however...

## `slice( indexA [, indexB ] )`

`slice` is a better version of `substring`. It supports negative indices, and doesn't swap them.

```js
var name = "Rattmann";
name.slice(0,3); // "Rat";
name.slice(5); // "ann";
name.slice(-4); // "mann";
name.slice(-5, -1); // "tman"
```

# Search Methods
* `String.indexOf()`
* `String.lastIndexOf()`

# `indexOf( needle [, fromIndex ] )` and `lastIndexOf( needle [, fromIndex ] )`

These two methods search the string (the 'haystack') for the 'needle', starting optionally at the fromIndex, and working forward or backwards. When the needle is found, it returns the index at which needle begins. If the needle isn't found, the method returns `-1`

```js
var boat = "HMS Surly Bracket";
console.log(boat.indexOf("HMS")); // 0
console.log(boat.indexOf("Surly")); // 4
console.log(boat.indexOf("Su")); // 4
console.log(boat.indexOf("whale")); // -1
console.log(boat.indexOf("r")); // 6
console.log(boat.indexOf("r", 6 + 1)); // 11
console.log(boat.lastIndexOf("HMS")); // 0
console.log(boat.lastIndexOf("Surly")); // 4
console.log(boat.lastIndexOf("r")); // 11
console.log(boat.lastIndexOf("r", 11 - 1)); // 6
```

To find all occurances of the letter 'r' in a string, we can do this:

```js
var pirate = "Arr! Shiver me timbers and Raise the anchor!";
pirate = pirate.toLowerCase();
var i = 0;
while (pirate.indexOf("r", i) > -1) {
	console.log(pirate.indexOf("r", i));
	i = boat.indexOf("r", i) + 1;
}
```

# Exercises
* Write a function that only returns true if its first parameter is a string longer than ten characters.
* Write a function that checks if the string contains the characters 'pip'. Extra for experts: Write it without `indexOf` or `lastIndexOf`
* Write a function that returns a count of the number of vowels in a string.
* Write a function that 'disemvowels' a string. Return the input string missing the characters 'AEIOUaeiou'. "Banana" -> "Bnn"
* Write a function that reverses a string. "Banana" becomes "ananaB"
* Write a function that detects palindromes. It should return true for "bob", "Tacocat", "A Toyota's a Toyota", "Go hang a salami, I'm a lasagna hog!", and false for "Banana" and "Nyan Cat". You will have to create a string that contains only the letters, reverse that string and check if it is the same.
