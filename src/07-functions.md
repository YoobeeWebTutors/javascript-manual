# Functions

Functions are like smaller programs within your larger program, and are sometimes referred to as *subroutines*.

Functions wrap a set of statements that work together, usually to compute one piece of output.

Those functions usually work with some input given to them.

Functions are essentially a variable that stores a function object.

## Calling a function

We can invoke or execute a function, by *calling* it. A function call looks like this:

* `alert()`

By using the name of the function followed by a pair of parentheses.

When we call a function we can *pass* it values as input. These values are called *parameters* or *arguments*.

* `parseInt("123", 10)`

Here the function `parseInt` is being called, passing it the string `"123"` as the first parameter and the number `10` as the second parameter. Functions, when they are defined, can capture these parameter values in parameter variables.

## Built-in Functions

You've already used some of JavaScript's built-in functions:

* `alert("Hello, world!");`
* `console.log("hello devs");`
* `Number("123.45");`
* `parseFloat("321.98");`
* `parseInt("123", 10);`

All these functions take a value, in order to do something with that value. Some of these functions return useful values that can be used in our own programming.

JavaScript has plenty more built in functions for you to research and discover. Let's look at some of the built in functions you'll find most useful at this stage:

### Modal functions

* `alert("for your information")`
* `var performDelete = confirm("Do you want to delete that?");`
* `var username = prompt("What's your name?");`

These three functions can be very useful when learning and debugging your code, but are considered bad practice for common use.

These three functions are *modal* -- they pause the whole browser tab from doing anything: repainting, further JavaScript execution. The user cannot interact with the web page until the modal is dismissed. Resources such as images and other files will continue to download, but the page will not be updated until the modal window is closed.

#### alert( *message* );

When the browser executes the `alert()` function, the browser will display a little window with your message in it, and clicking the OK button, pressing Enter or pressing Escape will dismiss it.

`alert()` always returns `undefined`.

#### confirm( *message* );

When the browser executes the `confirm()` function, the browser will display a little window with your message in it, along with two buttons: "OK" and "Cancel".

`confirm()` will return `true` or `false` depending on if OK or Cancel was clicked, respectively. You probably intend to capture this Boolean value in a variable for use later in your program.

#### prompt( *message*, [*defaultValue*] );

When the browser executes the `prompt()` function, the browser will display a little window with your message in it, along with a text field and two buttons "OK" and "Cancel". The text field will have focus and the user can enter a string as input.

If the second parameter *defaultValue* is provided, the text field will initially contain *defaultValue*. The text will be highlighted so it can be overwritten easily.

If the user clicks OK or presses Enter, `prompt()` returns the string entered into the text field. `prompt()` always returns a string, even when you enter a valid number. If you want a number, coerce the value `prompt()` returns into a number before you treat it as one.

If the user clicks Cancel or presses Escape, `prompt()` returns `null`. `null` is another value similar to `undefined` but represents the purposeful value of nothing. `null` is not a string, number or boolean.

### Development Console functions

The `console` object is a built-in object for your program to interact with the browser's developer console. Functions stored on an object are called *methods*. There are many `console` methods, which you can research. The ones to know are:

#### console.log( *message*, [...] );

This outputs values to the developer console panel. Note that different browsers output different values differently. For example, Chrome and Firefox will colour strings and numbers differently, but Firefox shows quotes around strings while Chrome does not.

#### console.info( *message*, [...] );
#### console.warn( *message*, [...] );
#### console.error( *message*, [...] );

These functions share the same *signature* as `console.log`, but act differently from each other. Depending on the browser, they might colour the output differently or put an icon next to the output in order to help you determine how important the output might be.

`console.info` is for informative output, a 'heads up' that something expected happened.

`console.warn` is for warnings: the program has detected something out of the ordinary.

`console.error` is for errors: the program cannot do what it should because something is wrong.

**Aside**: The developer console is not used by regular users, only by developers like you and me. Normally you'll want your program to output values to users by modifying a webpage. Output to the console only during development, and remove any `console` function calls before you deploy your code to production.
