# Data Types in JavaScript

JavaScript has **8 data types**: 7 primitives and 1 object type.

---

## Primitives

### String
```js
const name = 'Md Mudassir';
const city = "Moradabad";
const greeting = `Hello, ${name}`; // template literal
```

### Number
```js
const age = 36;
const pi = 3.14;
const invalid = NaN;    
const big = Infinity;
```

### BigInt
For integers larger than `Number.MAX_SAFE_INTEGER`.
```js
const big = 9007199254740991n;
```

### Boolean
```js
const isHero = true;
const isVillain = false;
```

### undefined
A variable declared but not assigned.
```js
let x;
console.log(x); // undefined
```

### null
Intentional absence of a value.
```js
const result = null;
```

### Symbol
Unique identifier, rarely used in day-to-day code.
```js
const id = Symbol('id');
```

---

## Object
Everything else - arrays, functions, plain objects - is an object.
```js
const person = { name: 'Mudassir', age: 24 };
const items  = [1, 2, 3];
const greet  = function() {};
```

---

## Checking Types

```js
typeof 'hello'       // 'string'
typeof 42            // 'number'
typeof true          // 'boolean'
typeof undefined     // 'undefined'
typeof null          // 'object'  
typeof {}            // 'object'
typeof []            // 'object'
typeof function(){}  // 'function'
```

> Use `Array.isArray([])` to check for arrays since `typeof []` returns `'object'`.