# Passing Functions to Other Functions

Functions in JavaScript are first-class values — they can be stored in variables, passed as arguments, and returned from other functions.

---

## Basic Example

```js
function greet(name) {
  return `Hello, ${name}!`;
}

function runWithBruce(fn) {
  return fn('Bruce'); // invoke the passed function
}

console.log(runWithBruce(greet)); // 'Hello, Bruce!'
```

---

## Invoking On Demand

The receiving function controls when and how the passed function is called.

```js
function withDelay(fn, ms) {
  setTimeout(fn, ms); // invokes fn after delay
}

withDelay(() => console.log('Fired!'), 1000);
```

```js
function repeat(fn, times) {
  for (let i = 0; i < times; i++) {
    fn(i); // invoked multiple times
  }
}

repeat(i => console.log(`Run ${i}`), 3);
// Run 0
// Run 1
// Run 2
```

---

## Callback Pattern

A callback is a function passed to another function to be called later.

```js
function fetchData(url, onSuccess, onError) {
  try {
    const data = getData(url);
    onSuccess(data);       // invoke on success
  } catch (error) {
    onError(error);        // invoke on failure
  }
}

fetchData(
  '/api/users',
  data => console.log('Got data:', data),
  error => console.error('Failed:', error.message)
);
```

---

## Higher Order Functions

A function that receives or returns another function.

```js
function multiplier(factor) {
  return function(number) {   // returns a function
    return number * factor;
  };
}

const double = multiplier(2);
const triple = multiplier(3);

console.log(double(5));  // 10
console.log(triple(5));  // 15
```

---

## Passing Named vs Anonymous Functions

```js
function processItems(items, transform) {
  return items.map(transform);
}

// Named function
function double(n) { return n * 2; }
processItems([1, 2, 3], double); // [2, 4, 6]

// Anonymous arrow function
processItems([1, 2, 3], n => n * 2); // [2, 4, 6]
```

---

## Practical: Event-like System

```js
function createButton(label, onClick) {
  return {
    label,
    click() {
      onClick(label); // invoke the callback with context
    }
  };
}

const btn = createButton('Submit', label => {
  console.log(`${label} was clicked`);
});

btn.click(); // 'Submit was clicked'
```

---

## Practical: Validator Pattern

```js
function validate(value, ...validators) {
  for (const validator of validators) {
    const error = validator(value); // each validator is a function
    if (error) return error;
  }
  return null;
}

const isRequired = v => (!v ? 'Required' : null);
const minLength = min => v => (v.length < min ? `Min ${min} chars` : null);
const isEmail = v => (!v.includes('@') ? 'Invalid email' : null);

validate('', isRequired);              // 'Required'
validate('hi', minLength(5));          // 'Min 5 chars'
validate('bruce', minLength(3), isEmail); // 'Invalid email'
validate('bruce@wayne.com', isRequired, isEmail); // null — valid
```