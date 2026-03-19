# Default Parameters

Default parameters let you set fallback values for function arguments when they are `undefined` or not provided.

---

## Basic Syntax
```js
function greet(name = 'Stranger') {
  return `Hello, ${name}!`;
}

console.log(greet('Bruce')); // 'Hello, Bruce!'
console.log(greet());        // 'Hello, Stranger!'
```

---

## Before Default Parameters (Old Way)
```js
function greet(name) {
  name = name || 'Stranger'; // works but has edge cases
  return `Hello, ${name}!`;
}
```

Problem with `||`: it uses the default even for falsy values like `0` or `''`.
```js
function setVolume(vol) {
  vol = vol || 50; // bug! 0 becomes 50
}
setVolume(0); // returns 50 — wrong!
```

Default parameters fix this:
```js
function setVolume(vol = 50) {
  return vol;
}
setVolume(0);         // 0 — correct
setVolume();          // 50 — correct
setVolume(undefined); // 50 — undefined triggers default
setVolume(null);      // null — null does NOT trigger default
```

---

## Multiple Default Parameters
```js
function createUser(name = 'Anonymous', role = 'user', active = true) {
  return { name, role, active };
}

createUser();                    // { name: 'Anonymous', role: 'user', active: true }
createUser('Bruce');             // { name: 'Bruce', role: 'user', active: true }
createUser('Bruce', 'admin');    // { name: 'Bruce', role: 'admin', active: true }
```

---

## Default Using Another Parameter
```js
function createRange(start = 0, end = start + 10) {
  return { start, end };
}

createRange();      // { start: 0, end: 10 }
createRange(5);     // { start: 5, end: 15 }
createRange(5, 20); // { start: 5, end: 20 }
```

---

## Default with a Function Call
```js
function getTimestamp() {
  return Date.now();
}

function createEvent(name, time = getTimestamp()) {
  return { name, time };
}

createEvent('Launch');      // uses current timestamp
createEvent('Launch', 100); // uses 100
```

---

## Default with Destructuring
```js
function connect({ host = 'localhost', port = 3000 } = {}) {
  return `${host}:${port}`;
}

connect();                    // 'localhost:3000'
connect({ port: 8080 });      // 'localhost:8080'
connect({ host: '0.0.0.0' }); // '0.0.0.0:3000'
```