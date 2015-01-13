
# Variables

<!--Loose values doesn't mean much to noobies. Perhaps introduce DRY here to make the point that a value that is being used frequently can be defined in one place,
then used over and over = efficiency.  Then we can bring in the idea that a variable can represent more complex things/concepts than just a value.  
Then you might like to refer to it again when you point out that everything is an opbject in JS-->

Loose values aren't all that useful in day to day programming. A value in one statement is more useful if we can use it in the next statement:

```js
var username;
username = "Earl";
console.log(username);
```

## Defining variables


The keyword `var` tells JavaScript to create a *variable*. A variable is a place in the computer memory that has been set aside to hold whatever value we put into it.

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

That said, some are universally accepted, such as `id`.
<!-- We haven't met arrays yet , and I'm not sure about "Code Smell" - I would use in when talking, but maybe not in writing -->
**Code Smell**: If you find yourself using variables such as `book1`, `book2`, `book3` and so on, you probably want an **Array**. That said, breaking a line into two parts, such as `address1` and `address2` is a notable exception.

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
```

Here, `username` is assigned the value `"Earl"`

We can also assign a value to a variable when it is defined.

```js
var username = "Earl";
```

## Using variables as values

```js
console.log(username);
```

Here the method `console.log` is being passed the `username` variable. What is actually taking place here is the value inside `username` is being *evaluated* to its value before being passed into `console.log`:

```js
console.log("Earl");
```
<!-- we haven't mentioned the idea that variables can be changed yet. Perhaps some exercises at this point to show the sorts of things we can do with them - eg concatenation -->
If the value obtained from the variable is changed, the value still in the variable is left unchanged.

## Reference Error: *variable* is not defined

When you attempt to use a variable that hasn't been defined, you may get an error:
```js
console.log(chunkyBacon);
```
<samp>Error: Uncaught ReferenceError: chunkyBacon is not defined.</samp>
<!-- BEST PRACTICE -->
To resolve this, make sure you define the variable in a statement before the line where you use the variable. If you already, *check your spelling* as one of them is probably spelled wrong or inconsistantly.


## Defining multiple variables at once

You can define multiple variables at once separating them with a comma `,`.

```js
var john, paul, george, ringo;
```

**Best Practice**: Only use the `,` with var when defining multiple variables that do not have initial values.

```js
var coach, captain, teamName;
var waterboy = "Bobby";
```
<!-- You have only mentioned variables that are strings.  We should probably broach the subject of numbers at least at this point, perhaps even a list of all the various types with a hint about which will be covered at what point in the near future -->