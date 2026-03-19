# Truthy and Falsy Values

In JavaScript, every value is either truthy or falsy when evaluated in a boolean context.

---

## Falsy Values
There are exactly **6 falsy values**:

```js
false
0
""        
null
undefined
NaN
```

```js
if (0)         { } // never runs
if ("")        { } // never runs
if (null)      { } // never runs
if (undefined) { } // never runs
```

---

## Truthy Values
Everything else is truthy — including some surprising ones:

```js
if (1)         { } // runs
if ("0")       { } // runs — non-empty string
if ([])        { } // runs — empty array is truthy
if ({})        { } // runs — empty object is truthy
if ("false")   { } // runs — non-empty string
```

---

## Explicit Boolean Conversion

```js
Boolean(0)         // false
Boolean('')        // false
Boolean(null)      // false
Boolean([])        // true
Boolean({})        // true
Boolean('hello')   // true

// Double negation shorthand
!!0       // false
!!'hello' // true
```
