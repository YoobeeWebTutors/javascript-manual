---
title: 02 – Statements
layout: page
---

JavaScript programs are written line by line. Each line, or *statement* is a command to the computer to do one thing.

A statement like:

```js
alert("Hello, world!");
```

will tell the browser to open an alert box with the message *Hello, World!* in it.

The text of the program is interpreted by the browser's JavaScript engine, or the language's *interpreter*. The interpreter's job is to take code and convert it into *machine language* that can be actually run.

Each statement in the program ends with a semi-colon or `;`. This helps JavaScript's interpreter to know where one statement begins and another ends.

**Aside**: Know your punctuation: Here's a word-picture to help your memory: A semi-colon `;` is a colon `:` 'that has been run over by a semi-trailer truck -- it's been squished a bit.

<!-- Figure: Some of the foreign students have a problem with words like colon, semi-colon, underscore, dash etc. Present side by side in 5em fonts to make it really obvious. -->

**Best Practice**: One statement per line of code. Because of this, the terms statement and line are used interchangeably.

A series of statements forms a **program**. A program is *run* or *executed* statement by statement in the order they are written.

```js
alert("Good Morning");
alert("Good Afternoon");
alert("Good Night");
```

In JavaScript, normally only one statement can be executed at any one time.

The program cannot go to the next line of code until the current line finishes executing, or *returns* from its task.

**Best Practice**: Reliability: Programs should always do the same thing each time they are run. Some programs may be coded to act randomly, but they should always react the same way to that randomness.

**Best Practice**: Even though JavaScript treats these semi-colons as optional, always put them in. Doing so avoids [Automatic Semi-colon Insertion (ASI)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Automatic_semicolon_insertion) issues.

**Best Practice**: To JavaScript, a statement can be as many characters long as it needs to be, but to programmers longer lines are harder to read. Try not to make a line longer than 80 characters, and certainly not longer than 120.

## Comments

Comments are lines of code that don't do anything, and we use them to leave helpful hints to other coders when they read this code in the future. Usually this is yourself, and yes, you'll always be a different coder in the future.

You should always ensure your code could be easily understood by other developers, and the main methods we have for this are comments and the way we name our variables and functions etc (you will see what these are very soon)_

```js
// one line comment
alert(10); // pieces of fruit available
```

*Best Practice*:

* Where possible, your code should be readable without comments. This is called self-documenting code. Soon you will be giving names to variables and functions, so name things so they are easily understood by anyone who reads your code.
* Comment briefly and clearly whenever necessary to ensure that your intentions for each piece of code are clearly understood. Refer to [Codeguide.co: CSS Comments](http://codeguide.co/#css-comments)

We can also comment out lines we don't need for the moment, while we get something to work. It's best to actually remove commented out code before you share it on a version control system, such as Git.

```js
// alert("You'll never see this unless you uncomment it");
```

There are also block comments. These are best for longer documentation.

```js
/* Longer comments can be written
that span over many lines
by using block comments */

/**
 * This style of comment is called a DocBlock, and is often found
 * in larger projects to serve as documentation for the thing that follows it.
 * JavaScript just sees a fancy block comment, but other tools will see the
 * asterisks and read the text and metadata in it and generate helpful books or
 * popups for you.
 *
 * @returns Boolean
 */
function doAThing() {
  return true;
}
```

Don't be surprised if you come back to some code you wrote six months later and say to yourself, "What was I thinking? How is this code even working? Surely I can do better now!"
