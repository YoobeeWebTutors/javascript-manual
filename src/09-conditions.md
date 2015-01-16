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

We covered `&&` (Logical AND), `||` (Logical OR) and `!` (Logical NOT) previously, but conditions are where these operators shine.

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
