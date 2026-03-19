# Popular Object Methods

All `Object.*` methods return new values — they do **not** mutate the original object.  
However, methods that return objects give you **shallow copies** — nested objects are still referenced.

---

## `Object.keys`
Returns an array of own property keys.
```js
const person = { name: 'Bruce', age: 36, city: 'Gotham' };
Object.keys(person); // ['name', 'age', 'city']
```

## `Object.values`
Returns an array of own property values.
```js
Object.values(person); // ['Bruce', 36, 'Gotham']
```

## `Object.entries`
Returns an array of `[key, value]` pairs.
```js
Object.entries(person);
// [['name', 'Bruce'], ['age', 36], ['city', 'Gotham']]
```

Useful for iterating:
```js
for (const [key, value] of Object.entries(person)) {
  console.log(`${key}: ${value}`);
}
```

---

## `Object.assign` — Shallow Copy (Mutable target)
Copies properties from source into target. **Mutates the target**.
```js
const target = { a: 1 };
const source = { b: 2, c: 3 };

Object.assign(target, source);
console.log(target); // { a: 1, b: 2, c: 3 } — mutated!
```

To create a copy without mutating:
```js
const copy = Object.assign({}, person);
```

> Prefer spread `{ ...obj }` over `Object.assign` for copying.

---

## Spread (Copy/Merge) — Immutable
```js
const original = { name: 'Bruce', age: 36 };
const copy = { ...original };

copy.name = 'Clark';
console.log(original.name); // 'Bruce' — unchanged
console.log(copy.name);     // 'Clark'
```

Merge two objects:
```js
const defaults = { theme: 'dark', language: 'en' };
const userPrefs = { language: 'fr' };
const settings = { ...defaults, ...userPrefs };
console.log(settings); // { theme: 'dark', language: 'fr' }
```

---

## `Object.freeze` — Makes Object Immutable
Prevents any modification. Returns the same object.
```js
const config = Object.freeze({ host: 'localhost', port: 3000 });
config.port = 8080; // silently fails (or throws in strict mode)
console.log(config.port); // 3000 — unchanged
```

---

## `Object.hasOwn` / `hasOwnProperty`
Checks if a property belongs to the object itself (not inherited).
```js
const person = { name: 'Bruce' };
Object.hasOwn(person, 'name');     // true
Object.hasOwn(person, 'toString'); // false — inherited from Object
```

---

## Shallow vs Deep Copy

`Object.assign` and spread are **shallow** — nested objects are still referenced.
```js
const original = { name: 'Bruce', address: { city: 'Gotham' } };
const copy = { ...original };

copy.address.city = 'Metropolis'; // mutates original too!
console.log(original.address.city); // 'Metropolis'
```

For a deep copy, use `structuredClone`:
```js
const deepCopy = structuredClone(original);
deepCopy.address.city = 'Metropolis';
console.log(original.address.city); // 'Gotham' — safe
```