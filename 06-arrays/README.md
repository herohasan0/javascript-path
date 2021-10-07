# Arrays

## Table of contents
* [Arrays](#arrays)
  - [Converting Arrays to Strings](#converting-arrays-to-strings)
  - [Popping and Pushing](#popping-and-pushing)
  - [Changing Elements](#changing-elements)
  - [Deleting Elements](#deleting-elements)
  - [Splicing an Array](#splicing-an-array)
  - [Merging Arrays](#merging-arrays)
  - [Slicing an Array](#slicing-an-array)
  - [Sorting an Array](#sorting-an-array)
  - [JavaScript Array Iteration](#javascript-array-iteration)
    * [forEach](#foreach)
    * [map](#map)
    * [filter](#filter)
    * [reduce](#reduce)
    * [every](#every)
    * [some](#some)
    * [indexOf](#indexof)
    * [lastIndexOf](#lastindexof)
    * [includes](#includes)
    * [find](#find)
    * [findIndex](#findindex)
    * [from](#from)
    * [keys](#keys)
* [Resources](#resources)

## Arrays

An array is a special variable, which can hold more than one value at a time. If you have a list of items (a list of car names, for example), storing the cars in single variables could look like this:

```js
let car1 = "Saab";
let car2 = "Volvo";
let car3 = "BMW";
```

However, what if you want to loop through the cars and find a specific one? And what if you had not 3 cars, but 300? The solution is an array! An array can hold many values under a single name, and you can access the values by referring to an index number.

```js
const cars = ["Saab", "Volvo", "BMW"];

//or

const cars = [];
cars[0]= "Saab";
cars[1]= "Volvo";
cars[2]= "BMW";

//or 

const cars = new Array("Saab", "Volvo", "BMW");

//The three examples above do exactly the same.
//There is no need to use new Array().
//For simplicity, readability and execution speed, use the first one (the array literal method).
```

```js
//accesing the first element
const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits[0];    // Returns "Banana"

//accesing the last element
const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits[fruits.length - 1];  // Returns "Mango"
```

### Converting Arrays to Strings

The JavaScript method `toString()` converts an array to a string of (comma separated) array values.

```js
const fruits = ["Banana", "Orange", "Apple", "Mango"];
document.getElementById("demo").innerHTML = fruits.toString();

// result Banana,Orange,Apple,Mango
```

The `join()` method also joins all array elements into a string. It behaves just like `toString()`, but in addition you can specify the separator:

```js
const fruits = ["Banana", "Orange", "Apple", "Mango"];
document.getElementById("demo").innerHTML = fruits.join(" * ");

// result Banana * Orange * Apple * Mango
```

### Popping and Pushing

When you work with arrays, it is easy to remove elements and add new elements. This is what popping and pushing is: Popping items out of an array, or pushing items into an array.

The `pop()` method removes the last element from an array:

```js
const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.pop();  // Removes "Mango" from fruits

// The pop() method returns the value that was "popped out":

const fruits = ["Banana", "Orange", "Apple", "Mango"];
let x = fruits.pop();  // x = "Mango"
```

The `push()` method adds a new element to an array (at the end):

```js
const fruits = ["Banana", "Orange", "Apple", "Mango"];
let x = fruits.push("Kiwi");   //  x = 5
```

Shifting is equivalent to popping, working on the first element instead of the last. The `shift()` method removes the first array element and "shifts" all other elements to a lower index.

```js
const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.shift();   // Removes "Banana" from fruits

// The shift() method returns the value that was "shifted out":

const fruits = ["Banana", "Orange", "Apple", "Mango"];
let x = fruits.shift();    // x = "Banana"
```

The `unshift()` method adds a new element to an array (at the beginning), and "unshifts" older elements:

```js
const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.unshift("Lemon");    // Adds "Lemon" to fruits

// The unshift() method returns the new array length.

const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.unshift("Lemon");    // Returns 5
```

### Changing Elements

```js
const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits[0] = "Kiwi";        // Changes the first element of fruits to "Kiwi"
```

The `length` property provides an easy way to append a new element to an array:

```js
const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits[fruits.length] = "Kiwi";          // Appends "Kiwi" to fruits
```

### Deleting Elements

Since JavaScript arrays are objects, elements can be deleted by using the JavaScript operator `delete`:

```js
const fruits = ["Banana", "Orange", "Apple", "Mango"];
delete fruits[0];           // Changes the first element in fruits to undefined
```

But, Using delete may leave undefined holes in the array. Use `pop()` or `shift()` instead.

### Splicing an Array

The `splice()` method can be used to add new items to an array:

```js
const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.splice(2, 0, "Lemon", "Kiwi");
```

The first parameter (`2`) defines the position where new elements should be added (spliced in). The second parameter (`0`) defines how many elements should be removed. The rest of the parameters (`"Lemon" , "Kiwi"`) define the new elements to be added. The `splice()` method returns an array with the deleted items.

With clever parameter setting, you can use `splice()` to remove elements without leaving "holes" in the array:

```js
const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.splice(0, 1);   // Removes the first element
```

The first parameter (`0`) defines the position where new elements should be added (spliced in). The second parameter (`1`) defines how many elements should be removed. The rest of the parameters are omitted. No new elements will be added.

### Merging Arrays

The `concat()` method creates a new array by merging (concatenating) existing arrays:

```js
const myGirls = ["Cecilie", "Lone"];
const myBoys = ["Emil", "Tobias", "Linus"];

// Concatenate (join) myGirls and myBoys
const myChildren = myGirls.concat(myBoys); 

// The concat() method can take any number of array arguments:
const arr1 = ["Cecilie", "Lone"];
const arr2 = ["Emil", "Tobias", "Linus"];
const arr3 = ["Robin", "Morgan"];
const myChildren = arr1.concat(arr2, arr3);

// The concat() method can also take strings as arguments:
const arr1 = ["Emil", "Tobias", "Linus"];
const myChildren = arr1.concat("Peter"); 
```

The `concat()` method does not change the existing arrays. It always returns a new array.

### Slicing an Array

The `slice()` method slices out a piece of an array into a new array. The `slice()` method creates a new array. It does not remove any elements from the source array.

```js
const fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
const citrus = fruits.slice(1);
console.log(citrus) // ['Orange', 'Lemon', 'Apple', 'Mango']
```

The `slice()` method can take two arguments like `slice(1, 3)`. The method then selects elements from the start argument, and up to (but not including) the end argument.

```js
const fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
const citrus = fruits.slice(1, 3);
```

### Sorting an Array

The `sort()` method sorts an array alphabetically:

```js
const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.sort();        // Sorts the elements of fruits
```

The `reverse()` method reverses the elements in an array. You can use it to sort an array in descending order:

```js
const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.sort();        // First sort the elements of fruits  ['Apple', 'Banana', 'Mango', 'Orange']
fruits.reverse();     // Then reverse the order of the elements ['Orange', 'Mango', 'Banana', 'Apple']
```

By default, the `sort()` function sorts values as strings. This works well for strings ("Apple" comes before "Banana"). However, if numbers are sorted as strings, "25" is bigger than "100", because "2" is bigger than "1". Because of this, the `sort()` method will produce incorrect result when sorting numbers. You can fix this by providing a compare function:

```js
const points = [40, 100, 1, 5, 25, 10];
points.sort(function(a, b){return a - b});
```

The purpose of the compare function is to define an alternative sort order. The compare function should return a negative, zero, or positive value, depending on the arguments:

```js
function(a, b){return a - b}
```

When the `sort()` function compares two values, it sends the values to the compare function, and sorts the values according to the returned (negative, zero, positive) value. If the result is negative `a` is sorted before `b`. If the result is positive `b` is sorted before `a`. If the result is `0` no changes are done with the sort order of the two values.

The compare function compares all the values in the array, two values at a time `(a, b)`. When comparing 40 and 100, the `sort()` method calls the compare `function(40, 100)`. The function calculates 40 - 100 `(a - b)`, and since the result is negative (-60),  the sort function will sort 40 as a value lower than 100.

### JavaScript Array Iteration

Array iteration methods operate on every array item.

#### forEach

The `forEach()` method calls a function (a callback function) once for each array element.

```js
const numbers = [45, 4, 9, 16, 25];
let txt = "";
numbers.forEach(myFunction);

function myFunction(value) {
  txt += value + "<br>"; 
}
```

#### map

The `map()` method creates a new array by performing a function on each array element. The `map()` method does not execute the function for array elements without values. The `map()` method does not change the original array. This example multiplies each array value by 2:

```js
const numbers1 = [45, 4, 9, 16, 25];
const numbers2 = numbers1.map(myFunction);

function myFunction(value) {
  return value * 2;
}
```

#### filter

The `filter()` method creates a new array with array elements that passes a test. This example creates a new array from elements with a value larger than 18:

```js
const numbers = [45, 4, 9, 16, 25];
const over18 = numbers.filter(myFunction);

function myFunction(value) {
  return value > 18;
}
```

#### reduce

The `reduce()` method runs a function on each array element to produce (reduce it to) a single value. The `reduce()` method works from left-to-right in the array. See also `reduceRight()`. The `reduce()` method does not reduce the original array.

```js
const numbers = [45, 4, 9, 16, 25];
let sum = numbers.reduce(myFunction);

function myFunction(total, value) {
  return total + value;
}

// The reduce() method can accept an initial value:

const numbers = [45, 4, 9, 16, 25];
let sum = numbers.reduce(myFunction, 100);

function myFunction(total, value) {
  return total + value;
}
```

#### every

The `every()` method check if all array values pass a test. This example check if all array values are larger than 18:

```js
const numbers = [45, 4, 9, 16, 25];
let allOver18 = numbers.every(myFunction);

function myFunction(value) {
  return value > 18;
}
```

#### some

The `some()` method check if some array values pass a test. This example check if some array values are larger than 18:

```js
const numbers = [45, 4, 9, 16, 25];
let someOver18 = numbers.some(myFunction);

function myFunction(value) {
  return value > 18;
}
```

#### indexOf

The `indexOf()` method searches an array for an element value and returns its position.

```js
const fruits = ["Apple", "Orange", "Apple", "Mango"];
let position = fruits.indexOf("Apple") + 1;
```

`Array.indexOf()` returns `-1` if the item is not found.

Syntax 

`array.indexOf(item, start)`

(item)	Required. The item to search for.

(start)	Optional. Where to start the search. Negative values will start at the given position counting from the end, and search to the end.

#### lastIndexOf

`Array.lastIndexOf()` is the same as `Array.indexOf()`, but returns the position of the last occurrence of the specified element.

```js
const fruits = ["Apple", "Orange", "Apple", "Mango"];
let position = fruits.lastIndexOf("Apple") + 1;
```

#### includes

ECMAScript 2016 introduced `Array.includes()` to arrays. This allows us to check if an element is present in an array (including `NaN`, unlike `indexOf`).

```js
const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.includes("Mango"); // is true
```

#### find

The `find()` method returns the value of the first array element that passes a test function. This example finds (returns the value of) the first element that is larger than 18:

```js
const numbers = [4, 9, 16, 25, 29];
let first = numbers.find(myFunction);

function myFunction(value) {
  return value > 18;
}
```

#### findIndex

The `findIndex()` method returns the index of the first array element that passes a test function. This example finds the index of the first element that is larger than 18:

```js
const numbers = [4, 9, 16, 25, 29];
let first = numbers.findIndex(myFunction);

function myFunction(value) {
  return value > 18;
}
```

#### from

The `Array.from()` method returns an Array object from any object with a length property or any iterable object.

```js
//Create an Array from a String:

Array.from("ABCDEFG")   // Returns [A,B,C,D,E,F,G]
```

#### keys

The `Array.keys()` method returns an Array Iterator object with the keys of an array.

```js
const fruits = ["Banana", "Orange", "Apple", "Mango"];
const keys = fruits.keys();

for (let x of keys) {
  text += x + "<br>";
}
```

## Resources:
* https://www.w3schools.com