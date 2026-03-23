# Difference Between `null` and `undefined`

Both represent "no value" — but they are used in different contexts.

---

## `undefined`
JavaScript sets this automatically when a value has not been assigned.

```js
let name;
console.log(name); // undefined — declared but not assigned

function greet(name) {
  console.log(name);
}
greet(); // undefined — argument not provided

const obj = {};
console.log(obj.city); // undefined — property doesn't exist

function doNothing() {}
console.log(doNothing()); // undefined — no return statement
```

---

## `null`
Explicitly set by the programmer to mean "intentionally empty".

```js
let user = null; // we chose to set this — no user yet

function findUser(id) {
  const user = database.find(id);
  if (!user) return null; // intentionally returning nothing
  return user;
}

const result = findUser(999);
console.log(result); // null — user not found
```

---

## Key Differences

```js
typeof undefined // 'undefined'
typeof null      // 'object' — historical bug in JS

undefined == null  // true  — loose equality
undefined === null // false — strict equality

Number(undefined) // NaN
Number(null)      // 0
```

---

## When to Use Each

| Use | When |
|-----|------|
| `undefined` | Let JS set it — don't assign manually |
| `null` | You explicitly want to say "no value here" |

```js
// Don't do this
let name = undefined; // pointless, just use: let name;

// Do this
let selectedUser = null; // intentional — no user selected yet
```

---

## Checking for Both

```js
function process(value) {
  if (value === undefined) { /* only undefined */ }
  if (value === null)      { /* only null */ }
  if (value == null)       { /* both null and undefined */ }
}
```

---

## Nullish Coalescing (`??`)
Returns the right side only when the left is `null` or `undefined` (not other falsy values).

```js
const name = null ?? 'Anonymous'; // 'Anonymous'
const score = 0 ?? 100;           // 0 — 0 is not null/undefined
const label = '' ?? 'default';    // '' — empty string is not null/undefined
```

Compare with `||` which fires on any falsy value:
```js
const score = 0 || 100;  // 100 — bug if 0 is valid!
const score = 0 ?? 100;  // 0   — correct
```