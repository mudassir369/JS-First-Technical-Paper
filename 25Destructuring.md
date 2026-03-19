# Destructuring

Destructuring extracts values from arrays or objects into variables.

---

## Object Destructuring

### Basic
```js
const person = { name: 'Bruce', age: 36, city: 'Gotham' };

const { name, age } = person;
console.log(name); // 'Bruce'
console.log(age);  // 36
```

### Rename while destructuring
```js
const { name: heroName, city: heroCity } = person;
console.log(heroName); // 'Bruce'
console.log(heroCity); // 'Gotham'
```

### Default values
```js
const { name, role = 'user' } = person;
console.log(role); // 'user' — not in person, uses default
```

### Nested objects
```js
const user = {
  name: 'Bruce',
  address: {
    city: 'Gotham',
    zip: '10001'
  }
};

const { name, address: { city } } = user;
console.log(city); // 'Gotham'
```

### In function parameters
```js
function greet({ name, city = 'Unknown' }) {
  return `${name} is from ${city}`;
}

greet({ name: 'Bruce', city: 'Gotham' }); // 'Bruce is from Gotham'
greet({ name: 'Clark' });                  // 'Clark is from Unknown'
```

---

## Array Destructuring

### Basic
```js
const scores = [82, 91, 75];

const [first, second, third] = scores;
console.log(first);  // 82
console.log(second); // 91
```

### Skip elements
```js
const [, second, , fourth] = [1, 2, 3, 4];
console.log(second); // 2
console.log(fourth); // 4
```

### Default values
```js
const [a = 0, b = 0, c = 0] = [10, 20];
console.log(c); // 0 — default used
```

### Rest in array destructuring
```js
const [first, ...rest] = [1, 2, 3, 4, 5];
console.log(first); // 1
console.log(rest);  // [2, 3, 4, 5]
```

### Swap variables
```js
let a = 1;
let b = 2;
[a, b] = [b, a];
console.log(a, b); // 2 1
```

---

## Destructuring in Loops
```js
const users = [
  { name: 'Bruce', role: 'admin' },
  { name: 'Clark', role: 'user' },
];

for (const { name, role } of users) {
  console.log(`${name} is ${role}`);
}
```

---

## Destructuring Function Return Values
```js
function getCoords() {
  return { x: 10, y: 20 };
}

const { x, y } = getCoords();
console.log(x, y); // 10 20
```