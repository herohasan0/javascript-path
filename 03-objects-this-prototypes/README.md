# Objects, this and Prototypes

## Table of contents
* [Objects](#objects)
  - [Display Objects](#display-objects)
  - [Getters and Setters](#getters-and-setters)
* [this](#this)
* [Prototypes](#prototypes)
* [Resources](#resources)

## Objects

In JavaScript, almost "everything" is an object.
* Booleans can be objects (if defined with the `new` keyword)
* Numbers can be objects (if defined with the `new` keyword)
* Strings can be objects (if defined with the `new` keyword)
* Dates are always objects
* Maths are always objects
* Regular expressions are always objects
* Arrays are always objects
* Functions are always objects
* Objects are always objects

All JavaScript values, except primitives, are objects. A primitive value is a value that has no properties or methods. A primitive data type is data that has a primitive value.

JavaScript defines 5 types of primitive data types:
* string
* number
* boolean
* null
* undefined

Primitive values are immutable (they are hardcoded and therefore cannot be changed).

A JavaScript object is a collection of named values

```js
const person = {firstName:"John", lastName:"Doe", age:50, eyeColor:"blue"};
```

There are different ways to create new objects:
* Create a single object, using an object literal.
* Create a single object, with the keyword `new`.
* Define an object constructor, and then create objects of the constructed type.
* Create an object using `Object.create()`.

Using an object literal:

```js
const person = {
  firstName: "John",
  lastName: "Doe",
  age: 50,
  eyeColor: "blue"
};
```

Or

```js
const person = {};
person.firstName = "John";
person.lastName = "Doe";
person.age = 50;
person.eyeColor = "blue";
```

With the keyword `new`:

```js
const person = new Object();
person.firstName = "John";
person.lastName = "Doe";
person.age = 50;
person.eyeColor = "blue";
```

The examples above do exactly the same. But there is no need to use `new Object()`. For readability, simplicity and execution speed, <ins>use the object literal method.</ins>

Objects are mutable: They are addressed by reference, not by value. If person is an object, the following statement will not create a copy of person:

```js
const x = person;  // Will not create a copy of person.
```

The object x is not a copy of person. It is person. Both x and person are the same object. Any changes to x will also change person, because x and person are the same object.

```js
const person = {
  firstName:"John",
  lastName:"Doe",
  age:50, eyeColor:"blue"
}

const x = person;
x.age = 10;      // Will change both x.age and person.age
```

### Display Objects

Displaying a JavaScript object will output `[object Object]`.

```js
const person = {
  name: "John",
  age: 30,
  city: "New York"
};

document.getElementById("demo").innerHTML = person;
```
Some common solutions to display JavaScript objects are:

* Displaying the Object Properties by name
* Displaying the Object Properties in a Loop
* Displaying the Object using Object.values()
* Displaying the Object using JSON.stringify()

Displaying object property

```js
const person = {
  name: "John",
  age: 30,
  city: "New York"
};

document.getElementById("demo").innerHTML =
person.name + "," + person.age + "," + person.city;
```

Object properties in a loop

```js
const person = {
  name: "John",
  age: 30,
  city: "New York"
};

let txt = "";
for (let x in person) {
txt += person[x] + " ";
};

document.getElementById("demo").innerHTML = txt;
```

You must use `person[x]` in the loop.

`person.x` will not work (Because `x` is a variable).

Using `object.values()`

Any JavaScript object can be converted to an array using `Object.values()`:

```js
const person = {
  name: "John",
  age: 30,
  city: "New York"
};

const myArray = Object.values(person);

//myArray is now a JavaScript array, ready to be displayed:
document.getElementById("demo").innerHTML = myArray;
```

Using `JSON.stringify()`

Any JavaScript object can be stringified (converted to a `string`) with the JavaScript function `JSON.stringify()`:

```js
const person = {
  name: "John",
  age: 30,
  city: "New York"
};

let myString = JSON.stringify(person);

//myString is now a JavaScript string, ready to be displayed:
document.getElementById("demo").innerHTML = myString;
```

### Getters and Setters

ECMAScript 5 (ES5 2009) introduced Getter and Setters. Getters and setters allow you to define Object Accessors (Computed Properties).

Why Using Getters and Setters?

- It gives simpler syntax
- It allows equal syntax for properties and methods
- It can secure better data quality
- It is useful for doing things behind-the-scenes

The `get` keyword

This example uses a lang property to get the value of the language property.

```js
// Create an object:
const person = {
  firstName: "John",
  lastName: "Doe",
  language: "en",
  get lang() {
    return this.language;
  }
};

// Display data from the object using a getter:
document.getElementById("demo").innerHTML = person.lang;
```

The `set` keyword

```js
const person = {
  firstName: "John",
  lastName: "Doe",
  language: "",
  set lang(lang) {
    this.language = lang;
  }
};

// Set an object property using a setter:
person.lang = "en";

// Display data from the object:
document.getElementById("demo").innerHTML = person.language;
```

Another method, Object.defineProperty()

```js
// Define object
const obj = {counter : 0};

// Define setters
Object.defineProperty(obj, "reset", {
  get : function () {this.counter = 0;}
});
Object.defineProperty(obj, "increment", {
  get : function () {this.counter++;}
});
Object.defineProperty(obj, "decrement", {
  get : function () {this.counter--;}
});
Object.defineProperty(obj, "add", {
  set : function (value) {this.counter += value;}
});
Object.defineProperty(obj, "subtract", {
  set : function (value) {this.counter -= value;}
});

// Play with the counter:
obj.reset;
obj.add = 5;
obj.subtract = 1;
obj.increment;
obj.decrement;
```

## this

```js
const person = {
  firstName: "John",
  lastName : "Doe",
  id       : 5566,
  fullName : function() {
    return this.firstName + " " + this.lastName;
  }
};
```
The JavaScript `this` keyword refers to the `object` it belongs to.
It has different values depending on where it is used:
1. In a method, `this` refers to the owner object.
2. Alone, `this` refers to the global object.
3. In a function, `this` refers to the global object.
4. In a function, in strict mode, `this` is undefined.
5. In an event, `this` refers to the element that received the event.
6. Methods like call(), and apply() can refer `this` to any object.

Read more from w3schools [here](https://www.w3schools.com/js/js_this.asp).

While it may often seem that `this` is related to "object-oriented patterns," in JS `this` is a different mechanism. If a function has a `this` reference inside it, that `this` reference usually points to an `object`. But which `object` it points to depends on how the function was called.

It's important to realize that `this` does not refer to the function itself, as is the most common misconception.

```js
function foo() {
	console.log( this.bar );
}

var bar = "global";

var obj1 = {
	bar: "obj1",
	foo: foo
};

var obj2 = {
	bar: "obj2"
};

// --------

foo();				// "global"
obj1.foo();			// "obj1"
foo.call( obj2 );		// "obj2"
new foo();			// undefined
```
There are four rules for how `this` gets set, and they're shown in those last four lines of that snippet.
1. `foo()` ends up setting `this` to the global object in non-strict mode -- in strict mode, `this` would be `undefined` and you'd get an error in accessing the bar property -- so "`global`" is the value found for `this.bar`.
2. `obj1.foo()` sets `this` to the `obj1` object.
3. `foo.call(obj2)` sets `this` to the `obj2` object.
4. `new foo()` sets `this` to a brand new empty object.

## Prototypes

When you reference a property on an object, if that property doesn't exist, JavaScript will automatically use that object's internal prototype reference to find another object to look for the property on. You could think of this almost as a fallback if the property is missing. 
The internal prototype reference linkage from one object to its fallback happens at the time the object is created. The simplest way to illustrate it is with a built-in utility called `Object.create(..)`.

```js
var foo = {
	a: 42
};

// create `bar` and link it to `foo`
var bar = Object.create( foo );

bar.b = "hello world";

bar.b;		// "hello world"
bar.a;		// 42 <-- delegated to `foo`
```
It may help to visualize the `foo` and `bar` objects and their relationship:

<img src="https://github.com/jumaschion/You-Dont-Know-JS-1/blob/master/up%20&%20going/fig6.png?raw=true">

The `a` property doesn't actually exist on the `bar` object, but because `bar` is prototype-linked to `foo`, JavaScript automatically falls back to looking for `a` on the `foo` object, where it's found.

This linkage may seem like a strange feature of the language. The most common way this feature is used -- and I would argue, abused -- is to try to emulate/fake a "class" mechanism with "inheritance."

But a more natural way of applying prototypes is a pattern called "behavior delegation," where you intentionally design your linked objects to be able to *delegate* from one to the other for parts of the needed behavior.

----

All JavaScript objects inherit properties and methods from a prototype.

```js
function Person(first, last, age, eyecolor) {
  this.firstName = first;
  this.lastName = last;
  this.age = age;
  this.eyeColor = eyecolor;
}

const myFather = new Person("John", "Doe", 50, "blue");
const myMother = new Person("Sally", "Rally", 48, "green");
```

We also learned that you can not add a new property to an existing object constructor:
```js
Person.nationality = "English";
```

To add a new property to a constructor, you must add it to the constructor function:
```js
function Person(first, last, age, eyecolor) {
  this.firstName = first;
  this.lastName = last;
  this.age = age;
  this.eyeColor = eyecolor;
  this.nationality = "English";
}
```

All JavaScript objects inherit properties and methods from a prototype:
* `Date` objects inherit from `Date.prototype`
* `Array` objects inherit from `Array.prototype`
* `Person` objects inherit from `Person.prototype`

The `Object.prototype` is on the top of the prototype inheritance chain:

`Date` objects, `Array` objects, and `Person` objects inherit from `Object.prototype`.

The JavaScript `prototype` property allows you to add new properties to object constructors:

```js
function Person(first, last, age, eyecolor) {
  this.firstName = first;
  this.lastName = last;
  this.age = age;
  this.eyeColor = eyecolor;
}

Person.prototype.nationality = "English";
```

The JavaScript `prototype` property also allows you to add new methods to objects constructors:

```js
function Person(first, last, age, eyecolor) {
  this.firstName = first;
  this.lastName = last;
  this.age = age;
  this.eyeColor = eyecolor;
}

Person.prototype.name = function() {
  return this.firstName + " " + this.lastName;
};
```

## Resources:
* https://www.w3schools.com
* You don't know JS from Kyle Simpson