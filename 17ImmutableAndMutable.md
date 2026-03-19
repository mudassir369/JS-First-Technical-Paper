# Immutable and Mutable Methods

## What is Mutability?

**Mutable** = the original value is changed in place.  
**Immutable** = the original value is not changed; a new value is returned.

---

## Mutable Array Methods
These modify the original array:

```js
const arr = [3, 1, 2];

arr.push(4);      // [3, 1, 2, 4]
arr.pop();        // [3, 1, 2]
arr.shift();      // [1, 2]        — removes first
arr.unshift(0);   // [0, 1, 2]    — adds to start
arr.splice(1, 1); // [0, 2]       — removes at index 1
arr.sort();       // [0, 2]       — sorts in place
arr.reverse();    // [2, 0]       — reverses in place
```

---

## Immutable Array Methods
These return a new array — original is untouched:

```js
const arr = [1, 2, 3, 4, 5];

arr.map(n => n * 2);        // [2, 4, 6, 8, 10]  — new array
arr.filter(n => n > 2);     // [3, 4, 5]          — new array
arr.slice(1, 3);             // [2, 3]             — new array
arr.concat([6, 7]);          // [1, 2, 3, 4, 5, 6, 7] — new array
arr.flat();                  // [1, 2, 3, 4, 5]   — new array

console.log(arr); // [1, 2, 3, 4, 5] — unchanged
```

---

## Why it Matters

Mutating data unexpectedly leads to hard-to-find bugs.

```js
// Bug — sort mutates the original
const scores = [82, 45, 91, 33];
const sorted = scores.sort((a, b) => a - b);
console.log(scores);  // [33, 45, 82, 91] — original changed!
console.log(sorted);  // [33, 45, 82, 91] — same reference
```

Safe version using spread to copy first:
```js
const scores = [82, 45, 91, 33];
const sorted = [...scores].sort((a, b) => a - b);
console.log(scores); // [82, 45, 91, 33] — original safe
console.log(sorted); // [33, 45, 82, 91]
```

---

## Immutable Object Operations

```js
const person = { name: 'Bruce', age: 36 };

// Mutable — modifies original
person.age = 37;

// Immutable — returns new object
const updated = { ...person, age: 37 };
console.log(person);  // { name: 'Bruce', age: 36 } — unchanged
console.log(updated); // { name: 'Bruce', age: 37 }
```

---

## Quick Reference

| Method         | Mutable? |
|----------------|----------|
| `push`         |  Yes   |
| `pop`          |  Yes   |
| `splice`       |  Yes   |
| `sort`         |  Yes   |
| `reverse`      |  Yes   |
| `map`          |  No    |
| `filter`       |  No    |
| `slice`        |  No    |
| `concat`       |  No    |
| `reduce`       |  No    |
| `flat`         |  No    |