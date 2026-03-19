# Popular String Utility Methods

Strings are **immutable** in JavaScript — all string methods return a new string. The original is never changed.

```js
const name = 'Bruce Wayne';
name.toUpperCase();
console.log(name); // 'Bruce Wayne' — unchanged
```

---

## Case

### `toUpperCase` / `toLowerCase`
```js
'hello'.toUpperCase(); // 'HELLO'
'HELLO'.toLowerCase(); // 'hello'
```

---

## Searching

### `includes`
Returns `true` or `false`.
```js
'Gotham City'.includes('Gotham'); // true
'Gotham City'.includes('Metropolis'); // false
```

### `startsWith` / `endsWith`
```js
'Bruce Wayne'.startsWith('Bruce'); // true
'Bruce Wayne'.endsWith('Wayne');   // true
```

### `indexOf`
Returns index of first match, or `-1`.
```js
'Batman'.indexOf('man'); // 3
'Batman'.indexOf('xyz'); // -1
```

---

## Extracting

### `slice`
Returns a portion of the string.
```js
'Bruce Wayne'.slice(0, 5);  // 'Bruce'
'Bruce Wayne'.slice(6);     // 'Wayne'
'Bruce Wayne'.slice(-5);    // 'Wayne' — from end
```

### `substring`
Similar to `slice` but doesn't support negative indices.
```js
'Bruce Wayne'.substring(6, 11); // 'Wayne'
```

### `charAt`
Returns character at a given index.
```js
'Batman'[0];         // 'B'
'Batman'.charAt(0);  // 'B'
```

---

## Modifying (returns new string)

### `replace`
Replaces first match.
```js
'I am Batman'.replace('Batman', 'Superman'); // 'I am Superman'
```

### `replaceAll`
Replaces all matches.
```js
'ha ha ha'.replaceAll('ha', 'ho'); // 'ho ho ho'
```

### `trim` / `trimStart` / `trimEnd`
Removes whitespace.
```js
'  hello  '.trim();      // 'hello'
'  hello  '.trimStart(); // 'hello  '
'  hello  '.trimEnd();   // '  hello'
```

### `padStart` / `padEnd`
Pads to a target length.
```js
'5'.padStart(3, '0'); // '005'
'5'.padEnd(3, '0');   // '500'
```

### `repeat`
```js
'ha'.repeat(3); // 'hahaha'
```

---

## Splitting

### `split`
Splits string into an array.
```js
'Bruce Wayne'.split(' ');   // ['Bruce', 'Wayne']
'a,b,c'.split(',');          // ['a', 'b', 'c']
'hello'.split('');           // ['h', 'e', 'l', 'l', 'o']
```

---

## Template Literals (not a method, but essential)
```js
const name = 'Bruce';
const city = 'Gotham';
const msg = `${name} lives in ${city}`; // 'Bruce lives in Gotham'
```

---

## Converting

### `toString`
```js
(42).toString();    // '42'
(3.14).toString();  // '3.14'
```

### `String()`
```js
String(42);        // '42'
String(null);      // 'null'
String(undefined); // 'undefined'
```