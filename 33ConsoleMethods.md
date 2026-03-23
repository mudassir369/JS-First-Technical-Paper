# Console Methods

The `console` object provides methods to output information to the terminal or browser dev tools.

---

## `console.log`
General purpose output.
```js
console.log('Hello');
console.log(42);
console.log({ name: 'Bruce', age: 36 });
console.log('Name:', 'Bruce', 'Age:', 36); // multiple args
```

---

## `console.error`
Outputs to stderr. Appears in red in terminals and dev tools.
```js
console.error('Something went wrong');
console.error('Failed to connect:', error.message);
```

---

## `console.warn`
Outputs a warning. Appears in yellow.
```js
console.warn('Deprecated method used');
console.warn('Memory usage is high:', memoryUsage);
```

---

## `console.info`
Like `console.log` — used for informational messages.
```js
console.info('Server started on port 3000');
console.info('User logged in:', userId);
```

---

## `console.table`
Displays arrays or objects as a formatted table — great for structured data.
```js
const users = [
  { name: 'Bruce', role: 'admin' },
  { name: 'Clark', role: 'user' },
  { name: 'Diana', role: 'user' },
];

console.table(users);
// ┌─────────┬─────────┬─────────┐
// │ (index) │  name   │  role   │
// ├─────────┼─────────┼─────────┤
// │    0    │ 'Bruce' │ 'admin' │
// │    1    │ 'Clark' │ 'user'  │
// │    2    │ 'Diana' │ 'user'  │
// └─────────┴─────────┴─────────┘
```

---

## `console.dir`
Displays an object's properties. More detail than `console.log` for nested objects.
```js
console.dir({ a: { b: { c: 1 } } }, { depth: null }); // fully expanded
```

---

## `console.time` / `console.timeEnd`
Measures how long code takes to run.
```js
console.time('loop');

let sum = 0;
for (let i = 0; i < 1000000; i++) sum += i;

console.timeEnd('loop'); // loop: 3.245ms
```

---

## `console.count`
Counts how many times it's been called with the same label.
```js
function processItem(type) {
  console.count(type);
}

processItem('apple');  // apple: 1
processItem('banana'); // banana: 1
processItem('apple');  // apple: 2
processItem('apple');  // apple: 3
```

---

## `console.group` / `console.groupEnd`
Groups related logs with indentation.
```js
console.group('User Details');
console.log('Name: Bruce');
console.log('Role: Admin');
console.groupEnd();

console.group('Settings');
console.log('Theme: Dark');
console.groupEnd();
```

---

## `console.assert`
Logs an error only if the condition is `false`.
```js
const age = -1;
console.assert(age >= 0, 'Age must be non-negative'); // logs error
console.assert(age < 200, 'Age is unrealistically high'); // no output
```

---

## `console.clear`
Clears the console.
```js
console.clear();
```

---

## Quick Reference

| Method | Use |
|--------|-----|
| `log` | General output |
| `error` | Errors (red) |
| `warn` | Warnings (yellow) |
| `info` | Informational |
| `table` | Tabular data |
| `dir` | Object inspection |
| `time/timeEnd` | Performance measurement |
| `count` | Call frequency |
| `group/groupEnd` | Grouped output |
| `assert` | Conditional logging |