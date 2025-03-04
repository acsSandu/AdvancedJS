# JS Tecniques Tricks and Operators

**!!! This project acts only as a self reminder of some js techniques in an attempt to write better cleaner code**

1. Use `let` and `const` Instead of `var`

   Avoid using `var` to declare variables. Instead, use `let` and `const` to ensure block-scoping and avoid hoisting issues.

```js
let name = "nome";
const age = 31;
```

2. Destructuring

   - Use it with default values to make code more robust.
   - Use it to extract values from arrays or properties from objects into distinct variables.

```js
// Default Values
const user = { name: "Alice" };
const { name, age = 25 } = user;

// Extraction
const person = { name: "Jane", age: 25 };
const { name, age } = person;

const numbers = [1, 2, 3];
const [first, second] = numbers;
```

3. Template Literals

   Template literals provide an easy way to interpolate variables and expressions into strings.

```js
const name = "John";
const greeting = `Hello, ${name}!`;
```

4. Default Parameters

   Set default values for function parameters to avoid `undefined` errors.

```js
function greet(name = "Guest") {
  return `Hello, ${name}!`;
}
```

5. Arrow Functions

   Arrow functions provide a concise syntax and lexically bind the `this` value.

```js
const getAllKeysFromObject = (obj) => Object.keys(obj);
```

6. Spread Operator `…`

   The spread operator allows you to expand elements of an iterable (like an array) or properties of an object.

```js
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5];

const obj1 = { name: "John" };
const obj2 = { ...obj1, age: 30 };
```

7. Rest Parameters `…`

   Rest parameters allow you to represent an indefinite number of arguments as an array.

```js
const getSumOfAllInputs = (...numbers) =>
  numbers.reduce((total, num) => total + num, 0);
```

8. Short-Circuit Evaluation && and ||

   Use short-circuit evaluation for conditional expressions and default values.

```js
---
const user = { name: 'John' };
const name = user.name || 'Guest';
---
const isAdmin = user.isAdmin && loadAdminOptions();
---
const isAuthenticated = true;
isAuthenticated && console.log("User is authenticated");
---
const fallback = "default";
const data = null || fallback;
console.log(data); // default
```

9. Object Property Shorthand

   Use shorthand syntax to create objects

```js
const name = "John";
const obj2 = { name, age: 30 };
```

10. Optional Chaining (?.) for Deep Object Access

    The optional chaining operator (?.) simplifies accessing nested properties without worrying about undefined errors.
    Useful in api calls.
    This removes the need for lengthy if checks and makes your code cleaner.

```js
const user = { address: { city: "New York" } };
console.log(user.address?.city); // New York
console.log(user.profile?.age); // undefined
```

11. Nullish Coalescing (??)

    While || is often used for fallback values, it treats 0, false, and '' as falsy. The ?? operator only checks for null or undefined.
    This subtle distinction can prevent unexpected behavior in logical operations.

```js
const value = 0;
console.log(value || 10); // 10 (fallback applied)
console.log(value ?? 10); // 0  (fallback not applied)
```

12. Array Methods: map(), filter(), reduce()

    Use array methods like `map()`, `filter()`, and `reduce()` to perform common operations on arrays in a functional way.

```js
const numbers = [1, 2, 3, 4, 5];

const doubled = numbers.map((num) => num * 2);
const evens = numbers.filter((num) => num % 2 === 0);
const sum = numbers.reduce((total, num) => total + num, 0);
```

13. Promise Chaining and Async/Await

    Handle asynchronous operations using Promises and the async/await syntax for cleaner, more readable code.

```js
// Promises
fetch("https://api.example.com/data")
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error("Error:", error));

// Async/Await
async function fetchData() {
  try {
    const response = await fetch("https://api.example.com/data");
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("Error:", error);
  }
}
```

14. Debouncing and Throttling for Performance

    Debouncing and throttling are vital for optimizing event handling.

    - Debouncing: Executes a function after a delay, resetting the timer if invoked again during the delay.
    - Throttling: Limits the function execution to once per specified interval.

```js
const debounce = (fn, delay) => {
  let timer;
  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => fn(...args), delay);
  };
};

const onResize = debounce(() => console.log("Resized!"), 300);
window.addEventListener("resize", onResize);

const throttle = (fn, interval) => {
  let lastTime = 0;
  return (...args) => {
    const now = Date.now();
    if (now - lastTime >= interval) {
      lastTime = now;
      fn(...args);
    }
  };
};

const onScroll = throttle(() => console.log("Scrolling!"), 500);
window.addEventListener("scroll", onScroll);
```

15. Using `for…of` for Iteration

Use the `for…of` loop for more readable iteration over arrays, strings, and other iterable objects. Use it as a fallback for empty arrays

```js
const numbers = [1, 2, 3, 4, 5];

for (const number of numbers) {
  console.log(number);
}
```

16. Cloning Objects and Arrays

Use the spread operator or `Object.assign()` to clone objects and arrays.

```js
const original = { name: "John", age: 30 };
const clone = { ...original };

const arr = [1, 2, 3];
const arrClone = [...arr];
```

17. Dynamic Property Names

Use computed property names to dynamically set object properties.
This is particularly handy for creating objects from user input or external data.

```js
const key = "dynamicKey";
const obj = {
  [key]: "value",
};
```

18. Using `setTimeout` and `setInterval`

Schedule code execution using `setTimeout` and `setInterval`.

```js
setTimeout(() => {
  callbackFun();
}, 2000);

const intervalId = setInterval(() => {
  callForUpdates();
}, 3000);

// To clear the interval
clearInterval(intervalId);
```

19. Asynchronous Iteration with for await...of

Handling asynchronous data streams is seamless with for await...of.
This pattern simplifies working with APIs, streams, and other asynchronous tasks.

```js
async function* fetchData() {
  yield await fetch("https://api.example.com/data1").then((res) => res.json());
  yield await fetch("https://api.example.com/data2").then((res) => res.json());
}

(async () => {
  for await (const data of fetchData()) {
    console.log(data);
  }
})();
```

20. Bonus: Memoization with Closures

Memoization is a technique to cache expensive function calls. JavaScript closures make this elegant.
This is a practical optimization for repetitive computational tasks.

```js
const memoizedUserData = (() => {
  const cache = {};
  return (userId) => {
    const key = `${userId}`;
    if (cache[key]) return cache[key];
    const userData = fetchUserData(userId);
    cache[key] = userData;
    return userData;
  };
})();

console.log(memoizedUserData("fgh_123")); // (calculated)
console.log(memoizedUserData("fgh_123")); // (cached)
```

21. Custom Map Iteration with forEach

Map objects maintain the insertion order of keys and allow for custom iterations.
Unlike plain objects, Map supports non-string keys and preserves order, making it ideal for advanced use cases.

````js
const map = new Map([
  ["key1", "value1"],
  ["key2", "value2"],
]);

map.forEach((value, key) => {
  console.log(`${key}: ${value}`);
});
```js
````
