# Implementing JavaScript Built-in Methods in Vanilla JS

A curated, **interview-focused** collection of JavaScript's most important built-in methods,
re-implemented **from scratch in plain vanilla JavaScript**. "Implement `X` without using the
built-in" is one of the most common front-end / JS interview rounds — it proves you understand
*how the language actually works*, not just how to call an API.

Each entry includes:

- **What it does** — the contract of the real built-in (inputs, output, edge cases).
- **How it works** — the intuition and the tricky bits, explained so it's easy to **remember**.
- **Company tags** — where this style of question has commonly been reported in interviews.
- **Implementation** — clean, commented vanilla JS (prefixed `my*` so it can sit next to the native one).
- **Gotchas** — the follow-up edge cases interviewers love to probe.

> **Note on company tags:** Tags are *indicative*, compiled from widely shared interview experiences
> (Glassdoor, LeetCode Discuss, GreatFrontend, FrontendInterviewHandbook, blogs). Interview content
> changes over time and varies by role/level — read them as "this kind of company asks this kind of
> question," not as a guarantee.

> **Naming convention:** Each polyfill is named `myMap`, `myCall`, etc. In a real polyfill you'd assign
> to the real name *only if it's missing*, e.g. `Array.prototype.map = Array.prototype.map || function(){…}`.

> **Related files:** `debounce`, `throttle`, `Promise.all`, `bind`/`call`/`apply` (and other higher-order
> patterns) are also covered in [`../../JavaScript-pattern/README.md`](../../JavaScript-pattern/README.md).
> This file focuses on faithfully re-creating the **built-in methods themselves**.

## Table of Contents

