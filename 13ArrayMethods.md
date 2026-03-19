# Popular Array Utility Methods

> **Mutable** = modifies the original array  
> **Immutable** = returns a new array, original unchanged

---

## Basics

### `Array.pop` — Mutable
Removes and returns the last element.
```js
const arr = [1, 2, 3];
const last = arr.pop();
console.log(last); // 3
console.log(arr);  // [1, 2]
```

### `Array.push` — Mutable
Adds one or more elements to the end. Returns new length.
```js
const arr = [1, 2];
arr.push(3, 4);
console.log(arr); // [1, 2, 3, 4]
```

### `Array.concat` — Immutable
Merges arrays and returns a new array.
```js
const a = [1, 2];
const b = [3, 4];
const result = a.concat(b);
console.log(result); // [1, 2, 3, 4]
console.log(a);      // [1, 2] — unchanged
```

### `Array.slice` — Immutable
Returns a portion of the array.
```js
const arr = [1, 2, 3, 4, 5];
const portion = arr.slice(1, 3); // from index 1, up to (not including) 3
console.log(portion); // [2, 3]
console.log(arr);     // [1, 2, 3, 4, 5] — unchanged
```

### `Array.splice` — Mutable
Removes/replaces/inserts elements in place. Returns removed elements.
```js
const arr = [1, 2, 3, 4, 5];
const removed = arr.splice(1, 2); // start at index 1, remove 2 items
console.log(removed); // [2, 3]
console.log(arr);     // [1, 4, 5]

// Insert
arr.splice(1, 0, 'a', 'b'); // at index 1, remove 0, insert 'a', 'b'
console.log(arr); // [1, 'a', 'b', 4, 5]
```

### `Array.join` — Immutable
Joins all elements into a string.
```js
const words = ['Hello', 'World'];
console.log(words.join(' '));  // 'Hello World'
console.log(words.join('-'));  // 'Hello-World'
console.log(words.join(''));   // 'HelloWorld'
```

### `Array.flat` — Immutable
Flattens nested arrays.
```js
const nested = [1, [2, 3], [4, [5]]];
console.log(nested.flat());    // [1, 2, 3, 4, [5]] — one level
console.log(nested.flat(2));   // [1, 2, 3, 4, 5]   — two levels
console.log(nested.flat(Infinity)); // fully flatten any depth
```

---

## Finding

### `Array.find` — Immutable
Returns first element matching the condition, or `undefined`.
```js
const scores = [10, 45, 82, 33];
const first = scores.find(score => score > 40);
console.log(first); // 45
```

### `Array.indexOf` — Immutable
Returns the index of the first match, or `-1`.
```js
const arr = ['a', 'b', 'c'];
console.log(arr.indexOf('b')); // 1
console.log(arr.indexOf('z')); // -1
```

### `Array.includes` — Immutable
Returns `true` or `false`.
```js
const arr = [1, 2, 3];
console.log(arr.includes(2)); // true
console.log(arr.includes(9)); // false
```

### `Array.findIndex` — Immutable
Returns the index of the first element matching the condition, or `-1`.
```js
const scores = [10, 45, 82, 33];
const index = scores.findIndex(score => score > 40);
console.log(index); // 1
```

---

## Higher Order Functions

### `Array.forEach` — Immutable (no return value)
Iterates — use when you don't need to build a new array.
```js
const names = ['Bruce', 'Clark', 'Diana'];
names.forEach(name => console.log(name));
```

### `Array.filter` — Immutable
Returns new array of elements that pass the test.
```js
const scores = [10, 45, 82, 33, 67];
const passing = scores.filter(score => score >= 50);
console.log(passing); // [82, 67]
```

### `Array.map` — Immutable
Returns new array of transformed values.
```js
const prices = [10, 20, 30];
const discounted = prices.map(price => price * 0.9);
console.log(discounted); // [9, 18, 27]
```

### `Array.reduce` — Immutable
Reduces array to a single value.
```js
const numbers = [1, 2, 3, 4, 5];
const sum = numbers.reduce((acc, n) => acc + n, 0);
console.log(sum); // 15
```

Count occurrences:
```js
const fruits = ['apple', 'banana', 'apple', 'orange', 'banana', 'apple'];
const count = fruits.reduce((acc, fruit) => {
  acc[fruit] = (acc[fruit] || 0) + 1;
  return acc;
}, {});
console.log(count); // { apple: 3, banana: 2, orange: 1 }
```

### `Array.sort` — Mutable
Sorts in place. Default sorts as strings — always provide a compare function for numbers.
```js
const names = ['Bruce', 'Diana', 'Clark'];
names.sort();
console.log(names); // ['Bruce', 'Clark', 'Diana'] — mutates!

const scores = [10, 82, 33, 5];
scores.sort((a, b) => a - b); // ascending
console.log(scores); // [5, 10, 33, 82]

scores.sort((a, b) => b - a); // descending
console.log(scores); // [82, 33, 10, 5]
```

---

## Advanced: Method Chaining
Chain multiple methods — each immutable method returns a new array.
```js
const students = [
  { name: 'Bruce', score: 82 },
  { name: 'Clark', score: 45 },
  { name: 'Diana', score: 91 },
  { name: 'Barry', score: 38 },
];

const topNames = students
  .filter(student => student.score >= 50)   // keep passing students
  .sort((a, b) => b.score - a.score)        // sort by score descending
  .map(student => student.name);            // extract names

console.log(topNames); // ['Diana', 'Bruce']
```