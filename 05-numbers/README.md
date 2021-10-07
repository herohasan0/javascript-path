# Numbers

## Table of contents
* [Numbers](#numbers)
  - [NaN](#nan)
  - [Infinity](#infinity)
  - [Number Methods](#number-methods)
    * [toString](#tostring)
    * [toExponential](#toexponential)
    * [toFixed](#tofixed)
    * [toPrecision](#toprecision)
    * [valueOf](#valueof)
    * [Converting Variables to Numbers](#converting-variables-to-numbers)
      - [The Number Method](#the-number-method)
      - [The parseInt Method](#the-parseint-method)
      - [The parseFloat Method](#the-parsefloat-method)
  - [Number Properties](#number-properties)
* [Resources](#resources)

## Numbers

JavaScript has only one type of number. Numbers can be written with or without decimals.

```js
let x = 3.14;    // A number with decimals
let y = 3;       // A number without decimals

//Extra large or extra small numbers can be written with scientific (exponent) notation:

let x = 123e5;    // 12300000
let y = 123e-5;   // 0.00123
```

JavaScript Numbers are Always 64-bit Floating Point

Unlike many other programming languages, JavaScript does not define different types of numbers, like integers, short, long, floating-point etc. JavaScript numbers are always stored as double precision floating point numbers, following the international IEEE 754 standard. This format stores numbers in 64 bits, where the number (the fraction) is stored in bits 0 to 51, the exponent in bits 52 to 62, and the sign in bit 63.

Integers (numbers without a period or exponent notation) are accurate up to 15 digits.

```js
let x = 999999999999999;   // x will be 999999999999999
let y = 9999999999999999;  // y will be 10000000000000000
```

The maximum number of decimals is 17, but floating point arithmetic is not always 100% accurate:

```js
let x = 0.2 + 0.1;         // x will be 0.30000000000000004
```

<ins>JavaScript uses the + operator for both addition and concatenation. Numbers are added. Strings are concatenated.</ins>

JavaScript will try to convert strings to numbers in all numeric operations:

```js
let x = "100";
let y = "10";
let z = x / y;       // z will be 10

let x = "100";
let y = "10";
let z = x * y;       // z will be 1000

let x = "100";
let y = "10";
let z = x - y;       // z will be 90

let x = "100";
let y = "10";
let z = x + y;       // z will not be 110 (It will be 10010)
```

### NaN

`NaN` is a JavaScript reserved word indicating that a number is not a legal number. Trying to do arithmetic with a non-numeric string will result in `NaN` (Not a Number):

```js
let x = 100 / "Apple";  // x will be NaN (Not a Number)
```

You can use the global JavaScript function `isNaN()` to find out if a value is a not a number:

```js
let x = 100 / "Apple";
isNaN(x);               // returns true because x is Not a Number
```

If you use `NaN` in a mathematical operation, the result will also be `NaN`:

```js
let x = NaN;
let y = 5;
let z = x + y;         // z will be NaN

//or

let x = NaN;
let y = "5";
let z = x + y;         // z will be NaN5
```

`NaN` is a number: `typeof NaN` returns `number`:

```js
typeof NaN;            // returns "number"
```

### Infinity

`Infinity` (or `-Infinity`) is the value JavaScript will return if you calculate a number outside the largest possible number.

```js
let myNumber = 2;
while (myNumber != Infinity) {   // Execute until Infinity
  myNumber = myNumber * myNumber;
}
```

Division by 0 (zero) also generates `Infinity`:

```js
let x =  2 / 0;       // x will be Infinity
let y = -2 / 0;       // y will be -Infinity
```

`Infinity` is a number: `typeof Infinity` returns `number`.

```js
typeof Infinity;     // returns "number"
```

### Number Methods

Primitive values (like `3.14` or `2014`), cannot have properties and methods (because they are not objects).

But with JavaScript, methods and properties are also available to primitive values, because JavaScript treats primitive values as objects when executing methods and properties.

#### toString

The `toString()` method returns a number as a string. All number methods can be used on any type of numbers (literals, variables, or expressions):

```js
let x = 123;
x.toString();            // returns 123 from variable x
(123).toString();        // returns 123 from literal 123
(100 + 23).toString();   // returns 123 from expression 100 + 23
```

#### toExponential

`toExponential()` returns a string, with a number rounded and written using exponential notation. A parameter defines the number of characters behind the decimal point:

```js
let x = 9.656;
x.toExponential(2);     // returns 9.66e+0
x.toExponential(4);     // returns 9.6560e+0
x.toExponential(6);     // returns 9.656000e+0
```

#### toFixed

`toFixed()` returns a string, with the number written with a specified number of decimals:

```js
let x = 9.656;
x.toFixed(0);           // returns 10
x.toFixed(2);           // returns 9.66
x.toFixed(4);           // returns 9.6560
x.toFixed(6);           // returns 9.656000
```

#### toPrecision

`toPrecision()` returns a string, with a number written with a specified length:

```js
let x = 9.656;
x.toPrecision();        // returns 9.656
x.toPrecision(2);       // returns 9.7
x.toPrecision(4);       // returns 9.656
x.toPrecision(6);       // returns 9.65600
```

#### valueOf

`valueOf()` returns a number as a number.

```js
let x = 123;
x.valueOf();            // returns 123 from variable x
(123).valueOf();        // returns 123 from literal 123
(100 + 23).valueOf();   // returns 123 from expression 100 + 23
```

In JavaScript, a number can be a primitive value `(typeof = number)` or an object `(typeof = object)`. The `valueOf()` method is used internally in JavaScript to convert Number objects to primitive values. There is no reason to use it in your code.

All JavaScript data types have a `valueOf()` and a `toString()` method.

#### Converting Variables to Numbers

There are 3 JavaScript methods that can be used to convert variables to numbers:

1. The `Number()` method
2. The `parseInt()` method
3. The `parseFloat()` method

These methods are not number methods, but global JavaScript methods.

##### The Number Method

`Number()` can be used to convert JavaScript variables to numbers:

```js
Number(true);          // returns 1
Number(false);         // returns 0
Number("10");          // returns 10
Number("  10");        // returns 10
Number("10  ");        // returns 10
Number(" 10  ");       // returns 10
Number("10.33");       // returns 10.33
Number("10,33");       // returns NaN
Number("10 33");       // returns NaN 
Number("John");        // returns NaN
```

`Number()` can also convert a date to a number.

```js
Number(new Date("1970-01-01"))
// returns 0
// bc: The Number() method returns the number of milliseconds since 1.1.1970.
```

##### The parseInt Method

`parseInt()` parses a string and returns a whole number. Spaces are allowed. Only the first number is returned:

```js
parseInt("-10");        // returns -10
parseInt("-10.33");     // returns -10
parseInt("10");         // returns 10
parseInt("10.33");      // returns 10
parseInt("10 20 30");   // returns 10
parseInt("10 years");   // returns 10
parseInt("years 10");   // returns NaN 
```

##### The parseFloat Method

`parseFloat()` parses a string and returns a number. Spaces are allowed. Only the first number is returned:

```js
parseFloat("10");        // returns 10
parseFloat("10.33");     // returns 10.33
parseFloat("10 20 30");  // returns 10
parseFloat("10 years");  // returns 10
parseFloat("years 10");  // returns NaN
```

### Number Properties

```js
// MAX_VALUE Returns the largest number possible in JavaScript
let x = Number.MAX_VALUE;

// MIN_VALUE Returns the smallest number possible in JavaScript
let x = Number.MIN_VALUE;

// POSITIVE_INFINITY Represents infinity (returned on overflow)
let x = Number.POSITIVE_INFINITY;

// NEGATIVE_INFINITY Represents negative infinity (returned on overflow)
let x = Number.NEGATIVE_INFINITY

// NaN Represents a "Not-a-Number" value
let x = Number.NaN;
```

## Resources:
* https://www.w3schools.com