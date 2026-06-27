# JavaScript Patterns Asked in Company Interviews

A curated collection of the most frequently asked JavaScript "machine coding" / implementation
patterns. Each pattern includes a short explanation, a working implementation, and **company tags**
indicating where this style of question has commonly been reported in interview rounds.

> **Note on company tags:** Tags are *indicative*, compiled from widely shared interview experiences
> (blogs, Glassdoor, LeetCode discuss, GreatFrontend, FrontendInterviewHandbook). Interview content
> changes over time and varies by role/level — treat tags as "this kind of company asks this kind of
> question," not as a guarantee.

## Table of Contents

1. [Debounce](#1-debounce)
2. [Throttle](#2-throttle)
3. [Currying](#3-currying)
4. [Deep Clone](#4-deep-clone)
5. [Function Composition (compose & pipe)](#5-function-composition-compose--pipe)
6. [Memoization](#6-memoization)
7. [Polyfill: Array.prototype.map](#7-polyfill-arrayprototypemap)
8. [Polyfill: Array.prototype.reduce](#8-polyfill-arrayprototypereduce)
9. [Polyfill: Function.prototype.bind / call / apply](#9-polyfill-functionprototypebind--call--apply)
10. [Promise.all Polyfill](#10-promiseall-polyfill)
11. [Promise.allSettled / race / any](#11-promiseallsettled--race--any)
12. [Promisify](#12-promisify)
13. [EventEmitter (Pub/Sub)](#13-eventemitter-pubsub)
14. [Flatten a Nested Array](#14-flatten-a-nested-array)
15. [Retry with Backoff](#15-retry-with-backoff)
16. [Singleton Pattern](#16-singleton-pattern)
17. [Observer Pattern](#17-observer-pattern)
18. [Factory Pattern](#18-factory-pattern)

---

## 1. Debounce

**What:** Delays invoking a function until a period of inactivity has elapsed. Every new call resets the
timer. Useful for search inputs, resize/scroll handlers, and autosave.

**Tags:** `Amazon` `Google` `Uber` `Microsoft` `Flipkart` `PayPal` `Atlassian` `Swiggy`

```js
function debounce(fn, delay) {
  let timer;
  return function (...args) {
    const context = this;
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(context, args), delay);
  };
}

// Bonus: leading-edge + cancel support (frequent follow-up)
function debounceAdvanced(fn, delay, { leading = false } = {}) {
  let timer = null;
  function debounced(...args) {
    const callNow = leading && !timer;
    clearTimeout(timer);
    timer = setTimeout(() => {
      timer = null;
      if (!leading) fn.apply(this, args);
    }, delay);
    if (callNow) fn.apply(this, args);
  }
  debounced.cancel = () => {
    clearTimeout(timer);
    timer = null;
  };
  return debounced;
}
```

---

## 2. Throttle

**What:** Ensures a function runs at most once every `limit` milliseconds, regardless of how many times
it's triggered. Useful for scroll, mousemove, and infinite-scroll handlers.

**Tags:** `Amazon` `Google` `Meta` `Uber` `Walmart` `Razorpay` `Adobe`

```js
function throttle(fn, limit) {
  let inThrottle = false;
  return function (...args) {
    const context = this;
    if (!inThrottle) {
      fn.apply(context, args);
      inThrottle = true;
      setTimeout(() => (inThrottle = false), limit);
    }
  };
}

// Timestamp-based variant (guarantees trailing accuracy)
function throttleByTime(fn, limit) {
  let last = 0;
  return function (...args) {
    const now = Date.now();
    if (now - last >= limit) {
      last = now;
      fn.apply(this, args);
    }
  };
}
```

---

## 3. Currying

**What:** Transform a function `f(a, b, c)` so it can be called as `f(a)(b)(c)` or `f(a, b)(c)`, etc.
A classic test of closures and recursion.

**Tags:** `Microsoft` `Adobe` `PayPal` `Cred` ` Flipkart` `Oracle` `ServiceNow`

```js
function curry(fn) {
  return function curried(...args) {
    if (args.length >= fn.length) {
      return fn.apply(this, args);
    }
    return (...next) => curried.apply(this, [...args, ...next]);
  };
}

// Usage
const sum = (a, b, c) => a + b + c;
const curriedSum = curry(sum);
curriedSum(1)(2)(3);   // 6
curriedSum(1, 2)(3);   // 6
curriedSum(1)(2, 3);   // 6
```

---

## 4. Deep Clone

**What:** Create a fully independent copy of an object, handling nested objects, arrays, `Date`, `Map`,
`Set`, and circular references. Tests memory/reference understanding.

**Tags:** `Amazon` `Google` `Uber` `Microsoft` `Atlassian` `Salesforce`

```js
function deepClone(value, seen = new WeakMap()) {
  if (value === null || typeof value !== "object") return value;
  if (value instanceof Date) return new Date(value);
  if (value instanceof RegExp) return new RegExp(value);
  if (seen.has(value)) return seen.get(value); // circular refs

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

  const result = Array.isArray(value) ? [] : {};
  seen.set(value, result);
  for (const key of Reflect.ownKeys(value)) {
    result[key] = deepClone(value[key], seen);
  }
  return result;
}
```

---

## 5. Function Composition (compose & pipe)

**What:** Combine multiple functions into one. `compose` runs right-to-left; `pipe` runs left-to-right.

**Tags:** `Meta` `Adobe` `Uber` `ThoughtWorks` `Gojek`

```js
const compose = (...fns) => (x) => fns.reduceRight((acc, fn) => fn(acc), x);
const pipe = (...fns) => (x) => fns.reduce((acc, fn) => fn(acc), x);

// Usage
const add2 = (n) => n + 2;
const double = (n) => n * 2;
compose(add2, double)(5); // add2(double(5)) = 12
pipe(add2, double)(5);    // double(add2(5)) = 14
```

---

## 6. Memoization

**What:** Cache results of expensive function calls keyed by arguments. Tests closures and caching.

**Tags:** `Amazon` `Google` `Microsoft` `Flipkart` `Intuit`

```js
function memoize(fn) {
  const cache = new Map();
  return function (...args) {
    const key = JSON.stringify(args);
    if (cache.has(key)) return cache.get(key);
    const result = fn.apply(this, args);
    cache.set(key, result);
    return result;
  };
}
```

---

## 7. Polyfill: Array.prototype.map

**What:** Re-implement `map` from scratch. Gateway question for `filter`, `forEach`, `reduce`.

**Tags:** `Amazon` `Walmart` `Paytm` `Flipkart` `Zomato`

```js
Array.prototype.myMap = function (callback, thisArg) {
  if (typeof callback !== "function") throw new TypeError(callback + " is not a function");
  const result = [];
  for (let i = 0; i < this.length; i++) {
    if (i in this) result[i] = callback.call(thisArg, this[i], i, this);
  }
  return result;
};
```

---

## 8. Polyfill: Array.prototype.reduce

**What:** Re-implement `reduce`, correctly handling the optional initial value.

**Tags:** `Amazon` `Microsoft` `Uber` `PhonePe`

```js
Array.prototype.myReduce = function (callback, initialValue) {
  if (typeof callback !== "function") throw new TypeError(callback + " is not a function");
  let accumulator = initialValue;
  let startIndex = 0;

  if (arguments.length < 2) {
    while (startIndex < this.length && !(startIndex in this)) startIndex++;
    if (startIndex >= this.length) throw new TypeError("Reduce of empty array with no initial value");
    accumulator = this[startIndex++];
  }

  for (let i = startIndex; i < this.length; i++) {
    if (i in this) accumulator = callback(accumulator, this[i], i, this);
  }
  return accumulator;
};
```

---

## 9. Polyfill: Function.prototype.bind / call / apply

**What:** Re-implement `this`-binding utilities. Tests deep understanding of `this`.

**Tags:** `Google` `Microsoft` `Amazon` `Adobe` `Cred` `Razorpay`

```js
Function.prototype.myCall = function (context, ...args) {
  context = context || globalThis;
  const fnKey = Symbol("fn");
  context[fnKey] = this;
  const result = context[fnKey](...args);
  delete context[fnKey];
  return result;
};

Function.prototype.myApply = function (context, args = []) {
  return this.myCall(context, ...args);
};

Function.prototype.myBind = function (context, ...boundArgs) {
  const fn = this;
  return function (...callArgs) {
    return fn.apply(context, [...boundArgs, ...callArgs]);
  };
};
```

---

## 10. Promise.all Polyfill

**What:** Resolve when all promises resolve (preserving order); reject as soon as any rejects.

**Tags:** `Amazon` `Google` `Uber` `Atlassian` `Meta` `Swiggy`

```js
function promiseAll(promises) {
  return new Promise((resolve, reject) => {
    const results = [];
    let completed = 0;
    if (promises.length === 0) return resolve(results);

    promises.forEach((p, index) => {
      Promise.resolve(p).then(
        (value) => {
          results[index] = value;
          completed++;
          if (completed === promises.length) resolve(results);
        },
        reject
      );
    });
  });
}
```

---

## 11. Promise.allSettled / race / any

**What:** Common follow-ups to `Promise.all`.

**Tags:** `Amazon` `Microsoft` `Uber` `Meta` `Salesforce`

```js
function promiseAllSettled(promises) {
  return Promise.all(
    promises.map((p) =>
      Promise.resolve(p).then(
        (value) => ({ status: "fulfilled", value }),
        (reason) => ({ status: "rejected", reason })
      )
    )
  );
}

function promiseRace(promises) {
  return new Promise((resolve, reject) => {
    promises.forEach((p) => Promise.resolve(p).then(resolve, reject));
  });
}

function promiseAny(promises) {
  return new Promise((resolve, reject) => {
    let rejectionCount = 0;
    const errors = [];
    promises.forEach((p, i) =>
      Promise.resolve(p).then(resolve, (err) => {
        errors[i] = err;
        rejectionCount++;
        if (rejectionCount === promises.length) {
          reject(new AggregateError(errors, "All promises were rejected"));
        }
      })
    );
  });
}
```

---

## 12. Promisify

**What:** Convert a Node-style callback function `(err, data) => {}` into a promise-returning function.

**Tags:** `Microsoft` `Amazon` `Oracle` `ServiceNow`

```js
function promisify(fn) {
  return function (...args) {
    return new Promise((resolve, reject) => {
      fn.call(this, ...args, (err, data) => {
        if (err) reject(err);
        else resolve(data);
      });
    });
  };
}
```

---

## 13. EventEmitter (Pub/Sub)

**What:** Implement `on`, `off`, `emit`, and `once`. Tests OOP and data-structure design.

**Tags:** `Amazon` `Uber` `Atlassian` `Meta` `Flipkart` `Cred`

```js
class EventEmitter {
  constructor() {
    this.listeners = new Map();
  }
  on(event, cb) {
    if (!this.listeners.has(event)) this.listeners.set(event, new Set());
    this.listeners.get(event).add(cb);
    return () => this.off(event, cb); // unsubscribe handle
  }
  off(event, cb) {
    this.listeners.get(event)?.delete(cb);
  }
  once(event, cb) {
    const wrapper = (...args) => {
      cb(...args);
      this.off(event, wrapper);
    };
    this.on(event, wrapper);
  }
  emit(event, ...args) {
    this.listeners.get(event)?.forEach((cb) => cb(...args));
  }
}
```

---

## 14. Flatten a Nested Array

**What:** Flatten arbitrarily nested arrays to a given depth. Tests recursion.

**Tags:** `Amazon` `Google` `Microsoft` `Walmart` `PayPal`

```js
function flatten(arr, depth = Infinity) {
  return arr.reduce((acc, item) => {
    if (Array.isArray(item) && depth > 0) {
      acc.push(...flatten(item, depth - 1));
    } else {
      acc.push(item);
    }
    return acc;
  }, []);
}

// Iterative version (stack) — common follow-up to avoid recursion
function flattenIterative(arr) {
  const stack = [...arr];
  const result = [];
  while (stack.length) {
    const next = stack.pop();
    if (Array.isArray(next)) stack.push(...next);
    else result.unshift(next);
  }
  return result;
}
```

---

## 15. Retry with Backoff

**What:** Retry a failing async operation N times, often with exponential backoff. Tests async control flow.

**Tags:** `Amazon` `Uber` `Stripe` `Atlassian` `Razorpay`

```js
async function retry(fn, retries = 3, delay = 500) {
  let lastError;
  for (let attempt = 0; attempt <= retries; attempt++) {
    try {
      return await fn();
    } catch (err) {
      lastError = err;
      if (attempt < retries) {
        await new Promise((res) => setTimeout(res, delay * 2 ** attempt));
      }
    }
  }
  throw lastError;
}
```

---

## 16. Singleton Pattern

**What:** Guarantee a class has only one instance with a global access point. Classic design pattern.

**Tags:** `Microsoft` `Oracle` `SAP` `Adobe`

```js
class Config {
  constructor() {
    if (Config.instance) return Config.instance;
    this.settings = {};
    Config.instance = this;
  }
  set(key, value) { this.settings[key] = value; }
  get(key) { return this.settings[key]; }
}

const a = new Config();
const b = new Config();
console.log(a === b); // true
```

---

## 17. Observer Pattern

**What:** A subject maintains a list of observers and notifies them of state changes. Foundation of
reactive UIs and state libraries.

**Tags:** `Amazon` `Meta` `Adobe` `ThoughtWorks`

```js
class Subject {
  constructor() {
    this.observers = [];
  }
  subscribe(observer) {
    this.observers.push(observer);
  }
  unsubscribe(observer) {
    this.observers = this.observers.filter((o) => o !== observer);
  }
  notify(data) {
    this.observers.forEach((observer) => observer.update(data));
  }
}
```

---

## 18. Factory Pattern

**What:** Delegate object creation to a factory function/method instead of using `new` directly.

**Tags:** `Microsoft` `Oracle` `SAP` `Walmart`

```js
function shapeFactory(type, options) {
  const shapes = {
    circle: () => ({ type: "circle", area: () => Math.PI * options.r ** 2 }),
    square: () => ({ type: "square", area: () => options.side ** 2 }),
    rectangle: () => ({ type: "rectangle", area: () => options.w * options.h }),
  };
  const create = shapes[type];
  if (!create) throw new Error(`Unknown shape: ${type}`);
  return create();
}
```

---

## How to Practice

1. **Implement from scratch** without looking at the solution.
2. **Handle edge cases** — empty inputs, `this` binding, circular references, sparse arrays.
3. **Be ready for follow-ups** — "now add a `cancel` method", "make it leading-edge", "avoid recursion".
4. **Explain trade-offs** — time/space complexity, when to use debounce vs throttle, etc.

---

*Contributions welcome. Add new patterns following the same format: explanation, company tags, and a
clean, commented implementation.*
