# Different Ways of Declaring a Function

## 1. Function Declaration
Hoisted. Can be called before it appears in code.
```js
function add(a, b) {
  return a + b;
}

add(2, 3); // 5
```

---

## 2. Function Expression
Assigned to a variable. Not hoisted.
```js
const add = function(a, b) {
  return a + b;
};

add(2, 3); // 5
```

---

## 3. Named Function Expression
Like a function expression but with a name — useful for recursion and stack traces.
```js
const factorial = function fact(n) {
  if (n <= 1) return 1;
  return n * fact(n - 1); // uses its own name
};

factorial(5); // 120
```

---

## 4. Arrow Function
Shorter syntax. Does not have its own `this`.
```js
const add = (a, b) => a + b;

add(2, 3); // 5
```

With a body:
```js
const add = (a, b) => {
  const result = a + b;
  return result;
};
```

Single parameter — parentheses optional:
```js
const double = n => n * 2;
```

---

## 5. Method Shorthand (inside objects)
```js
const calculator = {
  add(a, b) {
    return a + b;
  }
};

calculator.add(2, 3); // 5
```

---

## 6. Immediately Invoked Function Expression (IIFE)
Runs immediately when defined. Used to create an isolated scope.
```js
(function() {
  const mane = 'Md';
  console.log(name); // 'Md'
})();

console.log(name); // ReferenceError — contained
```

---

## 7. Constructor Function
Used to create objects before ES6 classes.
```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}

const bruce = new Person('Md', 24);
console.log(bruce.name); // 'Md'
```

---

## Quick Comparison

| Type                  | Hoisted | Own `this` | Use Case                  |
|-----------------------|---------|------------|---------------------------|
| Function Declaration  | Yes     | Yes        | General purpose           |
| Function Expression   | No      | Yes        | Assign to variable        |
| Arrow Function        | No      | No         | Callbacks, short functions|
| Method Shorthand      | No      | Yes        | Object methods            |
| IIFE                  | No      | Yes        | Isolated scope            |