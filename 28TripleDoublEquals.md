# `===` vs `==`

## `===` — Strict Equality
Compares **value AND type**. No type conversion.

```js
1 === 1        // true
1 === '1'      // false — different types
null === null  // true
null === undefined // false
```

---

## `==` — Loose Equality
Compares **value only** — performs type coercion (converts types before comparing).

```js
1 == '1'       // true — '1' converted to 1
0 == false     // true — false converted to 0
0 == ''        // true — '' converted to 0
null == undefined // true — special case
'' == false    // true
```

---

## Why `==` Causes Bugs

```js
const userInput = '0'; // string from a form

if (userInput == false) {
  console.log('no input'); // runs! '0' == false is true
}

if (userInput === false) {
  console.log('no input'); // doesn't run — correct
}
```

```js
const items = [];

if (items == false) {
  console.log('no items'); // runs! [] == false is true
}

if (items.length === 0) {
  console.log('no items'); // clearer and correct
}
```

---

## The Coercion Table (`==`)

| Comparison | Result | Why |
|------------|--------|-----|
| `0 == false` | `true` | `false` → `0` |
| `1 == true` | `true` | `true` → `1` |
| `'' == false` | `true` | both → `0` |
| `null == undefined` | `true` | special rule |
| `null == 0` | `false` | special rule |
| `[] == false` | `true` | `[]` → `''` → `0` |
| `[] == 0` | `true` | `[]` → `''` → `0` |

---

## Always Use `===`

```js
// Bad
if (score == '10') { }

// Good
if (score === 10) { }
```

The only acceptable use of `==` is checking for both `null` and `undefined` at once:
```js
if (value == null) { // catches both null and undefined
  // ...
}

// Equivalent to:
if (value === null || value === undefined) { }
```