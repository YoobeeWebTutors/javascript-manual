# Control Statements

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
if (username === "Emmet") {
  alert("Everything is awesome, Emmet!");
} else if (username === "Lucy") { // username is not Emmet, check another condition
  alert("Welcome back, Wyldstyle");
} else { // username is not Emmet and it's not Lucy.
  alert("Thank you for following the instructions.");
}
```

# Nested `if` Statements


# `switch`
