# Values Types and Values

## Table of contents
* [Values and Types](#values-and-types)
    1. [Values and Reference Types](#values-and-reference-types)
    2. [Comparing Values](#comparing-values)
        - [Coercion](#coercion)
        - [Truthy and Falsy](#truthy-and-falsy)
        - [Difference between null and undefined](#difference-between-null-and-undefined)
        - [Equality](#equality)
        - [Inequality](#inequality)
* [Scope](#scope)
  1. [Compiler Theory](#compiler-theory)
* [Variables](#variables)
    1. [Scoping Levels](#scoping-levels)
        - [Function Scopes](#function-scopes)
        - [Hoisting](#hoisting)
        - [Nested Scopes](#nested-scopes)
    2. [Difference between var and let](#difference-between-var-and-let)
        - [Hoisting Variable](#hoisting-variable)
        - [Creating global object property](#creating-global-object-property)
        - [Redeclaration](#redeclaration)
* [Resources](#resources)


## Values and Types

JavaScript the dynamic typing, meaning variables can hold values of any type without any type enforcement. JavaScript has typed values, not typed variables. The following built-in types are available:

- `string`
- `number`
- `boolean`
- `null`
- `undefined` 
- `object`
- `symbol` (new to ES6)

The primitive types are: string, number, and boolean, with these special types: null, and undefined. Composite types include object, array, and function (which are all object types).

You can use `typeof` operator that can examine a value and tell you what type it is:

```js
var a;
typeof a;				// "undefined"

a = "hello world";
typeof a;				// "string"

a = 42;
typeof a;				// "number"

a = true;
typeof a;				// "boolean"

a = null;
typeof a;				// "object" -- weird, bug

a = undefined;
typeof a;				// "undefined"

a = { b: "c" };
typeof a;				// "object"

function a() {}
typeof a;               //function

a = () => {}
typeof a;               //function
```

`typeof` a is not asking for the "type of `a`", but rather for the "type of the value currently in `a`." Only values have types in JavaScript; variables are just simple containers for those values.

`typeof null` is an interesting case, because it errantly returns `object`, when you'd expect it to return `null`.

This is a long-standing bug in JS, but one that is likely never going to be fixed. Too much code on the Web relies on the bug and thus fixing it would cause a lot more bugs!

Also, note `a = undefined`. We're explicitly setting a to the undefined value, but that is behaviorally no different from a variable that has no value set yet, like with the `var a`; line at the top of the snippet. A variable can get to this "undefined" value state in several different ways, including functions that return no values and usage of the void operator.

### Values and Reference Types

From a memory perspective, variables come in two different types: value types and reference types. Boolean values and numbers are value-based types, whereas strings, objects, arrays, and functions are reference types. 

Value types occupy a fixed size in memory. A boolean value for example only takes one bit. All numbers in JavaScript are 64-bit floating point numbers, so each number is represented by 8 bytes. A reference type variable holds a reference to the value whose length is not fixed and can be of any size.

Another difference between value and reference types is that value types are compared by value. Reference types, are compared by reference, rather than by value. Let's look at value types first:

```js
var x = 1;
var y = x;

console.log(x == y);    // => true
console.log(x === y);   // => true

x = 6;

console.log(x);         // => 6  
console.log(y);         // => 1

console.log(x == y);    // => false
console.log(x === y);   // => false
```

When variable `y` is assigned to `x` it copies its value and following the assignment any relationship between `x` and `y` is severed. So, changing the value of `x` has no impact on the value of `y`.

Consider this example where a reference type is copied:

```js
var x = { make: "Toyota" };
var y = x;

console.log(x == y);      // => true
console.log(x === y);     // => true

x.make = "Ford";

console.log(x.make);      // => Ford
console.log(y.make);      // => Ford
console.log(x == y);      // => true
console.log(x === y);     // => true
```

Following the execution of the second statement in which `x` is assigned to `y`, `y` refers to the same object that `x` refers to. JavaScript does not create a new copy of that object. If you make any changes to the underlying object through `x`, you can see these changes through `y` and vice-versa.

### Comparing Values

There are two main types of value comparison that you will need to make in your JS programs: equality and inequality. The result of any comparison is a strictly boolean value (true or false), regardless of what value types are compared.

#### Coercion

Coercion comes in two forms in JavaScript: explicit and implicit. Explicit coercion is simply that you can see obviously from the code that a conversion from one type to another will occur, whereas implicit coercion is when the type conversion can happen as more of a non-obvious side effect of some other operation.

An example of explicit coercion:

```js
var a = "42";

var b = Number( a );

a;				// "42"
b;				// 42 -- the number!
```

An example of implicit coercion:

```js
var a = "42";

var b = a * 1;	// "42" implicitly coerced to 42 here

a;				// "42"
b;				// 42 -- the number!
```

#### Truthy and Falsy

"falsy" values in JavaScript:
- "" (empty string)
- 0, -0, NaN (invalid number)
- null, undefined
- false

Any value that's not on this "falsy" list is "truthy."
- "hello"
- 42
- true
- [ ], [ 1, "2", 3 ] (arrays)
- { }, { a: 42 } (objects)
- function foo() { .. } (functions)

#### Difference between null and undefined

In JavaScript, `undefined` means a variable has been declared but has not yet been assigned a value, such as:

```js
var testVar;
alert(testVar); //shows undefined
alert(typeof testVar); //shows undefined
```

`null` is an assignment value. It can be assigned to a variable as a representation of no value:

```js
var testVar = null;
alert(testVar); //shows null
alert(typeof testVar); //shows object
```

#### Equality

There are four equality operators: `==`, `===`, `!=`, and `!==`. The ! forms are of course the symmetric "not equal" versions of their counterparts; non-equality should not be confused with inequality.

The difference between `==` and `===` is usually characterized that `==` checks for value equality and `===` checks for both value and type equality. However, this is inaccurate. The proper way to characterize them is that `==` checks for value equality with coercion allowed, and `===` checks for value equality without allowing coercion; `===` is often called "strict equality" for this reason.

Consider the implicit coercion that's allowed by the `==` loose-equality comparison and not allowed with the `===` strict-equality:

```js
var a = "42";
var b = 42;

a == b;			// true
a === b;		// false
```

In the `a == b` comparison, JS notices that the types do not match, so it goes through an ordered series of steps to coerce one or both values to a different type until the types match, where then a simple value equality can be checked.

If you think about it, there's two possible ways `a == b` could give true via coercion. Either the comparison could end up as `42 == 42` or it could be `"42" == "42"`. So which is it?

The answer: `"42"` becomes `42`, to make the comparison `42 == 42`.

You should take special note of the `==` and `===` comparison rules if you're comparing two non-primitive values, like objects (including function and array). Because those values are actually held by reference, both `==` and `===` comparisons will simply check whether the references match, not anything about the underlying values.

#### Inequality

The `<`, `>`, `<=`, and `>=` operators are used for inequality, referred to in the specification as "relational comparison." Typically they will be used with ordinally comparable values like numbers. It's easy to understand that `3 < 4`.

But JavaScript `string` values can also be compared for inequality, using typical alphabetic rules (`"bar" < "foo"`).

What about coercion? Similar rules as `==` comparison (though not exactly identical!) apply to the inequality operators. Notably, there are no "strict inequality" operators that would disallow coercion the same way `===` "strict equality" does.

```js
var a = 41;
var b = "42";
var c = "43";

a < b;		// true
b < c;		// true
```

What happens here? In section 11.8.5 of the ES5 specification, it says that if both values in the `<` comparison are strings, as it is with `b < c`, the comparison is made lexicographically (aka alphabetically like a dictionary). But if one or both is not a string, as it is with `a < b`, then both values are coerced to be numbers, and a typical numeric comparison occurs.

## Scope

One of the most fundamental paradigms of nearly all programming languages is the ability to store values in variables, and later retrieve or modify those values. In fact, the ability to store values and pull values out of variables is what gives a program state.

Without such a concept, a program could perform some tasks, but they would be extremely limited and not terribly interesting.

But the inclusion of variables into our program begets the most interesting questions we will now address: <ins>where do those variables live?</ins> In other words, <ins>where are they stored?</ins> And, most importantly, <ins>how does our program find them when it needs them?</ins>

These questions speak to the need for a well-defined set of rules for storing variables in some location, and for finding those variables at a later time. We'll call that set of rules: Scope.

But, where and how do these Scope rules get set?

### Compiler Theory

In a traditional compiled-language process, a chunk of source code, your program, will undergo typically three steps before it is executed, roughly called "compilation":

1. **Tokenizing/Lexing:** breaking up a string of characters into meaningful (to the language) chunks, called tokens. For instance, consider the program: `var a = 2;`. This program would likely be broken up into the following tokens: `var`, `a`, `=`, `2`, and `;`. Whitespace may or may not be persisted as a token, depending on whether it's meaningful or not.

2. **Parsing:** taking a stream (array) of tokens and turning it into a tree of nested elements, which collectively represent the grammatical structure of the program. This tree is called an "AST" (<b>A</b>bstract <b>S</b>yntax <b>T</b>ree).

    The tree for `var a = 2;` might start with a top-level node called `VariableDeclaration`, with a child node called `Identifier` (whose value is `a`), and another child called `AssignmentExpression` which itself has a child called `NumericLiteral` (whose value is `2`).

3. **Code-Generation:** the process of taking an AST and turning it into executable code. This part varies greatly depending on the language, the platform it's targeting, etc.

    So, rather than get mired in details, we'll just handwave and say that there's a way to take our above described AST for `var a = 2;` and turn it into a set of machine instructions to actually *create* a variable called `a` (including reserving memory, etc.), and then store a value into `a`.

The JavaScript engine is vastly more complex than just those three steps, as are most other language compilers. For instance, in the process of parsing and code-generation, there are certainly steps to optimize the performance of the execution, including collapsing redundant elements, etc.

For one thing, JavaScript engines don't get the luxury (like other language compilers) of having plenty of time to optimize, because JavaScript compilation doesn't happen in a build step ahead of time, as with other languages.

For JavaScript, the compilation that occurs happens, in many cases, mere microseconds (or less!) before the code is executed. To ensure the fastest performance, JS engines use all kinds of tricks (like JITs, which lazy compile and even hot re-compile, etc.) 

Let's just say, for simplicity's sake, that any snippet of JavaScript has to be compiled before (usually right before!) it's executed. So, the JS compiler will take the program `var a = 2;` and compile it first, and then be ready to execute it, usually right away.

For more details click [here](https://github.com/jumaschion/You-Dont-Know-JS-1/blob/master/scope%20%26%20closures/ch1.md#understanding-scope) to read you don't know JS Understanding Scope.

## Variables

There are 3 ways to declare a JavaScript variable:
* Using `var`
* Using `let`
* Using `const`

### Scoping Levels

In JavaScript, all variables that are defined outside functions are globally scoped; this means they are visible and accessible anywhere in the program. Variables that are defined inside a function have function scope, meaning they are only visible and accessible within the function, for the duration of that function.

#### Function Scopes

You use the `var` keyword to declare a variable that will belong to the current function scope, or the global scope if at the top level outside of any function.

##### Hoisting

Wherever a `var` appears inside a scope, that declaration is taken to belong to the entire scope and accessible everywhere throughout. Metaphorically, this behavior is called hoisting, when a `var` declaration is conceptually "moved" to the top of its enclosing scope. 

```js
var a = 2;

foo();					// works because `foo()`
						// declaration is "hoisted"

function foo() {
	a = 3;

	console.log( a );	// 3

	var a;				// declaration is "hoisted"
						// to the top of `foo()`
}

console.log( a );	// 2
```

It's not common or a good idea to rely on variable hoisting to use a variable earlier in its scope than its var declaration appears; it can be quite confusing. 

#### Nested Scopes

When you declare a variable, it is available anywhere in that scope, as well as any lower/inner scopes. For example:

```js
function foo() {
	var a = 1;

	function bar() {
		var b = 2;

		function baz() {
			var c = 3;

			console.log( a, b, c );	// 1 2 3
		}

		baz();
		console.log( a, b );		// 1 2
	}

	bar();
	console.log( a );				// 1
}

foo();
```

If you try to access a variable's value in a scope where it's not available, you'll get a `ReferenceError` thrown. If you try to set a variable that hasn't been declared, you'll either end up creating a variable in the top-level global scope (bad!) or getting an error, depending on "strict mode".

```js
function foo() {
	a = 1;	// `a` not formally declared
}

foo();
a;			// 1 -- oops, auto global variable :(
```

This is a very bad practice. Don't do it! Always formally declare your variables.

In addition to creating declarations for variables at the function level, ES6 lets you declare variables to belong to individual blocks (pairs of `{ .. }`), using the `let` keyword.

```js
function foo() {
	var a = 1;

	if (a >= 1) {
		let b = 2;

		while (b < 5) {
			let c = b * 2;
			b++;

			console.log( a + c );
		}
	}
}

foo();
// 5 7 9
```

Because of using `let` instead of `var`, `b` will belong only to the if statement and thus not to the whole foo() function's scope. Similarly, `c` belongs only to the while loop. Block scoping is very useful for managing your variable scopes in a more fine-grained fashion, which can make your code much easier to maintain over time.

### Difference between var and let

#### Scoping rules

The main difference is scoping rules. Variables declared by `var` keyword are scoped to the immediate function body (hence the function scope) while `let` variables are scoped to the immediate enclosing block denoted by `{ }` (hence the block scope).

```js
function run() {
  var foo = "Foo";
  let bar = "Bar";

  console.log(foo, bar); // Foo Bar

  {
    var moo = "Mooo"
    let baz = "Bazz";
    console.log(moo, baz); // Mooo Bazz
  }

  console.log(moo); // Mooo
  console.log(baz); // ReferenceError
}

run();
```

#### Hoisting Variable

While variables declared with `var` keyword are hoisted (initialized with `undefined` before the code is run) which means they are accessible in their enclosing scope even before they are declared:

```js
function run() {
  console.log(foo); // undefined
  var foo = "Foo";
  console.log(foo); // Foo
}

run();
```

`let` variables are not initialized until their definition is evaluated. Accessing them before the initialization results in a `ReferenceError`. Variable said to be in "temporal dead zone" from the start of the block until the initialization is processed.

```js
function checkHoisting() {
  console.log(foo); // ReferenceError
  let foo = "Foo";
  console.log(foo); // Foo
}

checkHoisting();
```

#### Creating global object property

At the top level, `let`, unlike `var`, does not create a property on the global object:

```js
var foo = "Foo";  // globally scoped
let bar = "Bar"; // not allowed to be globally scoped

console.log(window.foo); // Foo
console.log(window.bar); // undefined
```

#### Redeclaration

In strict mode, `var` will let you re-declare the same variable in the same scope while `let` raises a SyntaxError.

```js
'use strict';
var foo = "foo1";
var foo = "foo2"; // No problem, 'foo1' is replaced with 'foo2'.

let bar = "bar1"; 
let bar = "bar2"; // SyntaxError: Identifier 'bar' has already been declared
```

Read more [here](https://stackoverflow.com/questions/762011/whats-the-difference-between-using-let-and-var).


## Resources:
* https://www.w3schools.com
* You don't know JS from Kyle Simpson
* https://www.dofactory.com/javascript/builtin-types
* https://stackoverflow.com/questions/762011/whats-the-difference-between-using-let-and-var
