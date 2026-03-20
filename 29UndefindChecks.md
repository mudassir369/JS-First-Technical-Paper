# Why `value === undefined` is Better Than `!value`

---

## The Problem with `!value`

`!value` is falsy for **6 different things**: `false`, `0`, `''`, `null`, `undefined`, `NaN`.

```js
function processScore(score) {
  if (!score) {
    console.log('No score provided');
    return;
  }
  console.log('Score:', score);
}

processScore(undefined); // 'No score provided' — intended
processScore(null);      // 'No score provided' — maybe intended
processScore(0);         // 'No score provided' — BUG! 0 is a valid score
processScore('');        // 'No score provided' — BUG! empty string may be valid
processScore(false);     // 'No score provided' — BUG!
```

---

## `value === undefined` is Precise

```js
function processScore(score) {
  if (score === undefined) {
    console.log('No score provided');
    return;
  }
  console.log('Score:', score);
}

processScore(undefined); // 'No score provided' — correct
processScore(0);         // 'Score: 0' — correct, 0 is valid
processScore('');        // 'Score: ' — correct, handled
processScore(null);      // 'Score: null' — not undefined, passes through
```

---

## Real-World Example

```js
// Config object where 0, false, '' are all valid values
const config = {
  timeout: 0,       // 0ms timeout is valid
  retries: false,   // no retries is valid
  prefix: '',       // empty prefix is valid
};

function getConfig(key) {
  if (!config[key]) {
    return 'default'; // BUG — 0, false, '' all trigger this
  }
  return config[key];
}

getConfig('timeout'); // 'default' — wrong!

// Fixed
function getConfig(key) {
  if (config[key] === undefined) {
    return 'default';
  }
  return config[key];
}

getConfig('timeout'); // 0 — correct
```

---

## Checking for Both `null` and `undefined`

When you want to catch both, use `== null` (the one valid use of `==`):

```js
function process(value) {
  if (value == null) { // catches null AND undefined
    return 'nothing here';
  }
  return value;
}

process(null);      // 'nothing here'
process(undefined); // 'nothing here'
process(0);         // 0 — correct
process('');        // '' — correct
```

---

## Summary

| Check | Catches |
|-------|---------|
| `!value` | `false`, `0`, `''`, `null`, `undefined`, `NaN` |
| `value === undefined` | Only `undefined` |
| `value === null` | Only `null` |
| `value == null` | `null` and `undefined` |

Use the most specific check for what you actually mean.