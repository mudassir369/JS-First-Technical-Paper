# Searching MDN (Mozilla Developer Network)

MDN is the most reliable reference for JavaScript, HTML, and CSS.

URL: **https://developer.mozilla.org**

---

## How to Search Effectively

### 1. Search directly in Google
Add `mdn` to your query for fast results.
```
mdn array filter
mdn string includes
mdn object keys
mdn typeof
```

### 2. Use the MDN search bar
Go to https://developer.mozilla.org and type your query.

### 3. Know the URL pattern
Once you know the structure, you can guess URLs:
```
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let
```

---

## What to Look for on an MDN Page

### Syntax block
Shows the method signature — what arguments it accepts.
```js
filter(callbackFn)
filter(callbackFn, thisArg)
```

### Parameters section
Explains each argument.

### Return value section
Tells you what the function returns — critical for knowing if a method is mutable or not.

### Examples section
Real code samples — read these first if you're in a hurry.

### Browser compatibility table
At the bottom — tells you which browsers support it.

---

## Example: Looking up `Array.prototype.find`

1. Search: `mdn array find`
2. Read the **syntax** — `find(callbackFn)`
3. Read **return value** — returns the first element that satisfies the callback, or `undefined`
4. Read the **example**

```js
const scores = [10, 45, 82, 33];
const firstHigh = scores.find(score => score > 40);
console.log(firstHigh); // 45
```

---

## Tips
- Prefer MDN over random blog posts or Stack Overflow for accuracy
- The "Try it" editor on MDN lets you run examples live
- Bookmark: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference