# this and Prototypes

## Table of contents
* [this](#this)
* [Prototypes](#prototypes)

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

## Resources:
* https://www.w3schools.com
* You don't know JS from Kyle Simpson
