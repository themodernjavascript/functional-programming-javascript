# Functional Programming Javascript

Functional programming is a style that treats computation as the evaluation of mathematical functions and avoids changing-state and mutable data.

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

## Currying

Currying allows a function with multiple arguments to be translated into a sequence of functions. Curried functions can be tailored to match the signature of another function.

```javascript
const convertUnits = (toUnit, factor, offset = 0) => input => ((offset + input) * factor).toFixed(2).concat(toUnit);
const milesToKm = convertUnits('km', 1.60936, 0);
const poundsToKg = convertUnits('kg', 0.45460, 0);
const farenheitToCelsius = convertUnits('degrees C', 0.5556, -32);
milesToKm(10); // "16.09 km"
poundsToKg(2.5); // "1.14 kg"
farenheitToCelsius(98); // "36.67 degrees C"

const weightsInPounds = [5, 15.4, 9.8, 110];
// without currying
// const weightsInKg = weightsInPounds.map(x => convertUnits('kg', 0.45460, 0)(x));
// with currying
const weightsInKg = weightsInPounds.map(poundsToKg); // 2.27kg, 7.00kg, 4.46kg, 50.01kg
```
