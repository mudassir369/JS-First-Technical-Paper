# JavaScript Best Practices

---

## 1. Indentation
Use 2 spaces (most common in JS). Be consistent throughout the project.

```js
// Bad
function greet(name) {
    if (name) {
        return `Hello, ${name}`;
    }
}

// Good
function greet(name) {
  if (name) {
    return `Hello, ${name}`;
  }
}
```

---

## 2. Variable Naming
- Use `camelCase` for variables and functions
- Use `PascalCase` for classes and constructors
- Use `UPPER_SNAKE_CASE` for constants that never change
- Names should describe what the variable holds

```js
// Bad
const x = 'Bruce Wayne';
const d = new Date();
const arr = [1, 2, 3];

// Good
const userName = 'Bruce Wayne';
const currentDate = new Date();
const scores = [1, 2, 3];

// Constants
const MAX_RETRIES = 3;
const API_URL = 'https://api.example.com';

// Classes
class UserProfile {}
```

---

## 3. Loop Variable Naming
Use meaningful names — not just `i`, `j`, `k`.

```js
// Acceptable for simple index
for (let i = 0; i < arr.length; i++) {}

// Better — name reflects what you're iterating
const users = ['Bruce', 'Clark', 'Diana'];

for (let userIndex = 0; userIndex < users.length; userIndex++) {
  console.log(users[userIndex]);
}

// Best — use for...of when index isn't needed
for (const user of users) {
  console.log(user);
}

// forEach
users.forEach(user => console.log(user));
```

---

## 4. Use `const` by Default, `let` When Needed
```js
// Bad
var name = 'Bruce';
let city = 'Gotham'; // city never changes

// Good
const name = 'Bruce';
const city = 'Gotham';
let score = 0; // score will change
```

---

## 5. One Thing Per Function
Functions should do one thing only.

```js
// Bad — does too much
function processUser(user) {
  const validated = user.name && user.email;
  const formatted = { ...user, name: user.name.trim() };
  const saved = db.save(formatted);
  sendEmail(user.email);
  return saved;
}

// Good — split into focused functions
function validateUser(user) { return user.name && user.email; }
function formatUser(user) { return { ...user, name: user.name.trim() }; }
function saveUser(user) { return db.save(user); }
function notifyUser(email) { sendEmail(email); }
```

---

## 6. Use Guard Clauses Instead of Deep Nesting

```js
// Bad — arrow anti-pattern
function processOrder(order) {
  if (order) {
    if (order.items.length > 0) {
      if (order.user) {
        return fulfil(order);
      }
    }
  }
}

// Good — guard clauses
function processOrder(order) {
  if (!order) return;
  if (order.items.length === 0) return;
  if (!order.user) return;
  return fulfil(order);
}
```

---

## 7. Meaningful Function Names
Functions should read like sentences.

```js
// Bad
function doStuff(u) {}
function calc(a, b) {}

// Good
function sendWelcomeEmail(user) {}
function calculateTotalPrice(items, discount) {}
function isValidEmail(email) {}  // boolean functions start with is/has/can
function hasPermission(user, action) {}
```

---

## 8. Avoid Magic Numbers
Give numbers a name.

```js
// Bad
if (score > 85) { }
setTimeout(fn, 86400000);

// Good
const PASSING_SCORE = 85;
const ONE_DAY_MS = 86400000;

if (score > PASSING_SCORE) { }
setTimeout(fn, ONE_DAY_MS);
```

---

## 9. Keep Lines Short
Aim for under 80–100 characters per line.

```js
// Bad
const result = items.filter(item => item.active && item.score > 50).map(item => item.name).join(', ');

// Good
const result = items
  .filter(item => item.active && item.score > 50)
  .map(item => item.name)
  .join(', ');
```

---

## 10. Semicolons and Braces
Always use braces for `if`/`for`/`while` — even for single lines.

```js
// Bad
if (error) console.log(error);

// Good
if (error) {
  console.log(error);
}
```