**Array methods**
1. [Array.prototype.map](#1-arrayprototypemap)
2. [Array.prototype.filter](#2-arrayprototypefilter)
3. [Array.prototype.reduce](#3-arrayprototypereduce)
4. [Array.prototype.forEach](#4-arrayprototypeforeach)
5. [Array.prototype.find / findIndex](#5-arrayprototypefind--findindex)
6. [Array.prototype.some / every](#6-arrayprototypesome--every)
7. [Array.prototype.flat](#7-arrayprototypeflat)
8. [Array.prototype.indexOf / includes](#8-arrayprototypeindexof--includes)
9. [Array.prototype.slice](#9-arrayprototypeslice)
10. [Array.isArray](#10-arrayisarray)

**Function methods (this-binding)**
11. [Function.prototype.call](#11-functionprototypecall)
12. [Function.prototype.apply](#12-functionprototypeapply)
13. [Function.prototype.bind](#13-functionprototypebind)

**Object & operators**
14. [Object.assign](#14-objectassign)
15. [Object.create](#15-objectcreate)
16. [the `new` operator](#16-the-new-operator)
17. [the `instanceof` operator](#17-the-instanceof-operator)
18. [Deep clone (structuredClone-style)](#18-deep-clone-structuredclone-style)

**Promise statics**
19. [Promise.all](#19-promiseall)
20. [Promise.allSettled](#20-promiseallsettled)
21. [Promise.race / Promise.any](#21-promiserace--promiseany)

**String methods**
22. [String.prototype.repeat](#22-stringprototyperepeat)
23. [String.prototype.trim](#23-stringprototypetrim)

**Type utilities**
24. [A robust typeof (getType)](#24-a-robust-typeof-gettype)

### The 3 things almost every Array polyfill must handle

Interviewers grade these details. Bake them in by habit:

| Concern | Why it matters | How we handle it |
|---------|----------------|------------------|
| **Callback validation** | Native methods throw `TypeError` if the callback isn't a function. | `if (typeof cb !== 'function') throw new TypeError(...)` |
| **Sparse arrays (holes)** | `[1, , 3]` has a hole at index 1; native `map`/`filter`/`forEach` **skip** holes. | guard with `if (i in this)` |
| **`thisArg` + `(value, index, array)`** | Callbacks receive 3 args and an optional `this`. | `callback.call(thisArg, this[i], i, this)` |

---

## 1. Array.prototype.map

**What it does:** Returns a **new array** where each element is the result of calling `callback` on the
corresponding element. Length is preserved; the original array is untouched.

**How it works:** Walk the array, call the callback with `(value, index, array)`, store the returned value
at the **same index**. Skipping holes keeps sparseness consistent with the native method.

**Tags:** `Amazon` `Google` `Microsoft` `Uber` `Walmart` `Flipkart` `Paytm`

```js
Array.prototype.myMap = function (callback, thisArg) {
  if (typeof callback !== 'function') {
    throw new TypeError(callback + ' is not a function');
  }
  const result = new Array(this.length); // preserve length
  for (let i = 0; i < this.length; i++) {
    if (i in this) {                       // skip holes in sparse arrays
      result[i] = callback.call(thisArg, this[i], i, this);
    }
  }
  return result;
};

// [1, 2, 3].myMap(x => x * 2) -> [2, 4, 6]
```

**Gotchas:** Must return a *new* array (don't mutate); pass `index` and the `array` itself; respect `thisArg`.

---

## 2. Array.prototype.filter

**What it does:** Returns a **new array** containing only the elements for which `callback` returns a
truthy value.

**How it works:** Same loop as `map`, but instead of transforming, we **conditionally push** the original
element when the predicate passes.

**Tags:** `Amazon` `Google` `Adobe` `Microsoft` `Swiggy` `Razorpay`

```js
Array.prototype.myFilter = function (callback, thisArg) {
  if (typeof callback !== 'function') {
    throw new TypeError(callback + ' is not a function');
  }
  const result = [];
  for (let i = 0; i < this.length; i++) {
    if (i in this && callback.call(thisArg, this[i], i, this)) {
      result.push(this[i]);
    }
  }
  return result;
};

// [1, 2, 3, 4].myFilter(x => x % 2 === 0) -> [2, 4]
```

**Gotchas:** The result is densely packed (indices reset), unlike `map` which preserves positions.

---

## 3. Array.prototype.reduce

**What it does:** Boils an array down to a **single value** by repeatedly applying `callback(acc, cur,
index, array)`. With no `initialValue`, the **first element** seeds the accumulator and iteration starts
at index 1.

**How it works:** The only real subtlety is the missing-initial-value case:
- If an initial value is provided → `acc = initialValue`, start at index 0.
- If not → find the **first existing** element, use it as `acc`, start after it.
- Reducing an **empty array with no initial value** must throw `TypeError`.

**Tags:** `Amazon` `Google` `Meta` `Microsoft` `Atlassian` `PayPal` `Uber`

```js
Array.prototype.myReduce = function (callback, initialValue) {
  if (typeof callback !== 'function') {
    throw new TypeError(callback + ' is not a function');
  }
  const len = this.length;
  let acc;
  let i = 0;

  if (arguments.length >= 2) {        // initialValue was passed (even if undefined)
    acc = initialValue;
  } else {
    while (i < len && !(i in this)) i++; // skip leading holes
    if (i >= len) {
      throw new TypeError('Reduce of empty array with no initial value');
    }
    acc = this[i++];                   // seed with first real element
  }

  for (; i < len; i++) {
    if (i in this) acc = callback(acc, this[i], i, this);
  }
  return acc;
};

// [1, 2, 3].myReduce((a, b) => a + b)     -> 6
// [1, 2, 3].myReduce((a, b) => a + b, 10) -> 16
```

**Gotchas:** Use `arguments.length >= 2` (not `initialValue === undefined`) so an explicit `undefined`
seed still counts; throw on empty-array-without-seed.

---

## 4. Array.prototype.forEach

**What it does:** Runs `callback` once per element **for its side effects** and returns `undefined`.
You cannot `break` out of it (that's a common trap).

**How it works:** Identical loop to `map`, but we ignore the return value and return nothing.

**Tags:** `TCS` `Infosys` `Amazon` `Cognizant` `Accenture`

```js
Array.prototype.myForEach = function (callback, thisArg) {
  if (typeof callback !== 'function') {
    throw new TypeError(callback + ' is not a function');
  }
  for (let i = 0; i < this.length; i++) {
    if (i in this) callback.call(thisArg, this[i], i, this);
  }
  return undefined; // explicit: forEach never returns a value
};
```

**Gotchas:** `return` inside the callback only skips the current iteration — it does **not** stop the loop.

---

## 5. Array.prototype.find / findIndex

**What it does:** `find` returns the **first element** that satisfies the predicate (or `undefined`);
`findIndex` returns its **index** (or `-1`). Both, unlike `filter`, **stop early** on the first match.

**How it works:** Linear scan; return as soon as the predicate is truthy. Note: these iterate **dense**
(they do *not* skip holes — they treat holes as `undefined`).

**Tags:** `Amazon` `Google` `Flipkart` `Microsoft` `Oracle`

```js
Array.prototype.myFind = function (callback, thisArg) {
  if (typeof callback !== 'function') throw new TypeError(callback + ' is not a function');
  for (let i = 0; i < this.length; i++) {
    if (callback.call(thisArg, this[i], i, this)) return this[i];
  }
  return undefined;
};

Array.prototype.myFindIndex = function (callback, thisArg) {
  if (typeof callback !== 'function') throw new TypeError(callback + ' is not a function');
  for (let i = 0; i < this.length; i++) {
    if (callback.call(thisArg, this[i], i, this)) return i;
  }
  return -1;
};
```

**Gotchas:** `find` returns the *value*, `findIndex` returns the *index*; both short-circuit.

---

## 6. Array.prototype.some / every

**What it does:** `some` → `true` if **at least one** element passes (logical OR). `every` → `true` only
if **all** pass (logical AND). Both short-circuit. By spec, `some([])` is `false`, `every([])` is `true`.

**How it works:** Scan and return early on the deciding case; otherwise return the default.

**Tags:** `Amazon` `Google` `Adobe` `Uber` `Zomato`

```js
Array.prototype.mySome = function (callback, thisArg) {
  if (typeof callback !== 'function') throw new TypeError(callback + ' is not a function');
  for (let i = 0; i < this.length; i++) {
    if (i in this && callback.call(thisArg, this[i], i, this)) return true;
  }
  return false;
};

Array.prototype.myEvery = function (callback, thisArg) {
  if (typeof callback !== 'function') throw new TypeError(callback + ' is not a function');
  for (let i = 0; i < this.length; i++) {
    if (i in this && !callback.call(thisArg, this[i], i, this)) return false;
  }
  return true;
};
```

**Gotchas:** Remember the empty-array defaults — they trip people up: `every` is **vacuously true**.

---

## 7. Array.prototype.flat

**What it does:** Returns a new array with sub-array elements flattened up to the given `depth`
(default `1`). `Infinity` flattens completely.

**How it works:** Recurse into elements that are arrays while `depth > 0`, decrementing depth each level.
A simple recursive helper accumulating into one result array is the cleanest mental model.

**Tags:** `Amazon` `Google` `Microsoft` `Atlassian` `Flipkart` `Meta`

```js
Array.prototype.myFlat = function (depth = 1) {
  const result = [];
  (function flatten(arr, d) {
    for (let i = 0; i < arr.length; i++) {
      if (!(i in arr)) continue;              // skip holes
      if (Array.isArray(arr[i]) && d > 0) {
        flatten(arr[i], d - 1);               // go one level deeper
      } else {
        result.push(arr[i]);
      }
    }
  })(this, depth);
  return result;
};

// [1, [2, [3, [4]]]].myFlat()         -> [1, 2, [3, [4]]]
// [1, [2, [3, [4]]]].myFlat(Infinity) -> [1, 2, 3, 4]
```

**Gotchas:** Default depth is **1**, not infinite. A non-recursive variant uses a stack — a good follow-up.

---

## 8. Array.prototype.indexOf / includes

**What it does:** `indexOf` returns the first index of a value using **strict equality (`===`)**, else
`-1`. `includes` returns a boolean and uses **SameValueZero**, so it can find `NaN` (which `indexOf`
cannot).

**How it works:** Linear scan. The one nuance is `includes` treating `NaN === NaN` as a match — detect it
with the `x !== x` trick (only `NaN` is not equal to itself).

**Tags:** `Amazon` `Microsoft` `TCS` `Wipro` `Oracle`

```js
Array.prototype.myIndexOf = function (target, fromIndex = 0) {
  const len = this.length;
  let start = fromIndex < 0 ? Math.max(len + fromIndex, 0) : fromIndex;
  for (let i = start; i < len; i++) {
    if (i in this && this[i] === target) return i;  // strict equality
  }
  return -1;
};

Array.prototype.myIncludes = function (target, fromIndex = 0) {
  const len = this.length;
  let start = fromIndex < 0 ? Math.max(len + fromIndex, 0) : fromIndex;
  for (let i = start; i < len; i++) {
    const v = this[i];
    // SameValueZero: equal, OR both are NaN
    if (v === target || (v !== v && target !== target)) return true;
  }
  return false;
};

// [1, NaN, 3].myIndexOf(NaN)  -> -1   (=== can't match NaN)
// [1, NaN, 3].myIncludes(NaN) -> true (SameValueZero matches NaN)
```

**Gotchas:** The `NaN` difference between the two is the classic interview "aha"; also handle negative
`fromIndex`.

---

## 9. Array.prototype.slice

**What it does:** Returns a **shallow copy** of a portion of the array from `start` (inclusive) to `end`
(exclusive) without mutating the original. Supports negative indices counting from the end.

**How it works:** Normalize negative/out-of-range `start` and `end` into real indices, then copy that
range into a new array.

**Tags:** `Amazon` `Microsoft` `Adobe` `PayPal` `Flipkart`

```js
Array.prototype.mySlice = function (start = 0, end = this.length) {
  const len = this.length;

  // Normalize start
  let from = start < 0 ? Math.max(len + start, 0) : Math.min(start, len);
  // Normalize end
  let to = end < 0 ? Math.max(len + end, 0) : Math.min(end, len);

  const result = [];
  for (let i = from; i < to; i++) {
    if (i in this) result.push(this[i]);
  }
  return result;
};

// [1, 2, 3, 4, 5].mySlice(1, 3) -> [2, 3]
// [1, 2, 3, 4, 5].mySlice(-2)   -> [4, 5]
```

**Gotchas:** It's a **shallow** copy (nested objects are shared); don't mutate the source; negative index math.

---

## 10. Array.isArray

**What it does:** Reliably reports whether a value is an array — even across different execution contexts
(iframes/realms), where `instanceof Array` can fail.

**How it works:** `Object.prototype.toString.call(value)` returns a precise internal tag, `"[object
Array]"` for arrays, regardless of realm. This is the bullet-proof type check.

**Tags:** `Amazon` `Microsoft` `Google` `Adobe`

```js
function myIsArray(value) {
  return Object.prototype.toString.call(value) === '[object Array]';
}

// myIsArray([1, 2])   -> true
// myIsArray('hello')  -> false
// myIsArray({ length: 0 }) -> false
```

**Gotchas:** Explain *why* `instanceof Array` is unreliable (separate realms have separate `Array`
constructors), which is exactly why `Array.isArray` exists.

---

## 11. Function.prototype.call

**What it does:** Invokes a function with an explicit `this` value and arguments passed **individually**.

**How it works:** The trick: temporarily attach the function as a property of the target object, call it
as a method (so `this` becomes that object), then remove it. Use a `Symbol` key so we never clobber an
existing property.

**Tags:** `Amazon` `Google` `Meta` `Microsoft` `Uber` `Atlassian` `PayPal`

```js
Function.prototype.myCall = function (thisArg, ...args) {
  thisArg = thisArg == null ? globalThis : Object(thisArg); // box primitives, default to global
  const fnKey = Symbol('fn');
  thisArg[fnKey] = this;          // `this` is the function being called
  const result = thisArg[fnKey](...args);
  delete thisArg[fnKey];          // clean up
  return result;
};

function greet(greeting) { return `${greeting}, ${this.name}`; }
greet.myCall({ name: 'Ada' }, 'Hi'); // -> "Hi, Ada"
```

**Gotchas:** Box primitive `thisArg` with `Object(...)`; use a `Symbol` to avoid name collisions; default
`null`/`undefined` to the global object (non-strict semantics).

---

## 12. Function.prototype.apply

**What it does:** Same as `call`, but arguments are passed as a **single array** (or array-like).

**How it works:** Identical mechanism to `myCall`; just spread the array argument. Guard the case where no
args array is provided.

**Tags:** `Amazon` `Google` `Microsoft` `Uber` `Flipkart`

```js
Function.prototype.myApply = function (thisArg, argsArray) {
  thisArg = thisArg == null ? globalThis : Object(thisArg);
  const fnKey = Symbol('fn');
  thisArg[fnKey] = this;
  const result = Array.isArray(argsArray) ? thisArg[fnKey](...argsArray) : thisArg[fnKey]();
  delete thisArg[fnKey];
  return result;
};

const nums = [5, 1, 9, 3];
Math.max.myApply(null, nums); // -> 9
```

**Gotchas:** `apply` takes **one array**; `call` takes a **list**. Handle a missing/empty args array.

---

## 13. Function.prototype.bind

**What it does:** Returns a **new function** permanently bound to a given `this` and optionally some
**pre-filled (partial) arguments**. The bound function can later receive more arguments.

**How it works:** Close over the original function, target `this`, and bound args. On call, merge bound
args with new args. The hard part: when the bound function is used as a **constructor** (`new`), `this`
must be the freshly created instance — **not** the bound context — and the prototype chain must be
preserved.

**Tags:** `Amazon` `Google` `Meta` `Microsoft` `Uber` `Atlassian` `Razorpay`

```js
Function.prototype.myBind = function (thisArg, ...boundArgs) {
  const targetFn = this;
  if (typeof targetFn !== 'function') {
    throw new TypeError('Bind must be called on a function');
  }

  function boundFn(...callArgs) {
    // If called with `new`, `this` is a fresh instance -> ignore thisArg
    const calledWithNew = this instanceof boundFn;
    return targetFn.apply(
      calledWithNew ? this : thisArg,
      [...boundArgs, ...callArgs]   // partial application
    );
  }

  // Preserve the prototype chain so `new boundFn()` works correctly
  if (targetFn.prototype) {
    boundFn.prototype = Object.create(targetFn.prototype);
  }
  return boundFn;
};

function multiply(a, b) { return a * b; }
const double = multiply.myBind(null, 2);
double(5); // -> 10
```

**Gotchas:** The `new`-target case and prototype preservation are what separate a "good" answer from a
basic one. Also: `bind` returns a function, it does **not** call immediately (unlike `call`/`apply`).

---

## 14. Object.assign

**What it does:** Copies **own enumerable** properties from one or more source objects onto a target
object (a shallow merge), and returns the (mutated) target.

**How it works:** For each source, copy string keys *and* enumerable symbol keys. Skip `null`/`undefined`
sources. Throw if the target is nullish.

**Tags:** `Amazon` `Microsoft` `Adobe` `Flipkart` `PayPal`

```js
function myAssign(target, ...sources) {
  if (target == null) {
    throw new TypeError('Cannot convert undefined or null to object');
  }
  const to = Object(target);

  for (const source of sources) {
    if (source == null) continue;          // skip null/undefined sources
    const from = Object(source);

    for (const key of Object.keys(from)) { // own enumerable string keys
      to[key] = from[key];
    }
    for (const sym of Object.getOwnPropertySymbols(from)) {
      if (Object.prototype.propertyIsEnumerable.call(from, sym)) {
        to[sym] = from[sym];               // own enumerable symbol keys
      }
    }
  }
  return to;
}

// myAssign({ a: 1 }, { b: 2 }, { c: 3 }) -> { a: 1, b: 2, c: 3 }
```

**Gotchas:** It's a **shallow** copy; it triggers setters on the target; remember symbol keys and the
nullish-target throw.

---

## 15. Object.create

**What it does:** Creates a **new object** whose prototype is the object you pass in (or `null`), with
optional property descriptors.

**How it works:** Classic trick — make an empty constructor `F`, point its `.prototype` at the desired
proto, and `new F()`. That gives you an object that inherits from `proto` without running any real
constructor.

**Tags:** `Amazon` `Google` `Microsoft` `Oracle`

```js
function myObjectCreate(proto, propertiesObject) {
  if (typeof proto !== 'object' && typeof proto !== 'function') {
    throw new TypeError('Object prototype may only be an Object or null');
  }
  function F() {}
  F.prototype = proto;
  const obj = new F();
  if (propertiesObject !== undefined) {
    Object.defineProperties(obj, propertiesObject);
  }
  return obj;
}

const animal = { eats: true };
const rabbit = myObjectCreate(animal);
rabbit.eats; // -> true (inherited)
```

**Gotchas:** This is the foundation of prototypal inheritance and underpins `myNew` and `myBind` below.

---

## 16. the `new` operator

**What it does:** `new Constructor(args)` creates an instance: it (1) makes a fresh object linked to
`Constructor.prototype`, (2) runs the constructor with `this` = that object, and (3) returns the object —
**unless** the constructor explicitly returns its own object.

**How it works:** Replicate those 4 steps. The subtle rule: if the constructor returns a non-null
**object**, that object wins; otherwise the newly created instance is returned.

**Tags:** `Amazon` `Google` `Meta` `Microsoft` `Uber`

```js
function myNew(Constructor, ...args) {
  if (typeof Constructor !== 'function') {
    throw new TypeError('myNew requires a constructor function');
  }
  // 1 & 2: new object linked to the constructor's prototype
  const obj = Object.create(Constructor.prototype);
  // 3: run constructor with `this` = obj
  const result = Constructor.apply(obj, args);
  // 4: honor an explicit object return, else return obj
  const isObject = result !== null && (typeof result === 'object' || typeof result === 'function');
  return isObject ? result : obj;
}

function Person(name) { this.name = name; }
const p = myNew(Person, 'Grace');
p.name;                  // -> "Grace"
p instanceof Person;     // -> true
```

**Gotchas:** The "constructor returns an object" override is the part most people forget.

---

## 17. the `instanceof` operator

**What it does:** `obj instanceof Constructor` checks whether `Constructor.prototype` appears anywhere in
`obj`'s **prototype chain**.

**How it works:** Walk up the chain with `Object.getPrototypeOf` until you either hit the constructor's
prototype (→ `true`) or reach `null` (→ `false`).

**Tags:** `Amazon` `Google` `Microsoft` `Adobe`

```js
function myInstanceof(obj, Constructor) {
  if (obj === null || (typeof obj !== 'object' && typeof obj !== 'function')) {
    return false; // primitives are never instances
  }
  let proto = Object.getPrototypeOf(obj);
  const target = Constructor.prototype;
  while (proto !== null) {
    if (proto === target) return true;
    proto = Object.getPrototypeOf(proto); // climb the chain
  }
  return false;
}

// myInstanceof([], Array)  -> true
// myInstanceof([], Object) -> true  (Array inherits from Object)
// myInstanceof(5,  Number) -> false (primitive, not an object)
```

**Gotchas:** Primitives return `false`; it follows the **whole** chain, so subclasses match parent
constructors too.

---

## 18. Deep clone (structuredClone-style)

**What it does:** Produces a **fully independent** deep copy of nested data — changes to the copy never
affect the original. (`structuredClone` is the modern built-in; `JSON.parse(JSON.stringify(x))` is the
naive version but loses functions, `undefined`, `Date`, `Map`, `Set`, and breaks on cycles.)

**How it works:** Recurse through objects/arrays, cloning each value. Use a `WeakMap` to remember already-
cloned objects so **circular references** don't cause infinite recursion. Handle special types (`Date`,
`Map`, `Set`, `RegExp`) explicitly.

**Tags:** `Amazon` `Google` `Microsoft` `Atlassian` `Uber` `Flipkart`

```js
function deepClone(value, seen = new WeakMap()) {
  // Primitives (and functions) are returned as-is
  if (value === null || typeof value !== 'object') return value;

  // Circular reference guard
  if (seen.has(value)) return seen.get(value);

  // Special built-in objects
  if (value instanceof Date) return new Date(value);
  if (value instanceof RegExp) return new RegExp(value.source, value.flags);

  if (value instanceof Map) {
    const result = new Map();
    seen.set(value, result);
    value.forEach((v, k) => result.set(k, deepClone(v, seen)));
    return result;
  }
  if (value instanceof Set) {
    const result = new Set();
    seen.set(value, result);
    value.forEach((v) => result.add(deepClone(v, seen)));
    return result;
  }

  // Arrays & plain objects
  const result = Array.isArray(value) ? [] : {};
  seen.set(value, result);           // record BEFORE recursing (handles cycles)
  for (const key of Reflect.ownKeys(value)) {
    result[key] = deepClone(value[key], seen);
  }
  return result;
}

const a = { x: 1 }; a.self = a;      // circular
const b = deepClone(a);
b.self === b;                        // -> true (cycle preserved, no crash)
```

**Gotchas:** The `WeakMap` cycle guard and special-type handling are what make this "production-grade"
versus the JSON trick.

---

## 19. Promise.all

**What it does:** Takes an iterable of promises and returns a promise that resolves to an **array of all
results** (in input order) once **every** input resolves — or **rejects immediately** if any one rejects
(fail-fast).

**How it works:** Track a `completed` counter and a `results` array. Resolve each input with
`Promise.resolve` (so non-promise values work too), store each result at its **original index**, and
resolve the outer promise only when `completed === total`. Reject on the first error. Resolve immediately
for an empty input.

**Tags:** `Amazon` `Google` `Meta` `Microsoft` `Uber` `PayPal` `Atlassian`

```js
function myPromiseAll(iterable) {
  return new Promise((resolve, reject) => {
    const items = Array.from(iterable);
    const results = new Array(items.length);
    let completed = 0;

    if (items.length === 0) return resolve(results); // empty -> resolve now

    items.forEach((item, index) => {
      Promise.resolve(item).then(
        (value) => {
          results[index] = value;       // preserve order
          if (++completed === items.length) resolve(results);
        },
        reject                          // first rejection rejects the whole thing
      );
    });
  });
}

// myPromiseAll([1, Promise.resolve(2), 3]).then(console.log) -> [1, 2, 3]
```

**Gotchas:** Preserve order by index (not completion order); wrap with `Promise.resolve` for plain values;
handle the empty-iterable case.

---

## 20. Promise.allSettled

**What it does:** Waits for **all** promises to finish and **never rejects**. Resolves to an array of
status objects: `{ status: 'fulfilled', value }` or `{ status: 'rejected', reason }`.

**How it works:** Like `all`, but record an outcome object for both success and failure, and only ever
**resolve** (never reject) the outer promise.

**Tags:** `Amazon` `Google` `Microsoft` `Uber` `Razorpay`

```js
function myAllSettled(iterable) {
  return new Promise((resolve) => {
    const items = Array.from(iterable);
    const results = new Array(items.length);
    let completed = 0;

    if (items.length === 0) return resolve(results);

    items.forEach((item, index) => {
      Promise.resolve(item).then(
        (value)  => { results[index] = { status: 'fulfilled', value }; },
        (reason) => { results[index] = { status: 'rejected', reason }; }
      ).finally(() => {
        if (++completed === items.length) resolve(results);
      });
    });
  });
}
```

**Gotchas:** It must **never reject**; the shape of the result objects is fixed by the spec.

---

## 21. Promise.race / Promise.any

**What they do:**
- `race` settles as soon as the **first** promise settles — whether it **fulfills or rejects**.
- `any` resolves with the **first fulfillment**, and only rejects (with an `AggregateError`) if **all**
  reject.

**How they work:** `race` simply forwards the first settlement. `any` ignores rejections until it has
collected *all* of them, then rejects with an aggregate.

**Tags:** `Amazon` `Google` `Microsoft` `Uber` `Atlassian`

```js
function myRace(iterable) {
  return new Promise((resolve, reject) => {
    for (const item of iterable) {
      Promise.resolve(item).then(resolve, reject); // first to settle wins
    }
  });
}

function myAny(iterable) {
  return new Promise((resolve, reject) => {
    const items = Array.from(iterable);
    const errors = new Array(items.length);
    let rejectedCount = 0;

    if (items.length === 0) {
      return reject(new AggregateError([], 'All promises were rejected'));
    }

    items.forEach((item, index) => {
      Promise.resolve(item).then(
        resolve,                          // first fulfillment wins
        (err) => {
          errors[index] = err;
          if (++rejectedCount === items.length) {
            reject(new AggregateError(errors, 'All promises were rejected'));
          }
        }
      );
    });
  });
}
```

**Gotchas:** `race` is settled by the first *settlement* (could be a rejection); `any` waits out
rejections and only fails if **everything** fails.

---

## 22. String.prototype.repeat

**What it does:** Returns a new string with the original repeated `count` times. Throws `RangeError` for
negative counts.

**How it works:** A clean O(n) approach just appends in a loop. (A bonus O(log n) "exponentiation by
squaring" version doubles the string — a nice optimization to mention.)

**Tags:** `Amazon` `Microsoft` `TCS` `Adobe`

```js
String.prototype.myRepeat = function (count) {
  count = Math.floor(count);
  if (count < 0 || count === Infinity) {
    throw new RangeError('Invalid count value: ' + count);
  }
  let result = '';
  for (let i = 0; i < count; i++) result += this;
  return result;
};

// 'ab'.myRepeat(3) -> 'ababab'

// Bonus: O(log n) via doubling
String.prototype.myRepeatFast = function (count) {
  count = Math.floor(count);
  if (count < 0 || count === Infinity) throw new RangeError('Invalid count value');
  let result = '', chunk = String(this);
  while (count > 0) {
    if (count & 1) result += chunk; // add current chunk if bit is set
    chunk += chunk;                 // double the chunk
    count >>= 1;                    // halve the count
  }
  return result;
};
```

**Gotchas:** Negative / `Infinity` counts must throw `RangeError`; fractional counts are floored.

---

## 23. String.prototype.trim

**What it does:** Removes leading and trailing whitespace and returns a new string (original strings are
immutable).

**How it works:** A regex (`^\s+` and `\s+$`) is the cleanest. The manual two-pointer version is worth
knowing when interviewers ban regex — walk inward from both ends past whitespace, then slice.

**Tags:** `Amazon` `TCS` `Infosys` `Wipro` `Cognizant`

```js
// Regex version
String.prototype.myTrim = function () {
  return this.replace(/^\s+/, '').replace(/\s+$/, '');
};

// Manual two-pointer version (no regex)
String.prototype.myTrimManual = function () {
  const ws = new Set([' ', '\t', '\n', '\r', '\f', '\v', '\u00A0']);
  let start = 0, end = this.length - 1;
  while (start <= end && ws.has(this[start])) start++;
  while (end >= start && ws.has(this[end])) end--;
  return this.slice(start, end + 1);
};

// '   hi  '.myTrim() -> 'hi'
```

**Gotchas:** Strings are immutable, so return a new one; remember whitespace includes `\t`, `\n`, etc.

---

## 24. A robust typeof (getType)

**What it does:** Returns a precise, lowercase type string for **any** value — fixing the famous
`typeof null === 'object'` bug and distinguishing arrays, dates, regexes, maps, etc., which plain
`typeof` lumps together as `'object'`.

**How it works:** `Object.prototype.toString.call(value)` yields `"[object Type]"`; slice out the `Type`
and lowercase it. This is the same realm-safe trick behind `Array.isArray`.

**Tags:** `Amazon` `Google` `Microsoft` `Adobe` `Flipkart`

```js
function getType(value) {
  // "[object Null]" -> "null", "[object Array]" -> "array", etc.
  return Object.prototype.toString.call(value).slice(8, -1).toLowerCase();
}

getType(null);        // -> "null"      (typeof would say "object")
getType([]);          // -> "array"     (typeof would say "object")
getType(new Date());  // -> "date"
getType(/x/);         // -> "regexp"
getType(42);          // -> "number"
getType(() => {});    // -> "function"
```

**Gotchas:** This is the go-to answer for "how do you reliably detect type in JS?" — name-drop
`typeof null` and the array/object ambiguity.

---

## How to remember all of this (quick recall map)

| If the question is… | The core trick is… |
|----------------------|--------------------|
| `map` / `filter` / `forEach` | loop + `callback.call(thisArg, val, i, arr)` + skip holes |
| `reduce` | seed accumulator (use `arguments.length >= 2`), throw on empty + no seed |
| `some` / `every` / `find` | short-circuit; mind empty-array defaults |
| `flat` | recurse while `depth > 0` |
| `indexOf` vs `includes` | `===` vs SameValueZero (the `NaN` case) |
| `call` / `apply` | attach fn to object via a `Symbol` key, invoke, delete |
| `bind` | closure + partial args + `this instanceof boundFn` for `new` |
| `new` | `Object.create(proto)` → run ctor → honor object return |
| `instanceof` | climb the prototype chain with `getPrototypeOf` |
| deep clone | recurse + `WeakMap` for cycles + special types |
| `Promise.all` / `allSettled` / `any` | counter + results-by-index + the right resolve/reject rule |
| type detection | `Object.prototype.toString.call(x)` |

> **Interview tip:** When asked to implement a built-in, *narrate the contract first* (inputs, return
> value, edge cases), then write the happy path, then layer in the edge cases (callback validation, holes,
> `thisArg`, `NaN`, empty inputs). Interviewers score the **edge cases** as much as the core logic.
