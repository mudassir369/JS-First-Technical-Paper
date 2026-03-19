# Throwing Errors


## `throw new Error("message")`
Creates an `Error` object with a `name`, `message`, and `stack` trace.

```js
function getUser(id) {
  if (!id) throw new Error('User ID is required');
  return { id, name: 'Bruce' };
}

try {
  getUser(null);
} catch (error) {
  console.log(error.name);    // 'Error'
  console.log(error.message); // 'User ID is required'
  console.log(error.stack);   // full stack trace with line numbers
}
```

---

## `throw "message"` (throwing a string)
Throws a plain string — no `name`, no `stack` trace.

```js
function getUser(id) {
  if (!id) throw 'User ID is required';
}

try {
  getUser(null);
} catch (error) {
  console.log(error);         // 'User ID is required'
  console.log(error.message); // undefined — no message property
  console.log(error.stack);   // undefined — no stack trace
}
```

---

## Key Differences

| Feature         | `throw new Error("msg")` | `throw "msg"`     |
|-----------------|--------------------------|-------------------|
| `error.name`    | `'Error'`                | `undefined`       |
| `error.message` | `'msg'`                  | `undefined`       |
| `error.stack`   | Full stack trace         | `undefined`       |
| `instanceof Error` | `true`               | `false`           |
| Debuggability   |  Easy                  |  Hard           |

---

## Always Use `throw new Error()`
The stack trace tells you exactly where the error occurred — critical for debugging.

```js
// Bad
throw 'something went wrong';

// Good
throw new Error('something went wrong');
```

---

## Built-in Error Types
```js
throw new TypeError('Expected a string');
throw new RangeError('Value must be between 1 and 100');
throw new ReferenceError('Variable not defined');
throw new SyntaxError('Invalid JSON');
```

---

## Custom Error Classes
```js
class ValidationError extends Error {
  constructor(message) {
    super(message);
    this.name = 'ValidationError';
  }
}

function validateAge(age) {
  if (age < 0) throw new ValidationError('Age cannot be negative');
  if (age > 150) throw new ValidationError('Age is unrealistically high');
  return age;
}

try {
  validateAge(-5);
} catch (error) {
  if (error instanceof ValidationError) {
    console.log('Validation failed:', error.message);
  } else {
    throw error; // re-throw unexpected errors
  }
}
```