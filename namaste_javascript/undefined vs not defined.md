# undefined vs not defined in JS

`Memory Allocation Phase:`
In JavaScript, during the memory allocation phase, variables are given a `placeholder` value called `undefined`. This happens before your code starts executing. For example:

```javascript
var x;
console.log(x);  // Output: undefined
```
Here, x is declared but not assigned any value, so it has the default undefined value.

`Undefined:`
Undefined means that memory is allocated for a variable, but no value has been assigned to it yet. For example:

```javascript
var y;
console.log(y);  // Output: undefined


var z = undefined;  // Not recommended to assign undefined explicitly
console.log(z);  // Output: undefined
```
The first case is where y is declared but not assigned any value, so it's undefined. The second case explicitly assigns undefined to z, but it's not recommended to do so.

`Not Defined:`
When you try to access a variable that has not been declared at all, it results in a ReferenceError saying that the variable is not defined. For example:

```javascript
console.log(a);  // Uncaught ReferenceError: a is not defined
```
In this case, a is not declared or allocated any memory, so it's truly not defined.

`Loosely Typed Nature:`
JavaScript is indeed a loosely typed language, allowing variables to change types. You can declare a variable without specifying its data type, and later assign different types of values to it:

```javascript
var b = 5;
console.log(b);  // Output: 5

b = true;
console.log(b);  // Output: true

b = 'hello';
console.log(b);  // Output: hello
```
The variable b starts as a number, changes to a boolean, and then becomes a string.

Remember, you should avoid manually assigning undefined to variables. Instead, let JavaScript handle it during the memory allocation phase. Manually assigning undefined can make debugging and understanding your code more complex.
