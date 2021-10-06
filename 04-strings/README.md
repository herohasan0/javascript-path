# Strings and Numbers

## Table of contents
* [Strings](#strings)
  - [Escape Character](#escape-character)
  - [String can be an Object](#string-can-be-an-object)
  - [String Methods](#string-methods)
    - [String Length](#string-length)
    - [Extracting String Parts](#extracting-string-parts)
      - [The slice Method](#the-slice-method)
      - [The substring Method](#the-substring-method)
      - [The substr Method](#the-substr-method)
    - [Replacing String Content](#replacing-string-content)
    - [Converting to Upper and Lower Case](#converting-to-upper-and-lower-case)
    - [The concat Method](#the-concat-method)
    - [The trim Method](#the-trim-method)
    - [Padding](#padding)
    - [Extracting String Characters](#extracting-string-characters)
      - [charAt Method](#charAt-method)
      - [charCodeAt Method](#charCodeAt-method)
      - [Property Access](#property-access)
    - [Converting a String to an Array](#converting-a-string-to-an-array)
    - [String Search](#string-search)
      - [indexOf()](#indexOf())
      - [lastIndexOf()](#lastIndexOf())
      - [search()](#search())
      - [match()](#match())
      - [includes()](#includes())
      - [startsWith()](#startsWith())
      - [endsWith()](#endsWith())
  - [Template Literals](#template-literals)

## Strings

JavaScript strings are used for storing and manipulating text. A string is zero or more characters written inside quotes.

```js
let text = "John Doe";

let carName1 = "Volvo XC60";  // Double quotes
let carName2 = 'Volvo XC60';  // Single quotes

let answer1 = "It's alright";
let answer2 = "He is called 'Johnny'";
let answer3 = 'He is called "Johnny"';
```

### Escape Character

Because strings must be written within quotes, JavaScript will misunderstand this string:

```js
let text = "We are the so-called "Vikings" from the north.";
```

The string will be chopped to "We are the so-called ". The solution to avoid this problem, is to use the backslash escape character. The backslash `(\)` escape character turns special characters into string characters:

| Code        | Result      | Description  |
| ----------- | ----------- | -----------  | 
| `\'`        |    '        | Single quote |
| `\"`        |    "        | Double quote |
| `\\`        |    \        | Backslash    |

```js
let text = "We are the so-called \"Vikings\" from the north.";

let text= 'It\'s alright.';

let text = "The character \\ is called backslash.";
```

### String can be an Object

Normally, JavaScript strings are primitive values, created from literals:

`let firstName = "John";`

But strings can also be defined as objects with the keyword `new`:

`let firstName = new String("John");`

```js
let x = "John";
let y = new String("John");

// typeof x will return string
// typeof y will return object
```

<ins>BUT Don't create strings as objects. It slows down execution speed.
The `new` keyword complicates the code. This can produce some unexpected results. </ins>

```js
let x = "John";             
let y = new String("John");

// (x == y) is true because x and y have equal values

let x = "John";             
let y = new String("John");

// (x === y) is false because x and y have different types (string and object)

let x = new String("John");             
let y = new String("John");

// (x == y) is false because x and y are objects
```

### String Methods

Primitive values, like "`John Doe`", cannot have properties or methods (because they are not objects). But with JavaScript, methods and properties are also available to primitive values, because JavaScript treats primitive values as objects when executing methods and properties.

#### String Length

To find the length of a string, use the built-in `length` property:

```js
let text = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
text.length;    // Will return 26
```

#### Extracting String Parts

There are 3 methods for extracting a part of a string:

1. `slice(start, end)`
2. `substring(start, end)`
3. `substr(start, length)`

##### The slice Method

`slice()` extracts a part of a string and returns the extracted part in a new string. The method takes 2 parameters: the start position, and the end position (end not included). This example slices out a portion of a string from position 7 to position 12 (13-1):

```js
let str = "Apple, Banana, Kiwi";
str.slice(7, 13)     // Returns Banana

//Remember: JavaScript counts positions from zero. First position is 0.
```

If a parameter is negative, the position is counted from the end of the string. This example slices out a portion of a string from position -12 to position -6:

```js
let str = "Apple, Banana, Kiwi";
str.slice(-12, -6)    // Returns Banana

//If you omit the second parameter, the method will slice out the rest of the string:

str.slice(7);    // Returns Banana,Kiwi

str.slice(-12)    // Returns Banana,Kiwi
```

##### The substring Method

`substring()` is similar to `slice()`. The difference is that `substring()` cannot accept negative indexes. If you omit the second parameter, `substring()` will slice out the rest of the string.

```js
let str = "Apple, Banana, Kiwi";
substring(7, 13)    // Returns Banana
```

##### The substr Method

`substr()` is similar to `slice()`. The difference is that the second parameter specifies the length of the extracted part.

```js
let str = "Apple, Banana, Kiwi";
str.substr(7, 6)    // Returns Banana

//If you omit the second parameter, substr() will slice out the rest of the string.

let str = "Apple, Banana, Kiwi";
str.substr(7)    // Returns Banana,Kiwi

//If the first parameter is negative, the position counts from the end of the string.

let str = "Apple, Banana, Kiwi";
str.substr(-4)    // Returns Kiwi
```

### Replacing String Content

The `replace()` method replaces a specified value with another value in a string. By default, the replace() method replaces only the first match:

```js
let text = "Please visit Microsoft!";
let newText = text.replace("Microsoft", "W3Schools");
```

<ins>The replace() method does not change the string it is called on. It returns a new string.</ins>

By default, the replace() method is case sensitive. Writing MICROSOFT (with upper-case) will not work:

```js
let text = "Please visit Microsoft!";
let newText = text.replace("MICROSOFT", "W3Schools");
```

To replace case insensitive, use a regular expression with an `/i` flag (insensitive):

```js
let text = "Please visit Microsoft!";
let newText = text.replace(/MICROSOFT/i, "W3Schools");

//To replace all matches, use a regular expression with a /g flag (global match):

let text = "Please visit Microsoft and Microsoft!";
let newText = text.replace(/Microsoft/g, "W3Schools");
```

### Converting to Upper and Lower Case

```js
let text1 = "Hello World!";       // String
let text2 = text1.toUpperCase();  // text2 is text1 converted to upper

let text1 = "Hello World!";       // String
let text2 = text1.toLowerCase();  // text2 is text1 converted to lower
```

### The concat() Method

`concat()` joins two or more strings:

```js
let text1 = "Hello";
let text2 = "World";
let text3 = text1.concat(" ", text2);
```

The `concat()` method can be used instead of the plus operator. These two lines do the same:

```js
text = "Hello" + " " + "World!";
text = "Hello".concat(" ", "World!");
```

<ins>All string methods return a new string. They don't modify the original string.
Formally said: Strings are immutable: Strings cannot be changed, only replaced.</ins>

### The trim method

The `trim()` method removes whitespace from both sides of a string:

```js
let text = "       Hello World!        ";
text.trim()    // Returns "Hello World!"
```

### Padding

ECMAScript 2017 added two String methods: `padStart` and `padEnd` to support padding at the beginning and at the end of a string.

```js
let text = "5";
text.padStart(4,0)    // Returns 0005

let text = "5";
text.padEnd(4,0)     // Returns 5000
```

### Extracting String Characters

There are 3 methods for extracting string characters:

* `charAt(position)`
* `charCodeAt(position)`
* Property access [ ]

#### charAt Method

The `charAt()` method returns the character at a specified index (position) in a string:

```js
let text = "HELLO WORLD";
text.charAt(0)           // Returns H
```

#### charCodeAt Method

The `charCodeAt()` method returns the unicode of the character at a specified index in a string: The method returns a UTF-16 code (an integer between 0 and 65535).

```js
let text = "HELLO WORLD";
text.charCodeAt(0)       // Returns 72
```

#### Property Access

ECMAScript 5 (2009) allows property access [ ] on strings:

```js
let text = "HELLO WORLD";
text[0]                   // returns H
```

Property access might be a little unpredictable:

* It makes strings look like arrays (but they are not)
* If no character is found, [ ] returns undefined, while charAt() returns an empty string.
* It is read only. `str[0] = "A"` gives no error (but does not work!)

```js
let text = "HELLO WORLD";
text[0] = "A"             // Gives no error, but does not work
text[0]                   // returns H
```

### Converting a String to an Array

A string can be converted to an array with the `split()` method:

```js
text.split(",")          // Split on commas
text.split(" ")          // Split on spaces
text.split("|")          // Split on pipe
```

If the separator is omitted, the returned array will contain the whole string in index [0]. If the separator is `""`, the returned array will be an array of single characters:

```js
text.split("")           // Split in characters
```

Example

```js
const str = 'The quick brown fox jumps over the lazy dog.';

const words = str.split(' ');
console.log(words)
// expected output: ['The', 'quick', 'brown', 'fox', 'jumps', 'over', 'the', 'lazy', 'dog.']

console.log(words[3]);
// expected output: "fox"

const chars = str.split('');
console.log(chars[8]);
// expected output: "k"

const strCopy = str.split();
console.log(strCopy);
// expected output: Array ["The quick brown fox jumps over the lazy dog."]
```

### String Search

JavaScript methods for searching strings:

* `String.indexOf()`
* `String.lastIndexOf()`
* `String.startsWith()`
* `String.endsWith()`

#### indexOf()

The `indexOf()` method returns the index of (the position of) the first occurrence of a specified text in a string:

```js
let str = "Please locate where 'locate' occurs!";
str.indexOf("locate")    // Returns 7
```

#### lastIndexOf()

The `lastIndexOf()` method returns the index of the last occurrence of a specified text in a string:

```js
let str = "Please locate where 'locate' occurs!";
str.lastIndexOf("locate")    // Returns 21
```

Both `indexOf()`, and `lastIndexOf()` return `-1` if the text is not found:

```js
let str = "Please locate where 'locate' occurs!";
str.lastIndexOf("John")    // Returns -1
```

Both methods accept a second parameter as the starting position for the search:

```js
let str = "Please locate where 'locate' occurs!";
str.indexOf("locate", 15)    // Returns 21
```

The `lastIndexOf()` methods searches backwards (from the end to the beginning), meaning: if the second parameter is 15, the search starts at position 15, and searches to the beginning of the string.

```js
let str = "Please locate where 'locate' occurs!";
str.lastIndexOf("locate", 15)    // Returns 7
```

#### search()

The `search()` method searches a string for a specified value and returns the position of the match:

```js
let str = "Please locate where 'locate' occurs!";
str.search("locate")     // Returns 7
```

The two methods, `indexOf()` and `search()`, look like equal. But they are not. These are the differences:

* The `search()` method cannot take a second start position argument.
* The `indexOf()` method cannot take powerful search values (regular expressions).

#### match()

The `match()` method searches a string for a match against a regular expression, and returns the matches, as an Array object.

```js
let text = "The rain in SPAIN stays mainly in the plain"; 
text.match(/ain/g)    // Returns an array [ain,ain,ain]
```

If the regular expression does not include the `g` modifier (to perform a global search), the match() method will return only the first match in the string. The method will return `null` if no match is found. 

```js
let text = "The rain in SPAIN stays mainly in the plain"; 
text.match(/ain/gi)   // Returns an array [ain,AIN,ain,ain]
```

#### includes()

The `includes()` method returns true if a string contains a specified value.

```js
let text = "Hello world, welcome to the universe.";
text.includes("world")    // Returns true
```

```js
//Check if a string includes "world", starting the search at position 12:

let text = "Hello world, welcome to the universe.";
text.includes("world", 12)    // Returns false
```

#### startsWith()

The `startsWith()` method returns `true` if a string begins with a specified value, otherwise `false`:

```js
let text = "Hello world, welcome to the universe.";

text.startsWith("Hello")   // Returns true
```

```js
//second parameter: length. Optional. The length to search.

let text = "Hello world, welcome to the universe.";
text.startsWith("world", 5)    // Returns false

let text = "Hello world, welcome to the universe.";
text.startsWith("world", 6)    // Returns true
```

Note: The `startsWith()` method is case sensitive.

#### endsWith()

The `endsWith()` method returns `true` if a string ends with a specified value, otherwise `false`:

```js
var text = "John Doe";
text.endsWith("Doe")    // Returns true

//second parameter: length. Optional. The length to search.
let text = "Hello world, welcome to the universe.";
text.endsWith("world", 11)    // Returns true
```

Note: The `endsWith()` method is case sensitive.

### Template Literals

These are all the same thing, Template Literals, Template Strings, String Templates, Back-Tics Syntax.

Template Literals use back-ticks (``) rather than the quotes ("") to define a string:

```js
let text = `Hello World!`;

let text = `He's often called "Johnny"`;

let text =
`The quick
brown fox
jumps over
the lazy dog`;
```

Template literals provide an easy way to interpolate variables and expressions into strings.

```js
let firstName = "John";
let lastName = "Doe";

let text = `Welcome ${firstName}, ${lastName}!`;
```

Automatic replacing of variables with real values is called string interpolation.

## Resources:
* https://www.w3schools.com
* https://developer.mozilla.org