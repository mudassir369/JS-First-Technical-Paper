# Arrow Functions vs Regular Functions

## Syntax

```js
// Regular function
function add(a, b) {
  return a + b;
}

// Arrow function
const add = (a, b) => a + b;
```

---

## 1. `this` Binding — The Key Difference

**Regular functions** define their own `this` based on how they are called.

```js
const person = {
  name: 'Bruce',
  greet: function() {
    console.log(`Hello, I am ${this.name}`);
  }
};

person.greet(); // 'Hello, I am Bruce' — this = person
```

**Arrow functions** do NOT have their own `this` — they inherit it from the surrounding scope.

```js
const person = {
  name: 'Bruce',
  greet: () => {
    console.log(`Hello, I am ${this.name}`);
  }
};

person.greet(); // 'Hello, I am undefined' — this = outer scope (not person)
```

---

## 2. Arrow Functions Are Great for Callbacks

Since they inherit `this` from their enclosing scope, they avoid the classic `this` bug:

```js
// Bug with regular function
function Timer() {
  this.seconds = 0;
  setInterval(function() {
    this.seconds++; // this is undefined or window — bug!
  }, 1000);
}

// Fixed with arrow function
function Timer() {
  this.seconds = 0;
  setInterval(() => {
    this.seconds++; // this = Timer instance — correct
  }, 1000);
}
```

---

## 3. No `arguments` Object

Regular functions have `arguments`:
```js
function showArgs() {
  console.log(arguments); // [1, 2, 3]
}
showArgs(1, 2, 3);
```

Arrow functions do not:
```js
const showArgs = () => {
  console.log(arguments); // ReferenceError
};
```

Use rest parameters instead:
```js
const showArgs = (...args) => {
  console.log(args); // [1, 2, 3]
};
showArgs(1, 2, 3);
```

---

## 4. Cannot Be Used as Constructors

```js
function Person(name) {
  this.name = name;
}
const p = new Person('Bruce'); // OK

const PersonArrow = (name) => {
  this.name = name;
};
const p2 = new PersonArrow('Bruce'); // TypeError: PersonArrow is not a constructor
```

---

## 5. Implicit Return

Arrow functions with no `{}` implicitly return the expression:
```js
const double = n => n * 2;          // returns n * 2
const getObj = () => ({ key: 'val' }); // wrap object in () to return it
```

---

## When to Use Which

| Situation | Use |
|-----------|-----|
| Object methods (need `this`) | Regular function |
| Class methods (need `this`) | Regular function |
| Callbacks, `map`/`filter`/`forEach` | Arrow function |
| Short one-liners | Arrow function |
| Functions needing `arguments` | Regular function |
| Constructors | Regular function |