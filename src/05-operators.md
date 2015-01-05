# Operators

What can we do with values? Make new values from old ones. These are called *operations*.

We use *operators* to signify that we wish to perform these operations.

Operations are performed on one, two or three other values, called *operands*

## Numbers and Arithmetic

* `+` addition
* `-` subtraction
* `*` multiplication
* `/` division
* `%` remainder

Addition is performed with the `+` operator.

### Division Operator
`/` divides like a calculator divides.

`14 / 4` is 3.

### Remainder Operator
`%` is the remainder operator. It returns the remainder of an integer division.

`14 % 4` is 2. Because an integer division is happening, 14 ÷ 4 is 3 remainder 2.

While `%` is often called the 'modulo' operator in other languages, in Javascript `%` is not a true modulo on account of how negative operands are treated.

## Strings and Concatenation

* `+` concatenation "to link things together end to end"

If either operand around the `+` operator is a string value, `+` will not do addition, but instead will do *concatenation* and return the two values joined together as a string. If one operand is a string and the other is not, the other will be type coerced into to a string. Type coercion is talked about below.

* `10 + "10"` is `"1010"`. The number is coerced into a string, and a new string is created.

## Boolean values and Logical Operations

* `&&` logical AND
* `||` logical OR
* `!`  logical NOT (unary)

In Boolean logic, we can combine two boolean values into one using the boolean operators.

With `&&` the logical AND operator, both operands must be true to get a true result.

* `false && false` is false
* `true && false` is false
* `false && true` is false
* `true && true` is true

With `||` the logical OR operator, one or more of the operands must be true to get a true result.

* `false && false` is false
* `true && false` is true
* `false && true` is true
* `true && true` is true

With `!` the logical NOT operator, it only takes one operand, and the value of that operand is 'flipped':

* `! true` is false
* `! false` is true


**Aside**: The `&` symbol is called an *ampersand*, and the `|` is called the *vertical bar*, or in a command line interface a *pipe*

If an operand for a boolean operator is not a boolean value, it will be type coerced into a boolean value.

You may see `!!` in use: this is a double NOT. `!!` is often used to convert other value types to booleans.

* `!! true` is true
* `!! false` is false

## Formatting

Because good code is easily read, always put a space on both sides of an operator.

**Good**:
* `1 + 1`
* `"His name is " + " Robert Paulson."`
* `! true`
* `isWeekday && sunny`
* `(! forgotten || overAged)`

## Order of Operations

Some operators take precedence over others, and must be calculated or 'evaluated' first. Take for example:

* `9 + 9 * 9`

Is this 9 plus 9 equals 18, 18 times 9 equals 162?

* `9 + 9` -> `18`
* `18 * 9` -> `162`

Or is it 9 times 9 equals 81, 9 plus 81 equals 90?

* `9 * 9` -> `81`
* `9 + 81 ` -> `90`

In Programming, this is clearly defined. Each programming language has its own *order of operations*.

Mathematics has a standard 'order of operations', often memorised as PEMDAS or BEDMAS:

* Parentheses
* Exponents
* Multiplication
* Division
* Addition
* Subtraction

According to PEMDAS, `9 + 9 * 9` evaluates to `90`.

In programming, every operator takes a place in the language's order of operations hierarchy. All languages follow the order above, but there are more operators Most languages share the same order, but not all. Check out [JavaScript's Order of Operations](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence).

### Associativity

Multiplication and division actually share the same level in the order, as do addition and subtraction. Other operators are also grouped in levels. Depending on the operator, the left-most or the right-most operator might be evaluated first. This is called associativity. For example, the assignment operators have right-to-left associativity, where the arithmetic operators have left-to-right.

### Parentheses

* `()` - Grouping operators

Because the order of operations is hard to memorise, its best to be explicit with what order of operations you the programmer intend, by using parentheses to group operands with the desired operators.

* `9 + 9 * 9` -> 90 – the order of operations will be applied
* `9 + (9 * 9)` -> 90 – here the parentheses are optional, but document the intent.
* `(9 + 9) * 9` -> 162 – parentheses are required to override default order of operations

## Type Coercion

Operators expect certain types of values as operands. Other languages might throw an error of some sort if you try to, for example, do multiplication with strings. JavaScript however, will actually attempt to make your code work, and will do type coercion to get usable values.

The string `"1"` coerced to a number will give the number `1`.

### Coersion to Numbers

`true` will be coerced to `1`
`false` will be coerced to `0`
`""` will be coerced to 0
A string representing a valid number will be coerced to that number. If it contains non-number characters, such as `,`, `$`, `%`, or `NZD`, it will be `NaN`, mentioned below.

### Coersion to Strings

Booleans are coerced to `"true"` or `"false"` respectively.
Numbers are coerced to strings

### Coercion to Booleans

`0` will be coerced to a boolean `false`, every other number will be `true`

### NaN – not a number

When JavaScript cannot do a sensible type coercion, we get the very useless value `NaN`, representing a numeric value that is not a number. While it would be much more useful to get an error when this happens when a statement is executed, we don't get an error, and JavaScript can carry on to the next statement.

Any operation involving `NaN` results in `NaN`, earning the value a reputation of being *toxic*.
