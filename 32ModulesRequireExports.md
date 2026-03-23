# Importing and Exporting Modules (require / module.exports)

Node.js uses the CommonJS module system. Each file is its own module.

---

## `module.exports` — Exporting

### Export a single function
```js
// greet.js
function greet(name) {
  return `Hello, ${name}!`;
}

module.exports = greet;
```

### Export multiple functions
```js
// mathUtils.js
function add(a, b) { return a + b; }
function subtract(a, b) { return a - b; }
function multiply(a, b) { return a * b; }

module.exports = { add, subtract, multiply };
```

### Export an object/class
```js
// config.js
module.exports = {
  host: 'localhost',
  port: 3000,
  db: 'mydb'
};
```

---

## `require` — Importing

### Import a single export
```js
// app.js
const greet = require('./greet');

console.log(greet('Bruce')); // 'Hello, Bruce!'
```

### Import multiple exports
```js
const { add, subtract } = require('./mathUtils');

console.log(add(5, 3));      // 8
console.log(subtract(5, 3)); // 2
```

### Import everything
```js
const math = require('./mathUtils');

console.log(math.add(2, 3)); // 5
console.log(math.multiply(4, 5)); // 20
```

---

## Importing Built-in Node Modules
No path needed for built-ins:
```js
const fs   = require('fs');
const path = require('path');
const http = require('http');
```

---

## Importing npm Packages
```js
const express = require('express');
const lodash  = require('lodash');
```

---

## File Paths

| Path | Meaning |
|------|---------|
| `'./utils'` | Same directory |
| `'../utils'` | One level up |
| `'../../utils'` | Two levels up |
| `'fs'` | Built-in Node module |
| `'express'` | npm package |

---

## How `require` Caches Modules
`require` only executes the file once — subsequent calls return the cached export.

```js
// counter.js
let count = 0;
module.exports = {
  increment() { count++; },
  getCount() { return count; }
};

// a.js
const counter = require('./counter');
counter.increment();

// b.js
const counter = require('./counter'); // same instance!
console.log(counter.getCount()); // 1 — shares state with a.js
```