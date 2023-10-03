## Promises
```jsx
const cart=["shoes","pants","kurta"];
 createOrder(cart);//returns orderId
 proceedToPayment(orderId);
```
- Both apis are asynchronous and proceedToPayment func depends on createOrder.
- To handle this dependency in asynchronous code, we typically use techniques like callbacks, Promises, or async/await, as mentioned in the previous response. These techniques ensure that proceedToPayment is called only after createOrder has completed its asynchronous operation and provided the necessary data (orderId) for payment processing.

## How to handle async operation using callback
```jsx
createOrder(cart,function(orderId){
  proceedToPayment(orderId) 
  });
```
The code you've provided demonstrates a common scenario in asynchronous programming, where you have two asynchronous functions, createOrder and proceedToPayment, and proceedToPayment depends on the result of createOrder. You've used a callback function to handle this situation, but there's a potential issue known as "inversion of control." Let's explain this concept further.
Inversion of control is a programming principle where the control over the flow of a program is shifted from the main program to external components or functions. In your case, the callback function you've provided for createOrder is a form of inversion of control because it allows the createOrder function to dictate when it will call the callback. Here's how it works:
You call createOrder(cart, function(orderId) {...}), passing a callback function as an argument.
Inside the createOrder function, at some point in the future when the order is created, it calls the provided callback function and passes the orderId as an argument.
The callback function, which is now executed, calls proceedToPayment(orderId) to proceed with the payment.
The potential issue with this approach is that it can lead to callback hell or deeply nested callback functions, especially if you have more asynchronous operations to perform or if you need to handle errors. This can make the code harder to read, understand, and maintain.

To address the issue of inversion of control and make your code more readable, you can consider using modern JavaScript features such as Promises or async/await.



```jsx
const promise=createOrder(cart); //Attaching callback function to promise object
promise.then(function(orderId){  //`then` is the function available over promise object
proceedToPayment(orderId)})
```
or

```jsx
  createOrder(cart).then(function(orderId){
  proceedToPayment(orderId); 
  })
```
1. **Promise Object**: A Promise is an object representing the eventual completion or failure of an asynchronous operation. It serves as a placeholder for the result of that operation, which may not be available immediately. A Promise can be in one of three states: pending, resolved (fulfilled), or rejected.

2. **Promise Structure**: As you mentioned, a Promise typically has two main properties: `data` (or `value`) and `state`. The `data` property holds the result of the operation once it's completed, and the `state` property indicates whether the Promise is pending, resolved, or rejected.

3. **Automatic Callback Execution**: When you attach a `.then()` handler to a Promise, as in your example, the callback function you provide inside `.then()` is automatically called when the Promise's state transitions from pending to resolved (fulfilled). This happens when the asynchronous operation initiated by the Promise (in this case, the `createOrder` API call) successfully completes.

So, in your code:

```javascript
createOrder(cart).then(function(orderId) {
  proceedToPayment(orderId); 
})
```
- `createOrder(cart)` returns a Promise that represents the eventual result of the `createOrder` API call.
- When the `createOrder` operation completes successfully, the Promise's state changes to resolved (fulfilled), and the `then` callback function is automatically executed with the `orderId` as its argument.
- Inside the `then` callback, you proceed to call `proceedToPayment(orderId)`, which can safely use the `orderId` returned by `createOrder`.

This way, Promises make it easier to handle asynchronous operations in a more linear and readable fashion compared to nested callbacks, as they allow you to express the sequence of actions more clearly and handle errors uniformly with `.catch()`.

## Example:-
```jsx
const GITHUB_API = "https://api.github.com/users/krabhi1729";
const user = fetch(GITHUB_API); //check it what it returning by putting debugger here
// We use the `fetch` function, which is a built-in function provided by web browsers for making HTTP requests. You pass the `GITHUB_API` URL as an argument to `fetch`. The `fetch` function initiates an HTTP request to the specified URL and returns a Promise that represents the eventual result of that request. In this case, it will be a Promise representing the response from the GitHub API.

console.log(user);//returns promise object 
// At this point, you log the `user` variable to the console. However, the `user` variable holds a Promise object, which represents an asynchronous operation that may not have completed yet. Therefore, when you log it to the console, you see the Promise object's initial state, which is `"pending"`. This is because JavaScript executes code in a non-blocking manner, and the `fetch` function has not resolved the Promise yet, as it is still waiting for the API response.
```

```jsx
Promise{<pending>}
[[Prototype]]
 : 
Promise
[[PromiseState]]
 : 
"fulfilled"
[[PromiseResult]]
 :
```
-There are three states of promises:pending,fullfilled,rejected
-Promise object brings lot of trust in transaction because js guareentees that promise object can only be resolved once either it will be success or failure
-Promise object are immutable i.e no one can mutate the  data inside promise

