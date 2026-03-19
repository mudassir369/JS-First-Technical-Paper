# Spread Operator (`...`)

The spread operator expands an iterable (array, string, object) into individual elements.


## Spreading Arrays

### Copy an array
```js
const original = [1, 2, 3];
const copy = [...original];

copy.push(4);
console.log(original); // [1, 2, 3] — unchanged
console.log(copy);     // [1, 2, 3, 4]
```

### Merge arrays
```js
const a = [1, 2];
const b = [3, 4];
const merged = [...a, ...b];
console.log(merged); // [1, 2, 3, 4]
```

### Add items while copying
```js
const scores = [10, 20, 30];
const updated = [0, ...scores, 40];
console.log(updated); // [0, 10, 20, 30, 40]
```

---

## Spreading Objects

### Copy an object
```js
const person = { name: 'Bruce', age: 36 };
const copy = { ...person };

copy.age = 37;
console.log(person.age); // 36 — unchanged
```

### Merge objects
```js
const defaults = { theme: 'dark', language: 'en', fontSize: 14 };
const userPrefs = { language: 'fr', fontSize: 16 };

const settings = { ...defaults, ...userPrefs };
console.log(settings);
// { theme: 'dark', language: 'fr', fontSize: 16 }
// userPrefs overrides defaults for matching keys
```

### Add/override a property immutably
```js
const user = { name: 'Bruce', role: 'user' };
const admin = { ...user, role: 'admin' };

console.log(user.role);  // 'user'
console.log(admin.role); // 'admin'
```

---

## Spreading into Function Arguments

```js
function add(a, b, c) {
  return a + b + c;
}

const nums = [1, 2, 3];
console.log(add(...nums)); // 6
```

```js
const numbers = [5, 1, 9, 3, 7];
console.log(Math.max(...numbers)); // 9
```

---

## Spreading Strings

```js
const chars = [..."hello"];
console.log(chars); // ['h', 'e', 'l', 'l', 'o']
```

---

## Rest Parameters (opposite of spread)
Collects multiple arguments into an array:
```js
function sum(...numbers) {
  return numbers.reduce((acc, n) => acc + n, 0);
}

console.log(sum(1, 2, 3, 4, 5)); // 15
```

---

## Spread vs Rest

| Usage | Syntax | What it does |
|-------|--------|--------------|
| Spread | `[...arr]` | Expands into individual elements |
| Rest | `function(...args)` | Collects individual elements into array |