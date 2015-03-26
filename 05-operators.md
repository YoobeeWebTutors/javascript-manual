---
title: 05 – Operators
layout: page
---

What can we do with values? Make new values from old ones. These are called *operations*.

We use *operators* to signify that we wish to perform these operations.

Operations are performed on one, two or three other values, called *operands*

## Assignment Operator

* `=` value assignment – 'is set to'

The assignment operator assigns a value to a variable.

## Numbers and Arithmetic

* `+` addition
* `-` subtraction
* `*` multiplication
* `/` division
* `%` remainder

Addition is performed with the `+` operator.

### Division Operator

`/` divides like a calculator divides, so `10 / 4` is 2.5, and `12 / 4` is 3.

### Remainder Operator
`%` is the remainder operator. It returns the remainder of an integer division.

`14 % 4` is 2. Because an integer division is happening, 14 ÷ 4 is 3 remainder 2.

While `%` is often called the 'modulo' operator in other languages, in Javascript `%` is not a true modulo on account of how negative operands are treated.

## Strings and Concatenation

* `+` concatenation "to link things together end to end"

If either operand around the `+` operator is a string value, `+` will not do addition, but instead will do *concatenation* and return the two values joined together as a string. If one operand is a string and the other is not, the other will be type coerced into to a string. Type coercion is talked about below.

* `10 + "10"` is `"1010"`. The number is coerced into a string, and a new string is created.
* `"hello" + "world"` is `"helloworld"`. Note how no space is placed between the two words. JavaScript has no awareness of English or other written languages.
* `"hello " + "world"` is `"hello world"`. The space follows the world `hello` and so is included in the concatenation.

```js
var hello = "hello";
var world = "world";
console.log(hello + " " + world)
```
In the parentheses `"hello" + " " + "world"` is being computed, which is `"hello world"`.

## Boolean values and Logical Operations

* `&&` logical AND
* `||` logical OR
* `!`  logical NOT (unary)

In Boolean logic, we can combine two Boolean values into one using the Boolean operators.

With `&&` the logical AND operator, both operands must be true to get a true result.

* `false && false` is false
* `true && false` is false
* `false && true` is false
* `true && true` is true

With `||` the logical OR operator, one or more of the operands must be true to get a true result.

* `false && false` is false
* `true && false` is true
* `false && true` is true
* `true && true` is true

With `!` the logical NOT operator, it only takes one operand, and the value of that operand is 'flipped':

* `! true` is false
* `! false` is true


**Aside**: The `&` symbol is called an *ampersand*, and the `|` is called the *vertical bar*, or in a command line interface a *pipe*

If an operand for a Boolean operator is not a Boolean value, it will be type coerced into a Boolean value.

## Formatting

Because good code is easily read, always put a space on both sides of an operator.

**Good**:
* `1 + 1`
* `"His name is " + " Robert Paulson."`
* `! true`
* `isWeekday && sunny`
* `(! forgotten || overAged)`

## Order of Operations

Some operators take precedence over others, and must be calculated or 'evaluated' first. Take for example:

* `9 + 9 * 9`

Is this 9 plus 9 equals 18, 18 times 9 equals 162?

* `9 + 9` -> `18`
* `18 * 9` -> `162`

Or is it 9 times 9 equals 81, 9 plus 81 equals 90?

* `9 * 9` -> `81`
* `9 + 81 ` -> `90`

In Programming, this is clearly defined. Each programming language has its own *order of operations*.

Mathematics has a standard 'order of operations', often memorised as PEMDAS or BEDMAS:

* Parentheses
* Exponents
* Multiplication
* Division
* Addition
* Subtraction

According to PEMDAS, `9 + 9 * 9` evaluates to `90`.

In programming, every operator takes a place in the language's order of operations hierarchy. All languages follow the order above, but there are more operators Most languages share the same order, but not all. Check out [JavaScript's Order of Operations](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence).

The `=` assignment operator is very low in the order of operations, and thus all other calculations happen before a value is assigned to a variable.

```js
var result = 9 + 9 * 9;
console.log(result);
```

This code will write to the console the number `90`.

### Associativity

Multiplication and division actually share the same level in the order, as do addition and subtraction. Other operators are also grouped in levels. Depending on the operator, the left-most or the right-most operator might be evaluated first. This is called associativity. For example, the assignment operators have right-to-left associativity, where the arithmetic operators have left-to-right.

### Parentheses

* `()` - Grouping operators

Because the order of operations is hard to memorise, its best to be explicit with what order of operations you the programmer intend, by using parentheses to group operands with the desired operators.

* `9 + 9 * 9` -> 90 – the order of operations will be applied
* `9 + (9 * 9)` -> 90 – here the parentheses are optional, but document the intent.
* `(9 + 9) * 9` -> 162 – parentheses are required to override default order of operations

## Documenting Values with Variables

Sometimes when writing a calculation, you may want to multiply one number with another.

```js
var quantity = 2;
var total = quantity * 9;
```

*Bad Practice*: The `9` here is referred to as a *magic number* – it's unclear what it actually represents. Maybe you've figured out that `9` is the unit price, but you had to think about it, didn't you.

*Best Practice*: Document what a value is by putting it in a variable. We'll also make sure that it's clear we're calculating a price and not a unit total This makes for very readable code:

```js
var unitPrice = 9;
var quantity = 2;
var totalPrice = quantity * unitPrice;
```
*Best Practice*: By putting numbers we use multiple times in a variable, we can keep that value in one place. This builds maintainable code: if the unitPrice changes in the future, we only need to change it in one place.

*Aside*: Variables that aren't supposed to be changed while the program is running are called *Constants*. The value in the variable should stay the same.

Some languages have syntax to declare the variable as read-only, JavaScript does not. If you mean for a variable to be treated as a constant, type it in ALLCAPS as a sign to yourself and others that this variable should not be modified by the program. Using this formatting isn't always necessary, but it's an established pattern you will see in other's published code.

# Example

## Coffee Cup Calculator
We wish to calculate how much we need to pay for a number of cups of coffee at a certain price each. If a cup of coffee costs $3.60 and we want 3 cups, we can calculate this ourselves at $10.80.

We could write this program:

```js
console.log(3 * 3.60);
```

and we would get our answer logged to us: `10.8`.

However, this program is not as maintainable or user friendly as it could be. Is '3' or `3.60` the price? Clearly we know what each value represents, but to an outsider, this code doesn't document itself. Putting the values in variables solves this:

```js
var coffeeQuantity = 3;
var pricePerCoffee = 3.60;
var totalPrice = coffeeQuantity * pricePerCoffee;
console.log(coffeeQuantity + " coffees at $" + pricePerCoffee + " each comes to $" + totalPrice);
```

This program will do the calculation, and output an improved message providing us more context to what just happened:

* "3 coffees at $3.6 each comes to $10.8"

### Input, Computation, Output

1. Input
2. Computation
3. Output

Programs exist to do computation of some sort. They take Input, do some sort of Computation and generate some Output.

The input in this program is first two variables: `coffeeQuantity` and `pricePerCoffee`.

The computation is taking place on the third line and being stored in the `totalPrice` variable.

The output shows us the result of the computation, along with reiterating to us what the input was.

### Program Execution - Statement by Statement

Programs are stepped through statement by statement. This program has four statements, seperated by semicolons.

The first statement creates a variable called `coffeeQuantity` and assigns it the value `3`.

The next line creates a variable called `pricePerCoffee` and assigns it the value `3.6`.

Next line creates a variable called `totalPrice`

* `var totalPrice`

Then there are some operators to evaluate. The assignment operator `=` is very low on the order of operations, so the multiplication is performed first. We'll take parts of the statement one by one

* `coffeeQuantity * pricePerCoffee`

You can think of JavaScript looking at this calculation and substituting the variable names with their values:

* `3 * 3.6`

Nothing will happen to the variables or their values. JavaScript is reading the value of the variable and working with a copy of the value.

Now the multiplication operator can be evaluated:

* `3 * 3.6` -> `10.8`

Now that everything on the right of the `=` assignment operator is evaluated, the `=` can be evaluated:

* `totalPrice = 10.8`

The `totalPrice` variable is now contains the value `10.8`.

Next statement we have a call to the `console.log()` function. Because there are unresolved operators, before the call to `console.log()` is made, the many different values will be concatenated into one string. Numbers are being treated as strings as no `+` here has numbers as both operands.

After the concatenation completes, we will have one string:

* `3 coffees at $3.6 each comes to $10.8`

This one string is given to `console.log()` as its parameter. The function will output the string on the console for viewing.

# Exercises
Write a new program for each of these points below. Each program should output what the input was along with the computed value.

* Bagels cost $4.35 each (before tax). Write a program to calculate how much 9 bagels costs and output the total. Your program should output the answer $39.15.
* Scones cost $0.60 each. Write a program to calculate and output the total price of 27 scones. You should get 16.2.
* It costs me $3.80 to make 13 muffins. How much did each muffin cost to make? The answer is appx $0.29 each, but write a program to calculate this.
* I have $100. How many bagels can I buy with that? The answer is 22, but write a program to do the calculation.
  * The most sensible program uses a function that JavaScript provides to round a number down – go look it up. However, it is possible to program this using `+`,`-`,`*`, `/` and one of either `parseInt` or `%`.
* How many scones can I buy with $100? 166, but write the program.
* How much change is left over from buying $100 worth of bagels? With that change, how many scones can I buy? 22 bagels, 7 scones, but write one program to calculate all of this, bagels and scones. There should be $0.10 left over, too.

## Taxes Exercise

* GST is 15%. To add GST to a number, multiply it by 1.15. Duplicate your first bagel program to calculate and output the exclusive and inclusive GST prices.
* Getting the GST amount for an inclusive number is slightly harder: Multiply the inclusive price by 3 and divide by 23. Write a program that accepts a number including GST and output the amount of tax added on, as well as the number excluding tax.

# Research
* Weirdly, in JavaScript, `0.1 + 0.2` does not give you `0.3`.
  * What does JavaScript calculate it to be?
  * Why is the computer doing this?
  * How could this affect your calculations?
  * What should programmers do to avoid this kind of error?