## Promise also help in resolving callback hell issue.

```javascript
const cart = ["shoes", "pants", "kurta"];
createOrder(cart, function (orderId) {
  proceedToPayment(orderId, function (paymentInfo) {
    showOrderSummary(paymentInfo, function () {
      updateWalletBalance();
    });
  });
});
```
  -This is callback hell,our code starts to grow horizontally instead overtically,this is also known as pyramid of doom
  -This problem is solved or handled with the help of promise chaining,we always return promise from in promise when chaining it

`Promise Chaining Example:`

```javascript
createOrder(cart)
  .then(function (orderId) {
    return proceedToPayment(orderId);
  })
  .then(function (paymentInfo) {
    return showOrderSummary(paymentInfo);
  })
  .then(function () {
    return updateWalletBalance();
  });
```

OR

```jsx
 createOrder(cart)
  .then((orderId) => proceedToPayment(orderId))
  .then((paymentInfo) =>showOrderSummary(paymentInfo))
  .then((paymentInfo)  =>  updateWlletBalance(paymentInfo));
```
If any Promise in the chain rejects (encounters an error), the control is passed to the nearest .catch() or the next .then() with a rejection handler, allowing for error handling.
Using Promise chaining helps organize and simplify asynchronous code, making it more readable and maintainable compared to deeply nested callbacks. It's an important technique in modern JavaScript for managing asynchronous operations.

## Handling Promises: Creating and Consuming Promises in JavaScript

```javascript
const cart = ["shoes", "pants", "kurta"]; //defining an array cart that contains items to create an order for.
const promise = createOrder(cart); //calling the createOrder function, passing the cart array as an argument. This function returns a Promise that represents the asynchronous operation of creating an order.
console.log(promise); //print pending since createOrder api will take 5 sec to resolve by that time promise object will be in pending state
```
## How the Promise is produced:

```javascript
function createOrder(cart) {
  const pr = new Promise(function (resolve, reject) {
    // Promise constructor takes a function with parameters resolve and reject
    // Logic for handling what we need to do inside this function

    // Validate cart
    if (!validateCart(cart)) {
      const err = new Error("Cart is not valid");
      reject(err); // Reject the Promise with an error if the cart is not valid
    }

    // Logic for creating an order
    const orderId = "12345";
    if (orderId) {
      setTimeout(function () {
        resolve(orderId); // Resolving the Promise with an orderId after 5000 ms (5 seconds)
      }, 5000);
    }
  });

  return pr; // Return the Promise
}
```
A new Promise is created using the Promise constructor, which takes a function as an argument. This function has two parameters: resolve and reject. These are callback functions provided by JavaScript to indicate the outcome of the asynchronous operation.
The validateCart function is called to check if the cart is valid. If it's not valid, the Promise is rejected with an error using reject(err).
If the cart is valid, an orderId is generated (in this example, it's hardcoded as "12345"). After a delay of 5 seconds (simulated using setTimeout), the Promise is resolved with the orderId using resolve(orderId).
Finally, the Promise pr is returned from the createOrder function.

The consumer of this Promise can then use .then() to handle the resolved value (in this case, the orderId) and .catch() to handle any potential errors. In your example, you've used .then() to log the orderId when it's resolved.

```javascript
const cart = ["shoes", "pants", "kurta"];
const promise = createOrder(cart); // orderId
promise
  .then(function (orderId) {
    // This callback will be executed when the Promise is resolved successfully.
    console.log("Order ID:", orderId);
  })
  .catch(function (error) {
    // This callback will be executed if the Promise is rejected (encounters an error).
    console.error("Error:", error.message);
  });
```
In this code:

- The .then() method is chained to the promise object. Inside its callback function, you can access the resolved orderId and perform any actions you need. In this case, it logs the orderId.
- The .catch() method is also chained to the promise object. Inside its callback function, you can handle errors that may occur during the Promise's execution. If the Promise is rejected with an error (for example, when the cart is not valid), this callback will be executed, and it logs the error message.
- With this structure, you can cleanly separate your success and error handling logic. When the Promise is resolved successfully, the .then() callback is executed, and when an error occurs (the Promise is rejected), the .catch() callback handles it.

## Note:-
`In promise chaining, we use return from the top of the chain what we need down the chain`
```jsx
const cart = ["shoes", "pants", "kurta"];
createOrder(cart) //orderId
  .then(function (orderId) {
    console.log(orderId);
    return orderId;
  })
  .then(function (orderId) {
    return proceedToPayment(orderId); // caution: in promise chaining, we use return from the top of the chain what we need down the chain
  })
  .then(function (paymentInfo) {
    console.log(paymentInfo);
  })
  .catch(function (err) {
    // catch will handle any error down the chain, and if there is a then method after catch, it will get executed.
    console.log(err.message);
  });
```


