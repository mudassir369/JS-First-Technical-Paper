# What Happens When a Function Has No Return Statement

A function without a `return` statement returns `undefined` automatically.

---

## Default Return Value
```js
function greet(name) {
  console.log(`Hello, ${name}`);
  // no return
}

const result = greet('Bruce');
console.log(result); // undefined
```

---

## Comparing with a Return
```js
function add(a, b) {
  return a + b;
}

const sum = add(2, 3);
console.log(sum); // 5
```

---

## Early Return (Guard Clause)
`return` with no value also returns `undefined` — useful to exit early.
```js
function processUser(user) {
  if (!user) return; // exits early, returns undefined

  console.log(`Processing ${user.name}`);
}
```

---

## Common Bug
Forgetting `return` when you expect a value.
```js
function double(n) {
  n * 2; // forgot return!
}

const result = double(5);
console.log(result); // undefined — bug!
```

Fix:
```js
function double(n) {
  return n * 2;
}
```

---

## Arrow Function Implicit Return
Arrow functions with no `{}` return the expression automatically.
```js
const double = n => n * 2;
console.log(double(5)); // 10
```

But with `{}` you must use `return`:
```js
const double = n => {
  return n * 2; // required
};
```