# Named Functions vs Anonymous Functions

---

## Named Functions
Have an explicit name identifier.

```js
// Function declaration
function calculateTotal(price, tax) {
  return price + price * tax;
}

// Named function expression
const calculateTotal = function calculateTotal(price, tax) {
  return price + price * tax;
};
```

---

## Anonymous Functions
No name — assigned to a variable or passed inline.

```js
// Anonymous function expression
const calculateTotal = function(price, tax) {
  return price + price * tax;
};

// Anonymous arrow function
const calculateTotal = (price, tax) => price + price * tax;
```

---

## Key Differences

### 1. Stack Traces
Named functions show their name in error stack traces. Anonymous ones show as `anonymous`.

```js
// Anonymous — harder to debug
const process = function() {
  throw new Error('oops');
};

// Stack trace:
// Error: oops
//   at process (app.js:2:9)   ← shows variable name, not function name

// Named — clearer
const process = function processUserData() {
  throw new Error('oops');
};

// Stack trace:
// Error: oops
//   at processUserData (app.js:2:9)   ← named function, more helpful
```

### 2. Recursion
Named functions can reference themselves by name — anonymous ones cannot.

```js
// Anonymous — cannot self-reference
const factorial = function(n) {
  if (n <= 1) return 1;
  return n * factorial(n - 1); // works only via variable
};

// Named — self-reference by name (safer)
const factorial = function fact(n) {
  if (n <= 1) return 1;
  return n * fact(n - 1); // uses its own name
};
```

### 3. Hoisting
Named function declarations are hoisted. Anonymous expressions are not.

```js
greet(); // works — hoisted
function greet() { console.log('Hello'); }

greet(); // TypeError — not hoisted
const greet = function() { console.log('Hello'); };
```

---

## When to Use Each

| Use | Type |
|-----|------|
| Short callbacks (`map`, `filter`) | Anonymous arrow |
| Complex callbacks (reuse, debug) | Named function |
| Standalone utility functions | Named declaration |
| Recursion | Named function expression |
| Methods inside objects | Named shorthand |

```js
// Short callback — anonymous is fine
[1, 2, 3].map(n => n * 2);

// Complex — give it a name
function formatCurrency(amount) {
  return `$${amount.toFixed(2)}`;
}
[10, 20.5, 30].map(formatCurrency);
```