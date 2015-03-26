---
title: 09 – Conditions
layout: page
---

A condition is like a calculation but returns a Boolean `true` or `false`.

Conditions are used by programming languages to check, test, or *evaluate* the state of a variable's value. Soon, we'll use them to control what parts of our program will get run depending on the value of variables.

We can check to see if one value matches as another, or is lesser or greater.

# Equality Operators

* `===` Strict Equality
* `!==` Strict Inequality
* `==` Loose Equality
* `!=` Loose Inequality

*Strict* Equality or Inequality returns true if the two operands are the same type and have matching value.

*Loose* Inequality works the same as strict equality, except that if the two operands are of different types,
it will attempt to coerce the types to match, and then checks if they match.

Try putting these into the console:
```js
1 === 1 // true
"joe" === "joe" // true
"joe" === "Joe" // false, case sensitive
7 === 10 // false
1 === "1" // false -- types do not match

1 == 1 // true
"joe" == "joe" // true
7 == 10 // false
1 == "1" // true -- types are coerced and end up matching
```

Coercion is useful, but only when we can rely on it happening. Because loose equality coerces before it compares, we have no way to know what coercion took place. It is best to do our coercion explicitly, then use strict equality. This documents that we mean to compare two values that share a type, and not leave the comparison to chance coercion.

*Best Practice*: Use only `===` and `!==`. Because of the type coercion works unreliably, loose equality should be avoided.

# Comparison Operators

* `<` Less than
* `>` Greater than
* `<=` Less than or equal to
* `>=` Greater than or equal to


```js
1 < 2 // true
7 > 10 // false
2 <= 2 // true
2 <= 3 // true
8 >= 5 // true
10 >= 7 // false
```

Comparison operators are especially for numbers. While you can use them for strings, they operate by essentially sorting the two strings, which doesn't usually do what you want. Sorting will be covered later.

# Logical Operators

We covered `&&` (Logical AND), `||` (Logical OR) and `!` (Logical NOT) previously, but conditions are where these operators shine. They combine the Boolean value from other conditions.

```js
// Fruit Inventory
var apples = 10;
var bananas = 27;
var cherries = 2;
var shopOpen = true;

console.log(apples > cherries && apples < bananas);
  // true - more apples than cherries AND less apples than bananas.
console.log(apples > 1 || bananas > 1 || cherries > 1); // true
console.log(! shopOpen); // false
```

## Checking against a set of values

### JavaScript is not English

Most programming languages require the programmer to be explicit. JavaScript isn't English, and so does not follow the same rules as English.

If we want to check the variable `name` to see if it's either `"Felix"` or `"Ralph"`, we might write the following in English

> is `name` equal to `"Felix"` or `"Ralph"`?

***Aside***: Writing code out in English is a good way to think about what you want to write in code. This technique is referred to as *Pseudocode*: what is written is thought in terms of code, but it is not actually runnable code.

However, a beginner programmer will then write the following, but this code won't do what they intend it to do:
```js
// is `name` equal to `"Felix"` or `"Ralph"`?
console.log(name === "Felix" || "Ralph"); // (Always true, no matter the value in name).
```
This might seem correct at first glance, but it's not what you actually mean to happen. The condition has been written according to the syntax rules of English, not the syntax rules of JavaScript. In JavaScript, this evaluates to `true`, no matter what the value of `name` is.

In JavaScript, the condition on the left of the `||` operator is `name === "Felix"`, which could be `true` or `false`.

The other condition is just `"Ralph"`, which by itself is a non-empty string. The `||` operator can only work with Boolean values, so  the non-empty string will be coerced to `true`.

Because one side of the `||` operator is always `true`, it will always evaluate to `true`. Even when `var name = "Bob";`.

### JavaScript is more verbose than English.

So you must check the variable for equality with each string: `name === "Felix"` and `name === "Ralph"`. The equality operator `===` along with both of its operands must be present for each condition.

```js
// is `name` equal to `"Felix"` or `"Ralph"`?
console.log(name === "Felix" || name === "Ralph"); // (we check name with each string)
```

To an English reader, this seems unnatural, unnecessarily long, or *verbose*. English speakers don't talk or write like this.

Programming languages require us not to *imply* what we want, but rather we must be *explict* about what it is we're asking them to do for us.

Because a variable cannot contain both `"Felix"` and `"Ralph"`, using `&&` will not help us. Using `||` between the two conditions will tell us if the variable contains either of the strings.

```js
// Name checker
var name = "Bob";
console.log(name === "Felix" || name === "Ralph"); // false
console.log(name !== "Felix" && name !== "Ralph"); // true
```

As the list of names you want gets longer, other solutions are needed, such as Arrays, which will be covered later.

<!-- SY 5/2 Some of your more complex examples might be useful here

Write a combination of conditions which will decide ....
What will the following return? ....

-->

# Exercises
