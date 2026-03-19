# Template Literals

Template literals use backticks (`` ` ``) instead of quotes. They allow embedded expressions and multi-line strings.

---

## Basic Interpolation
```js
const name = 'Bruce';
const city = 'Gotham';

// Old way
const msg1 = 'Hello, ' + name + '. Welcome to ' + city + '.';

// Template literal
const msg2 = `Hello, ${name}. Welcome to ${city}.`;

console.log(msg2); // 'Hello, Bruce. Welcome to Gotham.'
```

---

## Any Expression Inside `${}`
```js
const a = 10;
const b = 20;

console.log(`Sum: ${a + b}`);          // 'Sum: 30'
console.log(`Double: ${a * 2}`);       // 'Double: 20'
console.log(`Is adult: ${a > 18}`);    // 'Is adult: false'
console.log(`Upper: ${'hello'.toUpperCase()}`); // 'Upper: HELLO'
```

---

## Calling Functions Inside `${}`
```js
function getGreeting(name) {
  return `Hi, ${name}!`;
}

const message = `Message: ${getGreeting('Bruce')}`;
console.log(message); // 'Message: Hi, Bruce!'
```

---

## Multi-line Strings
```js
// Old way — awkward
const old = 'Line 1\n' +
            'Line 2\n' +
            'Line 3';

// Template literal — natural
const modern = `Line 1
Line 2
Line 3`;
```

---

## Building HTML
```js
const user = { name: 'Bruce Wayne', role: 'Admin' };

const card = `
  <div class="card">
    <h2>${user.name}</h2>
    <p>Role: ${user.role}</p>
  </div>
`;
```

---

## Conditional in Template Literal
```js
const score = 75;
const result = `You ${score >= 50 ? 'passed' : 'failed'} the test.`;
console.log(result); // 'You passed the test.'
```

---

## Nested Template Literals
```js
const items = ['Batarang', 'Grapple Gun', 'Smoke Bomb'];
const list = `Items:\n${items.map(item => `  - ${item}`).join('\n')}`;
console.log(list);
// Items:
//   - Batarang
//   - Grapple Gun
//   - Smoke Bomb
```