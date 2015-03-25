---
Title: Variables
layout: post
---

# Variables

Values like we saw in the previous chapter aren't all that useful in day to day programming by themselves. A value in one statement is more useful if we can use it in the next statement:

```js
var username;
username = "Earl";
console.log(username);
```

## Defining variables

The keyword `var` tells JavaScript to create a *variable*. A variable is a place in the computer memory that has been set aside to hold whatever value (a string, number, Boolean, and others) we put into it.

A variable can hold one value and one value only. If we put a new value in, any previous value is discarded.

Think of computer memory as a giant wall of mailboxes or pigeon holes. Each box or hole has a label on it -- the variable's name. In the above example, the variable is called `username`.

The variable will exist for as long as the code it is defined in is being executed. You'll learn more about this when we come to functions and variable scope.

It is best to define your variables at the top of their scope, to avoid an issue called *hoisting*, which we'll also learn more about later.

## Variable Names

Names for things in JavaScript, such as variables, should be formed from the 26 upper and lower case letters (A .. Z, a .. z), the 10 digits (0 .. 9), and _ (underbar).

Variables and functions should start with a lower case letter.

Variables in JavaScript cannot start with a digit.

There are tons of reserved keywords in JavaScript that you can't use as a name. `var` is one of them. Check [Mozilla Developer Network's Lexical Grammar](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Keywords) page for the complete list of words you can't use. Notable reserved words inclued `class`, and `super`, but you can use `className` and `superMan`.

### Naming Conventions

By convention, JavaScript programmers use so-called `camelCase` for their variable names. The first word is lowercase, and following words have their initial letter capitalised. This resource will use `camelCase`.

You may also see variables named with `snake_case`, where the whole name is lowercase and words are separated with underscores `_`.

**Best Practice**: Code should always look like it has been written consistantly by a single person, even when written by a team. Use `camelCase` or `snake_case`, but remain consistent. When editing other people's code, obey the conventions you see being followed. "When in Rome, do as the Romans do."

<!-- you can't emphasise clear naming enough - feel free to repeat this frequently -->

Names should be meaningful. Avoid shortenings, abbreviations and acronyms. Don't be clever, be clear:

* `phNum` should be `phoneNumber`
* `addr2` should be `address2`
* `clr` should be `color`

It's best to use American English spelling where it matches HTML or CSS, most notably the word `color` and not the British "colour".

That said, some are universally accepted, such as `id` for identifier and `i` for iteration.

**Code Smell**: If you find yourself using variables such as `book1`, `book2`, `book3` and so on, you probably want an **Array**, a ordered collection of values. We'll explain arrays later. However, breaking a line into two parts, such as `address1` and `address2` is a notable exception.

## Initial Values - `undefined`

When you initialise a variable, the variable is considered to have the value `undefined`. This is a value all variables get before any other value is assigned to them.

```js
var name;
console.log(name);
```

This will output to the console `undefined`.


### Assigning values to variables

The `=` is called the *assignment operator*. Try not to think of this as "equals" but "is assigned the value".

```js
username = "Earl";
age = 27;
```

Here, `username` is assigned the value `"Earl"`

We can also assign a value to a variable when it is defined.

```js
var username = "Earl";
var age = 27;
var canDrive = true;
```

## Using variables as values

```js
console.log(username);
console.log(27);
console.log(canDrive);
```

Here the method `console.log` is being passed the `username` variable. What is actually taking place here is the value inside `username` is being *evaluated* to its value before being passed into `console.log`:

```js
console.log("Earl");
console.log(27);
console.log(true);
```

If the value obtained from the variable is changed, the value still in the variable is left unchanged.

## Changing a variable's value
```js
var coffeesConsumed = 2;
console.log(coffeesConsumed); // 2
coffeesConsumed = 3;
console.log(coffeesConsumed); // 3
```

We can replace a variable's value by assigning a new one into it. The old value is discarded permanently, unless of course, you copy it into another variable:

```js
var coffeesConsumed = 2;
console.log(coffeesConsumed); // 2
var coffeesPreviouslyConsumed = coffeesConsumed;
coffeesConsumed = 99;
console.log(coffeesConsumed); // 99
console.log(coffeesPreviouslyConsumed); // 2
```


## Reference Error: *variable* is not defined

When you attempt to use a variable that hasn't been defined, you may get an error:
```js
console.log(chunkyBacon);
```
<samp>Error: Uncaught ReferenceError: chunkyBacon is not defined.</samp>

*Best Practice*: To resolve this, make sure you define the variable in a statement before the line where you use the variable. If you already, *check your spelling* as one of them is probably spelled wrong or inconsistently.


## Defining multiple variables at once

You can define multiple variables at once separating them with a comma `,`.

```js
var john, paul, george, ringo;
```

**Best Practice**: Only use the `,` with var when defining multiple variables that do not have initial values.

```js
var coach, captain, teamName;
var waterboy = "Bobby";
var score = 2;
var winning = true;
```
