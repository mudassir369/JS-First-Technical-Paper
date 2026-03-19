# Different Types of For Loops

---

## 1. `for` with Numbers
Classic loop with an index counter.
```js
for (let i = 0; i < 5; i++) {
  console.log(i); // 0, 1, 2, 3, 4
}
```

Looping over an array by index:
```js
const heroes = ['Batman', 'Superman', 'Wonder Woman'];

for (let i = 0; i < heroes.length; i++) {
  console.log(heroes[i]);
}
```

---

## 2. `for...in`
Iterates over the **keys** of an object.
```js
const person = { name: 'Bruce', age: 36, city: 'Gotham' };

for (const key in person) {
  console.log(key, person[key]);
}
// name Bruce
// age 36
// city Gotham
```

> Avoid using `for...in` on arrays — it iterates over indices as strings and can include inherited properties.

---

## 3. `for...of`
Iterates over the **values** of any iterable (arrays, strings, sets, maps).
```js
const heroes = ['Batman', 'Superman', 'Wonder Woman'];

for (const hero of heroes) {
  console.log(hero);
}
```

Works on strings too:
```js
for (const char of 'Gotham') {
  console.log(char); // G, o, t, h, a, m
}
```

---

## 4. `forEach`
Array method. Calls a callback for each element. Cannot use `break` or `return` to exit early.
```js
const heroes = ['Batman', 'Superman', 'Wonder Woman'];

heroes.forEach((hero, index) => {
  console.log(index, hero);
});
// 0 Batman
// 1 Superman
// 2 Wonder Woman
```

---

## 5. `while`
Runs as long as a condition is true. Use when you don't know the number of iterations upfront.
```js
let count = 0;

while (count < 3) {
  console.log(count); // 0, 1, 2
  count++;
}
```

Infinite loop risk — always ensure the condition will eventually become false:
```js
// DANGER — never ends
while (true) {
  console.log('looping');
}
```

---

## Quick Comparison

| Loop        | Best for                              | Can break early? |
|-------------|---------------------------------------|------------------|
| `for`       | Index-based iteration, arrays         | Yes              |
| `for...in`  | Object keys                           | Yes              |
| `for...of`  | Array/string/iterable values          | Yes              |
| `forEach`   | Array iteration with a callback       | No               |
| `while`     | Unknown number of iterations          | Yes              |