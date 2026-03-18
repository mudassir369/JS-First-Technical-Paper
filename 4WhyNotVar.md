# Why We Must Not Use `var`

---

## 1. No Block Scope
`var` leaks out of blocks like `if`, `for`, `while`.
```js
for (var i = 0; i < 3; i++) {}
console.log(i); // 3 — leaked out of the loop
```

With `let`:
```js
for (let i = 0; i < 3; i++) {}
console.log(i); // ReferenceError — contained
```

---

## 2. Can Be Re-declared
Silently overwrites existing variables with no error.
```js
var user = 'Md';
var user = 'Mudassir'; // no error — dangerous
console.log(user);  // 'Mudassir'
```

`let` and `const` throw an error:
```js
let user = 'Md';
let user = 'Mudassir'; // SyntaxError
```

---

## 3. Hoisting Causes Confusion
`var` is hoisted and initialized as `undefined`, leading to silent bugs.
```js
console.log(name); // undefined — no error, just wrong
var name = 'Mudassir';
```

`let` throws a clear error instead:
```js
console.log(name); // ReferenceError: Cannot access before initialization
let name = 'Mudassir';
```

---

## 4. Pollutes the Global Object
In browsers, `var` at the top level attaches to `window`.
```js
var city = 'Moradabad';
console.log(window.city); // 'Moradabad' — pollutes global
```

`let` and `const` do not:
```js
let city = 'Moradabad';
console.log(window.city); // undefined — clean
```

---

## Summary
`var` was the original way to declare variables before ES6 (2015). `let` and `const` were introduced to fix all its problems. There is no reason to use `var` in modern JavaScript.