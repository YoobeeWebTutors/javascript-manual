# Control Statements

Up until this chapter our programs have been simple in that they are just a series of statements that all get executed one at a time in sequence.

Most computer programs are useful when they do certain things when given certain values. We write programs to check to see if a particular condition is true, and do a set of statements as a result.

```js
var username = prompt("What's your name?");

if (username === "Emmet") {
  alert("Everything is awesome!");
}

alert("Hi, " + username + "!");
```

The `if` statement here has two parts: the *condition* and the *block*. If the condition evaluates to `true`, the statements in the block will be executed.
