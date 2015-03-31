---
title: 01 – Client Side Javascript
layout: page
---
JavaScript is the most used programming language in the world - nearly every web page uses JavaScript in some way or another.

## What does JavaScript do?

JavaScript itself is just a programming language. What that language can do depends on the environment it is being used in.

JavaScript was created in 1994 by Brendan Eich working at Netscape as a means to add interactivity and behaviour to web pages. In this environment JavaScript can react to events such as mouse clicks and keypresses and change the page's elements accordingly. JavaScript can even talk directly to the web server, passing data back and forth.

More recently JavaScript is also being used on web servers in the form of *Node.js* applications to generate web pages, read and write files, interact with databases and other web servers, among other server-side application tasks. Node.js can do everything that other languages such as PHP, ASP.NET and Java can do.

Node.js is also being used by developers outside of the server environment as a powerful scripting and automation tool.

This book focuses on JavaScript in the web browser, and will not be touching on Node.js.

### The Web Browser

Browsers are simply programs designed to interpret client side code in order to create web pages to display. The code, along with the content, is separated by the browser into four layers:

Web pages can be broken into four layers:

1. Content (text, pictures, video, audio) – **Plain Text**
2. Document Semantics or 'markup' (headings, paragraphs, links, etc.) – **HTML**
3. Presentation Rules (font, colour, position, etc.) – **CSS**
4. Behaviours (interactivity, data handling, etc.) – **JavaScript**

JavaScript adds behaviour to web pages. This can be as simple as doing something when the page loads, or causing something to happen when different page elements are clicked, dragged, or written into, for example error messages that appear when a form field is filled in incorrectly.

## JavaScript for the Web Browser

This introductory course will only be exploring JavaScript in the web browser.

### Where to write JavaScript

1. In an HTML file, placing script between &lt;script&gt; tags.
2. In a separate `.js` file, referenced by HTML files.
3. When developing, Javascript can be written directly into the "developer console".

### 1. HTML Files

We can include JavaScript directly inside an .html file with the following code:

```html
<script>
	alert("Hello, world!");
</script>
```

### 2. JavaScript files

We can also keep our JavaScript in external files, and include those files on any pages that need it.

```html
<script src="js/form-validation.js"></script>
```

*Note*: When the `src` attribute is present, any script inside the script element is ignored. You can write comments here if you must, but actual code will be ignored.[1]

[1]:http://www.w3.org/TR/html5/scripting-1.html#inline-documentation-for-external-scripts

*Aside:* In older versions of Internet Explorer, the contents of the linked file would essentially be copied from the file and placed between the `<script>` tags as if it had been there all along. This made working JavaScript in IE harder as the browser would report incorrect line numbers with errors.

**Best Practice**: All script tags should live just above the closing `</body>` tag. This lets the browser focus on downloading CSS, Images and other external resources before trying to download and execute scripts, speeding up the page load time.

**Tired Practice**: Old HTML resources will recommend you put your `<script>` elements in the `<head>` element, however, this can potentially have a negative impact on the page's loading speed.

**Worst Practice**: JavaScript attributes:

* `<a href="javascript:alert('nope');">...</a>`
* `<span onclick="alert('nope');">...</span>`

In the same way in CSS you want to use `class` attributes over `style` attributes and clearly separating your presentation layer from the document, avoid writing JavaScript in attribute form like this. Keep your behaviour layer separate from your document and presentation layers.

**The Extra Mile**: The attributes `async` and `defer` can give better control over how your code will load. Research and discuss why these options have been provided

### 3. Developer Console

The console is a place where you can type JavaScript and see what it does straight away. What you type can even change the web page you have open.

Each web browser has a developer's console built in. Some browser's consoles are more powerful than others.

## Exercises

* Locate the developer's console in three web browsers:
    * Google Chrome
    * Firefox
    * Internet Explorer or Safari
* Find where you can type the following code into, and run it.
    * `alert("Hello, world!");`
* For your three web browsers, discover and memorise the keyboard shortcuts for toggling the JavaScript Console.
