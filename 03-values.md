---
title: 03 – Values
layout: page
---

Programs tell computers what to do. What do computers do best? Computation.

Computation is about about *systematic application of rules*, or doing certain things in a certain order when certain conditions are met. This is called *logic*

Note that computation says nothing about maths! Performing arithmetic and doing mathematics is called *calculation*

Computers are very efficient at calculations, but we as programmers have to tell them what to do and when to do it.

# Values

In JavaScript we can work with different values.

## Numeric Values

* `1`
* `10.5`
* `-3.14159`
* `0`
* `1.2308956109358613e+19`

Numbers in JavaScript can be whole numbers, called *integers* or have decimal places, called *floating point numbers* or just *floats*. Floats can contain up to 16 significant figures total, both before and after the decimal point.

While you may never intentionally use them, you might see numbers ending with `e+01` or `e-01` in some circumstances. These are called *exponents*: multiply the preceding number by this number of powers of ten. JavaScript automatically converts very large numbers to exponents where necessary. Honestly though, you won't see exponents in common use.

### Numerical Equivelence

```js
alert(100.00);
```

This alerts `100`. Why not `100.00`? Numbers in JavaScript have no concept of desired decimal places. There's not a simple way to tell it how many trailing zeroes you want.

In fact, when we write `3.60`, JavaScript stores the value `3.6`. `3.60` and `3.6` are numerically identical values.

There are functions we can write and use to present numbers in different formats, but out of the box, we get this behaviour.

### Know your limits

Integers in JavaScript can be any number between -9,007,199,254,740,992 and 9,007,199,254,740,992, or between positive and negative 2^53-1, before potentially being stored as an exponent.

Floating point numbers can have up to 16 significant decimal places, and, depending on the JS engine, an exponent between -324 and +308.

Go outside these ranges and you'll get magical values such as Infinity and -Infinity.

**Aside**: These may seem like strange numbers to have as limits, but on a computer, everything comes back to Binary and powers of two. JavaScript uses 64 bits to store numbers. 52 of these bits for the 16 significant figures, 1 bit for the sign (if it's positive or negative), and 11 bits for the exponent.


## String Values

* `"Hello"`
* `"hello"`
* `'An entire sentence. Complete with punctuation!'`
* `" "` (just a space)
* `""` (empty string)
* `'Can\'t stop, won\'t stop!'` (escaped quotes)
* ``
* `"123"`
* `"34.55"`
* `"$27.95"`

Strings are collections of characters in a particular order. Strings must start and end (be *delimited* by) either \"double quotes\" or \'single quotes\'. What delimiter a string is started with is what it must end with.

Typographically these symbols are called 'straight quotes' or inch and foot marks. Be sure not to use "curly typographer's quotes" as used in this paragraph. This is why word processors make for a terrible code editor for programmers.

### Escape Characters

Because of delimiters, how can we use a quote as part of a string?

* `"Don't worry, be happy."`
* `'The words "Gangnam Style" will tell you when this was written.'`

If we use double quotes as our delimiters, we can use single quotes inside safely, and vice versa.

* `"She said, "Mustn't there be a way?" to no-one in particular."`

The statement above is not a valid string. The interpreter will get as far as `"She said, "` as a string, but then it will get confused and throw an error such as this:

```
SyntaxError: Unexpected identifier.
```
<!-- I like the idea of introducing common errors that they will see. When they are relevant, rather than in one lump, although we might have a chapter (appendix?) on debugging where everything is lumped together?? -->

This is because the JavaScript interpreter doesn't know you mean by an `M` after that second double quote. The 'identifier' this error is referring to is it thinks that M is part of an identifier, such as a variable name or function -- we'll talk about these soon.

Syntax in a programming context simply means "the expected structure of statements". Because we've broken the rules of JavaScript's syntax, the error tells us that it is unable to figure out what we meant.

To fix our syntax error we must *escape* our quotes with a backslash `\`.

* `"She said, \"Mustn't there be a way?\" to no-one in particular."`

However, if we want a backslash in our string, we have to escape that also:

* `"The files were in E:\\Documents"` -> The files were in E:\Documents

Using this escaping technique, we can also encode other characters into a string:

* `\n` New Line
* `\t` Tab Character
* `\"` Double Quote
* `\'` Single Quote
* `\\` Backslash

There are others too.

**Aside**: In terms of English punctation, the backslash character was invented in 1961 specifically for computing. It was included in ASCII along with the regular forward-leaning slash so up `/\` and `\/` down arrow symbols could be typed.

<!-- Concatenation could be introduced here? -->

## Exercises
* Enter some of the above strings into your browser's JavaScript console. Be careful to get them right, but also see what happens when you get them wrong.
* Write these in the console as valid strings. The best answers here will use the least number of characters.
  * I'd think you wouldn't do that.
  * 'Bob's requested, "Please don't say goodbye"', said Alice.
  * "I'll take 1/3 of the prize pool", he said proudly.
* Experiment with putting strings with the `alert()` function, e.g.: `alert("Hello, world!");`. Test it with the escape characters in the table above like `\n` and `\t`.
* Try using `console.log()` instead of `alert()`. What's the difference?

## Boolean Values

Boolean values are very important. Computers work logically and in binary: true and false, 1 and 0, on and off, black and white. There is no 0.5, no almost off, no 'grey' or fuzzy area in this kind of logic.

* `true`
* `false`

Boolean values represent a non-numerical logic state. They are called *Boolean logic* values, or just `Booleans`. Booleans are named after 19th-century English mathematician George Boole (hence  why Boolean is always capitalised). His Boolean logic dictates that something logic describes is either true or false, not both or neither, and not somewhere between.

Booleans are extremely useful in programming when it comes to testing for a certain condition. For example, is 12 less than 15? Yes, 12 is less than 15. The answer to questions like this is either true or false. It is never both, neither, fuzzy or unknown.
