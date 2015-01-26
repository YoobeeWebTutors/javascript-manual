<!-- SY27/1/15

This one is really starting to show the need for a glossary.  I'm thinking about the first-time readers here, and the unfamiliar terms that might have been mentioned once or twice but not necessarily absorbed as basic vocab yet.



# Defining Custom Functions

We can define our own functions that we can call elsewhere in our own program:

```js
function hello (person) {
  console.log("Hello, " + person + "!");
}

hello("Dolly");
hello("World");
```

Here the function `hello` is being defined. The keyword `function` here is kind of like `var` in that it's creating a variable where the function will live. The function's name is `hello`, so the function will live in the `hello` variable, so we can use it later.

## Formatting

The `hello` function is followed a space and parentheses. The parentheses form the *parameter declaration*: what variables will be used to capture values passed to the function.

The `{ }` *curly braces* here create a group of statements, called a *block*. The statements contained within will become the body of the function.

## Coding Style and Indentation
<!-- SY 27/1/15
I think we should show an example of a simple, but uncommented and badly indented function alongside a properly commented and well laid out one.  The Don't Make Me Think approach to coding
-->
Coding style varies from language to language. JavaScript doesn't really mind where we put some symbols -- white space and line breaks are pretty much ignored by JavaScript. We humans however find them very useful.

There are many popular 'coding guides', but we will teach you the most common, often called 1TCS or One True Coding Style.
<!-- SY 27/1/15 - Links to online resources here -->

Different teams and projects use different styles for different languages. HTML will have one, CSS another, JavaScript yet another.

Curly braces are usually placed one space after the parameter parentheses to open, and on a line by itself to close. The closing bracket should be in the same column as the first character of the function declaration.

In the same way you indent HTML and CSS, we indent code. To make it clear what lines belong to what block, we indent them a level. Every line that belongs to a block should begin at the same column.

Usually we press the <kbd>tab</kbd> key to indent a line. Different editors treat this differently by default.

<!-- SY 27/1/15
Perhaps some hints about how to set this up in Sublime at least. 
-->

Some editors type hard tabs: the control character Horizontal Tab (ASCII code 9, `\t`). This traditionally has been rendered as eight spaces, the same as typewriters would. Some editors will type soft-tabs, substituting `\t` for eight, four or two actual space characters. Most editors will allow for both, letting you change the setting in the application's preferences.
<!-- SY 27/1/15  
Perhaps we should provide some examples of different styles - maybe in an aside or an appendix 
-->

As a programmer, your job is to learn the style being used in the code you are working on and work to it. Good code looks like it was written completely by one person, even though this is rarely the case.

## Parameters
<!-- SY 27/1/15
Unclear what this means -->
This normally calls a function, but because the keyword `function` is being used, it will be used as part of defining the function. The name `person` here is actually a variable that will be usable inside the new function. The value of this variable will be the first value passed into the function as an argument. The space before the parentheses is optional, but including it further reinforces to the reader that it is not a call but a declaration.


### Optional Parameters

Sometimes, a function will only want a parameter some of the time. If the function is not provided a value for a parameter, the capturing variable will be `undefined`.
<!-- Sy 27/1/15
Explain what this will do before showoing the example
-->


```js
function hello (person) {
  person = person || "world";
  console.log("Hello, " + person + "!");
}

hello("Dolly"); // "Hello, Dolly!"
hello();        // "Hello, world!"
```

Here, the Boolean operator for Logical OR serves as a *default operator*. Technically, the `||` operator will return the first operand if it's truthy, otherwise it returns the second operand. This behaviour is called *short-circuiting* — `&&` and `||` don't actually bother looking at the second operand if the first operand is enough.

When the first parameter is not provided to `hello()`, `person` is set to `undefined`, and `undefined` is falsy, so `||` returns `"world"`.

Also note that we don't have to use `var person` here. Because `person` is used inside the parentheses in the function definition, the variable is declared and initialised for us.

## Return Values
<!-- SY 27/1/15 

What are the other options for a function - what else can they do if they are not returning something
-->


Usually, a function will return a value for use in the code where the function was invoked. To make functions that provide this value back to its caller, we use the `return` keyword in a statement:

