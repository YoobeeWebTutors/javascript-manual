# Statements
*Brief, but there's not a lot to be said about statements.  I'm not sure about the semi-colon is a colon ... joke.  
Some of the foreign students have a problem with words like colon, semi-colon, underscore, dash etc, and we might like to provide a 
appendix which describes them, maybe 5em fonts to make it really obvious.
?? Where are we going to introduce consol.log() as a (really good) alternative to alert. ??
*

JavaScript programs are written line by line. Each line, or *statement* is a command to the computer to do one thing.

A statement like:

```js
alert("Hello, world!");
```

will tell the browser to open an alert box with the message *Hello, World!* in it.

The text of the program is interpreted by the browser's JavaScript engine, or the language's *interpreter*. The interpreter's job is to take code and convert it into *machine language* that can be actually run.

Each statement in the program ends with a semi-colon or `;`. This helps JavaScript's interpreter to know where one statement begins and another ends.

**Aside**: Know your punctuation: A semi-colon `;` is a colon `:` 'that has been run over by a semi truck -- it's been squished a bit.

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
