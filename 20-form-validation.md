---
title: 20 – Form Validation
layout: page
---

For this chapter, we'll be building a script to validate a simple contact form. Once we have it validating one form, we will extend the script so we can use it to validate almost any form.

HTML 5 validation is pretty good, but isn't perfect. Some email addresses are valid when they shouldn't be. Customising the style of the error messages is possible but not consistent across browsers. At time of writing Firefox, IE and Safari Mac do not support date fields.

We'll be disabling HTML5 validation and substituting our own.

## Form Validator Requirements

* Allow submission of form to its destination only if all the fields in the form are valid.
* Provide helpful error messages next to each field.
* Validate a field when it loses focus (is blurred).
* Check if a field:
  * is required (cannot be blank, unchecked or unselected).
  * must be a valid email address.
  * must contain a minimum or maximum length of characters.

## Finished Product:

* [Form Validation Demo](form-validation/form.html)
* [Finished JavaScript](form-validation/form-validation.js)

## Simple Form

Let's start with a simple form. For brevity, we'll show only the form fragment.

```html
    <form id="contact-form" method="POST" action="success.html">

      <div class="form-group">
        <label for="firstname">First Name</label>
        <input id="firstname" type="text" name="firstname" required>
        <span id="firstname-error"></span>
      </div>

      <div class="form-group">
        <button type="submit">Submit</button>
      </div>

    </form>
```

A first name field only, but the field is required. The label element is linked to the input field via the id field, making our form more accessible. We also have a span with the field's id followed by `-error`. This span will be where we output any errors related to the field.

### Getting Started

What we want our form validation to do right now is:

```js
// when the page loads:
	// find the form
	// disable HTML5 validation
	// When the form is submitted:
		// check every field in this form is filled
			// if a field is blank:
				// give the field an error class
				// give the error span a class and the error message.
		// if any field is found with an error:
			// prevent the form from submitting.
```

We'll make `form-validation.js` and add it to our form with a `<script>` element, just before the `</body>` tag.

```js
// when the page loads:
document.addEventListener('DOMContentLoaded', function() {

	// find the form
	var theForm = document.querySelector('#contact-form');
	// disable HTML5 validation
	theForm.noValidate = true;

	// When the form is submitted:
		// check every field in this form is filled
			// if a field  is blank:
				// give the field an error class
				// give the error span a class and the error message.
		// if any field is found with an error:
			// prevent the form from submitting.		
});
```

By setting the `noValidate` property to true, we prevent the browser from using HTML5 style validation on this form. We could also put the `novalidate` attribute directly on the form element, but this could be omitted. We'll leave nothing to chance.

### Form Submissions

Forms can be submitted in more than one way: clicking the submit button, or pressing 'return' in a field. Either of these would trigger their own click or keypress event, but once those are resolved, it further triggers the submit event on their parent &lt;form&gt; element. Listening for this event is the most reliable method we have here.

```js
document.addEventListener('DOMContentLoaded', function() {
	var theForm = document.querySelector('#contact-form');
	theForm.noValidate = true;

	// When the form is submitted:
	theForm.addEventListener('submit', function(evt) {
		// check every field in this form is filled
			// if a field  is blank:
				// give the field an error class
				// give the error span a class and the error message.
		// if any field is found with an error:
			// prevent the form from submitting.		
	});
});
```

### Preventing Submissions

We will be looking for an error on each field. To keep track of this, we start by assuming there are no errors, and if we find one, we will prevent the form from submitting.

```js
theForm.addEventListener('submit', function(evt) {
	// assume there are no errors
	var isError = false;

	// check every field in this form is filled
		// if a field is blank:
			// give the field an error class
			// give the error span a class and the error message.

	// if any field is found with an error:
	if (isError) {
		// prevent the form from submitting.
		evt.preventDefault();
	}
});

```

### Checking all the Form's fields

Now we need to find each field and check it.

```js
theForm.addEventListener('submit', function(evt) {
	var isError = false;

	// check every field in this form is filled
	var elements = this.elements;
	for (var i = 0; i < elements.length; i += 1) {
		console.log(elements[i]);
		// if a field is blank:
			// give the field an error class
			// give the error span a class and the error message.
	}

	if (isError) {
		evt.preventDefault();
	}
});
```

When submitting, the log shows:
```
input#firstname
button
```

What is 'this' within the submit event listener? It's the `form#contact-form` element. The `elements` property of the form is a collection of all the form elements. Right now, `elements.length` is 2: the `<input>` and the `<button>`.

### Checking the field

Now lets actually check the fields.

```js
theForm.addEventListener('submit', function(evt) {

	var isError = false;
	var elements = this.elements;
	for (var i = 0; i < elements.length; i += 1) {

		// get the field
		var field = elements[i];

		// if a field is blank:
		if (field.value.trim() === "") {
			// we found an error
			isError = true;

			// give the field an error class
			field.classList.add('invalid');

			// give the error span a class and the error message.
			var errorSpan = document.querySelector('#' + field.id + '-error');
			errorSpan.classList.add('danger');
			errorSpan.innerHTML = "This field is required.";
		}
	}

	if (isError) {
		evt.preventDefault();
	}
});
```

Here, we check the field's value property. If, after trimming it of leading and trailing spaces, it matches an empty string, the field is invalid. We set `isError` to true, and add the invalid class to the field.

We also find the error span for the element, set its class and output the error.

*Note*: The `classList` object works in everything except IE9, at time of writing. There are polyfills to make it work there.

### Refactor: Extract Function

The submit event listener is getting quite long. Let's refactor it: we'll extract the field checking code into its own function. We want a function to tell us if a field is valid or not.

```js
	theForm.addEventListener('submit', function(evt) {
		var isError = false;

		var elements = this.elements;
		for (var i = 0; i < elements.length; i += 1) {
			if (! isFieldValid(elements[i])) {
				isError = true;
			}
		}

		if (isError) {
			evt.preventDefault();
		}
	});

	function isFieldValid(field) {
		if (field.value.trim() === "") {
			field.classList.add('invalid');

			var errorSpan = document.querySelector('#' + field.id + '-error');
			errorSpan.classList.add('danger');
			errorSpan.innerHTML = "This field is required.";

			// we found an error
			return false;
		}
		return true;
	}
```

### Fields that are always valid

If we use the debugger, we'll discover our code works for our first name field, but it won't work for the button, as the button doesn't have an ID or an error span.

A button element is always valid. There are several elements that we can assume are always valid, `submit`, `reset`, `button`, `hidden`, `fieldset`

Let's write a function to check if the field needs to be checked:

```js
function isFieldValid(field) {
	// skip fields that are are always considered valid.
	if (! needsToBeValidated(field)) {
		return true;
	}
	if (field.value.trim() === "") {

		field.classList.add('invalid');

		var errorSpan = document.querySelector('#' + field.id + '-error');
		errorSpan.classList.add('danger');
		errorSpan.innerHTML = "This field is required.";

		return false;
	}
	return true;
}

function needsToBeValidated(field) {
	return ['submit', 'reset', 'button', 'hidden', 'fieldset'].indexOf(field.type) === -1;
}
```

Before we check for the error, we pass the field through to `needsToBeValidated`. This function will return true if the field needs to be validated. The way it does this is checks an array of all the automatically valid types to see if it contains the field's type. If the field has type 'text', `indexOf` returns -1, and `-1 === -1` is true, so returns true.

If the field does not need to be validated, we return true as this field is as valid as it will get.

### Only `required` Fields

Right now, every field is being treated as required. We only want to check fields that have the `required` attribute. Let's add that in.

```js
function isFieldValid(field) {
	if (! needsToBeValidated(field)) {
		return true;
	}
	if (field.required && field.value.trim() === "") {

		// give the field an error class
		field.classList.add('invalid');

		// give the error span a class and the error message.
		var errorSpan = document.querySelector('#' + field.id + '-error');
		errorSpan.classList.add('danger');
		errorSpan.innerHTML = "This field is required.";

		// we found an error
		return false;
	}
	return true;
}
```


### Add another field.

At this point, the script works if we try submit the blank form, and if we correct the form, the form will submit.

Let's add the last name field.

```html
<form id="contact-form" method="POST" action="success.html">
  <div class="form-group">
    <label for="firstname">First Name</label>
    <input id="firstname" type="text" name="firstname" required>
    <span id="firstname-error"></span>
  </div>

  <div class="form-group">
    <label for="lastname">Last Name</label>
    <input id="lastname" type="text" name="lastname" required>
    <span id="lastname-error"></span>
  </div>

  <div class="form-group">
    <button type="submit">Submit</button>
  </div>
</form>
```

Now if validate this form with both fields blank, both fields will get errors. If we then fix both, the form will submit successfully. However, if we only fix one of the fields, that field's error messages don't go away. We need to reset the error message and classes before we validate the form again.

```js
function isFieldValid(field) {
	if (! needsToBeValidated(field)) {
		return true;
	}
	// remove the invalid class of the field
	field.classList.remove('invalid');
	// find the error span, clear it
	var errorSpan = document.querySelector('#' + field.id + '-error');
	errorSpan.classList.remove('danger');
	errorSpan.innerHTML = "";

	if (field.required && field.value.trim() === "") {

		// give the field an error class
		field.classList.add('invalid');

		// give the error span a class and the error message.
		errorSpan.classList.add('danger');
		errorSpan.innerHTML = "This field is required.";

		// we found an error
		return false;
	}
	return true;
}
```

### Make it Portable

We'd like this script to be portable: it should work for any form we point at it. Let's turn our code into a function that we can point at any form.

Let's move the `DOMContentLoaded` event listener into the HTML, where we will find the form element we want to validate, and pass that element into a function. That function will set that element up for form validation.

```html
  <script src="form-validation.js"></script>
  <script>
    document.addEventListener('DOMContentLoaded', function() {
		addFormValidation(document.querySelector('#contact-form'))
    });
  </script>
```

```js
function addFormValidation(theForm) {

	theForm.noValidate = true;

	theForm.addEventListener('submit', function(evt) {
		var isError = false;

		var elements = this.elements;
		for (var i = 0; i < elements.length; i += 1) {
			if (! isFieldValid(elements[i])) {
				isError = true;
			}
		}

		if (isError) {
			evt.preventDefault();
		}
	});

	function isFieldValid(field) {
		if (! needsToBeValidated(field)) {
			return true;
		}
		field.classList.remove('invalid');

		var errorSpan = document.querySelector('#' + field.id + '-error');
		errorSpan.classList.remove('danger');
		errorSpan.innerHTML = "";

		if (field.required && field.value.trim() === "") {
			field.classList.add('invalid');

			errorSpan.classList.add('danger');
			errorSpan.innerHTML = "This field is required.";

			return false;
		}
		return true;
	}

	function needsToBeValidated(field) {
		return ['submit', 'reset', 'button', 'hidden', 'fieldset'].indexOf(field.type) === -1;
	}
}
```

### Preventing Developer Screw-ups

But humans are forgetful creatures. How can we protect our developers from using the script wrong? What assumptions do we make?

We assume they will pass a `<form>` element into `addFormValidation`. What if they don't? Our script won't function. We can communicate that to our developer by throwing an exception.

```js
function addFormValidation(theForm) {
	if (formElement === null || formElement.tagName.toUpperCase() !== 'FORM') {
		throw new Error("expected first parameter to addFormValidation to be a FORM.");
	}
	// addFormValidation continues, including everything else in the file…
}
```

This way, if `addFormValidation` is passed an element that it can't use, it will die loudly on the console:

> Uncaught Error: expected first parameter to addFormValidation to be a FORM.   
>   addFormValidation @ form-validation.js:4   
>   (anonymous function) @ form.html:37

We also assume they've given fields `id` attributes, and made matching error spans. If they haven't done these, when we try to find it, `errorSpan` will be set to null, and on the next line we'll get the error:

> Uncaught TypeError: Cannot read property 'classList' of null

To solve this, when `isFieldValid` is passed, we'll add some more exceptions:

```js
function isFieldValid(field) {
	if (! needsToBeValidated(field)) {
		return true;
	}

	if (field.id.length === 0 || field.name.length === 0) {
		console.error("error: ", field);
		throw new Error("found a field that is missing an id and/or name attribute. name should be there. id is required for determining the field's error message element.");
	}

	field.classList.remove('invalid');

	var errorSpan = document.querySelector('#' + field.id + '-error');

	if (errorSpan === null) {
		console.error("error: ", field);
		throw new Error("could not find the '#" + field.id + "-error' element. It's needed for error messages if #" + field.id + " is ever invalid.");
	}

	errorSpan.classList.remove('danger');
	errorSpan.innerHTML = "";

	// isFieldValid continues…
}
```

### Email Field

Let's add an Email field:

```html
  <div class="form-group">
    <label for="email">Email Address</label>
    <input id="email" type="email" name="email" required>
    <span id="email-error"></span>
  </div>
```

To validate an Email field better than HTML5 does, we'll need a way to test for a valid email address. Put this below `needsToBeValidated`, making sure it's still inside addFormValidation:

```
function isEmail(input) {
	return input.match(/^([a-z0-9_.\-+]+)@([\da-z.\-]+)\.([a-z\.]{2,})$/);
}
```

Let's add the following above the required test in `isFieldValid`:

```js
if (field.type === "email" && !isEmail(field.value)) {
	field.classList.add('invalid');

	errorSpan.classList.add('danger');
	errorSpan.innerHTML = "This field is required.";

	return false;
}

if (field.required && field.value.trim() === "") {
	field.classList.add('invalid');

	errorSpan.classList.add('danger');
	errorSpan.innerHTML = "This field is required.";

	return false;
}
```

### Refactor: Reduce Duplication of Code (make it DRY)

This is working, but we have some duplication between the email and required checks. We should reduce that duplication to make our code more DRY.

```js
	function isFieldValid(field) {
		var errorMessage = "";

		if (! needsToBeValidated(field)) {
			return true;
		}

		if (field.id.length === 0 || field.name.length === 0) {
			console.error("error: ", field);
			throw new Error("found a field that is missing an id and/or name attribute. name should be there. id is required for determining the field's error message element.");
		}

		field.classList.remove('invalid');

		var errorSpan = document.querySelector('#' + field.id + '-error');

		if (errorSpan === null) {
			console.error("error: ", field);
			throw new Error("could not find the '#" + field.id + "-error' element. It's needed for error messages if #" + field.id + " is ever invalid.");
		}

		errorSpan.classList.remove('danger');
		errorSpan.innerHTML = "";

		if (field.type === "email" && !isEmail(field.value)) {
			errorMessage = "This should be a valid email address.";
		}

		if (field.required && field.value.trim() === "") {
			errorMessage = "This field is required.";
		}

		if (errorMessage !== "") {
			field.classList.add('invalid');

			errorSpan.classList.add('danger');
			errorSpan.innerHTML = errorMessage;
			return false;
		}

		return true;
	}
```

Here we add an `errorMessage` variable at the top to store our error message. Our email and required checks now just set that variable to the error. At the end, if that variable isn't a blank string, we put that error message in the error span, and add the error classes.


### Minimum Length

Let's say that our name fields are still required, but now must be two or more characters long.

```html
    <form id="contact-form" method="POST" action="success.html">

      <div class="form-group">
        <label for="firstname">First Name</label>
        <input id="firstname" type="text" name="firstname" required minlength="2">
        <span id="firstname-error"></span>
      </div>

      <div class="form-group">
        <label for="lastname">Last Name</label>
        <input id="lastname" type="text" name="lastname" required minlength="2">
        <span id="lastname-error"></span>
      </div>

      <div class="form-group">
        <label for="email">Email Address</label>
        <input id="email" type="email" name="email" required>
        <span id="email-error"></span>
      </div>

      <div class="form-group">
        <button type="submit">Submit</button>
      </div>

    </form>
```

The shortest names (in English) are two characters minimum. This also prevents people just filling the name field with one character.

So let's add another check. We'll put this above the email check:

```js
if (field.minLength > 0 && field.value.length < field.minLength) {
	errorMessage = "Must be " + field.minLength + " or more characters long.";
}
```

It's that simple! To add support for `maxlength`, we do something similar:

```js
if (field.maxLength > -1 && field.value.length > field.maxLength) {
	errorMessage = "Must be " + field.maxLength + " characters or less.";
}
```

That should do it for our form. Here's some stuff we get for free:

If `required` is on a checkbox, it will be invalid if it is not checked.
If `required` is on a `select` box, it will be invalid if set to an option with `value=""`.

If you need to validate a radio box, make one of them checked by default.

## Exercises

* Add support for min and max numeric values
* Add support for a 'confirm password' field -- it will only be valid if its value matches another field's value. To pull this off, research data attributes.
