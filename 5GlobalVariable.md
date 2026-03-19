# Why Using Global Variables is Bad

---

## 1. Name Collisions
Any part of your code (or a library) can overwrite a global.
```js
// file1.js
var user = 'Md';

// file2.js (runs later)
var user = 'Mudassir'; // silently overwrites

// file3.js
console.log(user); // 'Mudassir' — unexpected!
```

---

## 2. Hard to Debug
When a global changes, it's difficult to trace where it happened.
```js
let score = 0;

function addPoints() { score += 10; }
function applyPenalty() { score -= 5; }
function resetGame() { score = 0; }

// After 100 function calls, what is score? Hard to know.
```

Prefer passing values explicitly:
```js
function addPoints(score) { return score + 10; }
function applyPenalty(score) { return score - 5; }

let score = addPoints(0);  // explicit, traceable
```

---

## 3. Tight Coupling
Functions that rely on globals are harder to reuse and test.
```js
// Bad — depends on global
let discount = 0.1;
function getPrice(price) {
  return price - price * discount; // relies on global
}

// Good — self-contained
function getPrice(price, discount) {
  return price - price * discount;
}
```

---

## 4. Memory
Globals live for the entire lifetime of the program and are never garbage collected.

