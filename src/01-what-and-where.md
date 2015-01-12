# Client Side Javascript
**Js should be changed to Javascript throughout**
JavaScript is the most used programming language in the world - nearly every web page uses JavaScript in some way or another.

## What does JavaScript do?

JS itself is just a programming language. What that language can do depends on the environment it is being used in.

*Javascript  is a programming language which historically, since its creation in ????, has been used to create event-controlled interaction in web pages. 
More recently it is also being used server side to interact with databases, read and wwrite files etc. Everything that is currently being performed by languages like PHP, ASP.NET etc*


### The Web Browser

This book focusses on JS in the web browser. Here, JS is used to add behaviour to a page. This can be as simple as doing something when the page loads, or causing something to happen when different page elements are clicked, dragged, or written into.

Web pages can be broken into four layers

1. Content (text, pictures, video, audio) – **Plain Text**
2. Document Semantics (headings, paragraphs, links, etc.) – **HTML**
3. Presentation Rules (font, colour, position, etc.) – **CSS**
4. Behaviours (interactivity, data handling, etc.) – **JavaScript**

JS can also communicate with web servers without having to load the page again. This is called AJAX, which will be covered towards the end of this book.
* Leave this line out  - explain further down in the "where to write JS" section*
JS can also be tinkered with in the browser's developer console.

### The Server

JavaScript can also be used on the server through a platform called [node.js](http://nodejs.org). Whole server-side applications can be written in JavaScript. These Node apps can talk to databases, read and write files to disk, even interact with other servers on the internet.
*This Introductory course will not be exploring this aspect
* Perhaps don't mention the command line environment
### Developer's Command Line Environment

When node.js is installed locally, developers can take advantage of plenty of open-source tools to help automate web development. Tools like *grunt* or *gulp* can be set up to automatically process *Sass* or *Less* stylesheets into regular CSS, optimising images, and compressing CSS and JS so they can be downloaded as quickly as possible.

*
## Where to write JavaScript
1. In an HTML script between <script> tags
2) In a separate file which is referred to in the HTML files eg
3) When developing, Javascript can be written directly into the "developer console"
*

### Developer Console

The console is a place where you can type JS and see what it does straight away. What you type can even change the web page you have open.

Each web browser has a developer's console built in. Some browser's consoles are more powerful than others.

###### Exercise:

* Locate the developer's console in three web browsers:
	* Google Chrome
	* Firefox
	* Internet Explorer or Safari
* Find where you can type the following code into, and run it.
	* `alert("Hello, world!");`
* For your three web browsers, discover and memorise the keyboard shortcuts for toggling the JS Console. 

### HTML Files

We can include JavaScript directly inside an .html file with the following code:

```html
<script>
	alert("Hello, world!");
</script>
```

### JS files

We can also keep our JavaScript in external files, and include those files on any pages that need it.

```html
<script src="js/form-validation.js"></script>
```

*Note*: When the `src` attribute is present, any script inside the script element is ignored. You can write comments here if you must, but actual code will be ignored.[1]

[1]:http://www.w3.org/TR/html5/scripting-1.html#inline-documentation-for-external-scripts

*Aside:* In older versions of Internet Explorer, the contents of the linked file would essentially be copied from the file and placed between the `<script>` tags as if it had been there all along. This made working JS in IE harder as the browser would report incorrect line numbers with errors.

**Best Practice**: All script tags should live just above the closing `</body>` tag. This lets the browser focus on downloading CSS, Images and other external resources before trying to download and execute scripts, speeding up the page load time.

**Tired Practice**: Old HTML resources will recommend you put your `<script>` elements in the `<head>` element, however, this can potentially have a negative impact on the page's loading speed.

**Worst Practice**: JavaScript attributes:

* `<a href="javascript:alert('nope');">...</a>`
* `<span onclick="alert('nope');">...</span>`

In the same way in CSS you want to use `class` attributes over `style` attributes and clearly separating your presentation layer from the document, avoid writing JS in attribute form like this. Keep your behaviour layer separate from your document and presentation layers.

**The Extra Mile**: The attributes `async` and `defer` can give better control over how your code will load. * Research and discuss why these options have been provided