```js
function giveMeALetter(letter) {
  return letter + "!";
}
giveMeALetter("A"); // returns "A!"
```

When JavaScript executes a `return` statement, it will stop working through the function and return to the code that called the function. No other code inside the function after the `return` statement will execute.

```js
function meaningOfLife() {
  console.log("You will see this.");
  return 42;
  console.log("You will never see this.");
}
```

*Aside*: While we recommend you always use semi-colons at the end of statements, even though they are optional in JavaScript, JavaScript's Automatic Semi-colon Insertion is the weakest around `return` statements and can cause problems if you omit them.

## What makes a good function?

A function should do one thing only. As a guideline, functions that are more than five statements long should probably be broken up into smaller functions.

A function should be named well. It should do what it says on the label. This builds *self-documenting code*.

A function should behave reliably. When given input, it should give the same output each time. Except when you intend it to behave randomly, as you might want in a video game.

If a function returns a value, it should not (strictly speaking) have 'side effects' – it should not change any variables outside its scope, or create output.

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

<!-- SY 27/1/15
BIG EMPHASIS 
This is a fundamental BEST PRACTICE and needs to be explained, emphasised and explained again. At least make this very bold and clear.  
It does become apparent in the following  paragraphs but we need to make them want to NEVER repeat themselves, or at least to notice when have they done so as a trigger to improve their code to get around it
-->

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

<!-- 27/1/15
What is 'scope"?
Why do we have different 'scopes'
My initial explanation is along the lines of 'We like to give precise and unmistakeable directions to computers because they are not actually all that clever. Controlling the scope is one way to help this process'.

Would you want to introduce the notion of namespacing at this point, even simplistically with a hint that it something they will come across in more advanced programming?

-->

# Variable Scope

In the coffee calculator above, you may notice that the statement inside the `calculateCoffeeTotal` function uses a variable that is not defined inside the function. This function is taking advantage of something called *variable scope*. `calculateCoffeeTotal` is a global variable as it is not defined inside a function.

In JavaScript, variables are scoped to functions. Variables defined inside functions are said to be *locally scoped*, and are only accessible to code written within that function, even to functions defined within that function.

Variables not declared in any function are said to be *global scoped*. This means the variable can be accessed from anywhere. This might sound great, but it is considered bad practice to define global variables.

To see why global variables are bad, consider this example. On a typical web page you may have many different  JavaScript programs running. If these programs used global variables, they may unintentionally use the same variable names as each other. This means one variable could be being shared across more than one programs. If one program overwrites such a variable, the other program will use the unintended value, which is bad.

## Globally-Scoped Variables
```js
var greeting = "hello";
console.log(greeting);

function greet () {
  console.log(greeting);
}

greet();
```

Because `greeting` is declared outside or the `greet` function, the function has access to it.


## Locally-Scoped Variables
```js
function greet () {
  var greeting = "hello";
  console.log(greeting);
}

greet();
console.log(greeting); // gives uncaught ReferenceError: greeting is not defined.
```
In the code above, the variable `greeting` only exists inside the `greet()` function. When the function ends, the variable does not remain usable outside the function.

## Locally-scoped Variables Obscure Globally-scoped Variables
```js
var message = "bye"

function goodbye () {
  var message = "farewell";
  console.log(message);
}

goodbye();
console.log(message);
```
In this code, there are two variables called `message`. One is globally scoped, one is scoped to `goodbye()`. They both contain different values.

Because a `message` variable is being declared inside `goodbye()`, it obscures access to the global `message`.

Obscuring is not normally a problem: reusing variable names is normally fine, but if they do conflict with global variables you will have problems.

# Exercises
<!-- SY 27/1/15
I like these.  They will have to think for themselves
-->
* Write a function that returns the input string with French « guillemets » around it. These are not two angle brackets together, but one character.
* Write a function that returns the input string surrounded with Spanish exclamation marks around it: ¡Arriba! ¿Se puede hacer otra con signos de interrogación españoles?
* Write a function that takes one number as a parameter, calculates GST, and returns the original number including GST. Write code that uses the function to demonstrate that it works.
* Write a function that takes a number including GST and returns the number excluding GST.
