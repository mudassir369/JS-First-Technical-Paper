# Importance of the catch Block

## Without `catch` — Program Crashes

```js
const data = JSON.parse('invalid json'); // SyntaxError — crashes everything
console.log('This never runs');
```

---

## With `catch` — Program Recovers

```js
let data = null;

try {
  data = JSON.parse('invalid json');
} catch (error) {
  console.error('Failed to parse JSON:', error.message);
  data = {}; // safe fallback
}

console.log('Program continues with:', data); // {}
```

---

## 1. Prevents Silent Failures
An empty catch swallows errors — you'll never know something went wrong.

```js
// Bad — silent failure
try {
  riskyOperation();
} catch (error) {
  // nothing — bug hidden!
}

// Good — always log at minimum
try {
  riskyOperation();
} catch (error) {
  console.error('riskyOperation failed:', error.message);
}
```

---

## 2. Provides Fallback Behaviour

```js
function getUserName(user) {
  try {
    return user.profile.name;
  } catch (error) {
    return 'Anonymous'; // graceful fallback
  }
}

console.log(getUserName(null));             // 'Anonymous'
console.log(getUserName({ profile: { name: 'Bruce' } })); // 'Bruce'
```

---

## 3. Prevents One Error From Breaking Everything

```js
const users = [
  { name: 'Bruce', age: 36 },
  null,
  { name: 'Diana', age: 32 },
];

users.forEach(user => {
  try {
    console.log(user.name.toUpperCase());
  } catch (error) {
    console.error('Skipping invalid user:', error.message);
  }
});

// BRUCE
// Skipping invalid user: Cannot read properties of null...
// DIANA
```

---

## 4. Re-throw Unexpected Errors
Only catch what you can handle — re-throw the rest.

```js
try {
  processPayment(order);
} catch (error) {
  if (error instanceof PaymentError) {
    showUserMessage('Payment declined. Try another card.');
  } else {
    throw error; // unexpected — let it bubble up
  }
}
```

---

## Rules

1. **Always log the error** — never leave `catch` empty
2. **Provide a fallback** when possible
3. **Re-throw** errors you can't handle
4. **Never use `catch` to hide bugs** — fix them