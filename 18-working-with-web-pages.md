---
title: 18 – Working with Web Pages
layout: page
---

Programming is about taking some input, doing a calculation or computation with that input, and creating output. Up until this point, we've been working with `prompt()` for input and `alert()` and `console.log()` for output. These are useful for learning, but no good for professional work.

## The Document

Every element in the current page is accessible via the `document` object. This object lets us access different parts of the page.

When JavaScript was first released, CSS wasn't a thing yet. Over time, the DOM has evolved through levels, from Level 0 where we could change very little, to Level 3, which is faster, less cumbersome, and lets us control nearly everything.

As of this writing, Level 4 is still in development.

To inspect or change an element, we must first find the element's node.

## DOM Level 0

While we won't go into much detail about DOM Level 0, these are the only ways you could access elements until Netscape 6 and IE 5.

* `document.images[]` -- a NodeList of all the images on the page.
* `document.forms[]` -- a NodeList of all the forms on the page.
* `document.forms[].elements[]` -- all the form fields inside a given form.
* `document.links[]` -- all the links (&lt;a href&gt;) on the page.
* `document.anchors[]`, -- all the anchors (&lt;a name&gt;) on the page.

***Best Practice***: Don't use the properties above. As you'll see, we have much more useful ways of getting elements these days.

These properties contained NodeList objects. A NodeList is a collection of elements. It behaves very much like a read-only array; it has a length and you can access the array elements like normal, but a NodeList is missing all the methods arrays normally have, such as `push` and `sort`.

***Aside:*** There were also ways of working with the `location`, `window`, `screen`, and even control the browser through `history` and `navigator`, many of which we still use today.

Once we have an element, we can look at and manipulate some of its properties.

- `element.value` -- the current value of the form element
- `element.checked` -- if a checkbox or radio box is checked or not
- `element.name` -- the name attribute of an element
- `element.type` -- the type attribute of a form element
- `element.href` -- the href attribute of a link
- `element.text` -- the text inside an link or anchor.

For the curious:
* [Netscape Client-Side JavaScript Reference v1.3](http://web.archive.org/web/19991012215641/http://developer.netscape.com/docs/manuals/js/client/jsref/index.htm)

## DOM Level 1

Every element was made accessible in DOM Level 1, first supported by Internet Explorer 5 and Netscape 6.

You could now navigate or 'walk' it like a tree using some properties like `document.childNodes[].childNodes[]`, and navigate back up the tree with `element.parentNode`. Doing this, however, is slow and cumbersome for the programmer, and is rarely performed.

Level 1 also added the ability to add, move and delete elements, but this too was cumbersome, and rife with inconsistencies across browsers. Libraries such as jQuery later came along and provided easier way to work with the DOM in a cross-browser friendly manner. Browsers have been slowly fixed over time, with Internet Explorer 9 fixing the last of the true DOM problems.

DOM Level 1 formalised many properties on an element too, the most useful being:

- `element.id` -- the id attribute of an element
- `element.title` -- the title attribute of an element
- `formelement.disabled` -- the disabled attribute of a form element
- `formelement.readOnly` -- the readonly attribute of a form element

## DOM Level 2

DOM Level 2 became usable with Internet Explorer 6 and Mozilla (which later became Firefox). Level 2 made it easy to find an element: You could now get an element by its (unique) id attribute, or get groups of tags by their tag name. This was the first turning point for JavaScript being taken seriously.

### `document.getElementById( string )`

`getElementById` takes a string as input, searches the document for an element with the id attribute matching the string (case sensitive), and returns a Element object of some kind. If no element with that id is found, it returns `null`.

```js
var sidebarDiv = document.getElementById('sidebar'); // returns an HTMLDivElement, or null.
```

### `document.getElementsByTagName( string )`
### `element.getElementsByTagName( string )`

`getElementsByTagName` takes a string as input, searches the document for all elements of that tag name, and returns them as a HTMLCollection. If no elements are found, the collection will have a length of zero.

HTMLCollections are like NodeLists, but are also considered 'live': if more elements are added to the page that have the same element name, this object will include it.

If called as a method of an element instead of a method of `document`, it will search only inside that element.

```js
var sidebarDiv = document.getElementById('sidebar'); // returns an HTMLDivElement, or null.
var sidebarLinksList = sidebarDiv.getElementsByTagName('a');
```

DOM 2 also added support for working with CSS.

- `element.className` -- the class attribute of an element.
- `element.style` -- an object representing the CSS properties applied directly to the element, initially via the style attribute.

Microsoft had always broken away from the standards, but for the first time, made something so useful that other browsers imitated:

- `element.innerHTML` -- view or replace the contents of an element, including creating new elements inside it.

***Aside***: Microsoft has continued bucking the standards, and would go on to have success with XMLHttpRequest, what we now know as AJAX.

With DOM Level 2 making everything on the page fair game, and `innerHTML` making modifications really easy, pages using JavaScript really exploded.

```js
// try this in the console at a site like http://medium.com
var articlesList = document.getElementsByTagName('div');
for (var i = 0; i < articlesList.length; i += 1) {
  if (articlesList[i].className.indexOf('article')) {
    var headingsList = articlesList[i].getElementsByTagName('h2');
    if (headingsList.length > 0) {
      console.log(headingsList[0].innerHTML);
    }
  }
}
```

## DOM Level 3

DOM Level 2 most notably improved the Event model, and DOM Level 3 added further support for more events, among other things. I've purposefully avoided mentioning events here, We'll look at events in the next chapter.

Level 3 became rapidly supported in Firefox and Apple's Safari (i.e. Webkit, which went on to be used in Google Chrome), and was eventually supported in IE 9.

## DOM Level 4 - HTML 5

When WHAT-WG started working on would what eventually become HTML 5, many non-standards things (such as `innerHTML`) became part of the standard for the first time. HTML 5 also codified improvements to the DOM, including these methods to find elements with the CSS selector syntax:

### `document.querySelector( cssSelectorString )`
### `element.querySelector( cssSelectorString )`

With `querySelector` we can get one element. If no matching element is found, `null` is returned.

### `document.querySelectorAll( cssSelectorString )`
### `element.querySelectorAll( cssSelectorString )`

With `querySelectorAll` we get an NodeList of elements. This is not an HTMLCollection, so it is not a live collection. If no elements are found, the collection will have a length of zero.

```js
var articlesList = document.querySelectorAll("main article"); // all the articles in the main element
for(var i = 0; i < articlesList.length; i += 1) {
  var article = articlesList[i];
  var author = article.querySelector('.meta .author').innerHTML;
}
```

These two methods work in all modern browsers, and in Internet Explorer since version 10. They work very efficiently, and as a whole work faster and better than the DOM Level 1 methods.

You can get quite expressive with CSS Selectors and these two methods.

### `element.classList[]`

HTML 5 also formalised the `classList` collection. Each item in this array-like object represents each individual class applied to that element. The object also has methods:

* `element.classList.contains( string )` -- returns true if this element has that class on it
* `element.classList.toggle( string )` -- adds the class if not already present, removes the class if already present.
