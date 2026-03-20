# Array Method Chaining

Chaining means calling multiple array methods one after another. Each immutable method returns a new array, which the next method acts on.

---

## Basic Chain

```js
const numbers = [5, 3, 8, 1, 9, 2, 7, 4, 6];

const result = numbers
  .filter(n => n > 4)       // [5, 8, 9, 7, 6]
  .map(n => n * 2)           // [10, 16, 18, 14, 12]
  .sort((a, b) => a - b);   // [10, 12, 14, 16, 18]

console.log(result);
```

---

## Real Example: Process Student Data

```js
const students = [
  { name: 'Bruce', score: 82, grade: 'A' },
  { name: 'Clark', score: 45, grade: 'F' },
  { name: 'Diana', score: 91, grade: 'A' },
  { name: 'Barry', score: 38, grade: 'F' },
  { name: 'Arthur', score: 67, grade: 'B' },
];

const topStudentNames = students
  .filter(student => student.score >= 60)    // passing students
  .sort((a, b) => b.score - a.score)         // highest score first
  .map(student => student.name);             // extract names only

console.log(topStudentNames); // ['Diana', 'Bruce', 'Arthur']
```

---

## Chain Ending with `reduce`

```js
const orders = [
  { product: 'Batarang', qty: 3, price: 10 },
  { product: 'Grapple', qty: 1, price: 50 },
  { product: 'Smoke Bomb', qty: 5, price: 5 },
];

const total = orders
  .filter(order => order.qty > 1)              // qty > 1
  .map(order => order.qty * order.price)       // calculate line total
  .reduce((sum, lineTotal) => sum + lineTotal, 0); // sum all

console.log(total); // 3*10 + 5*5 = 55
```

---

## Chain with `flat` and `map` (flatMap)

```js
const sentences = ['hello world', 'foo bar baz'];

const words = sentences
  .map(s => s.split(' '))  // [['hello', 'world'], ['foo', 'bar', 'baz']]
  .flat();                  // ['hello', 'world', 'foo', 'bar', 'baz']

// Or use flatMap (map + flat in one step)
const words2 = sentences.flatMap(s => s.split(' '));
```

---

## Tips

- **Format chains vertically** — one method per line is easier to read
- **Each step should have one clear job** — filter, then transform, then aggregate
- **Don't chain mutable methods** like `sort` without copying first

```js
// Safe sort in a chain
const sorted = [...arr]
  .sort((a, b) => a - b)
  .filter(n => n > 0);
```

- **Name intermediate results** if the chain is complex

```js
const activeUsers = users.filter(u => u.active);
const topActive   = activeUsers.sort((a, b) => b.score - a.score).slice(0, 5);
const topNames    = topActive.map(u => u.name);
```