# Reading Error Messages and Stack Traces

The stack trace is your map to finding bugs. Reading it is one of the most important skills in programming.

---

## Anatomy of a Stack Trace

```
TypeError: Cannot read properties of undefined (reading 'name')
    at getHeroName (app.js:12:18)
    at processHero (app.js:7:20)
    at main (app.js:3:3)
    at Object.<anonymous> (app.js:1:1)
```

| Part | Meaning |
|------|---------|
| `TypeError` | The type of error |
| `Cannot read properties of undefined (reading 'name')` | What went wrong |
| `at getHeroName (app.js:12:18)` | File, line 12, column 18 — where it broke |
| Lines below | The call chain — how we got there |

**Always read from the top** — the first `at` line is where the error actually occurred.

---

## Example 1: TypeError

```js
// app.js
function getHeroName(hero) {
  return hero.name; // line 2
}

const result = getHeroName(undefined); // line 5
```

```
TypeError: Cannot read properties of undefined (reading 'name')
    at getHeroName (app.js:2:15)
    at Object.<anonymous> (app.js:5:16)
```

**Reading it:**
1. `TypeError` — we accessed a property on something that isn't an object
2. `reading 'name'` — the `.name` property caused it
3. `app.js:2:15` — go to line 2, column 15 in app.js
4. `app.js:5:16` — `getHeroName` was called from line 5

**Fix:** `undefined` was passed — add a guard:
```js
function getHeroName(hero) {
  if (!hero) return 'Unknown';
  return hero.name;
}
```

---

## Example 2: ReferenceError

```js
function greet() {
  console.log(message); // line 2 — not defined
}
greet(); // line 4
```

```
ReferenceError: message is not defined
    at greet (app.js:2:15)
    at Object.<anonymous> (app.js:4:1)
```

**Reading it:**
- `message is not defined` — we used a variable that doesn't exist
- `app.js:2:15` — the problem is on line 2

---

## Example 3: Deeply Nested Call

```js
function a() { b(); }   // line 1
function b() { c(); }   // line 2
function c() { null.x; } // line 3 — error here
a();                     // line 4
```

```
TypeError: Cannot read properties of null (reading 'x')
    at c (app.js:3:16)
    at b (app.js:2:16)
    at a (app.js:1:16)
    at Object.<anonymous> (app.js:4:1)
```

**Reading it (bottom-up for context):**
- `a()` called `b()` which called `c()` — the call chain
- The error happened in `c` on line 3 — start debugging there

---

## Common Error Types

| Error | Common Cause |
|-------|-------------|
| `TypeError` | Accessing property on `null`/`undefined`, calling non-function |
| `ReferenceError` | Using variable that doesn't exist |
| `SyntaxError` | Invalid JavaScript syntax |
| `RangeError` | Value out of allowed range (e.g., invalid array length) |

---

## Debugging Workflow

1. **Read the error type** — narrows down the category
2. **Read the message** — tells you what went wrong
3. **Go to the first `at` line** — that's where the crash happened
4. **Trace up the call stack** — find what passed bad data
5. **Add `console.log`** before the error line to inspect values

```js
function getHeroName(hero) {
  console.log('hero value:', hero); // inspect before crash
  return hero.name;
}
```

> Practice: deliberately cause `TypeError`, `ReferenceError`, and `SyntaxError` in a test file and read the stack trace every day for 2 weeks. This skill becomes instinctive.