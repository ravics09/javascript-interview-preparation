# JavaScript Patterns Asked in Company Interviews

A curated collection of the most frequently asked JavaScript "machine coding" / implementation
patterns. Each pattern includes:

- **What it is** — a short definition.
- **When to use it** — the signals that tell you this pattern is the right tool.
- **Real-world use cases** — concrete scenarios where it shows up in production.
- **Company tags** — where this style of question has commonly been reported in interview rounds.
- **Implementation** — clean, commented code, plus common follow-up variants.
- **Pitfalls / gotchas** — what interviewers probe after you write the happy path.

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

### Quick "When to use" cheat sheet

| Pattern | Reach for it when… |
|---------|--------------------|
| Debounce | You want to act **only after activity stops** (search box, autosave, resize). |
| Throttle | You want to act **at a steady max rate** during continuous activity (scroll, mousemove, drag). |
| Currying | You want to **pre-fill arguments** and build specialized functions / improve reuse. |
| Deep Clone | You need a **fully independent copy** of nested data without shared references. |
| Compose / Pipe | You want to **chain small pure functions** into a readable data pipeline. |
| Memoization | A function is **pure and expensive**, and inputs repeat. |
| Polyfills (map/reduce/bind…) | You must **support old environments** or prove you understand the built-in. |
| Promise.all / race / any | You're coordinating **multiple async tasks** with different "done" rules. |
| Promisify | You're wrapping a **callback-style API** to use with async/await. |
| EventEmitter | Parts of the app need to **communicate without tight coupling**. |
| Flatten | You have **arbitrarily nested arrays** to normalize. |
| Retry | An async op **fails transiently** (network, rate limits) and is safe to repeat. |
| Singleton | You need **exactly one shared instance** (config, cache, DB connection). |
| Observer | Many parts must **react to one source's state changes**. |
| Factory | Object creation logic is **complex or conditional** and should be centralized. |

---

## 1. Debounce

**What:** Delays invoking a function until a period of inactivity has elapsed. Every new call resets the
timer, so the function ultimately runs **once**, after the burst of calls has stopped.

**When to use it:**
- The event fires rapidly but you only care about the **final state** after the user pauses.
- Each invocation is relatively **expensive** (network call, heavy computation, DOM write).
- It's acceptable — even desirable — to **skip** intermediate calls.

**Real-world use cases:**
- **Search-as-you-type / autocomplete** — wait until the user stops typing before hitting the API.
- **Autosave** in editors (Google Docs style) — save a few hundred ms after the last keystroke.
- **Window `resize`** — recompute layout only once the user finishes dragging the window edge.
- **Form validation** — validate after the user stops editing a field.

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

**Pitfalls:** Forgetting to preserve `this`/`args`; not exposing a `cancel` method for cleanup on unmount;
confusing leading vs. trailing edge behavior.

---

## 2. Throttle

**What:** Ensures a function runs **at most once every `limit` milliseconds**, no matter how many times
it's triggered. Unlike debounce (which waits for a pause), throttle fires at a **steady cadence** during
continuous activity.

**When to use it:**
- The event fires continuously and you want **regular updates**, not just the final one.
- You need to **cap the rate** of an expensive handler to protect performance.
- Dropping *some* intermediate events is fine, but you can't wait for activity to fully stop.

**Real-world use cases:**
- **Scroll handlers** — update a sticky header / "scroll progress" bar every ~100ms.
- **Infinite scroll** — check "near bottom?" at a fixed rate instead of on every scroll tick.
- **Mousemove / drag-and-drop** — update element position smoothly without flooding the main thread.
- **Rate-limiting API calls** behind a button that can be mashed.

**Debounce vs. Throttle:** Debounce = "wait until it's quiet, then act once." Throttle = "act on a fixed
heartbeat while it's noisy." Search box → debounce. Scroll position → throttle.

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

**Pitfalls:** Missing the **trailing call** (the very last event may be dropped); mixing up throttle with
debounce semantics in the explanation.

---

## 3. Currying

**What:** Transform a function `f(a, b, c)` so it can be called as `f(a)(b)(c)` or `f(a, b)(c)`, etc.
A classic test of closures and recursion.

**When to use it:**
- You want to **fix some arguments now** and supply the rest later (partial application).
- You're building **reusable, specialized functions** from a generic one.
- You want cleaner **point-free / functional pipelines** where functions take one argument at a time.

**Real-world use cases:**
- **Configuration helpers** — `const log = curriedLog("ERROR"); log("disk full")`.
- **Event handler factories** — `const onClick = handleClick(itemId)` in React lists.
- **Reusable validators / formatters** — `const toUSD = formatCurrency("USD")`.
- Libraries like **Ramda/Lodash-fp** rely heavily on currying for composition.

**Tags:** `Microsoft` `Adobe` `PayPal` `Cred` `Flipkart` `Oracle` `ServiceNow`

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

**Pitfalls:** Relying on `fn.length` breaks with default/rest params; not handling multiple args per call.

---

## 4. Deep Clone

**What:** Create a fully independent copy of an object, handling nested objects, arrays, `Date`, `Map`,
`Set`, and **circular references**. Tests memory/reference understanding.

**When to use it:**
- You must **mutate a copy** without affecting the original (shallow copy / spread isn't enough).
- The data is **deeply nested** and shares references you don't want leaking.
- You need **snapshots** of state for undo/redo, time-travel, or comparison.

**Real-world use cases:**
- **Immutable state updates** in Redux/Vuex when nested objects change.
- **Undo/redo history** — store independent snapshots of a document/canvas.
- **Cloning default config/templates** before customizing per user.
- **Caching API responses** so downstream mutations don't corrupt the cache.

> In modern environments prefer `structuredClone()` for most cases; interviewers ask you to *implement*
> it to test understanding, and because it doesn't clone functions/DOM nodes.

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

**Pitfalls:** `JSON.parse(JSON.stringify(obj))` loses `undefined`, functions, `Date` (becomes string),
`Map`/`Set`, and throws on circular refs — mention this trade-off.

---

## 5. Function Composition (compose & pipe)

**What:** Combine multiple functions into one. `compose` runs **right-to-left**; `pipe` runs
**left-to-right**.

**When to use it:**
- You have several **small, single-purpose, pure** transformations to apply in sequence.
- You want to **name a pipeline** of steps rather than nesting calls or using temp variables.
- You're embracing a **functional style** and want reusable, testable building blocks.

**Real-world use cases:**
- **Data transformation pipelines** — `pipe(parse, normalize, validate, save)`.
- **Middleware chains** (Redux middleware, Express-style handlers) compose via this pattern.
- **String/number formatting** — `pipe(trim, toLowerCase, slugify)`.
- **Selectors** that derive view data from raw state in steps.

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

**Pitfalls:** Order confusion (compose is right-to-left); only threads a single value — multi-arg steps
need currying/adapters.

---

## 6. Memoization

**What:** Cache results of expensive function calls keyed by their arguments, returning the cached result
on repeat inputs. Tests closures and caching.

**When to use it:**
- The function is **pure** (same input ⇒ same output, no side effects).
- It's **computationally expensive** or called **repeatedly with the same inputs**.
- You can afford the **extra memory** to store results.

**Real-world use cases:**
- **Expensive calculations** — Fibonacci, factorial, layout/geometry math.
- **Derived data in UI** — React's `useMemo` / Reselect selectors avoid recomputing on every render.
- **Caching pure API request transformations** keyed by params.
- **Dynamic programming** solutions (top-down memoized recursion).

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

**Pitfalls:** `JSON.stringify` keys fail for functions/circular args and ignore arg order subtleties;
unbounded cache can leak memory (consider an LRU/size cap); never memoize impure functions.

---

## 7. Polyfill: Array.prototype.map

**What:** Re-implement `map` from scratch. Gateway question that leads into `filter`, `forEach`, `reduce`.

**When to use it (polyfills in general):**
- You must **support legacy browsers/runtimes** that lack a modern method.
- You want to **demonstrate deep understanding** of how the built-in behaves (callback signature,
  `thisArg`, sparse arrays, immutability).

**Real-world use cases:**
- Shipping libraries that **run in old environments** (older IE, embedded WebViews).
- **Babel/core-js** style transpilation polyfills for newer Array/String/Promise APIs.
- Building a **mental model** of the standard library that helps debug edge cases.

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

**Pitfalls:** Skipping the `thisArg`, ignoring **sparse arrays** (`i in this`), or mutating the source.

---

## 8. Polyfill: Array.prototype.reduce

**What:** Re-implement `reduce`, correctly handling the **optional initial value** (and the empty-array
error case).

**When to use it:** Same rationale as map polyfills — legacy support and demonstrating mastery of the
trickiest array method (initial-value semantics trip many people up).

**Real-world use cases:**
- The foundation under **sum/group-by/flatten/compose** implementations.
- Building **aggregation utilities** (totals, frequency maps, pipelines).

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

**Pitfalls:** Not distinguishing "no initial value provided" (use `arguments.length`, not `!initialValue`);
not throwing on empty array with no initial value.

---

## 9. Polyfill: Function.prototype.bind / call / apply

**What:** Re-implement the `this`-binding utilities. Tests deep understanding of `this` and execution
context.

**When to use it:**
- You need to **fix `this`** for a callback (event handlers, `setTimeout`, passing methods around).
- You want **partial application** (pre-bound arguments) via `bind`.
- Demonstrating you understand how the engine resolves `this`.

**Real-world use cases:**
- **Pre-React class components** binding methods in the constructor (`this.handleClick.bind(this)`).
- **Borrowing methods** — `Array.prototype.slice.call(arguments)` to arrayify array-likes.
- **Function.prototype.apply** to spread args (`Math.max.apply(null, arr)` pre-spread syntax).

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

**Pitfalls:** Polluting the context object (use a `Symbol` and `delete`); not handling `new` with a bound
function; forgetting to merge bound + call-time args.

---

## 10. Promise.all Polyfill

**What:** Resolve when **all** promises resolve (preserving input order); reject as soon as **any** rejects.

**When to use it:**
- You have **independent async tasks** and need **all** results before continuing.
- A single failure should **abort** the whole batch (fail-fast).

**Real-world use cases:**
- **Parallel API calls** for a dashboard — fetch user, settings, and notifications together.
- **Loading multiple resources** (images, scripts, config) before rendering.
- **Batch DB queries** that must all succeed for a transaction-like flow.

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

**Pitfalls:** Losing **result order** (use the index, not push); not wrapping non-promise values with
`Promise.resolve`; forgetting the empty-array case.

---

## 11. Promise.allSettled / race / any

**What:** The common follow-ups to `Promise.all`, each with different "done" rules:
- **allSettled** — wait for all, never rejects; reports each outcome.
- **race** — settles as soon as the **first** promise settles (resolve *or* reject).
- **any** — resolves on the **first fulfillment**; rejects only if **all** reject.

**When to use it:**
- **allSettled** — you want **every** result even if some fail (no fail-fast).
- **race** — you care about the **fastest** outcome, or want a **timeout**.
- **any** — you want the **first success** and can tolerate some failures.

**Real-world use cases:**
- **allSettled** — fire several analytics/notification calls; log which failed but don't block.
- **race** — `Promise.race([fetchData(), timeout(5000)])` to enforce a request timeout.
- **any** — query **multiple mirrors/CDNs** and use whichever responds successfully first.

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

**Pitfalls:** Confusing `race` (first to settle, even rejection) with `any` (first to **fulfill**).

---

## 12. Promisify

**What:** Convert a Node-style callback function `(err, data) => {}` into a **promise-returning** function
so it works with `async/await`.

**When to use it:**
- You're consuming an **older callback-based API** but want modern async syntax.
- You want to **compose** callback APIs with `Promise.all`, `await`, etc.

**Real-world use cases:**
- Wrapping legacy **Node core APIs** (`fs.readFile`) — Node ships `util.promisify` for exactly this.
- Modernizing **third-party SDKs** that still use callbacks.
- Turning **`setTimeout`** into an awaitable `delay(ms)` helper.

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

**Pitfalls:** Losing `this` binding; assuming the callback is always `(err, data)` (some APIs differ).

---

## 13. EventEmitter (Pub/Sub)

**What:** Implement `on`, `off`, `emit`, and `once`. A subject lets parts of the app **subscribe** to named
events and get **notified** when they fire. Tests OOP and data-structure design.

**When to use it:**
- Components need to communicate but should stay **decoupled** (no direct references).
- You have a **one-to-many** relationship — one event, many interested listeners.
- You want **dynamic** subscribe/unsubscribe at runtime.

**Real-world use cases:**
- **Node.js** core is built on `EventEmitter` (streams, sockets, HTTP servers).
- **DOM events** and custom event buses in front-end apps.
- **Cross-component messaging** — e.g., a global "user-logged-out" event many widgets react to.
- **WebSocket / real-time** message dispatching.

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

**Pitfalls:** Memory leaks from never unsubscribing; iterating while mutating the listener set; `once`
wrapper must remove the **wrapper**, not the original callback.

---

## 14. Flatten a Nested Array

**What:** Flatten arbitrarily nested arrays to a given depth. Tests recursion (and an iterative follow-up).

**When to use it:**
- Your data arrives **nested** but you need a **flat list** to render/iterate/aggregate.
- You need control over **how deep** to flatten.

**Real-world use cases:**
- **Normalizing tree/menu/category data** into a flat list for search or rendering.
- **Combining paginated/grouped API results** (`[[...], [...]]`) into one array.
- **Comment threads / nested replies** flattened for display.

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

**Pitfalls:** Stack overflow on very deep arrays (offer the iterative version); honoring the `depth` arg.

---

## 15. Retry with Backoff

**What:** Retry a failing async operation N times, often with **exponential backoff** between attempts.
Tests async control flow and error handling.

**When to use it:**
- Failures are **transient/intermittent** (network blips, rate limits, cold starts).
- The operation is **idempotent** (safe to repeat without side effects).
- A short delay is likely to let the issue **resolve itself**.

**Real-world use cases:**
- **Flaky network requests** — retry a fetch a few times before surfacing an error.
- **Rate-limited APIs (HTTP 429)** — back off and retry instead of failing immediately.
- **Connecting to a DB/queue** that may not be ready yet at startup.
- **Cloud SDK calls** (most AWS/GCP SDKs have built-in retry with backoff).

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

**Pitfalls:** Retrying **non-idempotent** operations (double charges!); no cap/jitter causing thundering
herd; retrying errors that will never succeed (e.g., 400/auth errors).

---

## 16. Singleton Pattern

**What:** Guarantee a class has **only one instance** with a single global access point. Classic design
pattern.

**When to use it:**
- Exactly **one shared instance** should exist across the app.
- That instance manages **shared/global state or a costly resource**.

**Real-world use cases:**
- **App configuration / feature flags** loaded once and read everywhere.
- **Database connection pool** or HTTP client reused across the app.
- **Logger** or **caching layer** shared by all modules.
- **Redux store** is effectively a singleton source of truth.

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

**Pitfalls:** Singletons act as **hidden global state** — they hurt testability and can cause coupling;
mention this trade-off. (In JS, a frozen module-level object is often a simpler "singleton".)

---

## 17. Observer Pattern

**What:** A subject maintains a list of observers and **notifies** them of state changes. Foundation of
reactive UIs and state libraries. (EventEmitter is a close cousin — observers register interest and react.)

**When to use it:**
- One object's **state change** must automatically update **many dependents**.
- You want **loose coupling** between the source of truth and its consumers.

**Real-world use cases:**
- **Reactivity systems** — Vue's reactivity, MobX, RxJS observables.
- **UI bindings** — model changes auto-update the views watching it.
- **Stock tickers / live dashboards** — many widgets observe one data stream.
- **Notification systems** — subscribers get pushed updates.

**Observer vs. Pub/Sub:** Observer usually means observers are **directly registered** on the subject;
Pub/Sub adds an **event-channel/broker** in between for fuller decoupling.

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

**Pitfalls:** Forgetting to unsubscribe (leaks); errors in one observer breaking the notify loop (wrap in
try/catch if needed).

---

## 18. Factory Pattern

**What:** Delegate object creation to a factory function/method instead of calling `new` directly,
centralizing the "which object to build" logic.

**When to use it:**
- Object creation is **complex** or depends on **runtime conditions/config**.
- You want callers to depend on an **interface**, not concrete classes.
- You need to **swap implementations** without touching call sites.

**Real-world use cases:**
- **UI component factories** — build a widget based on a `type` from server config.
- **Cross-platform abstractions** — return the right notification/storage impl per environment.
- **Parsers/loaders** — pick a handler based on file type (`.csv` vs `.json`).
- **Database/driver selection** — create the correct client from a connection string.

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

**Pitfalls:** Letting the factory grow into a giant switch (consider a registry/map, as above); over-using
it where a plain constructor would do.

---

## How to Practice

1. **Implement from scratch** without looking at the solution.
2. **Handle edge cases** — empty inputs, `this` binding, circular references, sparse arrays.
3. **Be ready for follow-ups** — "now add a `cancel` method", "make it leading-edge", "avoid recursion".
4. **Explain when and why** — interviewers care as much about *choosing* the right pattern as coding it.
5. **Explain trade-offs** — time/space complexity, debounce vs throttle, singleton's hidden-state cost, etc.

---

*Contributions welcome. Add new patterns following the same format: What → When to use → Use cases →
Company tags → Implementation → Pitfalls.*
