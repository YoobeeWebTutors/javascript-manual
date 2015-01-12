# Defining Custom Functions

We can define our own functions that we can call elsewhere in our own program:

```js
function hello (person) {
  alert("Hello, " + person + "!");
}

hello("Dolly");
hello("World");
```

Here the function `hello` is being defined. The keyword `function` here is kind of like `var` in that it's creating a variable where the function will live. The function's name is `hello`, so the function will live in the `hello` variable, so we can use it later.

The `hello` function is followed a space and parentheses. This normally calls a function, but because the keyword `function` is being used, it will be used as part of defining the function. The name `person` here is actually a variable that will be usable inside the new function. The value of this variable will be the first value passed into the function as an argument. The space before the parentheses is optional, but including it further reinforces to the reader that it is not a call but a declaration.

The `{ }` *curly braces* here create a group of statements, called a *block*. The statements contained within will become the body of the function.

## What makes a good function?

A function should do one thing only. As a guideline, functions that are more than five statements long should probably be broken up into smaller functions.

A function should be named well. It should do what it says on the label.

A function should behave reliably. When given input, it should give the same output each time. Except when you intend it to behave randomly, as you might want in a video game.

A function should

# Example: Calculator

Let's take our coffee order calculator we wrote previously.

```js
var coffeeQuantity = 3;
var pricePerCoffee = 3.60;
var totalPrice = coffeeQuantity * pricePerCoffee;
console.log(coffeeQuantity + " coffees at $" + pricePerCoffee + " each comes to $" + totalPrice);
```

This is good, but what if our program needs to calculate two or more orders rather than just one?

You might be tempted to copy-paste the code to calculate it twice:

```js
var coffeeQuantity = 3;
var pricePerCoffee = 3.60;
var totalPrice = coffeeQuantity * pricePerCoffee;
console.log(coffeeQuantity + " coffees at $" + pricePerCoffee + " each comes to $" + totalPrice);

coffeeQuantity = 17;
pricePerCoffee = 3.60;
totalPrice = coffeeQuantity * pricePerCoffee;
console.log(coffeeQuantity + " coffees at $" + pricePerCoffee + " each comes to $" + totalPrice);
```

Note that we don't use var to redeclare the variables, as they are already defined above. You can safely leave the extra vars in, but they are superfluous.

Hopefully you can see here that this will work, but at the cost of making our code harder to maintain. We've duplicated code. Our calculation is now in two different places. Our `pricePerCoffee` is set twice. And our output string is duplicated too.

**Best Practice**: D.R.Y. — Don't Repeat Yourself
D.I.E. — Duplication Is Evil

If we have to change any one of these things, we now have to change it in two places. This isn't so bad for a small trivial program such as this, but if you imagine a larger program, repeating yourself with code scattered throughout your application, this quickly can become a nightmare to maintain.

We make code reusable by creating a function for it.

```js
var pricePerCoffee = 3.6;
function calculateCoffeeTotal (quantity) {
  return quantity * pricePerCoffee;
}

var coffeeQuantity = 3;
var totalPrice = calculateCoffeeTotal(coffeeQuantity);
console.log(coffeeQuantity + " coffees at $" + pricePerCoffee + " each comes to $" + totalPrice);

var coffeeQuantity = 17;
var totalPrice = calculateCoffeeTotal(coffeeQuantity);
console.log(coffeeQuantity + " coffees at $" + pricePerCoffee + " each comes to $" + totalPrice);
```

This hasn't reduced the length of our code that much, but now the calculation is happening in one place. If we want to modify that function to also add GST, we can do so:

```js
function calculateCoffeeTotal (quantity) {
  var gst = 1.15;
  return quantity * pricePerCoffee * gst;
}
```

Note here that there are no *magic numbers* in the calculation -- every value is documented by its variable name.


We can further reduce duplication by putting our `console.log` call in a function:

```js
var pricePerCoffee = 3.6;

function calculateCoffeeTotal (quantity) {
  return quantity * pricePerCoffee;
}

function outputCoffeePrice (price, quantity, total) {
  console.log(quantity + " coffees at $" + price + " each comes to $" + total);
}

var coffeeQuantity = 3;
var totalPrice = calculateCoffeeTotal(coffeeQuantity);
outputCoffeePrice(pricePerCoffee, coffeeQuantity, totalPrice);

var coffeeQuantity = 17;
var totalPrice = calculateCoffeeTotal(coffeeQuantity);
outputCoffeePrice(pricePerCoffee, coffeeQuantity, totalPrice);

```

This function accepts three values as *parameters*

Much better! Our code is much more maintainable. If we want to change the output message, we can do it in one place.


## Variable Scope

In the coffee calculator above, you may notice that the statement inside the `calculateCoffeeTotal` function uses a variable that is not defined inside the function. This function is taking advantage of something called *variable scope*. `calculateCoffeeTotal` is a global variable as it is not defined inside a function.

In JavaScript, variables are scoped to functions. Variables defined inside functions are only accessible

Variables not declared in any function are said to be *global scoped*. This means the variable can be accessed from anywhere. This might sound great, but it is considered bad practice to define global variables.

To see why global variables are bad, consider this example. On a typical web page you may have many different  JavaScript programs running. If these programs used global variables, they may unintentionally use the same variable names as each other. This means one variable could be being shared across more than one programs. If one program overwrites such a variable, the other program will use the unintended value, which is bad.

### Using a globally-scoped variable
```js
var greeting = "hello";

function greet () {
  alert(greeting);
}

greet();
alert(greeting)
```

Because `greeting` is declared outside or the `greet` function, the function has access to it.


### Using a function-scoped variable
```js
function greet () {
  var greeting = "hello"
  alert ("hello");
}

greet();
```
