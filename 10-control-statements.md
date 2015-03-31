---
title: 10 – Control Statements
layout: page
---

<!-- SY 5/2 This is good.  More exercises in switch case would be good, comparing them to if elses.  

There's a funny article that I can't find right now about if code had been invented by the English
perchance this is true, notwithstanding this circumstance, etc.  It's actually helped some people understand what programmers are on about
-->

Up until this chapter our programs have been simple in that they are just a series of statements that all get executed one at a time in sequence.

Most computer programs are useful when they do certain things when given certain values. We write programs to check to see if a particular condition is true, and do a set of statements as a result.

# `if`

The `if` statement documentation looks like this:

> if (*condition*) *statement*

What this tells JavaScript is:
> if the *condition* evaluates to `true`, then execute the statement.

Typically *statement* there is a block of code, just like we have with functions:

```js
if (1 > 0) {
  console.log("condition is true");
}
```

A more interesting example:

```js
var username = prompt("What's your name?");

if (username === "Emmet") {
  alert("Everything is awesome!");
}

alert("Hi, " + username + "!");
```

The `if` statement here has two parts: the *condition* and the *block*. If the condition evaluates to `true`, the statements in the block will be executed.

So this code gets a string from the user, and checks if that string is the same as the string `"Emmet"`. If they are the same string, we alert a message. Then we alert another message that includes the entered string.

Any condition can go in the `if`'s parentheses, including conditions including `||` and `&&`:

```js
if (username === "Emmet" || username === "Lucy") {
  alert("Everything is awesome, " + username + "!");
}
```

Just remember to use full conditions on both sides of the logical operators.

# `if`…`else`

`if` by itself checks if a condition is true. What if you want the opposite?

If you're only interested in the false, you can 'flip' the logic:

```js
if (username !== "Emmet" && username !== "Lucy") {
  alert("Thank you for following the instructions.");
}
```

You could put these one after each other, and you'd have code that does something on `true` and on `false`.

Ah, but we're essentially repeating the condition! We're supposed to keep code DRY : Don't Repeat Yourself. So programming languages provide the `else` statement:

```js
if (username === "Emmet" || username === "Lucy") {
  alert("Everything is awesome, " + username + "!");
} else {
  alert("Thank you for following the instructions.");
}
```

# `if`…`else if`…`else`

You can even check additional conditions if the first was false.

```js
if (age < 1) {
  console.log("infant");
} else if (age < 2) {
  console.log("toddler");
} else if (age < 13) {
  console.log("child");
} else if (age < 16) {
  console.log("adolescent");
} else {
  console.log("adult");
}
```
## `else` the anti-pattern

Often times you might write something like above, but a little refactoring can make this much easier to read and maintain. We can put the logic in a function and eliminate the `else`s:

```js
function ageNoun (age) {
  if (age < 1) return "infant";
  if (age < 2) return "toddler";
  if (age < 13) return "child";
  if (age < 16) return "adolescent";
  return "adult";
}
console.log(ageNoun(age));
```

Remember, return ends the function, so none of the following statements will be executed.

`if` statements are only looking for one statement after their condition. If that's one statement or one block of statements, that's okay.


# Nested `if` Statements

You can even put `if`s inside other `if`s, or inside functions.

```js
function genderNoun(gender, age) {
  var adultAge = 16;
  if (gender === "f") { // female
    if (age > adultAge) {
      return "woman";
    } else {
      return "girl";
    }
  } else { // male
    if (age > adultAge) {
      return "man";
    } else {
      return "boy";
    }
  }
}
```

Some programmers would say this is a border-line example of too much nesting. Breaking each nested `if` into its own function and eliminating the `else` is decidedly more readable and maintainable. The function names help document the intent of the code.
<!--  a best practice guideline here would be useful -->

```js
var adultAge = 16;
function genderNoun(gender, age) {
  if (gender === "f") {
    return femaleAgeNoun(age);
  }
  return maleAgeNoun(age);
}

function maleAgeNoun(age) {
  if (age > adultAge) {
    return "man";
  }
  return "boy";
}

function femaleAgeNoun(age) {
  if (age > adultAge) {
    return "woman";
  }
  return "girl";
}
```
***Best Practice***: Deeply nested `if`s are a sure *code smell* that your code needs refactoring into functions.


# `switch`
Sometimes a stack of `if` statements is not the best for maintainability or readability.

```js
switch(name) {
  case "Emmet":
    console.log("Everything is Awesome!");
    break;
  case "Lucy":
    console.log("Welcome, Wyldstyle.");
    break;
  default:
    console.log("Hello, citizen.");
}
```

Here, depending on the value of `name` and its equality with the values on each of the `case` statements, the code after that `case` will be executed.

Because we don't usually want all the code after that `case` statement to be run, such as the code after the next `case` statement, we use `break` to drop out of the `switch`'s block.

*Best Practice*: Always use a `break`. If you don't want a break, group cases together, or if you mean to have an uncommon 'fall-through', comment `// no break` so you know the fall-through is intentional.

`default` is a case that catches anything that doesn't match any of the `case` values.

## Exercises

* Coffees are $3.50 each, but if you order more than 10, you get a 15% discount. Write a program that asks for the quantity and correctly calculates the total after discount.
* Muffins are $2.35 each, but buy 10 or more they're $2.10 each, but buy 25 or more and they're $1.90 each. Accept quantity as an input, output the unit price and the total.
* Steak dinners are $25.60 each, but if you buy two, you get the third for free. Get the quantity as input, and output the total price, and the number of free steaks!
  * Mushroom sauce is an extra $2, but the free steaks don't get free sauce. Get the number of mushroom sauce servings as another input, and adjust the total.
