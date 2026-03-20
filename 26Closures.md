# Closures

A closure is a function that **remembers the variables from its outer scope** even after the outer function has finished executing.

---

## Basic Example

```js
function makeCounter() {
  let count = 0; // outer variable

  return function() {
    count++;       // inner function remembers count
    return count;
  };
}

const counter = makeCounter();
console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3
```

`count` is private — can't be accessed directly. Only the returned function can touch it.

---

## Each Closure Gets Its Own Scope

```js
const counterA = makeCounter();
const counterB = makeCounter();

counterA(); // 1
counterA(); // 2
counterB(); // 1 — independent, starts fresh
```

---

## Practical Use: Private State

```js
function createWallet(initialBalance) {
  let balance = initialBalance;

  return {
    deposit(amount) {
      balance += amount;
    },
    withdraw(amount) {
      if (amount > balance) {
        console.log('Insufficient funds');
        return;
      }
      balance -= amount;
    },
    getBalance() {
      return balance;
    }
  };
}

const wallet = createWallet(100);
wallet.deposit(50);
wallet.withdraw(30);
console.log(wallet.getBalance()); // 120
console.log(balance);             // ReferenceError — private!
```

---

## Practical Use: Function Factories

```js
function multiplyBy(factor) {
  return function(number) {
    return number * factor;
  };
}

const double = multiplyBy(2);
const triple = multiplyBy(3);

console.log(double(5));  // 10
console.log(triple(5));  // 15
```

---

## Practical Use: Memoization

```js
function memoize(fn) {
  const cache = {};

  return function(n) {
    if (cache[n] !== undefined) {
      console.log('from cache');
      return cache[n];
    }
    cache[n] = fn(n);
    return cache[n];
  };
}

const expensiveCalc = memoize(n => n * n);
expensiveCalc(5); // calculates: 25
expensiveCalc(5); // from cache: 25
```

---

## Common Pitfall: Closures in Loops

```js
// Bug — all callbacks share the same `i`
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
// Prints: 3, 3, 3

// Fix — use let (block-scoped, each iteration gets its own i)
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
// Prints: 0, 1, 2
```

This is one more reason to never use `var`.