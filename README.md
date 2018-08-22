# Functional Programming Javascript

Functional programming is a way of writing clearner code through clever way of mutating, combinding, and using functions.

## Arrow Functions (Fat Arrows)

Arrow functions create a concise expression that encapsulates a small piece of functionality. Additionally, arrows retain the scope of the caller inside the function eliminating the need of `self = this`.

For example:

```javascript
//  const multiply = function(x, y) {
//    return x * y;
//  }

// Can be rewritten as:
// const multiply = (x, y) => { return x * y };

// Since the function is a single expression return and braces are not needed:
const multiply = (x, y) => x * y;
console.log(multiply(5,10)) // 50
```

<a href="https://codepen.io/Bunlong/pen/QBgdJb" target="_blank">Edit on Codepen</a>

## Scope

* Global scope
* Local Scope
* Function scope
* Block scope
* Function hoisting and scopes
* Functions do not have access to each other's scopes
* Nested scopes

## Closure

Clousure is the functions that have access to the parent scope, even when the parent function has closed.

For every closure there are 3 scopes: 

* Local Scope ( Own scope) 
* Outer Functions Scope 
* Global Scope.

## Function Delegates

Function delegates encapsulate a method allowing functions to be composed or passed as data.

For example:

```javascript
const isZero = n => n === 0;
const a = [0, 1, 0, 3, 4, 0];
console.log(a.filter(isZero)); // [0, 0, 0]
```

<a href="https://codepen.io/Bunlong/pen/zLzNbd" target="_blank">Edit on Codepen</a>

## Expressions Instead of Statements

Statements define an action and are executed for their side effect. Expressions produce a result without mutating state.

For example:

Statement

```javascript
const getSalutation = function(hour) {
  var salutation; // temp value
  
  if (hour < 12) {
    salutation = "Good Morning";
  } else {
    salutation = "Good Afternoon"
  }
  
  return salutation; // mutated value
}

console.log(getSalutation(10)); // Good Morning
```

Expression

```javascript
const getSalutation = (hour) => hour < 12 ? "Good Morning" : "Good Afternoon";
console.log(getSalutation(10)); // Good Morning
```

<a href="https://codepen.io/Bunlong/pen/mjwWeY" target="_blank">Edit on Codepen</a>

## Higher Order Functions

A function that accepts another function as a parameter, or returns another function.

For example:

```javascript
function mapConsecutive(values, fn) {
  let result = [];
  
  for(let i=0; i < values.length -1; i++) {
    result.push(fn(values[i], values[i+1]));
  }
  
  return result;
}

const letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g'];
let twoByTwo = mapConsecutive(letters, (x, y) => [x, y]);
console.log(twoByTwo); // [[a, b], [b, c], [c, d], [d, e], [e, f], [f, g]]
```

<a href="https://codepen.io/Bunlong/pen/JBJWRa" target="_blank">Edit on Codepen</a>

## Pure Functions

A function that given the same input, will always return the same output. A pure function produces no side effects.

Note: Side effects may include:

* changing the file system
* inserting a record into a database
* making an http call
* mutations
* printing to the screen / logging
* obtaining user input
* querying the DOM
* accessing system state

For example:

```javascript
var xs = [1, 2, 3, 4, 5];

// ==== pure ====
xs.slice(0, 3);
//=> [1, 2, 3]

xs.slice(0, 3);
//=> [1, 2, 3]

xs.slice(0, 3);
//=> [1, 2, 3]

// ==== pure ====
xs.splice(0, 3);
//=> [1, 2, 3]

xs.splice(0, 3);
//=> [4, 5]

xs.splice(0, 3);
//=> []

// pure
var checkAge = function(age) {
  var minimum = 21;
  return age >= minimum;
};

// impure
var minimum = 21;

var checkAge = function(age) {
  return age >= minimum;
};
```

<a href="https://codepen.io/Bunlong/pen/OwOXzz" target="_blank">Edit on Codepen</a>

## Recursion

Recursion is the ability to call a function from within itself.

For example:

```javascript
function countUp(n) {
  console.log(n);
  if(n < 10) countUp(n+1);
}

countUp(1);
```

<a href="https://codepen.io/Bunlong/pen/zLPBPO" target="_blank">Edit on Codepen</a>

## Anonymous Functions

Anonymous function is the function that was declared without any named identifier to refer to it.

For example:

```javascript
// Normal function
function sayHi() {
  alert('Hello world!');
}
sayHi();

// Anonymous function assigned to sayHi variable
var sayHi = function() { 
  alert('Hello World!');
}

// Use as an argument to other functions
setTimeout(function() {
  console.log('Hello World!');
}, 1000);

// Use as a closure
(function() {
  alert('Hello World!');
})();

// Use as a closure with parameters
(function(msg) {
  alert(msg);
}('Hello World!'));

// An anonymous function can refer to itself via arguments.callee local variable, useful for recursive anonymous functions
console.log(
  (function(n) {
    return (1 < n) ? arguments.callee(n - 1) + n : 1;
  })(10)
);

// Instead of using arguments.callee, you can use named function expression instead
console.log(
  (function sum(n) {
    return (n <= 1) ? 1 : sum(n-1) + n
  })(10)
);
```

## Currying

Currying allows a function with multiple arguments to be translated into a sequence of functions. Curried functions can be tailored to match the signature of another function.

