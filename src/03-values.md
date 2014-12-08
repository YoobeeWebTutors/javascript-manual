# Computation vs Calculation

Programs tell computers what to do. What do computers do best? Computation.

Computation is about about *systematic application of rules*, or doing certain things in a certain order when certain conditions are met. This is called *logic*

Note that computation says nothing about maths! Performing arithmetic and doing mathematics is called *calculation*

Computers are very efficient at calculations, but we as programmers have to tell them what to do and when to do it.

# Values

In JavaScript we can work with different values.

## Numbers

* `1`
* `10.5`
* `-3.14159`
* `0`
* `1.2308956109358613e+19`

Numbers in JavaScript can be whole numbers, called *integers* or have decimal places, called *floating point numbers* or just *floats*

Integers in JavaScript can be any number between -9007199254740992 and 9007199254740992, or between positive and negative 2^53-1. 

**Aside**: These may seem like strange numbers to have as limits, but on a computer, everything comes back to Binary and powers of two. JavaScript uses 64 bits to store numbers. 52 of these bits for the significant figures, 1 bit for the sign (if it's positive or negative), and 11 bits for the exponent.

**Exercises**

## Strings

* `"Hello"`
* `"hello"`
* `'An entire sentence. Complete with punctuation!'`
* `" "` (just a space)
* `""` (empty string)
* `'Can\'t stop, won\'t stop!'` (escaped quotes)
* ``
* `"123"`
* `"34.55"`
* `"$27.95"`

Strings are collections of characters in a particular order. Strings must start and end (be *delimited* by) either \"double quotes\" or \'single quotes\'. What delimiter a string is started with is what it must end with.

Typographically these symbols are called 'straight quotes' or inch and foot marks. Be sure not to use "curly typographer's quotes" as used in this paragraph. This is why word processors make for a terrible code editor for programmers.

### Escape Characters

Because of delimiters, how can we use a quote as part of a string?

* `"Don't worry, be happy."`
* `'The words "Gangnam Style" will help date this guide.'`

If we use double quotes as our delimiters, we can use single quotes inside safely, and vice versa.

* `"She said, "Mustn't there be a way?" to no-one in particular."`

The statement above is not a valid string. The interpreter will get as far as `"She said, "` as a string, but after that second double quote it will get confused and throw an error such as this:

```
SyntaxError: Unexpected identifier.
```

Syntax in a programming context simply means "the expected structure of statements". Because we've broken the rules of JavaScript's syntax, the error tells us that it is unable to figure out what we meant.

To fix our syntax error we must *escape* our quotes with a backslash `\`.

* `"She said, \"Mustn't there be a way?\" to no-one in particular."`

However, if we want a backslash in our string, we have to escape that also:

* `The files were in E:\\Documents` -> The files were in E:\Documents

Using this escaping technique, we can also encode other characters into a string:

| Code   | Output        |
|--------|---------------|
| \n     | New Line      |
| \t     | Tab Character |
| \"     | Double Quote  |
| \'     | Single Quote  |
| \\     | Backslash     |

There are others too.

**Aside**: In terms of English punctation, the backslash character was invented in 1961 specifically for computing. It was included in ASCII along with the regular forward-leaning slash so up `/\` and `\/` down arrow symbols could be typed.

**Exercises**:
