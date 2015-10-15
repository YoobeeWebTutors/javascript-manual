---
title: 15 – Objects
layout: page
---

Objects are collections of properties, with each property storing a value. If arrays are ordered lists, objects are more like dictionaries, only you can't sort an object.

Everything in JavaScript is actually an object. Strings have properties such as `length`, `charAt`, and `split`. Numbers have properties like `toFixed`, and even Booleans have `toString`.

Some of these properties contain simple values: strings, numbers and Booleans. When a property contains a function, we call that property a **method**. Many of the examples above are methods. The `console` object has many methods on it, the most commonly used one is `log`.

Objects that share a common set of properties and methods are said to be of the same class. Strings are all of the String class, Numbers are all of the Number class, and so on.

## Creating Objects

We can create custom objects:

```js
var car = {};
```

This is an empty object. It is actually of the Object class, which does have the odd method or two, but for all intents and purposes, we consider this empty.

We can fill the car with properties like so:

```js
var car = {
  make:       "Morris",
  model:      "1100",
  year:       1966,
  paintColor: "blue",
  odometer:   207293.1, // km
  fuel:       30,       // l
  maxFuel:    38.6,     // l
  kmPerLitre: 13.9      // kpl
}
```

Some of these properties are likely to be permanent: cars don't change their make, model, year, and maxFuel. Some will change rarely, like their colour. Some will change frequently, like the amount of fuel in the tank, and the odometer.

The name of a property is sometimes called a **key**.

## Accessing Properties

We use the `.` Member operator to access properties of objects.

```js
console.log(car.make + " " + car.model);
car.paintColor = "red";
car.odometer += 15;
car.fuel -= 1.07;
```

Sometimes, we want to access properties programmatically. We can pass a variable into some square brackets like we would an array:

```js
var thing = 'make';
console.log(car[prop]); // "Morris"
car['paintColor'] = "green"; // <-- this would be better written as car.paintColor
```

## JavaScript Object Notation (JSON)

Objects that are described in the curly brace notation can sometimes be valid JSON, a popular way to share data records between servers and browsers. JSON has some stricter rules than JavaScript, and works with not just JS, but every popular programming language.

<!-- talk more about JSON -->

## Creating Methods

When we put a function into a property, we call that function a method. Methods can use the `this` keyword to refer to the object they are a part of:

```js
car.drive = function (distanceKm) {
  var fuelConsumption = distanceKm / this.kmPerLitre;
  if (fuelConsumption > this.fuel) {
    return false;
  }
  this.fuel -= fuelConsumption;
  this.odometer += distanceKm;
  return this.odometer;
}

car.fuel = car.maxFuel;
console.log(car.odometer);  // 207308.1
console.log(car.drive(20)); // 207328.1
console.log(car.fuel);      // 37.161151079136694

```

## `prototype` property and `new` keyword

(( coming soon ))
