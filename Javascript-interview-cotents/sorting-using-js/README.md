# Sorting Algorithms in Vanilla JavaScript

A complete, interview-focused guide to the classic sorting algorithms, implemented **from scratch in
vanilla JavaScript** — no built-in `Array.prototype.sort()` used in the core implementations.

Each algorithm includes:

- **What it is & how it works** — the intuition, step by step.
- **Complexity** — time (best / average / worst) and space.
- **Properties** — stable? in-place? adaptive?
- **When to use it** — the situations where it's the right choice.
- **Company tags** — where this style of question has commonly been reported in interviews.
- **Implementation** — clean, commented vanilla JS.

> At the **end of the file** there's a section showing how you'd achieve the same result with the
> **built-in `sort()`** — only as a reference for real-world code, not as a substitute for understanding
> the algorithms.

> **Note on company tags:** Tags are *indicative*, compiled from widely shared interview experiences
> (Glassdoor, LeetCode discuss, blogs). They mean "this kind of company asks this kind of question," not
> a guarantee.

## Table of Contents

1. [Big-O Comparison Cheat Sheet](#big-o-comparison-cheat-sheet)
2. [Bubble Sort](#1-bubble-sort)
3. [Selection Sort](#2-selection-sort)
4. [Insertion Sort](#3-insertion-sort)
5. [Merge Sort](#4-merge-sort)
6. [Quick Sort](#5-quick-sort)
7. [Heap Sort](#6-heap-sort)
8. [Counting Sort](#7-counting-sort)
9. [Radix Sort](#8-radix-sort)
10. [Bucket Sort](#9-bucket-sort)
11. [Shell Sort](#10-shell-sort)
12. [Doing it with the built-in `sort()`](#doing-it-with-the-built-in-sort)
13. [How to Pick the Right Sort](#how-to-pick-the-right-sort)

---

## Big-O Comparison Cheat Sheet

| Algorithm | Best | Average | Worst | Space | Stable | In-place |
|-----------|------|---------|-------|-------|--------|----------|
| Bubble Sort | O(n) | O(n²) | O(n²) | O(1) | ✅ Yes | ✅ Yes |
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) | ❌ No | ✅ Yes |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) | ✅ Yes | ✅ Yes |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) | ✅ Yes | ❌ No |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) | ❌ No | ✅ Yes |
| Heap Sort | O(n log n) | O(n log n) | O(n log n) | O(1) | ❌ No | ✅ Yes |
| Counting Sort | O(n + k) | O(n + k) | O(n + k) | O(k) | ✅ Yes | ❌ No |
| Radix Sort | O(nk) | O(nk) | O(nk) | O(n + k) | ✅ Yes | ❌ No |
| Bucket Sort | O(n + k) | O(n + k) | O(n²) | O(n) | ✅ Yes* | ❌ No |
| Shell Sort | O(n log n) | O(n^1.25)† | O(n²) | O(1) | ❌ No | ✅ Yes |

\* Bucket sort's stability depends on the sub-sort used per bucket.
† Shell sort's average depends on the gap sequence; bounds vary.
*`n` = number of elements, `k` = range/number of buckets/digits.*

---

## 1. Bubble Sort

**What it is & how it works:** Repeatedly step through the list, compare each **adjacent pair**, and swap
them if they're in the wrong order. After each full pass the largest unsorted element "bubbles up" to its
correct position at the end. An optimized version stops early if a pass makes no swaps (array already
sorted).

**Complexity:** Best **O(n)** (already sorted, with the early-exit flag), Average/Worst **O(n²)**.
Space **O(1)**.

**Properties:** Stable ✅ · In-place ✅ · Adaptive ✅ (with the swap flag).

**When to use it:**
- Teaching/learning, tiny arrays, or when simplicity beats performance.
- Detecting whether a nearly-sorted array needs minimal work (early exit).
- Rarely used in production — it's mostly an interview warm-up to test loop/swap fundamentals.

**Tags:** `Amazon` `TCS` `Infosys` `Wipro` `Cognizant` `Accenture`

```js
function bubbleSort(arr) {
  const n = arr.length;
  for (let i = 0; i < n - 1; i++) {
    let swapped = false;
    // Last i elements are already in place
    for (let j = 0; j < n - 1 - i; j++) {
      if (arr[j] > arr[j + 1]) {
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]]; // swap
        swapped = true;
      }
    }
    if (!swapped) break; // already sorted -> early exit
  }
  return arr;
}

// bubbleSort([5, 1, 4, 2, 8]) -> [1, 2, 4, 5, 8]
```

---

## 2. Selection Sort

**What it is & how it works:** Divide the array into a sorted part (front) and unsorted part (rest). On
each pass, **find the minimum** of the unsorted part and swap it into the next sorted position. It always
does the same number of comparisons regardless of input.

**Complexity:** Best/Average/Worst **O(n²)**. Space **O(1)**. Notably, it makes at most **O(n) swaps** —
useful when writes are expensive.

**Properties:** Stable ❌ (the long-distance swap can reorder equal keys) · In-place ✅ · Not adaptive.

**When to use it:**
- When the **cost of swapping/writing is high** and you want to minimize writes (only n−1 swaps).
- Small arrays where simplicity matters and stability is irrelevant.

**Tags:** `TCS` `Infosys` `Capgemini` `Amazon` `Oracle`

```js
function selectionSort(arr) {
  const n = arr.length;
  for (let i = 0; i < n - 1; i++) {
    let minIndex = i;
    for (let j = i + 1; j < n; j++) {
      if (arr[j] < arr[minIndex]) minIndex = j;
    }
    if (minIndex !== i) {
      [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]]; // swap min into place
    }
  }
  return arr;
}

// selectionSort([64, 25, 12, 22, 11]) -> [11, 12, 22, 25, 64]
```

---

## 3. Insertion Sort

**What it is & how it works:** Build the sorted array one item at a time. Take the next element and
**insert it into its correct position** among the already-sorted elements on its left, shifting larger
elements one step right. This is how most people sort playing cards in hand.

**Complexity:** Best **O(n)** (already sorted), Average/Worst **O(n²)**. Space **O(1)**.

**Properties:** Stable ✅ · In-place ✅ · Adaptive ✅ (fast on nearly-sorted data).

**When to use it:**
- **Small** or **nearly-sorted** datasets — it's genuinely fast here.
- As the base case inside hybrid sorts (e.g., Timsort/Introsort switch to insertion sort for small
  partitions).
- **Online sorting** — when elements arrive one at a time and must be kept sorted.

**Tags:** `Amazon` `Microsoft` `Adobe` `Infosys` `Goldman Sachs`

```js
function insertionSort(arr) {
  const n = arr.length;
  for (let i = 1; i < n; i++) {
    const current = arr[i];
    let j = i - 1;
    // Shift larger elements one position to the right
    while (j >= 0 && arr[j] > current) {
      arr[j + 1] = arr[j];
      j--;
    }
    arr[j + 1] = current; // insert into the gap
  }
  return arr;
}

// insertionSort([12, 11, 13, 5, 6]) -> [5, 6, 11, 12, 13]
```

---

## 4. Merge Sort

**What it is & how it works:** A **divide-and-conquer** algorithm. Recursively split the array in half
until each piece has one element (which is sorted by definition), then **merge** sorted halves back
together in order. The merge step walks two sorted lists with two pointers, always taking the smaller
front element.

**Complexity:** Best/Average/Worst **O(n log n)** — guaranteed. Space **O(n)** (extra arrays for merging).

**Properties:** Stable ✅ · Not in-place (standard version) · Excellent for large data and linked lists.

**When to use it:**
- You need a **guaranteed O(n log n)** worst case (no quadratic blowup like Quick Sort).
- **Stability** matters (e.g., sorting records by one key while preserving another).
- **External sorting** of huge datasets that don't fit in memory, and sorting **linked lists**.

**Tags:** `Amazon` `Google` `Microsoft` `Uber` `Flipkart` `Goldman Sachs` `Adobe`

```js
function mergeSort(arr) {
  if (arr.length <= 1) return arr;

  const mid = Math.floor(arr.length / 2);
  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));

  return merge(left, right);
}

function merge(left, right) {
  const result = [];
  let i = 0, j = 0;

  while (i < left.length && j < right.length) {
    // "<=" keeps it STABLE (equal elements keep their original order)
    if (left[i] <= right[j]) {
      result.push(left[i++]);
    } else {
      result.push(right[j++]);
    }
  }
  // Append whatever remains
  while (i < left.length) result.push(left[i++]);
  while (j < right.length) result.push(right[j++]);

  return result;
}

// mergeSort([38, 27, 43, 3, 9, 82, 10]) -> [3, 9, 10, 27, 38, 43, 82]
```

---

## 5. Quick Sort

**What it is & how it works:** Another **divide-and-conquer** sort. Pick a **pivot**, **partition** the
array so elements smaller than the pivot go left and larger go right, then recursively sort each side.
The pivot ends up in its final sorted position after each partition.

**Complexity:** Best/Average **O(n log n)**, Worst **O(n²)** (bad pivots, e.g., already-sorted input with
a naive last-element pivot). Space **O(log n)** for the recursion stack.

**Properties:** Not stable (typical in-place version) · In-place ✅ · Usually the **fastest in practice**
due to cache-friendly access and low constant factors.

**When to use it:**
- General-purpose, **in-memory** sorting where average-case speed matters most.
- When extra memory is constrained (it sorts in place, unlike Merge Sort).
- Mitigate the worst case with **randomized** or **median-of-three** pivot selection.

**Tags:** `Amazon` `Google` `Microsoft` `Meta` `Uber` `Bloomberg` `Goldman Sachs` `Flipkart`

```js
function quickSort(arr, low = 0, high = arr.length - 1) {
  if (low < high) {
    const pivotIndex = partition(arr, low, high);
    quickSort(arr, low, pivotIndex - 1);  // sort left of pivot
    quickSort(arr, pivotIndex + 1, high); // sort right of pivot
  }
  return arr;
}

// Lomuto partition scheme using the last element as pivot
function partition(arr, low, high) {
  const pivot = arr[high];
  let i = low - 1; // boundary of elements smaller than pivot

  for (let j = low; j < high; j++) {
    if (arr[j] < pivot) {
      i++;
      [arr[i], arr[j]] = [arr[j], arr[i]];
    }
  }
  [arr[i + 1], arr[high]] = [arr[high], arr[i + 1]]; // place pivot
  return i + 1;
}

// quickSort([10, 7, 8, 9, 1, 5]) -> [1, 5, 7, 8, 9, 10]
```

> **Avoiding the O(n²) trap:** randomize the pivot, e.g.
> `const r = low + Math.floor(Math.random() * (high - low + 1)); [arr[r], arr[high]] = [arr[high], arr[r]];`
> before partitioning.

---

## 6. Heap Sort

**What it is & how it works:** Build a **max-heap** from the array (a complete binary tree where each
parent ≥ its children), then repeatedly swap the root (the max) with the last element, shrink the heap,
and **heapify** down to restore the heap property. Each extraction places one more element in its final
spot.

**Complexity:** Best/Average/Worst **O(n log n)** — guaranteed. Space **O(1)** (sorts in place using array
indices for the tree).

**Properties:** Not stable · In-place ✅ · No worst-case blowup like Quick Sort, but typically slower in
practice due to poor cache locality.

**When to use it:**
- You need **guaranteed O(n log n)** *and* **O(1) extra space** (Merge Sort gives the time but not the
  space; Quick Sort gives the space but not the worst-case guarantee).
- Building a **priority queue** / finding the **top-k** elements (the heap structure itself is the value).

**Tags:** `Amazon` `Google` `Microsoft` `Bloomberg` `Uber` `Oracle`

```js
function heapSort(arr) {
  const n = arr.length;

  // 1. Build a max-heap (start from last non-leaf node)
  for (let i = Math.floor(n / 2) - 1; i >= 0; i--) {
    heapify(arr, n, i);
  }

  // 2. Extract elements one by one
  for (let i = n - 1; i > 0; i--) {
    [arr[0], arr[i]] = [arr[i], arr[0]]; // move current max to the end
    heapify(arr, i, 0);                  // restore heap on the reduced range
  }
  return arr;
}

// Sift node i down so the subtree rooted at i satisfies the max-heap property
function heapify(arr, heapSize, i) {
  let largest = i;
  const left = 2 * i + 1;
  const right = 2 * i + 2;

  if (left < heapSize && arr[left] > arr[largest]) largest = left;
  if (right < heapSize && arr[right] > arr[largest]) largest = right;

  if (largest !== i) {
    [arr[i], arr[largest]] = [arr[largest], arr[i]];
    heapify(arr, heapSize, largest);
  }
}

// heapSort([12, 11, 13, 5, 6, 7]) -> [5, 6, 7, 11, 12, 13]
```

---

## 7. Counting Sort

**What it is & how it works:** A **non-comparison** sort. Count how many times each value occurs, compute
prefix sums to find each value's position, then place elements into the output array. Works only for
**integers (or mappable keys) within a known, limited range `k`**.

**Complexity:** **O(n + k)** time, **O(k)** space (plus output). Beats the O(n log n) comparison lower
bound because it doesn't compare elements.

**Properties:** Stable ✅ (when built with prefix sums and iterating from the end) · Not in-place.

**When to use it:**
- Sorting **integers / small-range keys** (ages, grades 0–100, ASCII chars) where `k` is not huge.
- As a **subroutine inside Radix Sort**.
- **Not** suitable when the value range `k` is much larger than `n` (wastes memory).

**Tags:** `Amazon` `Google` `Microsoft` `Flipkart` `Adobe`

```js
function countingSort(arr) {
  if (arr.length === 0) return arr;

  const min = Math.min(...arr);
  const max = Math.max(...arr);
  const count = new Array(max - min + 1).fill(0);

  // 1. Count occurrences
  for (const num of arr) count[num - min]++;

  // 2. Prefix sums -> position of each value
  for (let i = 1; i < count.length; i++) count[i] += count[i - 1];

  // 3. Build output from the end to keep it STABLE
  const output = new Array(arr.length);
  for (let i = arr.length - 1; i >= 0; i--) {
    const num = arr[i];
    output[--count[num - min]] = num;
  }
  return output;
}

// countingSort([4, 2, 2, 8, 3, 3, 1]) -> [1, 2, 2, 3, 3, 4, 8]
```

---

## 8. Radix Sort

**What it is & how it works:** A **non-comparison** sort for integers. Sort the numbers **digit by digit**,
from the least significant digit (LSD) to the most significant, using a **stable** sort (counting sort)
at each digit. After processing all digits, the array is fully sorted.

**Complexity:** **O(n·k)** where `k` is the number of digits (passes). Space **O(n + b)** where `b` is the
base (usually 10).

**Properties:** Stable ✅ · Not in-place · Linear-ish when `k` (digit count) is small relative to `n`.

**When to use it:**
- Large sets of **fixed-width integers** or strings (IDs, fixed-length keys, IP addresses).
- When the key length `k` is small, it can outperform O(n log n) comparison sorts.

**Tags:** `Amazon` `Google` `Microsoft` `Uber` `Bloomberg`

```js
function radixSort(arr) {
  if (arr.length === 0) return arr;

  const max = Math.max(...arr);
  // Process each digit place: 1, 10, 100, ...
  for (let exp = 1; Math.floor(max / exp) > 0; exp *= 10) {
    countingSortByDigit(arr, exp);
  }
  return arr;
}

function countingSortByDigit(arr, exp) {
  const n = arr.length;
  const output = new Array(n);
  const count = new Array(10).fill(0);

  // Count occurrences of each digit at this place
  for (let i = 0; i < n; i++) {
    const digit = Math.floor(arr[i] / exp) % 10;
    count[digit]++;
  }
  // Prefix sums
  for (let i = 1; i < 10; i++) count[i] += count[i - 1];

  // Build output (iterate from end for stability)
  for (let i = n - 1; i >= 0; i--) {
    const digit = Math.floor(arr[i] / exp) % 10;
    output[--count[digit]] = arr[i];
  }
  // Copy back
  for (let i = 0; i < n; i++) arr[i] = output[i];
}

// radixSort([170, 45, 75, 90, 802, 24, 2, 66]) -> [2, 24, 45, 66, 75, 90, 170, 802]
// (This version assumes non-negative integers.)
```

---

## 9. Bucket Sort

**What it is & how it works:** Distribute elements into a number of **buckets** based on their value
range, sort each bucket individually (often with insertion sort or recursively), then concatenate the
buckets in order. Works best when input is **uniformly distributed** over a range.

**Complexity:** Average **O(n + k)**, Worst **O(n²)** (all values land in one bucket). Space **O(n)**.

**Properties:** Stability depends on the per-bucket sort · Not in-place.

**When to use it:**
- Input is **uniformly distributed** floating-point numbers in a known range (e.g., `[0, 1)`).
- Sorting data that naturally **partitions into ranges** (e.g., scores into grade bands).

**Tags:** `Amazon` `Google` `Adobe` `Samsung`

```js
function bucketSort(arr, bucketCount = 5) {
  if (arr.length <= 1) return arr;

  const min = Math.min(...arr);
  const max = Math.max(...arr);
  const range = (max - min) / bucketCount || 1;

  const buckets = Array.from({ length: bucketCount }, () => []);

  // 1. Distribute into buckets
  for (const num of arr) {
    const idx = Math.min(Math.floor((num - min) / range), bucketCount - 1);
    buckets[idx].push(num);
  }

  // 2. Sort each bucket (insertion sort) and 3. concatenate
  const result = [];
  for (const bucket of buckets) {
    insertionSort(bucket);
    result.push(...bucket);
  }
  return result;
}

// Reuses the insertionSort defined above.
// bucketSort([0.42, 0.32, 0.73, 0.12, 0.91, 0.55]) -> [0.12, 0.32, 0.42, 0.55, 0.73, 0.91]
```

---

## 10. Shell Sort

**What it is & how it works:** A generalization of insertion sort. Instead of comparing only adjacent
elements, it compares and swaps elements a **gap** apart, then progressively shrinks the gap until it
becomes 1 (a final insertion-sort pass). Sorting distant elements early moves items closer to their final
spot quickly, reducing total shifting.

**Complexity:** Best **O(n log n)**, Worst **O(n²)** — depends heavily on the **gap sequence**. Space
**O(1)**.

**Properties:** Not stable · In-place ✅ · Adaptive (faster on partially sorted data).

**When to use it:**
- **Medium-sized** arrays where a simple in-place sort with better-than-O(n²) behavior is desired.
- Embedded/memory-constrained contexts (no recursion, no extra arrays).

**Tags:** `Amazon` `Microsoft` `Oracle` `Samsung`

```js
function shellSort(arr) {
  const n = arr.length;
  // Start with a big gap, then reduce it (gap = n/2, n/4, ... , 1)
  for (let gap = Math.floor(n / 2); gap > 0; gap = Math.floor(gap / 2)) {
    // Gapped insertion sort
    for (let i = gap; i < n; i++) {
      const temp = arr[i];
      let j = i;
      while (j >= gap && arr[j - gap] > temp) {
        arr[j] = arr[j - gap];
        j -= gap;
      }
      arr[j] = temp;
    }
  }
  return arr;
}

// shellSort([12, 34, 54, 2, 3]) -> [2, 3, 12, 34, 54]
```

---

## Doing it with the built-in `sort()`

Once you understand the algorithms above, in **real-world code** you'd almost always use JavaScript's
built-in `Array.prototype.sort()`. Modern JS engines (V8) implement it as **Timsort** — a hybrid of merge
sort and insertion sort — which is stable and runs in O(n log n).

```js
// IMPORTANT: default sort converts items to strings and sorts lexicographically.
[10, 2, 1].sort();            // [1, 10, 2]  ❌ not numeric!

// Numbers ascending — pass a comparator:
[10, 2, 1].sort((a, b) => a - b);   // [1, 2, 10] ✅

// Numbers descending:
[10, 2, 1].sort((a, b) => b - a);   // [10, 2, 1]

// Strings (locale-aware):
["banana", "apple", "cherry"].sort((a, b) => a.localeCompare(b));

// Sort objects by a property:
const users = [{ name: "Sam", age: 30 }, { name: "Ann", age: 25 }];
users.sort((a, b) => a.age - b.age); // by age ascending

// sort() mutates in place; use a copy if you need to preserve the original:
const sorted = [...users].sort((a, b) => a.age - b.age);

// toSorted() (ES2023) returns a NEW sorted array without mutating:
const safe = [3, 1, 2].toSorted((a, b) => a - b); // [1, 2, 3]
```

**Key gotchas with built-in `sort()`:**
- Default comparison is **string-based** — always pass a comparator for numbers.
- It **mutates** the original array (use spread or `toSorted()` to avoid that).
- The comparator must return a number (`<0`, `0`, `>0`); returning a boolean is a common bug.

---

## How to Pick the Right Sort

- **Small or nearly-sorted array?** → Insertion Sort (simple, adaptive, stable).
- **Need guaranteed O(n log n) + stability?** → Merge Sort.
- **Need guaranteed O(n log n) + O(1) space?** → Heap Sort.
- **Fastest general-purpose, average case, in memory?** → Quick Sort (randomized pivot).
- **Integers in a small range?** → Counting Sort.
- **Fixed-width integers / long keys?** → Radix Sort.
- **Uniformly distributed floats in a range?** → Bucket Sort.
- **Writing real application code?** → Built-in `sort()` with a proper comparator.

---

*Contributions welcome. Add new algorithms following the same format: What & how → Complexity →
Properties → When to use → Company tags → Implementation.*
