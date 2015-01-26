# Type Casting and Coercion

<!-- Maybe a link to a glossary for terms which might be unfamiliar eg operands -->
Operators expect certain types of values as operands. Other languages might throw an error of some sort if you try to, for example, do multiplication with strings. JavaScript however, will actually attempt to make your code work, and will do type coercion to get usable values.

## Type Coercion
<!-- what is coercion?   OK I know, but I think we need a simple one-liner for the nwbies -->
### Coercion to Numbers

`true` will be coerced to `1`
`false` will be coerced to `0`
`""` will be coerced to 0
A string representing a valid number will be coerced to that number. If it contains non-number characters, such as `,`, `$`, `%`, or `NZD`, it will be `NaN`, mentioned below.

### Coercion to Strings
<!-- examples reqd I think -->
Booleans are coerced to `"true"` or `"false"` respectively.
Numbers are coerced to strings as they would be output normally.

### Coercion to Booleans
<!-- examples reqd I think -->
`0` will be coerced to a boolean `false`, every other number will be `true`
`""` (empty string) is coerced to False

### NaN – not a number
<!-- examples reqd I think -->
When JavaScript cannot do a sensible type coercion, we get the very useless value `NaN`, representing a numeric value that is not a number. While it would be much more useful to get an error when this happens when a statement is executed, we don't get an error, and JavaScript can carry on to the next statement.

Any operation involving `NaN` results in `NaN`, earning the value a reputation of being *toxic*.

## Type Casting

Type casting is when you want to intentionally convert a value to another type, and do not wish to leave it to the whims of the interpreter.
<!-- examples reqd I think - why and when would we want to do this -->
### Strings to Numbers
* `string * 1`

This will trigger automatic number coercion as documented above.

* `Number(string)`
* `parseFloat(string);`
* `parseInt(string, 10);`

These are three built-in functions that do the conversion for us. The parentheses let us pass *parameters* or *arguments* for the function to work with.

These functions can take a string beginning with a valid number and cast it to either an integer or a floating-point number.

When functions are executed, they return a value, just as a variable returns its contents. Unlike a variable, a function returns a value derived from the function's input. We can then use that value in the rest of the statement

* `var score = Number("12");`
* `var averageGoals = parseFloat("2.1");`
* `var teammates = parseInt("15", 10);`

The first parameter is a string that (hopefully) has a number in it. `Number()` and `parseFloat()` only need the one parameter.
<!-- what will happen if there is not a number in it -->

**Aside**: `Number()` starts a capital letter because the function is also the object prototype for all number values. While this will be explained more later, functions should always start with a lower-case letter, but start with a capital letter if they are object prototypes.

These functions are actually a bit more useful than the automatic type coersion, as they are a bit more liberal in ignoring any trailing non-number string characters, and thus may return `NaN` less than type coersion.

For `parseInt`, it takes the two parameters.  The first is the same as `parseFloat()`, but the second parameter is a radix: the base the number is in. Usually you want `10` for base-10, but you can use any number between 2 and 36. Always provide the radix, otherwise older browsers' JavaScript intepreters will try to guess the base of the number, and may get it wrong.
<!-- define radix -->
**Best Practice**: Use `Number()`, `parseInt()` and `parseFloat()` on strings when you mean to work with a number value. Always provide a radix to `parseInt`.

### Numbers to Strings
* `number + ""`

To coerce a number into a string, just concatenate an empty string to the number.

### Numbers and Strings to Booleans

* `!! value` – double Boolean NOT

You may see `!!` in use: this is a double NOT. `!!` is often used to convert other value types to booleans, following the automatic rules above.
<!-- examples reqd I think - when might we see this -->
* `!! true` is true
* `!! false` is false
