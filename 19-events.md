---
title: 19 – Events
layout: page
---

Up until now, our code has been running when the page hits the `<script>` element. It runs while the page is loading.

We often don't want our JavaScript code to run until some particular thing happens. For example:

* The page finishes loading.
* A button is clicked.
* A key on the keyboard is pressed.
* The mouse moves into an element.
* Some time passes.

These are all DOM *events*.

We want to know when certain events occur to certain elements, and when they do, we want a part of our code to start running. To do this, we must find the element we're interested in, then register a function as an *event listener*.

## The Old Way

Before DOM Level 2 the only way to add an event was by writing JavaScript directly into elements such as `onclick="linkClick();"` and `onload="pageLoad();"` etc. We could also add them in via an element's event property, such as `el.onClick` or `document.onload`. These worked great for simple things, but in bigger projects things quickly became problematic:

Because only one piece of JavaScript could be in an attribute or property, when multiple scripts wanted to listen for the same event, they could place their own code in the property and inadvertently replace an existing piece of code from another script.

In early browsers, some elements ignored some or all of their event attributes and properties.

## The Current Way

DOM Level 2 set out to solve these issues, and at the same time, make events more useful and controllable.

### `element.addEventListener( event, function )`

Here, the behaviour we want is:

* When the duck picture is clicked:
  * tell the user "Quack!"

```html
<img src="duck.jpg" id="duck">
```
```js
var duckPic = document.querySelector("#duck");
duckPic.addEventListener('click', function () {
  alert("Quack!");
});
```

Here, we use `querySelector` to search the document for the `#duck` element, then using `addEventListener`, add an anonymous function as an event listener to that element, stating we want it to be run when the element is `click`ed.

### Events in IE 8 and below

`addEventListener` was added in DOM Level 2, but was first implemented in Internet Explorer 9. For IE 8 and below, you would have to do something like this:

```js
if (el.addEventListener) {
  el.addEventListener('click', modifyText);
} else if (el.attachEvent)  {
  el.attachEvent('onclick', modifyText);
}
```

## The Main Events

There are many useful events to listen for. Here are the most common and useful and when they fire:

* `DOMContentLoaded` -- fires when the elements inside the element being listened to have all been downloaded and put on the page. This triggers before all the resources are downloaded.
* `click` -- when the element is clicked or activated via the keyboard.
* `focus` -- when the element receives keyboard focus, such as a link or input field.
* `blur` -- when the element loses keyboard focus.
* `change` -- when an input, textarea, or select element value is committed (usually when element loses keyboard focus and its value has changed since it gained focus).
* `submit` -- when the form element is submitted (by a submit button being clicked or otherwise triggering the submit).

Less common but no less useful:

* `load` -- when the element such as an image, or more commonly the entire `document` and its resources has finished downloading.
* `dblclick` -- when the element is double clicked.
* `mouseenter` -- when the mouse is moved into an element.
* `mouseover` -- when the mouse is moved into an element, and retriggers when moving to and from child elements.
* `mousemove` -- when the mouse moves while inside an element.
* `mouseleave` -- when the mouse moves out of an element.
* `mouseout` -- when the mouse moves out of an element, and retriggers when moving to and from child elements.
* `keyup` -- when a key is pressed down.
* `keypress` -- when a key is pressed down and that key normally produces a character value.
* `keydown` -- when a key is released.
* `input` -- when an input or textarea element is changed as each character changes the element's value.

Some events are not available in some older browsers, especially IE 8 and below. Always test your code in old browsers!

## Event Information

Some of the above events provide some extra information. Every event listener function is passed an Event object as the first parameter.

This Event object has several properties and methods that are very useful.

### `Event.type`

You can have one function be triggered by several event listeners. To find out what event occurred, look at the `type` property.

```js
var firstNameField = document.querySelector("#first-name");
firstNameField.addEventListener('focus', firstNameFieldEvent);
firstNameField.addEventListener('blur', firstNameFieldEvent);

function firstNameFieldEvent(evt) {
  console.log("first name field: " + evt.type);
}
```

### `Event.target`

You can have several elements trigger the same function

```js
var firstNameField = document.querySelector("#first-name");
var lastNameField = document.querySelector("#last-name");
firstNameField.addEventListener('focus', nameFieldEvent);
lastNameField.addEventListener('focus', nameFieldEvent);

function nameFieldEvent(evt) {
  console.log(evt.target.id + " received: " + evt.type);
}
```

### Other things
For some events, you can also find out what modifier keys were being held down while the event occurred. You can find out the position of the mouse, what keys were pressed, and many other things. Be sure to look at the JavaScript documentation to learn more.

## Preventing the default action

When certain events are triggered by the user, there are default actions that occur even without JavaScript. Clicking a link will navigate the window to its destination. Clicking a submit button will cause the form to send its data and navigate to the resulting page. These are usually intended, but sometimes you want to prevent them from happening.

To prevent a default action from occurring, we must run the `preventDefault()` method on the event object passed into the event listener function.

```js
var navLinks = document.querySelectorAll("nav a");
for (var i = 0; i < navLinks.length; i += 1) {
  navLinks[i].addEventListener('click', function (evt) {
    evt.preventDefault();
  });
}
```

# Timed events

- setTimeout()
- awareness of setInterval(), it's pitfalls
- awareness of clearTimeout()
