# let, var, const

---

## `const`
Cannot be reassigned. Use by default.
```js
const name = 'Md';
name = 'Mudassir'; // TypeError: Assignment to constant variable
```

Objects/arrays declared with `const` can still be mutated:
```js
const person = { name: 'Md' };
person.name = 'Mudassir'; // OK — mutating, not reassigning
person = {};           // TypeError
```

---

## `let`
Can be reassigned. Use when the value needs to change.
```js
let score = 0;
score = 10; // OK
```

Block-scoped:
```js
for (let i = 0; i < 3; i++) {
  console.log(i); // 0, 1, 2
}
console.log(i); // ReferenceError
```

---

## `var`
Function-scoped, hoisted, no block scope. **Avoid using it.**
```js
var x = 1;

if (true) {
  var x = 2; // overwrites the outer x
}

console.log(x); // 2 — unexpected!
```

---

## Quick Comparison

| Feature        | `var`      | `let`      | `const`    |
|----------------|------------|------------|------------|
| Scope          | Function   | Block      | Block      |
| Reassignable   | Yes        | Yes        | No         |
| Hoisted        | Yes (undefined) | Yes (TDZ) | Yes (TDZ) |
| Re-declarable  | Yes        | No         | No         |

> **Rule of thumb:** Use `const` by default. Use `let` only when reassignment is needed. Never use `var`.