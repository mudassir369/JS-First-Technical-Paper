# Error Handling (try...catch)

## Basic Syntax

```js
try {
  // code that might throw
} catch (error) {
  // handle the error
} finally {
  // always runs (optional)
}
```

---

## Example

```js
function divide(a, b) {
  if (b === 0) throw new Error('Cannot divide by zero');
  return a / b;
}

try {
  const result = divide(10, 0);
  console.log(result);
} catch (error) {
  console.error('Something went wrong:', error.message);
} finally {
  console.log('Done');
}

// Output:
// Something went wrong: Cannot divide by zero
// Done
```

---

## The `error` Object

```js
try {
  null.name; // TypeError
} catch (error) {
  console.log(error.name);    // 'TypeError'
  console.log(error.message); // "Cannot read properties of null"
  console.log(error.stack);   // full stack trace
}
```

---

## Catching Specific Errors

```js
try {
  JSON.parse('invalid json');
} catch (error) {
  if (error instanceof SyntaxError) {
    console.log('Invalid JSON:', error.message);
  } else {
    throw error; // re-throw unexpected errors
  }
}
```

---

## `finally`
Runs whether or not an error occurred — useful for cleanup.

```js
function readFile() {
  let file = null;
  try {
    file = openFile('data.txt');
    return file.read();
  } catch (error) {
    console.error('Failed to read:', error.message);
  } finally {
    if (file) file.close(); // always clean up
  }
}
```

---

## Async Error Handling

```js
async function fetchUser(id) {
  try {
    const response = await fetch(`/api/users/${id}`);
    const user = await response.json();
    return user;
  } catch (error) {
    console.error('Fetch failed:', error.message);
  }
}
```