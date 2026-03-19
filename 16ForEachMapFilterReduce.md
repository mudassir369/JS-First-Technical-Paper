# When to Use forEach vs map, filter, reduce

## Use `forEach` when:
- You want to **do something** with each item (side effects)
- You don't need a new array back
- Examples: logging, updating the DOM, writing to a file

```js
const names = ['Bruce', 'Clark', 'Diana'];

// Logging — no return value needed
names.forEach(name => console.log(name));

// Sending emails — side effect, not transforming data
names.forEach(name => sendEmail(name));
```

---

## Use `map` when:
- You want to **transform** every item
- You need a new array of the same length
- Examples: formatting data, converting types, extracting fields

```js
const prices = [10, 20, 30];
const withTax = prices.map(price => price * 1.18);
console.log(withTax); // [11.8, 23.6, 35.4]

const users = [{ name: 'Bruce', age: 36 }, { name: 'Clark', age: 34 }];
const names = users.map(user => user.name);
console.log(names); // ['Bruce', 'Clark']
```

---

## Use `filter` when:
- You want to **keep** only items that match a condition
- You need a subset of the original array

```js
const scores = [22, 75, 88, 43, 91];
const passing = scores.filter(score => score >= 50);
console.log(passing); // [75, 88, 91]

const users = [
  { name: 'Bruce', active: true },
  { name: 'Clark', active: false },
  { name: 'Diana', active: true }
];
const active = users.filter(user => user.active);
```

---

## Use `reduce` when:
- You want to **combine** all items into a single value
- Examples: sum, count, group, build an object from an array

```js
// Sum
const numbers = [1, 2, 3, 4, 5];
const total = numbers.reduce((acc, n) => acc + n, 0);
console.log(total); // 15

// Group by
const orders = [
  { product: 'apple', qty: 2 },
  { product: 'banana', qty: 3 },
  { product: 'apple', qty: 1 },
];
const grouped = orders.reduce((acc, order) => {
  acc[order.product] = (acc[order.product] || 0) + order.qty;
  return acc;
}, {});
console.log(grouped); // { apple: 3, banana: 3 }
```

---

## Quick Rule

| I want to...                        | Use        |
|-------------------------------------|------------|
| Do something with each item         | `forEach`  |
| Transform every item                | `map`      |
| Keep only matching items            | `filter`   |
| Combine all items into one value    | `reduce`   |

> `forEach` returns `undefined`. If you find yourself pushing to an array inside `forEach`, switch to `map` instead.

```js
// Bad — use map instead
const doubled = [];
[1, 2, 3].forEach(n => doubled.push(n * 2));

// Good
const doubled = [1, 2, 3].map(n => n * 2);
```