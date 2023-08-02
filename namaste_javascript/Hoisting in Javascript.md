**Hoisting in JavaScript:**

Hoisting is a JavaScript behavior where variable declarations and function declarations are moved (conceptually) to the top of their containing scope during the Memory Creation Phase of the Execution Context. This means that you can access variables and functions even before they are declared in your code. However, it's important to note that only the declarations are hoisted, not their assignments or initializations.

**Hoisting with Variables:**

Let's consider the following example:

```js
console.log(x); // Output: undefined
var x = 7;
```

In the above code, JavaScript hoists the variable declaration `var x;` to the top of the execution context. So, during the memory creation phase, `x` is allocated memory with an initial value of `undefined`. That's why the `console.log(x)` statement doesn't throw an error, but it prints `undefined`. However, the assignment `x = 7;` is not hoisted, so the value of `x` remains `undefined` until the assignment is reached during the code execution phase.

**Hoisting with Functions:**

Let's consider another example with functions:

```js
getName(); // Output: Namaste JavaScript
console.log(getName); // Output: [Function: getName]
function getName() {
  console.log("Namaste JavaScript");
}
```

In this example, the function declaration `function getName() { ... }` is hoisted to the top of the execution context during the memory creation phase. So, you can call the function before its actual declaration in the code. That's why `getName();` doesn't throw an error and successfully prints "Namaste JavaScript." Similarly, `console.log(getName);` prints the function definition because the function is hoisted, and its entire code is available in memory during the execution.

**Hoisting with Function Expressions:**

Now, let's observe how hoisting works with function expressions:

```js
getName(); // Output: Uncaught TypeError: getName is not a function
console.log(getName);
var getName = function() {
  console.log("Namaste JavaScript");
};
```

In this example, the variable declaration `var getName;` is hoisted to the top of the execution context during the memory creation phase, but the function expression `getName = function() { ... };` is not hoisted. As a result, when `getName();` is called before the assignment, JavaScript treats `getName` as `undefined`, and attempting to call `undefined` as a function results in a TypeError.

**Debugging Example:**

Let's use a debugging example to illustrate hoisting further:

```js
var x = 10;

function foo() {
  console.log("x in foo:", x);
  var x = 20;
  console.log("x in foo after declaration:", x);
}

foo();
console.log("x in global:", x);
```

The output of this code will be:

```
x in foo: undefined
x in foo after declaration: 20
x in global: 10
```
