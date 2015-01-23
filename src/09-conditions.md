# Conditions

A condition is like a calculation but returns a Boolean `true` or `false`.

We can check to see if one value matches as another, or is lesser or greater.

# Equality Operators

* `===` Strict Equality
* `!==` Strict Inequality
* `==` Loose Equality
* `!=` Loose Inequality

*Strict* Equality or Inequality returns true if the two operands are the same type and have matching value.

*Loose* Inequality works the same as strict equality, except that if the two operands are of different types, it will attempt to coerce the types to match, and then checks if they match.

```js
console.log(1 === 1); // true
console.log("joe" === "joe"); // true
console.log("joe" === "Joe"); // false, case sensitive
console.log(7 === 10); // false
console.log(1 === "1"); // false -- types do not match

console.log(1 == 1); // true
console.log("joe" == "joe"); // true
console.log(7 == 10); // false
console.log(1 == "1"); // true -- types are coerced and end up matching
```

*Best Practice*: Use only `===` and `!==`. Because of the type coercion works unreliably, loose equality should be avoided.

# Comparison Operators

* `<` Less than
* `>` Greater than
* `<=` Less than or equal to
* `>=` Greater than or equal to

```js
console.log(1 < 2); // true
console.log(7 > 10); // false
console.log(2 <= 2); // true
console.log(2 <= 3); // true
console.log(8 >= 5); // true
console.log(10 >= 7); // false
```

Comparison operators are especially for numbers. While you can use them for strings, they operate by essentially sorting the two strings, which doesn't usually do what you want. Sorting will be covered later.

# Logical Operators

We covered `&&` (Logical AND), `||` (Logical OR) and `!` (Logical NOT) previously, but conditions are where these operators shine. They combine the Boolean value from other conditions.

```js
// Fruit Inventory
var apples = 10;
var bananas = 27;
var cherries = 2;
var shopOpen = true;

console.log(apples > cherries && apples < bananas);
  // true - more apples than cherries AND less apples than bananas.
console.log(apples > 1 || bananas > 1 || cherries > 1); // true
console.log(! shopOpen); // false
```

## Checking against a set of values

Note that we have to use the logical operator to separate two discreet conditions. You can do the following, but it won't do what you want it to:
```js
console.log(name === "Felix" || "Ralph"); // Always true, no matter the value in name.
```
The first condition is `name === "Felix"`, which could be `true` or `false`.

The other condition is just `"Ralph"`, which by itself is a non-empty string, which is coerced to `true`.

So you must check the variable for equality with each string: `name === "Felix"` and `name === "Ralph"`. The equality operator `===` along with both of its operands must be present for each condition.

Because a variable cannot contain both `"Felix"` and `"Ralph"`, using `&&` will not help us. Using `||` between the two conditions will tell us if the variable contains either of the strings.

```js
// Name checker
var name = "Bob";
console.log(name === "Felix" || name === "Ralph"); // false
console.log(name !== "Felix" && name !== "Ralph"); // true
```

As the list of names you want gets longer, other solutions are needed, such as Arrays, which will be covered later.
