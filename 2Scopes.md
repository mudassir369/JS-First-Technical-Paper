# Scopes in JavaScript

Scope determines where a variable is accessible.

---

## Global Scope
Declared outside any function or block. Accessible everywhere.
```js
const city = 'Moradabad';

function printCity() {
  console.log(city); // 'Moradabad'
}
```

---

## Function Scope
Variables declared inside a function are only accessible within it.
```js
function getHero() {
  const name = 'Mudassir';
  console.log(name); // 'Mudassir'
}

console.log(name); // ReferenceError: name is not defined
```

---

## Block Scope
`let` and `const` are scoped to the nearest `{}` block.
```js
if (true) {
  let state = 'Uttar Pradesh';
  console.log(state); // 'Uttar Pradesh'
}

console.log(state); // ReferenceError
```

`var` is NOT block-scoped --- it leaks out of blocks:
```js
if (true) {
  var state = 'Uttar Pradesh';
}
console.log(state); // 'Uttar Pradesh' — leaks!
```

---

## Lexical Scope
Inner functions have access to outer function variables.
```js
function outer() {
  const name = 'Md Mudassir';

  function inner() {
    console.log(name); // accessible 
  }

  inner();
}
```
