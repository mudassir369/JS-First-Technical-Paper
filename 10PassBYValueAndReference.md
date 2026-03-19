# Pass by Value and Pass by Reference


## Pass by Value (Primitives)
When you pass a primitive (string, number, boolean, etc.), a **copy** is passed. The original is unaffected.

```js
function increment(n) {
  n = n + 1;
  console.log('inside:', n); // 6
}

let score = 5;
increment(score);
console.log('outside:', score); // 5 — unchanged
```

```js
function rename(name) {
  name = 'Md';
  console.log('inside:', name); // 'Md'
}

let name = 'Mudassir';
rename(name);
console.log('outside:', name); // 'Mudassir' — unchanged
```

---

## Pass by Reference (Objects & Arrays)
When you pass an object or array, the **reference** (memory address) is passed. Mutations inside the function affect the original.

```js
function addSkill(person) {
  person.add = 'Moradabad'; // mutates the original
}

const md = { name: 'Mudassir' };
addSkill(md);
console.log(md); // { name: 'Mudassir', add: 'Moradabad' }
```

```js
function addItem(arr) {
  arr.push('Horse Riding'); // mutates the original
}

const hobbies = ['Chess'];
addItem(hobbies);
console.log(hobbies); // ['Chess', 'Horse Riding']
```

---

## Reassigning an Object Does NOT Affect the Original
Reassignment only changes the local reference, not the original.

```js
function replaceObject(obj) {
  obj = { name: 'Ansari' }; // only changes local reference
}

const md = { name: 'Mudassir' };
replaceObject(md);
console.log(md); // { name: 'Mudassir' } — unchanged
```

---

## Avoiding Unintended Mutations
Use spread or `Object.assign` to work on a copy:

```js
function addSkill(person) {
  return { ...person, hobby: 'Chess' }; // returns new object
}

const md = { name: 'Mudassir' };
const updated = addSkill(md);

console.log(md);   // { name: 'Mudassir' } — original safe
console.log(updated); // { name: 'Mudassir', hobby: 'chess' }
```

```js
function addItem(arr) {
  return [...arr, 'Horse Riding']; // returns new array
}

const hobbies = ['Chees'];
const updated = addItem(hobbies);

console.log(hobbies); // ['Chees'] — original safe
console.log(updated); // ['Chees', 'Horse Riding']
```

---

## Summary

| Type       | What is passed | Original affected? |
|------------|----------------|--------------------|
| Primitive  | A copy         | No                 |
| Object     | A reference    | Yes (if mutated)   |
| Array      | A reference    | Yes (if mutated)   |