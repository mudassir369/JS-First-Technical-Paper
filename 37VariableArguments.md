# Variable Number of Arguments

---

## Rest Parameters (`...args`)
Collects all remaining arguments into an array. The modern, preferred approach.

```js
function sum(...numbers) {
  return numbers.reduce((acc, n) => acc + n, 0);
}

console.log(sum(1, 2, 3));          // 6
console.log(sum(1, 2, 3, 4, 5));    // 15
console.log(sum());                  // 0
```

### Fixed + Variable Arguments
```js
function log(level, ...messages) {
  messages.forEach(msg => console.log(`[${level}] ${msg}`));
}

log('INFO', 'Server started', 'Listening on port 3000');
// [INFO] Server started
// [INFO] Listening on port 3000

log('ERROR', 'Connection failed');
// [ERROR] Connection failed
```

### Rest Must Be Last
```js
// Bad
function bad(...args, last) {} // SyntaxError

// Good
function good(first, ...rest) {
  console.log(first); // first argument
  console.log(rest);  // all remaining
}

good('a', 'b', 'c', 'd');
// 'a'
// ['b', 'c', 'd']
```

---

## `arguments` Object (Old Way — Regular Functions Only)
An array-like object available in regular functions. Not available in arrow functions.

```js
function sum() {
  let total = 0;
  for (let i = 0; i < arguments.length; i++) {
    total += arguments[i];
  }
  return total;
}

console.log(sum(1, 2, 3)); // 6
```

Problems with `arguments`:
- Not a real array — can't use `map`, `filter`, etc.
- Not available in arrow functions
- Confusing and outdated

Prefer rest parameters instead:
```js
// Instead of arguments
function sum(...nums) {
  return nums.reduce((acc, n) => acc + n, 0); // nums is a real array
}
```

---

## Practical Examples

### Accept any number of items to merge
```js
function mergeObjects(...objects) {
  return Object.assign({}, ...objects);
}

const result = mergeObjects(
  { name: 'Bruce' },
  { city: 'Gotham' },
  { role: 'admin' }
);
console.log(result); // { name: 'Bruce', city: 'Gotham', role: 'admin' }
```

### Validate with any number of validators
```js
function validate(value, ...validators) {
  for (const validator of validators) {
    const error = validator(value);
    if (error) return error;
  }
  return null;
}

const isRequired = v => (!v ? 'Required' : null);
const isPositive = v => (v < 0 ? 'Must be positive' : null);

validate(-5, isRequired, isPositive); // 'Must be positive'
validate(10, isRequired, isPositive); // null — valid
```

### Logging with severity
```js
function createLogger(prefix) {
  return function(...args) {
    console.log(`[${prefix}]`, ...args);
  };
}

const info  = createLogger('INFO');
const error = createLogger('ERROR');

info('Server started', 'port', 3000);  // [INFO] Server started port 3000
error('DB connection failed');          // [ERROR] DB connection failed
```