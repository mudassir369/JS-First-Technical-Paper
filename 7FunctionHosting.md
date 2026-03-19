# Function Hoisting

Hoisting is JavaScript's behaviour of moving declarations to the top of their scope before execution.

---

## Function Declarations are Fully Hoisted
You can call them before they appear in the code.
```js
greet(); // 'Hello!'

function greet() {
  console.log('Hello!');
}
```

JS internally treats it as:
```js
function greet() { console.log('Hello!'); } 
greet();
```

---

## Function Expressions are NOT Hoisted
```js
greet(); // TypeError: greet is not a function

const greet = function() {
  console.log('Hello!');
};
```

The variable `greet` is hoisted (as `undefined` with `var`, or in TDZ with `let`/`const`), but the function value is not assigned until that line executes.

---

## Arrow Functions are NOT Hoisted
Same behaviour as function expressions.
```js
greet(); // ReferenceError

const greet = () => {
  console.log('Hello!');
};
```

---

## var Hoisting vs let/const

```js
// var — hoisted as undefined
console.log(sayHi); // undefined (no error)
var sayHi = function() { console.log('hi'); };

// let/const — hoisted but in Temporal Dead Zone (TDZ)
console.log(sayHello); // ReferenceError
const sayHello = function() { console.log('hello'); };
```

---

## Best Practice
Declare functions before you use them regardless of hoisting. Relying on hoisting makes code harder to read.