---
title: 11 – Loops
layout: page
---

Computers are very good at doing repetitive tasks. How do we get computers to do something repeatedly until some condition is met?

A trivial example might be we want to show a string five times:

```js
var username = prompt("What's your name?");
console.log(username);
console.log(username);
console.log(username);
console.log(username);
console.log(username);
```

Here we're repeating code. If we need to change the variable, we need to change it five times. There's a better way:

## `while`

> `while` (*condition*) *statement*

```js
while (conditionIsTrue) {
  // code
}
```

This is a loop. The statements in the block between `do` and `while` will be run once, after which the `while` condition will be evaluated. If true, the block will be run again, creating a loop. Each time through the loop is sometimes called an *iteration*.

```js
var username = prompt("What's your name?");
var outputCount = 5;
while (outputCount > 0) {
  console.log(username);
  outputCount -= 1; // subtract 1 from outputCount and keep the new value
};
```

This code will ask for a string, and output that string five times.

Before it runs the loop block, it will check to see if `outputCount` is greater than zero, and if that condition is true. If true, it will run the loop block: output the string, and decrement `outputCount` by one. After each loop iteration, it checks the `while` condition again, and as long as the condition is true, it will continue to run the loop block.

## Exercise — Infinite Loops

It's very easy to write an *infinite loop* - a loop that doesn't end. Browsers these days will detect that a section of code hasn't ended for a few seconds and will prompt the user that the page has stopped responding, giving you your exit from the infinite loop.

You'll want this message while you're programming, but you'll never want your users to see this message because they may come to believe your page or site is broken.

```js
while (true) { // always run the code again
  console.log("Yo JavaScript, I’m really happy for you and Imma let you finish, but this loop is the best loop of all time. OF ALL TIME… — Kanye West");
}
```

Try this code above by pasting it into a browser's JavaScript console and see how the different browsers behave. Try and use the page while the code runs (Spoiler: you can't). Open up your Activity Monitor on a Mac or Task Manager on Windows and see your CPU usage skyrocket.

If an alert box doesn't appear, close the tab or crash the browser application. Try putting it in an HTML page and see what happens when you (as a regular user) would load that page.

## `do`…`while`

> `do` *statement* `while` (*condition*)

```js
do {
  // code
} while (conditionIsTrue);
```

`do`…`while` is identical to `while`, except that `do`…`while` will run the loop block a minimum of one time before checking the condition.

`while` by itself checks the condition before running the block, and so if the condition is false the first time through it may never run the loop block at all.

### Do while loop exercise
Using a do-while loop, create a game that will flip a coin X amounts of times in a succession. For example, in order for the game to finish, your code will need to flip "heads" 10 times in a row. Each time the coin flips the wrong side, the game starts again.

Keep a tally of how many flips were made during the entire game. Also keep in mind that the more successions you require (10 in a row, 30 in a row etc), the longer it may take for the game to finish.

Note: Browsers typically ask if you want to kill JavaScript after 15 seconds of continuous processing.

## `for`

> `for` ( *init*, *condition*, *final* ) *statement*

```js
for (var i = 0; i < 10; i += 1) {
  console.log(i);
}
```

A `for` loop is just like a `while` loop. It may not run the block code at all. The main difference however is the loop control statements are grouped together in the `for` parameters, rather than dotted around the `while` statement.

The first parameter is the *initialiser* statement: the statement here will only be run once, before the first time through the loop. It is used to initialise the count variable.

The second parameter is the *condition*. Just like the other loops, if this condition is true, it will run the loop block.

The third parameter is the *final* statement: after running the loop block, the final statement will run, followed by checking the condition to see if it should loop again. This is used to increment or decrement the count variable.

The code above uses `i` as a variable. This convention is as old as the hills, when programming languages could only have single letter variables. `i` here stands for *iteration*, keeping count of how many times through the loop it has or has yet to go.

***Aside***: Be aware of inclusiveness when writing your loop's condition -- If you want the loop to run exactly ten times, you could
* Start at `i` at 1 and check for `i < 11`, or
* Start at `i` at 0 and check for `i < 10`.

Hopefully you can see why starting at 0 is important: after it's been through once, `i` will be `1` and after ten times it will be `10`.

## What loop when?

* If you know exactly how many times a loop should run, use a `for` loop.
* If you must run the contents of the loop at least once, use a `do`…`while` loop.
* All other times use a `while` loop.

## `break`

You can break out of a loop early with `break`:

```js
alert("Welcome to the clubhouse...");
while (true) {
  var password = prompt("...what's the password?");
  if (password === "banana") {
    break;
  }
  alert("Nope, that's not it. View the source and try again.");
}
alert("You know the password? Awesome! Have a squishy, yellow day!");
```

## Exercises
* Make a loop that outputs an asterisk `*` for every character in a string.
  * do some research on getting the length of a string value.
* Make a loop that outputs every number from 1 to 100.
* Make a loop that outputs every even number, starting at 100, going to 0 (aka descending order).
* *Fizz-Buzz*: Output every number between 1 and 100, except when the number divides evenly by 3 or 5: instead of the number, output "fizz" or "buzz" respectively, and output "fizzbuzz" when it's evenly divisible by both.
* *99 Bottles…*: Write a program to output the [lyrics to the song "99 bottles of beer"](http://www.99-bottles-of-beer.net/lyrics.html) -- there are answers on that site, but none of them are actually simple, nor get the lyrics exactly right.
* Make a Christmas tree out of asterisks.

## Research
* What does the `continue` keyword do when used in a loop?
