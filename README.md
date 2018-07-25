# Functional Programming Javascript

Functional programming is a style that treats computation as the evaluation of mathematical functions and avoids changing-state and mutable data.

## Arrow Functions (Fat Arrows)

Arrow functions create a concise expression that encapsulates a small piece of functionality. Additionally,
arrows retain the scope of the caller inside the function eliminating the need of `self = this`.

For example:

```javascript
// const multiply = function(x,y) {
//
return x * y;
// }
// Can be rewritten as:
// const multiply = (x, y) => { return x * y };
// Since the function is a single expression return and braces are not
needed.
const multiply = (x, y) => x * y;
console.log(multiply(5,10)) //50
```
