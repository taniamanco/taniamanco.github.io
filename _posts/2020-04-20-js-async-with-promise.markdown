
Async function
=============
Asynchronous functions operate in a separate order than the rest of the code, returning an implicit Promise as its result. But the syntax and structure of code using async functions look like standard synchronous functions.
The power of async functions becomes more evident when there are multiple steps needed. 

```
function resolveAfter2Seconds() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('I am the promise');
    }, 2000);
  });
}

async function asyncCall() {
  console.log('I am the async function');
  const result = await resolveAfter2Seconds();
  console.log(result);
}

asyncCall();
```

The await keyword is only valid inside async functions.

While the async function is paused, the calling function continues running.
Important to remember is that Async functions always return a promise. 

The purpose of async/await is to simplify using promises synchronously, and to perform some behavior on a group of Promises.

Promise
=======
![promise](../assets/promises.png)

A Promise is in one of these states:

* pending: initial state, neither fulfilled nor rejected.
* fulfilled: meaning that the operation completed successfully.
* rejected: meaning that the operation failed.


As the Promise.prototype.then() and Promise.prototype.catch() methods return promises, they can be chained.
Promises give us an easier way to deal with async in the code. 

A promise comes with some guarantees:
* Callbacks will never be called before the completion of the current run of the JavaScript event loop.
* Callbacks added with .then(), even after the success or failure of the asynchronous operation.
Multiple callbacks may be added by calling .then() several times. Each callback is executed one after another, in the order in which they were inserted.
the .then() function returns a new promise, different from the original:

```
const secondPromise = promise.then(successCallback, failureCallback);

```


resources: https://developer.mozilla.org