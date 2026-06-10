# AMA questions and answers

## 1. Difference between `throw` and `throw new Error()`

### `throw`

Throws any value (string, number, object, etc.).

```javascript
throw "Something went wrong";
throw 404;
throw { message: "Error" };
```

### `throw new Error()`

Creates and throws an Error object with useful debugging information like stack trace.

```javascript
throw new Error("Something went wrong");
```

| `throw`                        | `throw new Error()`              |
| ------------------------------ | -------------------------------- |
| Can throw any value            | Throws an Error object           |
| Less debugging information     | Includes message and stack trace |
| Not recommended for production | Preferred approach               |

---

## 2. What are Higher Order Functions (HOF)?

A higher order function is a function that:

* accepts another function as an argument, or
* returns another function.

Example:

```javascript
const numbers = [1, 2, 3];

numbers.map(num => num * 2);
```

Here `map()` is a higher order function because it receives a callback function.

Other examples:

* `map()`
* `filter()`
* `reduce()`
* `forEach()`

---

## 3. What is Currying?

Currying converts a function with multiple arguments into multiple functions that each take one argument.

Without currying:

```javascript
function add(a, b) {
    return a + b;
}

add(2, 3);
```

With currying:

```javascript
function add(a) {
    return function(b) {
        return a + b;
    };
}

add(2)(3); // 5
```

Benefits:

* Function reuse
* Partial application
* Cleaner functional programming

---

## 4. Difference between `Map` and `WeakMap`

| Map                                 | WeakMap                                                    |
| ----------------------------------- | ---------------------------------------------------------- |
| Keys can be any type                | Keys must be objects                                       |
| Iterable                            | Not iterable                                               |
| Has `size` property                 | No `size` property                                         |
| Prevents garbage collection of keys | Keys can be garbage collected if no other reference exists |

Example:

```javascript
const map = new Map();
map.set("name", "John");

const weakMap = new WeakMap();
const obj = {};
weakMap.set(obj, "data");
```

---

## 5. What does `export` do?

`export` makes variables, functions, or classes available to other files.

```javascript
// math.js
export function add(a, b) {
    return a + b;
}
```

Importing:

```javascript
import { add } from "./math.js";
```

It enables modular and reusable code.

---

## 6. Why do we use asynchronous programming?

Without async programming:

* Every task waits for the previous one.
* Slow operations block the application.

With async programming:

* Long operations (API calls, file reading, timers) happen in the background.
* JavaScript can continue executing other code.

```javascript
console.log("Start");

setTimeout(() => {
    console.log("Done");
}, 2000);

console.log("End");
```

Output:

```
Start
End
Done
```

This keeps applications responsive.

---

## 7. Can we use `await` outside an async function?

Normally **No**.

```javascript
await fetch(url); // ❌ SyntaxError
```

Inside async function:

```javascript
async function getData() {
    const res = await fetch(url);
}
```

Modern ES modules also support **top-level await**:

```javascript
const res = await fetch(url);
```

but only in module files.

---

## 8. What are Web APIs in the browser?

Web APIs are features provided by the browser, not JavaScript itself.

Examples:

* DOM API
* Fetch API
* Local Storage
* Geolocation
* `setTimeout()`

When JavaScript calls them, the browser handles the operation and returns the result later through the event loop.

---

## 9. Difference between Rest and Spread Operator (`...`)

### Spread

Expands elements.

```javascript
const arr1 = [1, 2];
const arr2 = [...arr1, 3];
```

Output:

```
[1, 2, 3]
```

### Rest

Collects multiple values into one array.

```javascript
function sum(...nums) {
    return nums;
}

sum(1, 2, 3);
```

Output:

```
[1, 2, 3]
```

| Spread                                  | Rest                                                 |
| --------------------------------------- | ---------------------------------------------------- |
| Expands values                          | Collects values                                      |
| Used in arrays, objects, function calls | Used mainly in function parameters and destructuring |

---

## 10. Difference between Callback and Higher Order Function

### Callback

A function passed as an argument.

```javascript
function greet() {
    console.log("Hello");
}

setTimeout(greet, 1000);
```

`greet` is the callback.

### Higher Order Function

A function that accepts or returns another function.

```javascript
numbers.map(num => num * 2);
```

`map()` is the higher order function.

**Relationship:** A callback is often passed into a higher order function.

---

## 11. Difference between Package and Dependencies

### Package

Any reusable JavaScript project/library published to npm.

Examples:

* Express
* React
* Lodash

### Dependencies

Packages that **your project requires**.

```json
{
  "dependencies": {
    "express": "^5.0.0"
  }
}
```

So:

* **Package** → reusable module.
* **Dependency** → package your project depends on.

---

## 12. What are `setTimeout()` and `setInterval()`?

### `setTimeout()`

Runs a function **once** after a delay.

```javascript
setTimeout(() => {
    console.log("Hello");
}, 2000);
```

### `setInterval()`

Runs a function **repeatedly** at fixed intervals.

```javascript
setInterval(() => {
    console.log("Hello");
}, 2000);
```

To stop it:

```javascript
const id = setInterval(fn, 1000);

clearInterval(id);
```

---

## 13. What does an async function return?

An async function **always returns a Promise**.

```javascript
async function test() {
    return 10;
}
```

Actually returns:

```javascript
Promise.resolve(10)
```

Example:

```javascript
test().then(value => {
    console.log(value); // 10
});
```

---

## 14. Why do we need the DOM?

The DOM (Document Object Model) represents an HTML page as a tree of JavaScript objects.

It allows JavaScript to:

* Read page content
* Modify elements
* Change styles
* Handle events
* Create or remove elements dynamically

Example:

```javascript
document.getElementById("title").textContent = "Welcome";
```

Without the DOM, JavaScript could not interact with or update web pages.

---

## 15. Why do we need the Critical Rendering Path?

The Critical Rendering Path (CRP) is the sequence the browser follows to display a page.

```
HTML
   ↓
DOM
   ↓
CSS
   ↓
CSSOM
   ↓
Render Tree
   ↓
Layout
   ↓
Paint
   ↓
Display
```

Understanding the CRP helps developers:

* Reduce page load time
* Improve First Contentful Paint (FCP)
* Avoid render-blocking resources
* Optimize CSS and JavaScript loading
* Deliver a faster user experience

In short, optimizing the Critical Rendering Path directly improves website performance and perceived speed.
