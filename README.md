# Functional Programming Javascript

Functional programming is a style that treats computation as the evaluation of mathematical functions and avoids changing-state and mutable data.

## Arrow Functions (Fat Arrows)

Arrow functions create a concise expression that encapsulates a small piece of functionality. Additionally, arrows retain the scope of the caller inside the function eliminating the need of `self = this`.

For example:

```javascript
// const multiply = function(x,y) {
//   return x * y;
// }

// Can be rewritten as:
// const multiply = (x, y) => { return x * y };

// Since the function is a single expression return and braces are not needed:
const multiply = (x, y) => x * y;
console.log(multiply(5,10)) //50
```

## Function Delegates

Function delegates encapsulate a method allowing functions to be composed or passed as data.

For example:

```javascript
const isZero = n => n === 0;
const a = [0,1,0,3,4,0];
console.log(a.filter(isZero).length); // 3
```

## Expressions Instead of Statements

Statements define an action and are executed for their side effect. Expressions produce a result without mutating state.

For example:

Statement

```javascript

```

Expression

```javascript

```