```javascript
// Statement
// function convertUnits(toUnit = 0, factor, offset) {
//   return function(input) {
//     return ((offset + input) * factor).toFixed(2).concat(toUnit)
//   }
// }

// Can be written as an expression
const convertUnits = (toUnit, factor, offset = 0) => input => ((offset + input) * factor).toFixed(2).concat(toUnit);

const milesToKm = convertUnits('km', 1.60936, 0);
const poundsToKg = convertUnits('kg', 0.45460, 0);
const farenheitToCelsius = convertUnits('degrees C', 0.5556, -32);

console.log(milesToKm(10)); //"16.09 km"
console.log(poundsToKg(2.5)); //"1.14 kg"
console.log(farenheitToCelsius(98)); //"36.67 degrees C"

const weightsInPounds = [5, 15.4, 9.8, 110];

// Without currying
// const weightsInKg = weightsInPounds.map(x => convertUnits('kg', 0.45460, 0)(x));

// With currying
const weightsInKg = weightsInPounds.map(poundsToKg);
console.log(weightsInKg); // 2.27kg, 7.00kg, 4.46kg, 50.01kg
```

<a href="https://codepen.io/Bunlong/pen/rrwmWR" target="_blank">Edit on Codepen</a>

## Array Manipulation Functions

Array Functions are the gateway to functional programming in JavaScript. These functions make short work of most imperative programming routines that work on arrays and collections.

***[].every(fn)***

Checks if all elements in an array pass a test.

***[].some(fn) | [].includes(fn)***

Checks if any of the elements in an array pass a test.

***[].find(fn)***

Returns the value of the first element in the array that passes a test.

***[].filter(fn)***

Creates an array filled with only the array elements that pass a test.

***[].map(fn)***

Creates a new array with the results of a function applied to every element in the array.

***[].reduce(fn(accumulator, currentValue))***

Executes a provided function for each value of the array (from left-to-right). Returns a single value, the accumulator.

***[].sort(fn(a,b))*** warning, mutates state!

Modifies an array by sorting the items within an array. An optional compare function can be used to customize sort behavior. Use the spread operator to avoid mutation. [...arr].sort()

***[].reverse()*** warning, mutates state!

Reverses the order of the elements in an array. Use the spread operator to avoid mutation. [...arr] . reverse()

For example:

```javascript
const names = [
  {text: "Alpha", value: 5}, 
  {text: "Beta", value: 2}, 
  {text: "Gamma", value: 4},
];

//Checks if all elements in an array pass a test.
let everyResult = names.every(x => x.value > 0); //true

// Checks if any of the elements in an array pass a test.
let someResult = names.some(x => x.text === "Alpha"); //true

// Returns the value of the first element in the array that passes a test.
let findResult = names.find(x => x.text === "Gamma"); //{text: "Gamma", value: 4}

// Creates an array filled with only the array elements that pass a test.
let filterResult = names.filter(x => x.value > 3); //[{text: "Alpha", value: 5}, {text: "Gamma", value: 4}]

// Creates a new array with the results of a function applied to every element in the array.
let mapResult = names.map(x => ({...x, value: x.value *10}));
//[{text: "Alpha", value: 50}, {text: "Beta", value: 20}, {text: "Gamma", value: 40}];

// Executes a provided function for each value of the array (from left-to-right). The returns a single value, the accumulator.
let reduceResult = names.reduce((accumulator, currentValue) =>  currentValue.value > accumulator.value ? currentValue : accumulator);
// Get the largest object by value: {"text":"Alpha","value":5}

// Modifies an array by sorting the items within an array. An optional compare function can be used to customize sort behavior. Use the spread operator to avoid mutation. [...arr].sort()
let sortResult = [...names].sort((a,b) => b.value - a.value);

// reverses the order of the elements in an array. Use the spread operator to avoid mutation. [...arr].reverse()
let reverseResult = [...names].reverse();

// Results
const appDiv = document.getElementById('app');
appDiv.innerHTML = `
<p>every: ${everyResult}</p>
<p>some: ${someResult}</p>
<p>find: ${JSON.stringify(findResult)}</p>
<p>filter: ${JSON.stringify(filterResult)}</p>
<p>map: ${JSON.stringify(mapResult)}</p>
<p>reduce: ${JSON.stringify(reduceResult)}</p>
<p>reverse: ${JSON.stringify(reverseResult)}</p>
<p>sort: ${JSON.stringify(sortResult)}</p>`;
```

## Method Chaining

Method chains allow a series of functions to operate in succession to reach a final result. Method chains allow function composition similar to a pipeline.

For example:

```javascript
let cart = [
  { name: "Drink", price: 3.12 }, 
  { name: "Steak", price: 45.15}, 
  { name: "Drink", price: 11.01}
];

let drinkTotal = cart.filter(x=> x.name === "Drink")
                     .map(x=> x.price)
                     .reduce((t,v) => t + v)
                     .toFixed(2); 

console.log(`Total Drink Cost $${drinkTotal}`); // Total Drink Cost $14.13
```

<a href="https://codepen.io/Bunlong/pen/yqXbXQ" target="_blank">Edit on Codepen</a>

## Pipelines

A pipeline allows for easy function composition when performing multiple operations on a variable. Since JavaScript lacks a Pipeline operator, a design pattern can be used to accomplish the task.

```javascript
const pipe = functions => data => {
  return functions.reduce(
    (value, func) => func(value),
    data
  );
};

let cart = [3.12, 45.15, 11.01];
const addSalesTax = (total, taxRate) => (total * taxRate) + total;

const tally = orders => pipe([
  x => x.reduce((total, val) => total + val), // sum the order
  x => addSalesTax(x, 0.09),
  x => `Order Total = ${x.toFixed(2)}` // convert to text
])(orders);

console.log(tally(cart)); // Order Total = 64.62
```

<a href="https://codepen.io/Bunlong/pen/qyjmPO" target="_blank">Edit on Codepen</a>
