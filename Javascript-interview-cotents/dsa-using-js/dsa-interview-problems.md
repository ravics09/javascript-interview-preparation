# DSA Interview Problems by Pattern (JavaScript)

A companion to [`dsa-pattern.md`](./dsa-pattern.md). Where that file teaches you to *recognize* patterns,
this file gives you **many worked interview problems** for each pattern — with full JavaScript solutions
and detailed reasoning.

Every problem follows the same structure: **Problem → Company tags → Why this is a `<pattern>` problem →
Approach → Solution (JavaScript) → Complexity → 💡 Interview tip**.

> **Note on company tags:** Tags are *indicative*, compiled from widely shared interview experiences. They
> mean "this kind of company asks this kind of question," not a guarantee.

---

# 📑 Index of Patterns & Questions

Use this index to memorize the patterns and the questions under each. Click any item to jump to it.

### 1. [Sliding Window](#1-sliding-window)
- 1.1 [Maximum Sum Subarray of Size K](#11-maximum-sum-subarray-of-size-k)
- 1.2 [Smallest Subarray With Sum ≥ Target](#12-smallest-subarray-with-sum--target)
- 1.3 [Longest Substring Without Repeating Characters](#13-longest-substring-without-repeating-characters)
- 1.4 [Longest Substring with At Most K Distinct Characters](#14-longest-substring-with-at-most-k-distinct-characters)
- 1.5 [Fruits into Baskets](#15-fruits-into-baskets)
- 1.6 [Permutation in a String](#16-permutation-in-a-string)
- 1.7 [Longest Repeating Character Replacement](#17-longest-repeating-character-replacement)

### 2. [Two Pointers](#2-two-pointers)
- 2.1 [Pair with Target Sum (Sorted Array)](#21-pair-with-target-sum-sorted-array)
- 2.2 [Remove Duplicates from a Sorted Array](#22-remove-duplicates-from-a-sorted-array)
- 2.3 [Squares of a Sorted Array](#23-squares-of-a-sorted-array)
- 2.4 [Three Sum](#24-three-sum)
- 2.5 [Three Sum Closest](#25-three-sum-closest)
- 2.6 [Container With Most Water](#26-container-with-most-water)
- 2.7 [Move Zeroes](#27-move-zeroes)

### 3. [Fast & Slow Pointers](#3-fast--slow-pointers)
- 3.1 [Linked List Cycle Detection](#31-linked-list-cycle-detection)
- 3.2 [Start of the Cycle](#32-start-of-the-cycle)
- 3.3 [Middle of the Linked List](#33-middle-of-the-linked-list)
- 3.4 [Happy Number](#34-happy-number)
- 3.5 [Palindrome Linked List](#35-palindrome-linked-list)
- 3.6 [Find the Duplicate Number](#36-find-the-duplicate-number)

### 4. [Merge Intervals](#4-merge-intervals)
- 4.1 [Merge Overlapping Intervals](#41-merge-overlapping-intervals)
- 4.2 [Insert Interval](#42-insert-interval)
- 4.3 [Interval List Intersections](#43-interval-list-intersections)
- 4.4 [Minimum Meeting Rooms](#44-minimum-meeting-rooms)
- 4.5 [Can Attend All Meetings](#45-can-attend-all-meetings)
- 4.6 [Non-overlapping Intervals (Min Removals)](#46-non-overlapping-intervals-min-removals)

### 5. [Cyclic Sort](#5-cyclic-sort)
- 5.1 [Find the Missing Number](#51-find-the-missing-number)
- 5.2 [Find All Missing Numbers](#52-find-all-missing-numbers)
- 5.3 [Find the Duplicate Number (Cyclic)](#53-find-the-duplicate-number-cyclic)
- 5.4 [Find All Duplicates](#54-find-all-duplicates)
- 5.5 [First Missing Positive](#55-first-missing-positive)
- 5.6 [Set Mismatch](#56-set-mismatch)

### 6. [In-place Linked List Reversal](#6-in-place-linked-list-reversal)
- 6.1 [Reverse a Linked List](#61-reverse-a-linked-list)
- 6.2 [Reverse a Sub-list](#62-reverse-a-sub-list)
- 6.3 [Reverse Nodes in K-Group](#63-reverse-nodes-in-k-group)
- 6.4 [Swap Nodes in Pairs](#64-swap-nodes-in-pairs)
- 6.5 [Rotate a Linked List](#65-rotate-a-linked-list)

### 7. [Tree BFS](#7-tree-bfs)
- 7.1 [Binary Tree Level Order Traversal](#71-binary-tree-level-order-traversal)
- 7.2 [Zigzag Level Order Traversal](#72-zigzag-level-order-traversal)
- 7.3 [Minimum Depth of a Binary Tree](#73-minimum-depth-of-a-binary-tree)
- 7.4 [Binary Tree Right Side View](#74-binary-tree-right-side-view)
- 7.5 [Average of Levels](#75-average-of-levels)
- 7.6 [Connect Level-Order Siblings](#76-connect-level-order-siblings)

### 8. [Tree DFS](#8-tree-dfs)
- 8.1 [Path Sum (Root-to-Leaf)](#81-path-sum-root-to-leaf)
- 8.2 [All Root-to-Leaf Paths with Sum](#82-all-root-to-leaf-paths-with-sum)
- 8.3 [Count Paths for a Sum](#83-count-paths-for-a-sum)
- 8.4 [Diameter of a Binary Tree](#84-diameter-of-a-binary-tree)
- 8.5 [Maximum Path Sum](#85-maximum-path-sum)
- 8.6 [Lowest Common Ancestor](#86-lowest-common-ancestor)
- 8.7 [Validate a Binary Search Tree](#87-validate-a-binary-search-tree)

### 9. [Graph Traversal](#9-graph-traversal)
- 9.1 [Number of Islands](#91-number-of-islands)
- 9.2 [Clone Graph](#92-clone-graph)
- 9.3 [Flood Fill](#93-flood-fill)
- 9.4 [Rotting Oranges](#94-rotting-oranges)
- 9.5 [Word Ladder (Shortest Transformation)](#95-word-ladder-shortest-transformation)
- 9.6 [Pacific Atlantic Water Flow](#96-pacific-atlantic-water-flow)

### 10. [Topological Sort](#10-topological-sort)
- 10.1 [Course Schedule (Can Finish?)](#101-course-schedule-can-finish)
- 10.2 [Course Schedule II (Order)](#102-course-schedule-ii-order)
- 10.3 [Alien Dictionary](#103-alien-dictionary)
- 10.4 [Minimum Height Trees](#104-minimum-height-trees)
- 10.5 [Task Scheduling Order](#105-task-scheduling-order)

### 11. [Two Heaps](#11-two-heaps)
- 11.1 [Find Median from a Data Stream](#111-find-median-from-a-data-stream)
- 11.2 [Sliding Window Median](#112-sliding-window-median)
- 11.3 [Maximize Capital (IPO)](#113-maximize-capital-ipo)
- 11.4 [Next Interval](#114-next-interval)

### 12. [Top-K Elements](#12-top-k-elements)
- 12.1 [Kth Largest Element in an Array](#121-kth-largest-element-in-an-array)
- 12.2 [Top K Frequent Elements](#122-top-k-frequent-elements)
- 12.3 [K Closest Points to Origin](#123-k-closest-points-to-origin)
- 12.4 [Sort Characters by Frequency](#124-sort-characters-by-frequency)
- 12.5 [Reorganize String](#125-reorganize-string)
- 12.6 [K Closest Numbers](#126-k-closest-numbers)

### 13. [K-way Merge](#13-k-way-merge)
- 13.1 [Merge K Sorted Lists](#131-merge-k-sorted-lists)
- 13.2 [Kth Smallest in a Sorted Matrix](#132-kth-smallest-in-a-sorted-matrix)
- 13.3 [Smallest Range Covering K Lists](#133-smallest-range-covering-k-lists)
- 13.4 [Find K Pairs with Smallest Sums](#134-find-k-pairs-with-smallest-sums)

### 14. [Modified Binary Search](#14-modified-binary-search)
- 14.1 [Search in Rotated Sorted Array](#141-search-in-rotated-sorted-array)
- 14.2 [Find First and Last Position](#142-find-first-and-last-position)
- 14.3 [Find Minimum in Rotated Sorted Array](#143-find-minimum-in-rotated-sorted-array)
- 14.4 [Find Peak Element](#144-find-peak-element)
- 14.5 [Koko Eating Bananas (Search the Answer)](#145-koko-eating-bananas-search-the-answer)
- 14.6 [Search a 2D Matrix](#146-search-a-2d-matrix)

### 15. [Subsets / Backtracking](#15-subsets--backtracking)
- 15.1 [Generate All Subsets](#151-generate-all-subsets)
- 15.2 [Permutations](#152-permutations)
- 15.3 [Combination Sum](#153-combination-sum)
- 15.4 [Letter Combinations of a Phone Number](#154-letter-combinations-of-a-phone-number)
- 15.5 [Generate Parentheses](#155-generate-parentheses)
- 15.6 [Word Search](#156-word-search)
- 15.7 [N-Queens](#157-n-queens)

### 16. [Dynamic Programming](#16-dynamic-programming)
- 16.1 [Climbing Stairs](#161-climbing-stairs)
- 16.2 [House Robber](#162-house-robber)
- 16.3 [Coin Change (Minimum Coins)](#163-coin-change-minimum-coins)
- 16.4 [Longest Common Subsequence](#164-longest-common-subsequence)
- 16.5 [Longest Increasing Subsequence](#165-longest-increasing-subsequence)
- 16.6 [0/1 Knapsack](#166-01-knapsack)
- 16.7 [Edit Distance](#167-edit-distance)
- 16.8 [Word Break](#168-word-break)

### 17. [Greedy](#17-greedy)
- 17.1 [Jump Game](#171-jump-game)
- 17.2 [Jump Game II (Min Jumps)](#172-jump-game-ii-min-jumps)
- 17.3 [Gas Station](#173-gas-station)
- 17.4 [Task Scheduler](#174-task-scheduler)
- 17.5 [Partition Labels](#175-partition-labels)
- 17.6 [Assign Cookies](#176-assign-cookies)

### 18. [Monotonic Stack](#18-monotonic-stack)
- 18.1 [Next Greater Element](#181-next-greater-element)
- 18.2 [Daily Temperatures](#182-daily-temperatures)
- 18.3 [Next Greater Element II (Circular)](#183-next-greater-element-ii-circular)
- 18.4 [Largest Rectangle in Histogram](#184-largest-rectangle-in-histogram)
- 18.5 [Trapping Rain Water](#185-trapping-rain-water)
- 18.6 [Remove K Digits](#186-remove-k-digits)

### 19. [Prefix Sum](#19-prefix-sum)
- 19.1 [Subarray Sum Equals K](#191-subarray-sum-equals-k)
- 19.2 [Product of Array Except Self](#192-product-of-array-except-self)
- 19.3 [Range Sum Query (Immutable)](#193-range-sum-query-immutable)
- 19.4 [Find Pivot Index](#194-find-pivot-index)
- 19.5 [Contiguous Array (Equal 0s and 1s)](#195-contiguous-array-equal-0s-and-1s)
- 19.6 [Subarray Sums Divisible by K](#196-subarray-sums-divisible-by-k)

### 20. [Trie](#20-trie)
- 20.1 [Implement a Trie](#201-implement-a-trie)
- 20.2 [Add and Search Word (Wildcard)](#202-add-and-search-word-wildcard)
- 20.3 [Word Search II](#203-word-search-ii)
- 20.4 [Replace Words](#204-replace-words)
- 20.5 [Longest Word in Dictionary](#205-longest-word-in-dictionary)

### 21. [Union-Find](#21-union-find)
- 21.1 [Number of Connected Components](#211-number-of-connected-components)
- 21.2 [Redundant Connection](#212-redundant-connection)
- 21.3 [Number of Provinces](#213-number-of-provinces)
- 21.4 [Accounts Merge](#214-accounts-merge)
- 21.5 [Graph Valid Tree](#215-graph-valid-tree)

### 22. [Bitwise XOR](#22-bitwise-xor)
- 22.1 [Single Number](#221-single-number)
- 22.2 [Single Number III (Two Uniques)](#222-single-number-iii-two-uniques)
- 22.3 [Missing Number (XOR)](#223-missing-number-xor)
- 22.4 [Find the Difference](#224-find-the-difference)
- 22.5 [Counting Bits](#225-counting-bits)

---

> **Reusable Min/Max Heap.** JavaScript has no built-in heap. Several problems below use this small heap
> class — assume it's available in scope.
>
> ```js
> class Heap {
>   constructor(compare) { this.data = []; this.compare = compare; }
>   size() { return this.data.length; }
>   peek() { return this.data[0]; }
>   push(val) {
>     this.data.push(val);
>     let i = this.data.length - 1;
>     while (i > 0) {
>       const parent = (i - 1) >> 1;
>       if (this.compare(this.data[i], this.data[parent]) >= 0) break;
>       [this.data[i], this.data[parent]] = [this.data[parent], this.data[i]];
>       i = parent;
>     }
>   }
>   pop() {
>     const top = this.data[0];
>     const last = this.data.pop();
>     if (this.data.length) {
>       this.data[0] = last;
>       let i = 0; const n = this.data.length;
>       while (true) {
>         let best = i, l = 2 * i + 1, r = 2 * i + 2;
>         if (l < n && this.compare(this.data[l], this.data[best]) < 0) best = l;
>         if (r < n && this.compare(this.data[r], this.data[best]) < 0) best = r;
>         if (best === i) break;
>         [this.data[i], this.data[best]] = [this.data[best], this.data[i]];
>         i = best;
>       }
>     }
>     return top;
>   }
> }
> ```

---

## 1. Sliding Window

### 1.1 Maximum Sum Subarray of Size K

**Problem:** Given an array of positive integers and a number `k`, find the maximum sum of any contiguous
subarray of size `k`.

**Company tags:** `Amazon` `Microsoft` `Goldman Sachs`

**Why this is a Sliding Window problem:** It asks for an optimal value over a **contiguous, fixed-size**
range; adjacent windows overlap by `k-1` elements, so we reuse work instead of recomputing.

**Approach:** Seed the sum of the first `k` elements, then slide — add the incoming element and subtract
the outgoing one — tracking the max.

```js
function maxSumSubarray(arr, k) {
  let windowSum = 0;
  for (let i = 0; i < k; i++) windowSum += arr[i];
  let maxSum = windowSum;
  for (let end = k; end < arr.length; end++) {
    windowSum += arr[end] - arr[end - k];
    maxSum = Math.max(maxSum, windowSum);
  }
  return maxSum;
}
// maxSumSubarray([2,1,5,1,3,2], 3) -> 9
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** State brute force O(n·k) first, then the "add new − remove old" optimization to O(n).

---

### 1.2 Smallest Subarray With Sum ≥ Target

**Problem:** Given an array of positive integers and a target `S`, find the length of the smallest
contiguous subarray whose sum is ≥ `S` (0 if none).

**Company tags:** `Amazon` `Google` `Microsoft` `Flipkart`

**Why this is a Sliding Window problem:** Smallest *contiguous* range satisfying a sum condition → a
**variable-size** window that grows to meet the target, then shrinks to minimize length.

**Approach:** Expand `end` adding to the sum; while the sum ≥ `S`, record the window length and shrink from
`start`.

```js
function smallestSubarrayWithSum(arr, S) {
  let windowSum = 0, start = 0, minLen = Infinity;
  for (let end = 0; end < arr.length; end++) {
    windowSum += arr[end];
    while (windowSum >= S) {
      minLen = Math.min(minLen, end - start + 1);
      windowSum -= arr[start++];
    }
  }
  return minLen === Infinity ? 0 : minLen;
}
// smallestSubarrayWithSum([2,1,5,2,3,2], 7) -> 2
```

**Complexity:** Time **O(n)** (each element added/removed once), Space **O(1)**.

**💡 Interview tip:** Note this works because values are **positive** (so shrinking always reduces the sum).
With negatives you'd need prefix sums instead.

---

### 1.3 Longest Substring Without Repeating Characters

**Problem:** Find the length of the longest substring without repeating characters.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Adobe` `Bloomberg`

**Why this is a Sliding Window problem:** Longest contiguous substring under a "no repeats" constraint —
the window grows while valid and jumps forward when a repeat appears.

**Approach:** Track each char's last index; when a char repeats inside the window, move `start` past its
previous position.

```js
function lengthOfLongestSubstring(s) {
  const lastIndex = new Map();
  let start = 0, maxLen = 0;
  for (let end = 0; end < s.length; end++) {
    const ch = s[end];
    if (lastIndex.has(ch) && lastIndex.get(ch) >= start) start = lastIndex.get(ch) + 1;
    lastIndex.set(ch, end);
    maxLen = Math.max(maxLen, end - start + 1);
  }
  return maxLen;
}
// lengthOfLongestSubstring("abcabcbb") -> 3
```

**Complexity:** Time **O(n)**, Space **O(min(n, charset))**.

**💡 Interview tip:** The `>= start` guard prevents moving `start` backward for chars already outside the
window — the most common bug.

---

### 1.4 Longest Substring with At Most K Distinct Characters

**Problem:** Find the length of the longest substring with at most `k` distinct characters.

**Company tags:** `Amazon` `Google` `Uber` `Meta`

**Why this is a Sliding Window problem:** "Longest substring under a distinct-count constraint" → variable
window with a frequency map that triggers shrinking when distinct keys exceed `k`.

**Approach:** Expand and count chars; while map size > `k`, shrink from the left and delete zeroed counts.

```js
function longestKDistinct(s, k) {
  if (k === 0) return 0;
  const freq = new Map();
  let start = 0, maxLen = 0;
  for (let end = 0; end < s.length; end++) {
    freq.set(s[end], (freq.get(s[end]) || 0) + 1);
    while (freq.size > k) {
      const left = s[start++];
      freq.set(left, freq.get(left) - 1);
      if (freq.get(left) === 0) freq.delete(left);
    }
    maxLen = Math.max(maxLen, end - start + 1);
  }
  return maxLen;
}
// longestKDistinct("araaci", 2) -> 4
```

**Complexity:** Time **O(n)**, Space **O(k)**.

**💡 Interview tip:** This is the template for all "at most K" window problems. "Exactly K" = `atMost(K) -
atMost(K-1)`.

---

### 1.5 Fruits into Baskets

**Problem:** You have trees in a row (`fruits[i]` is the fruit type). You may pick from at most 2 fruit
types into 2 baskets. Find the maximum number of fruits (longest subarray with at most 2 distinct values).

**Company tags:** `Amazon` `Google` `Microsoft`

**Why this is a Sliding Window problem:** It's literally "longest subarray with at most 2 distinct" — a
special case of 1.4 with `k = 2`.

**Approach:** Same as K-distinct with `k = 2`.

```js
function totalFruit(fruits) {
  const freq = new Map();
  let start = 0, maxLen = 0;
  for (let end = 0; end < fruits.length; end++) {
    freq.set(fruits[end], (freq.get(fruits[end]) || 0) + 1);
    while (freq.size > 2) {
      const left = fruits[start++];
      freq.set(left, freq.get(left) - 1);
      if (freq.get(left) === 0) freq.delete(left);
    }
    maxLen = Math.max(maxLen, end - start + 1);
  }
  return maxLen;
}
// totalFruit([1,2,1,2,3]) -> 4
```

**Complexity:** Time **O(n)**, Space **O(1)** (at most 3 keys).

**💡 Interview tip:** Recognizing this as "K-distinct with k=2" instantly is exactly the pattern-mapping
skill interviewers test.

---

### 1.6 Permutation in a String

**Problem:** Given strings `s1` and `s2`, return true if `s2` contains a permutation of `s1` (a substring
that is an anagram of `s1`).

**Company tags:** `Amazon` `Microsoft` `Meta` `Bloomberg`

**Why this is a Sliding Window problem:** We slide a **fixed-size window** of length `s1.length` over `s2`,
checking whether the window's character counts match `s1`'s.

**Approach:** Build a need-count for `s1`. Slide a window of size `s1.length`, maintaining counts and a
`matched` counter; when all required counts match, return true.

```js
function checkInclusion(s1, s2) {
  if (s1.length > s2.length) return false;
  const need = new Map();
  for (const c of s1) need.set(c, (need.get(c) || 0) + 1);

  let matched = 0, start = 0;
  for (let end = 0; end < s2.length; end++) {
    const c = s2[end];
    if (need.has(c)) {
      need.set(c, need.get(c) - 1);
      if (need.get(c) === 0) matched++;
    }
    if (end - start + 1 > s1.length) {
      const left = s2[start++];
      if (need.has(left)) {
        if (need.get(left) === 0) matched--;
        need.set(left, need.get(left) + 1);
      }
    }
    if (matched === need.size) return true;
  }
  return false;
}
// checkInclusion("ab", "eidbaooo") -> true
```

**Complexity:** Time **O(n)**, Space **O(1)** (bounded charset).

**💡 Interview tip:** Track a `matched` count instead of comparing whole maps each step — that keeps it
O(n) rather than O(n·26).

---

### 1.7 Longest Repeating Character Replacement

**Problem:** Given a string and an integer `k`, you may replace at most `k` characters. Find the length of
the longest substring containing the same letter after replacements.

**Company tags:** `Amazon` `Google` `Meta`

**Why this is a Sliding Window problem:** Window is valid while `(windowLength − countOfMostFrequentChar) ≤
k` (the chars we'd need to replace). Expand while valid; shrink otherwise.

**Approach:** Track char counts and the max single-char frequency in the window. If the window needs more
than `k` replacements, shrink it.

```js
function characterReplacement(s, k) {
  const count = new Map();
  let start = 0, maxFreq = 0, maxLen = 0;
  for (let end = 0; end < s.length; end++) {
    count.set(s[end], (count.get(s[end]) || 0) + 1);
    maxFreq = Math.max(maxFreq, count.get(s[end]));
    // replacements needed = window size - most frequent char count
    if (end - start + 1 - maxFreq > k) {
      count.set(s[start], count.get(s[start]) - 1);
      start++;
    }
    maxLen = Math.max(maxLen, end - start + 1);
  }
  return maxLen;
}
// characterReplacement("AABABBA", 1) -> 4
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** The subtlety: we never need to decrease `maxFreq` — the answer only grows when a
better window exists, so a stale `maxFreq` doesn't cause wrong results.

---

## 2. Two Pointers

### 2.1 Pair with Target Sum (Sorted Array)

**Problem:** In a **sorted** array, find indices of two numbers adding to a target.

**Company tags:** `Amazon` `Microsoft` `Adobe`

**Why this is a Two Pointers problem:** Sorted input means moving a pointer predictably changes the sum, so
two converging pointers find the answer in one pass.

**Approach:** Left/right pointers; if sum too small move left up, too big move right down.

```js
function pairWithTargetSum(arr, target) {
  let left = 0, right = arr.length - 1;
  while (left < right) {
    const sum = arr[left] + arr[right];
    if (sum === target) return [left, right];
    sum < target ? left++ : right--;
  }
  return [-1, -1];
}
// pairWithTargetSum([1,2,3,4,6], 6) -> [1,3]
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** If unsorted, a hash map gives O(n) without sorting — mention the trade-off.

---

### 2.2 Remove Duplicates from a Sorted Array

**Problem:** Remove duplicates in place from a sorted array; return the new length.

**Company tags:** `Amazon` `Microsoft` `Adobe`

**Why this is a Two Pointers problem:** A slow pointer marks the last unique slot while a fast pointer
scans ahead — same-direction two pointers for in-place rewriting.

**Approach:** When `arr[fast]` differs from `arr[slow]`, advance `slow` and copy.

```js
function removeDuplicates(arr) {
  if (arr.length === 0) return 0;
  let slow = 0;
  for (let fast = 1; fast < arr.length; fast++) {
    if (arr[fast] !== arr[slow]) arr[++slow] = arr[fast];
  }
  return slow + 1;
}
// removeDuplicates([2,3,3,3,6,9,9]) -> 4
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Stress in-place O(1) space — allocating a new array misses the point of the question.

---

### 2.3 Squares of a Sorted Array

**Problem:** Given a sorted array (may contain negatives), return a sorted array of the squares.

**Company tags:** `Amazon` `Meta` `Adobe`

**Why this is a Two Pointers problem:** The largest squares are at the two **ends** (most negative or most
positive). Compare ends and fill the result from the back.

**Approach:** Pointers at both ends; place the larger square at the current highest free index.

```js
function sortedSquares(arr) {
  const n = arr.length, result = new Array(n);
  let left = 0, right = n - 1, pos = n - 1;
  while (left <= right) {
    const l = arr[left] * arr[left];
    const r = arr[right] * arr[right];
    if (l > r) { result[pos--] = l; left++; }
    else { result[pos--] = r; right--; }
  }
  return result;
}
// sortedSquares([-4,-1,0,3,10]) -> [0,1,9,16,100]
```

**Complexity:** Time **O(n)**, Space **O(n)** (output).

**💡 Interview tip:** Sorting the squares is O(n log n); the two-pointer fill-from-back is the O(n) upgrade.

---

### 2.4 Three Sum

**Problem:** Find all unique triplets summing to zero.

**Company tags:** `Amazon` `Google` `Meta` `Microsoft` `Bloomberg`

**Why this is a Two Pointers problem:** After sorting, fix one element and reduce to a two-pointer pair
search on the rest.

**Approach:** Sort; for each anchor, two-pointer search for `-anchor`; skip duplicates.

```js
function threeSum(nums) {
  nums.sort((a, b) => a - b);
  const res = [];
  for (let i = 0; i < nums.length - 2; i++) {
    if (i > 0 && nums[i] === nums[i - 1]) continue;
    let l = i + 1, r = nums.length - 1;
    while (l < r) {
      const sum = nums[i] + nums[l] + nums[r];
      if (sum === 0) {
        res.push([nums[i], nums[l], nums[r]]);
        while (l < r && nums[l] === nums[l + 1]) l++;
        while (l < r && nums[r] === nums[r - 1]) r--;
        l++; r--;
      } else if (sum < 0) l++;
      else r--;
    }
  }
  return res;
}
// threeSum([-1,0,1,2,-1,-4]) -> [[-1,-1,2],[-1,0,1]]
```

**Complexity:** Time **O(n²)**, Space **O(1)** (besides sort/output).

**💡 Interview tip:** Duplicate handling is the real test — walk through the skip logic explicitly.

---

### 2.5 Three Sum Closest

**Problem:** Find the triplet sum closest to a target; return that sum.

**Company tags:** `Amazon` `Google` `Bloomberg`

**Why this is a Two Pointers problem:** Same fix-one-then-two-pointer structure as 3Sum, but tracking the
closest sum instead of an exact match.

**Approach:** Sort; for each anchor, move two pointers, updating the closest sum by absolute difference.

```js
function threeSumClosest(nums, target) {
  nums.sort((a, b) => a - b);
  let closest = nums[0] + nums[1] + nums[2];
  for (let i = 0; i < nums.length - 2; i++) {
    let l = i + 1, r = nums.length - 1;
    while (l < r) {
      const sum = nums[i] + nums[l] + nums[r];
      if (Math.abs(sum - target) < Math.abs(closest - target)) closest = sum;
      if (sum === target) return sum;
      sum < target ? l++ : r--;
    }
  }
  return closest;
}
// threeSumClosest([-1,2,1,-4], 1) -> 2
```

**Complexity:** Time **O(n²)**, Space **O(1)**.

**💡 Interview tip:** Early-return on an exact match, and compare via absolute difference — a common slip is
comparing raw sums.

---

### 2.6 Container With Most Water

**Problem:** Given heights, pick two lines forming the container holding the most water.

**Company tags:** `Amazon` `Google` `Meta` `Bloomberg`

**Why this is a Two Pointers problem:** Start with the widest container and move the **shorter** wall
inward — width shrinks, so only a taller wall can improve area.

**Approach:** Two ends; compute area, move the pointer at the shorter height.

```js
function maxArea(height) {
  let left = 0, right = height.length - 1, max = 0;
  while (left < right) {
    const area = Math.min(height[left], height[right]) * (right - left);
    max = Math.max(max, area);
    height[left] < height[right] ? left++ : right--;
  }
  return max;
}
// maxArea([1,8,6,2,5,4,8,3,7]) -> 49
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Justify *why* moving the shorter wall is safe — moving the taller one can never
increase the area.

---

### 2.7 Move Zeroes

**Problem:** Move all zeros to the end in place while keeping the relative order of non-zeros.

**Company tags:** `Amazon` `Meta` `Microsoft` `Adobe`

**Why this is a Two Pointers problem:** A slow pointer marks the next non-zero slot while a fast pointer
scans — same-direction two pointers.

**Approach:** When `nums[fast]` is non-zero, swap it into `nums[slow]` and advance `slow`.

```js
function moveZeroes(nums) {
  let slow = 0;
  for (let fast = 0; fast < nums.length; fast++) {
    if (nums[fast] !== 0) {
      [nums[slow], nums[fast]] = [nums[fast], nums[slow]];
      slow++;
    }
  }
  return nums;
}
// moveZeroes([0,1,0,3,12]) -> [1,3,12,0,0]
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Swapping (not copying then zero-filling) preserves order in a single clean pass.

---

## 3. Fast & Slow Pointers

### 3.1 Linked List Cycle Detection

**Problem:** Determine whether a singly linked list has a cycle.

**Company tags:** `Amazon` `Microsoft` `Meta` `Bloomberg`

**Why this is a Fast & Slow Pointers problem:** A 2x-speed pointer laps a 1x pointer **inside a cycle**, so
they meet; if the list ends, `fast` hits null — Floyd's algorithm.

**Approach:** Advance slow by 1, fast by 2; meeting ⇒ cycle.

```js
function hasCycle(head) {
  let slow = head, fast = head;
  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
    if (slow === fast) return true;
  }
  return false;
}
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Contrast with the hash-set approach (O(n) space). O(1) space is why Floyd's wins.

---

### 3.2 Start of the Cycle

**Problem:** Return the node where the cycle begins, or null.

**Company tags:** `Amazon` `Microsoft` `Meta`

**Why this is a Fast & Slow Pointers problem:** After the pointers meet, the distance math means resetting
one pointer to head and advancing both by 1 makes them meet at the cycle start.

**Approach:** Detect meeting point; reset `slow` to head; advance both by 1 until equal.

```js
function detectCycle(head) {
  let slow = head, fast = head;
  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
    if (slow === fast) {
      let p = head;
      while (p !== slow) { p = p.next; slow = slow.next; }
      return p; // cycle start
    }
  }
  return null;
}
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Be ready to sketch the `a = (n−1)·loop + (loop − b)` distance argument that proves the
reset trick.

---

### 3.3 Middle of the Linked List

**Problem:** Return the middle node (second middle if even length).

**Company tags:** `Amazon` `Microsoft` `Adobe`

**Why this is a Fast & Slow Pointers problem:** When `fast` (2x) reaches the end, `slow` (1x) is exactly at
the middle.

**Approach:** Advance slow by 1, fast by 2; return slow when fast finishes.

```js
function middleNode(head) {
  let slow = head, fast = head;
  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
  }
  return slow;
}
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** This "find middle" is a building block for merge-sorting a list and palindrome checks.

---

### 3.4 Happy Number

**Problem:** Repeatedly replace `n` with the sum of squares of its digits; return true if it reaches 1.

**Company tags:** `Amazon` `Google` `Uber` `Twitter`

**Why this is a Fast & Slow Pointers problem:** The transform sequence either reaches 1 or enters a cycle —
detect the loop without extra memory.

**Approach:** Slow does one transform, fast does two; loop until equal; happy iff value is 1.

```js
function isHappy(n) {
  const next = (num) => {
    let sum = 0;
    while (num > 0) { const d = num % 10; sum += d * d; num = Math.floor(num / 10); }
    return sum;
  };
  let slow = n, fast = n;
  do { slow = next(slow); fast = next(next(fast)); } while (slow !== fast);
  return slow === 1;
}
// isHappy(19) -> true
```

**Complexity:** Time **O(log n)** per step, Space **O(1)**.

**💡 Interview tip:** Most use a Set (O(n) space); fast/slow shows pattern fluency with O(1) space.

---

### 3.5 Palindrome Linked List

**Problem:** Return true if a singly linked list reads the same forwards and backwards.

**Company tags:** `Amazon` `Microsoft` `Meta` `Adobe`

**Why this is a Fast & Slow Pointers problem:** Use fast/slow to find the middle, reverse the second half
in place, then compare halves — combining two pointer techniques.

**Approach:** Find middle (fast/slow), reverse the second half, compare node by node.

```js
function isPalindrome(head) {
  let slow = head, fast = head;
  while (fast && fast.next) { slow = slow.next; fast = fast.next.next; }
  // reverse second half
  let prev = null;
  while (slow) { const next = slow.next; slow.next = prev; prev = slow; slow = next; }
  // compare
  let first = head, second = prev;
  while (second) {
    if (first.val !== second.val) return false;
    first = first.next; second = second.next;
  }
  return true;
}
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Mention you could restore the list afterward if mutation isn't allowed.

---

### 3.6 Find the Duplicate Number

**Problem:** An array of `n+1` integers in range `1..n` has exactly one duplicate. Find it without
modifying the array, in O(1) space.

**Company tags:** `Amazon` `Google` `Microsoft` `Bloomberg`

**Why this is a Fast & Slow Pointers problem:** Treat values as "next index" pointers; the duplicate
creates a cycle, and the cycle's entrance is the duplicate (Floyd's on an implicit linked list).

**Approach:** Phase 1 find the meeting point; phase 2 reset one pointer to start to find the cycle entrance.

```js
function findDuplicate(nums) {
  let slow = nums[0], fast = nums[0];
  do { slow = nums[slow]; fast = nums[nums[fast]]; } while (slow !== fast);
  slow = nums[0];
  while (slow !== fast) { slow = nums[slow]; fast = nums[fast]; }
  return slow;
}
// findDuplicate([1,3,4,2,2]) -> 2
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** This reframing of an *array* as a *linked list with a cycle* is a classic "aha" — name
it explicitly. (Cyclic sort also solves it if array modification is allowed.)

---


## 4. Merge Intervals

### 4.1 Merge Overlapping Intervals

**Problem:** Merge all overlapping intervals.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Salesforce`

**Why this is a Merge Intervals problem:** It combines overlapping `[start, end]` ranges; sorting by start
makes overlaps adjacent.

**Approach:** Sort by start; extend the last merged interval when it overlaps, else push a new one.

```js
function merge(intervals) {
  if (intervals.length <= 1) return intervals;
  intervals.sort((a, b) => a[0] - b[0]);
  const out = [intervals[0]];
  for (let i = 1; i < intervals.length; i++) {
    const last = out[out.length - 1], cur = intervals[i];
    if (cur[0] <= last[1]) last[1] = Math.max(last[1], cur[1]);
    else out.push(cur);
  }
  return out;
}
// merge([[1,3],[2,6],[8,10],[15,18]]) -> [[1,6],[8,10],[15,18]]
```

**Complexity:** Time **O(n log n)**, Space **O(n)**.

**💡 Interview tip:** `Math.max` on the end matters for a contained interval (`[2,6]` inside `[1,8]`).

---

### 4.2 Insert Interval

**Problem:** Given sorted, non-overlapping intervals and a new interval, insert it and merge if needed.

**Company tags:** `Amazon` `Google` `Meta` `LinkedIn`

**Why this is a Merge Intervals problem:** Insertion into sorted intervals reduces to merging the new one
with any overlaps — a three-phase interval merge.

**Approach:** Add all intervals ending before the new one; merge all overlapping into the new one; add the
rest.

```js
function insert(intervals, newInterval) {
  const out = [];
  let i = 0, n = intervals.length;
  while (i < n && intervals[i][1] < newInterval[0]) out.push(intervals[i++]);
  while (i < n && intervals[i][0] <= newInterval[1]) {
    newInterval[0] = Math.min(newInterval[0], intervals[i][0]);
    newInterval[1] = Math.max(newInterval[1], intervals[i][1]);
    i++;
  }
  out.push(newInterval);
  while (i < n) out.push(intervals[i++]);
  return out;
}
// insert([[1,3],[6,9]], [2,5]) -> [[1,5],[6,9]]
```

**Complexity:** Time **O(n)** (already sorted), Space **O(n)**.

**💡 Interview tip:** Because the input is pre-sorted, this is O(n) — no need to re-sort.

---

### 4.3 Interval List Intersections

**Problem:** Given two lists of sorted, disjoint intervals, return their intersections.

**Company tags:** `Amazon` `Meta` `Google`

**Why this is a Merge Intervals problem:** Two-pointer sweep over sorted intervals computing overlap
ranges — an interval-merge variant.

**Approach:** For each pair, the overlap is `[max(starts), min(ends)]`; advance the interval that ends
first.

```js
function intervalIntersection(A, B) {
  const out = [];
  let i = 0, j = 0;
  while (i < A.length && j < B.length) {
    const lo = Math.max(A[i][0], B[j][0]);
    const hi = Math.min(A[i][1], B[j][1]);
    if (lo <= hi) out.push([lo, hi]);
    A[i][1] < B[j][1] ? i++ : j++;
  }
  return out;
}
// intervalIntersection([[0,2],[5,10]], [[1,5],[8,12]]) -> [[1,2],[5,5],[8,10]]
```

**Complexity:** Time **O(m + n)**, Space **O(m + n)**.

**💡 Interview tip:** The overlap test `lo <= hi` and "advance the smaller end" invariant are the crux.

---

### 4.4 Minimum Meeting Rooms

**Problem:** Find the minimum number of rooms so no meetings overlap in the same room.

**Company tags:** `Amazon` `Google` `Meta` `Uber` `Bloomberg`

**Why this is a Merge Intervals problem:** The peak number of simultaneously overlapping intervals = rooms
needed.

**Approach (sweep line):** Sort starts and ends; sweep, adding a room when a meeting starts before the
earliest end, freeing one otherwise; track the peak.

```js
function minMeetingRooms(intervals) {
  if (!intervals.length) return 0;
  const starts = intervals.map(i => i[0]).sort((a, b) => a - b);
  const ends = intervals.map(i => i[1]).sort((a, b) => a - b);
  let rooms = 0, maxRooms = 0, s = 0, e = 0;
  while (s < starts.length) {
    if (starts[s] < ends[e]) { rooms++; s++; }
    else { rooms--; e++; }
    maxRooms = Math.max(maxRooms, rooms);
  }
  return maxRooms;
}
// minMeetingRooms([[0,30],[5,10],[15,20]]) -> 2
```

**Complexity:** Time **O(n log n)**, Space **O(n)**.

**💡 Interview tip:** Offer the min-heap-of-end-times alternative; it generalizes if asked which meetings
share rooms.

---

### 4.5 Can Attend All Meetings

**Problem:** Given meeting intervals, return true if a person can attend all (no overlaps).

**Company tags:** `Amazon` `Microsoft` `Facebook`

**Why this is a Merge Intervals problem:** Sort by start; any overlap between consecutive intervals makes
it impossible — a direct overlap check.

**Approach:** Sort; if any interval starts before the previous ends, return false.

```js
function canAttendMeetings(intervals) {
  intervals.sort((a, b) => a[0] - b[0]);
  for (let i = 1; i < intervals.length; i++) {
    if (intervals[i][0] < intervals[i - 1][1]) return false;
  }
  return true;
}
// canAttendMeetings([[0,30],[5,10]]) -> false
```

**Complexity:** Time **O(n log n)**, Space **O(1)**.

**💡 Interview tip:** This is the warm-up to "min meeting rooms" — mention how the two relate.

---

### 4.6 Non-overlapping Intervals (Min Removals)

**Problem:** Return the minimum number of intervals to remove so the rest are non-overlapping.

**Company tags:** `Amazon` `Google` `Meta`

**Why this is a Merge Intervals problem:** It's interval-overlap management; a greedy choice (keep the
interval that ends earliest) maximizes how many fit.

**Approach:** Sort by end; greedily keep intervals that start at/after the last kept end, count the rest as
removals.

```js
function eraseOverlapIntervals(intervals) {
  if (!intervals.length) return 0;
  intervals.sort((a, b) => a[1] - b[1]);
  let prevEnd = intervals[0][1], removals = 0;
  for (let i = 1; i < intervals.length; i++) {
    if (intervals[i][0] < prevEnd) removals++;       // overlaps -> remove
    else prevEnd = intervals[i][1];                  // keep
  }
  return removals;
}
// eraseOverlapIntervals([[1,2],[2,3],[3,4],[1,3]]) -> 1
```

**Complexity:** Time **O(n log n)**, Space **O(1)**.

**💡 Interview tip:** Sorting by **end** (not start) is the greedy insight — keeping earliest-ending
intervals leaves the most room.

---

## 5. Cyclic Sort

### 5.1 Find the Missing Number

**Problem:** An array has `n` distinct numbers from `0..n` (one missing). Find it.

**Company tags:** `Amazon` `Microsoft` `Adobe` `Apple`

**Why this is a Cyclic Sort problem:** Values map to indices in `0..n`; placing each at its index exposes
the gap.

**Approach:** Swap each value to its index (skip `n`); the first mismatched index is the answer.

```js
function missingNumber(nums) {
  const n = nums.length;
  let i = 0;
  while (i < n) {
    const correct = nums[i];
    if (nums[i] < n && nums[i] !== nums[correct]) {
      [nums[i], nums[correct]] = [nums[correct], nums[i]];
    } else i++;
  }
  for (let j = 0; j < n; j++) if (nums[j] !== j) return j;
  return n;
}
// missingNumber([4,0,3,1]) -> 2
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** XOR or sum-formula (`n(n+1)/2 - sum`) also work; cyclic sort generalizes to
"find-all" follow-ups.

---

### 5.2 Find All Missing Numbers

**Problem:** Array of `n` integers in `1..n`; some appear twice, some are missing. Return all missing.

**Company tags:** `Amazon` `Google` `Microsoft`

**Why this is a Cyclic Sort problem:** Bounded range `1..n` → place each value at index `value-1`; mismatched
indices reveal missing values.

**Approach:** Cyclic placement, then collect indices where `nums[i] !== i+1`.

```js
function findDisappearedNumbers(nums) {
  let i = 0;
  while (i < nums.length) {
    const correct = nums[i] - 1;
    if (nums[i] !== nums[correct]) [nums[i], nums[correct]] = [nums[correct], nums[i]];
    else i++;
  }
  const missing = [];
  for (let j = 0; j < nums.length; j++) if (nums[j] !== j + 1) missing.push(j + 1);
  return missing;
}
// findDisappearedNumbers([4,3,2,7,8,2,3,1]) -> [5,6]
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Index-negation marking is an alternative; cyclic sort is easier to explain.

---

### 5.3 Find the Duplicate Number (Cyclic)

**Problem:** Array of `n+1` integers in `1..n` with one duplicate. Find it.

**Company tags:** `Amazon` `Google` `Microsoft`

**Why this is a Cyclic Sort problem:** Placing each value at index `value-1`; when a value's target slot is
already occupied by the same value, that's the duplicate.

**Approach:** Cyclic placement; when `nums[i] === nums[nums[i]-1]` but indices differ, return it.

```js
function findDuplicate(nums) {
  let i = 0;
  while (i < nums.length) {
    if (nums[i] !== i + 1) {
      const correct = nums[i] - 1;
      if (nums[i] === nums[correct]) return nums[i]; // duplicate found
      [nums[i], nums[correct]] = [nums[correct], nums[i]];
    } else i++;
  }
  return -1;
}
// findDuplicate([1,4,4,3,2]) -> 4
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** If modifying the array is disallowed, switch to **Floyd's cycle** (see 3.6).

---

### 5.4 Find All Duplicates

**Problem:** Array of `n` integers in `1..n`; some appear twice. Return all that appear twice.

**Company tags:** `Amazon` `Google` `Microsoft`

**Why this is a Cyclic Sort problem:** Bounded range mapping to indices; after placement, mismatched slots
hold duplicates.

**Approach:** Cyclic placement; collect `nums[i]` where `nums[i] !== i+1`.

```js
function findDuplicates(nums) {
  let i = 0;
  while (i < nums.length) {
    const correct = nums[i] - 1;
    if (nums[i] !== nums[correct]) [nums[i], nums[correct]] = [nums[correct], nums[i]];
    else i++;
  }
  const dups = [];
  for (let j = 0; j < nums.length; j++) if (nums[j] !== j + 1) dups.push(nums[j]);
  return dups;
}
// findDuplicates([4,3,2,7,8,2,3,1]) -> [2,3]
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Same skeleton as 5.2 — only the final collection step differs.

---

### 5.5 First Missing Positive

**Problem:** Find the smallest missing positive integer in an unsorted array. O(n) time, O(1) space.

**Company tags:** `Amazon` `Google` `Microsoft` `Stripe`

**Why this is a Cyclic Sort problem:** The answer lies in `1..n+1`; placing each in-range positive at its
index reveals the first gap.

**Approach:** Cyclic-place values in `1..n`; the first index with `nums[i] !== i+1` gives the answer.

```js
function firstMissingPositive(nums) {
  const n = nums.length;
  let i = 0;
  while (i < n) {
    const correct = nums[i] - 1;
    if (nums[i] > 0 && nums[i] <= n && nums[i] !== nums[correct]) {
      [nums[i], nums[correct]] = [nums[correct], nums[i]];
    } else i++;
  }
  for (let j = 0; j < n; j++) if (nums[j] !== j + 1) return j + 1;
  return n + 1;
}
// firstMissingPositive([3,4,-1,1]) -> 2
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Ignoring out-of-range values (≤0 or >n) is the key filter — they can't be the answer's
position.

---

### 5.6 Set Mismatch

**Problem:** A set `1..n` had one number duplicated (replacing a missing one). Return `[duplicate, missing]`.

**Company tags:** `Amazon` `Microsoft`

**Why this is a Cyclic Sort problem:** Bounded range; after placement, the mismatched index holds the
duplicate and reveals the missing.

**Approach:** Cyclic-place; the index where `nums[i] !== i+1` gives the duplicate (`nums[i]`) and missing
(`i+1`).

```js
function findErrorNums(nums) {
  let i = 0;
  while (i < nums.length) {
    const correct = nums[i] - 1;
    if (nums[i] !== nums[correct]) [nums[i], nums[correct]] = [nums[correct], nums[i]];
    else i++;
  }
  for (let j = 0; j < nums.length; j++) if (nums[j] !== j + 1) return [nums[j], j + 1];
  return [-1, -1];
}
// findErrorNums([1,2,2,4]) -> [2,3]
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** One pass yields both answers — neat payoff of the cyclic-sort placement.

---

## 6. In-place Linked List Reversal

### 6.1 Reverse a Linked List

**Problem:** Reverse a singly linked list; return the new head.

**Company tags:** `Amazon` `Microsoft` `Meta` `Google` `Adobe`

**Why this is an In-place Reversal problem:** Re-point each node's `next` to its predecessor using a few
pointers — no extra structure.

**Approach:** Track `prev`/`curr`; save `next`, flip the link, advance.

```js
function reverseList(head) {
  let prev = null, curr = head;
  while (curr) {
    const next = curr.next;
    curr.next = prev;
    prev = curr;
    curr = next;
  }
  return prev;
}
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Save `next` *before* flipping — losing it is the classic bug. Know the recursive form
too.

---

### 6.2 Reverse a Sub-list

**Problem:** Reverse the nodes from position `m` to `n` (1-indexed) in one pass.

**Company tags:** `Amazon` `Microsoft` `Meta`

**Why this is an In-place Reversal problem:** Reverse a bounded segment in place, then re-stitch it to the
unreversed parts.

**Approach:** Walk to the node before `m`, reverse `n-m+1` nodes, reconnect.

```js
function reverseBetween(head, m, n) {
  const dummy = { next: head };
  let prev = dummy;
  for (let i = 0; i < m - 1; i++) prev = prev.next;
  let curr = prev.next;
  for (let i = 0; i < n - m; i++) {
    const next = curr.next;
    curr.next = next.next;
    next.next = prev.next;
    prev.next = next;
  }
  return dummy.next;
}
// reverseBetween(1->2->3->4->5, 2, 4) -> 1->4->3->2->5
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** A dummy head simplifies the case `m = 1`. The "head-insertion" swap moves each node to
the front of the segment.

---

### 6.3 Reverse Nodes in K-Group

**Problem:** Reverse the list `k` nodes at a time; leftover tail (< k) stays as-is.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Bloomberg`

**Why this is an In-place Reversal problem:** Repeated bounded reversal with careful re-linking between
groups.

**Approach:** Verify `k` nodes remain; reverse them; recurse for the rest and connect.

```js
function reverseKGroup(head, k) {
  let node = head;
  for (let i = 0; i < k; i++) { if (!node) return head; node = node.next; }
  let prev = null, curr = head;
  for (let i = 0; i < k; i++) {
    const next = curr.next; curr.next = prev; prev = curr; curr = next;
  }
  head.next = reverseKGroup(curr, k);
  return prev;
}
```

**Complexity:** Time **O(n)**, Space **O(n/k)** recursion (O(1) iterative).

**💡 Interview tip:** Clarify the leftover rule up front; offer the iterative O(1)-space version if pushed.

---

### 6.4 Swap Nodes in Pairs

**Problem:** Swap every two adjacent nodes; return the new head.

**Company tags:** `Amazon` `Microsoft` `Adobe`

**Why this is an In-place Reversal problem:** It's "reverse in groups of 2" — pointer rewiring without
extra memory.

**Approach:** Use a dummy; repeatedly swap the next two nodes and advance.

```js
function swapPairs(head) {
  const dummy = { next: head };
  let prev = dummy;
  while (prev.next && prev.next.next) {
    const first = prev.next, second = first.next;
    first.next = second.next;
    second.next = first;
    prev.next = second;
    prev = first;
  }
  return dummy.next;
}
// swapPairs(1->2->3->4) -> 2->1->4->3
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** A special case of reverse-k-group with `k = 2`; mention the generalization.

---

### 6.5 Rotate a Linked List

**Problem:** Rotate the list to the right by `k` places.

**Company tags:** `Amazon` `Microsoft` `Adobe`

**Why this is an In-place Reversal-family problem:** It rewires links in place — connect the tail to the
head to form a ring, then break it at the new position.

**Approach:** Find length, make it circular, then break `len - k%len` nodes ahead.

```js
function rotateRight(head, k) {
  if (!head || !head.next || k === 0) return head;
  let len = 1, tail = head;
  while (tail.next) { tail = tail.next; len++; }
  tail.next = head;               // make circular
  k = k % len;
  let stepsToNewTail = len - k;
  let newTail = head;
  for (let i = 1; i < stepsToNewTail; i++) newTail = newTail.next;
  const newHead = newTail.next;
  newTail.next = null;            // break the ring
  return newHead;
}
// rotateRight(1->2->3->4->5, 2) -> 4->5->1->2->3
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Reducing `k % len` avoids redundant full rotations — handle `k > len` cleanly.

---

## 7. Tree BFS

> Assume a binary tree node `{ val, left, right }`. Arrays are used as queues (`shift`/`push`); for very
> large inputs, mention a head-index queue for O(1) dequeues.

### 7.1 Binary Tree Level Order Traversal

**Problem:** Return node values grouped level by level, top to bottom.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Flipkart`

**Why this is a Tree BFS problem:** Level-by-level output is the textbook BFS-with-a-queue signal.

**Approach:** Snapshot each level's size, dequeue that many nodes, collect values, enqueue children.

```js
function levelOrder(root) {
  const res = [];
  if (!root) return res;
  const queue = [root];
  while (queue.length) {
    const size = queue.length, level = [];
    for (let i = 0; i < size; i++) {
      const node = queue.shift();
      level.push(node.val);
      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }
    res.push(level);
  }
  return res;
}
```

**Complexity:** Time **O(n)**, Space **O(n)**.

**💡 Interview tip:** Snapshotting `size` before the inner loop is what separates levels cleanly.

---

### 7.2 Zigzag Level Order Traversal

**Problem:** Level-order traversal but alternate left-to-right and right-to-left per level.

**Company tags:** `Amazon` `Microsoft` `Meta` `LinkedIn`

**Why this is a Tree BFS problem:** Standard level traversal with a direction flag controlling insertion
order.

**Approach:** Same BFS; reverse each level (or push to front) on alternate levels.

```js
function zigzagLevelOrder(root) {
  const res = [];
  if (!root) return res;
  const queue = [root];
  let leftToRight = true;
  while (queue.length) {
    const size = queue.length, level = [];
    for (let i = 0; i < size; i++) {
      const node = queue.shift();
      if (leftToRight) level.push(node.val);
      else level.unshift(node.val);
      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }
    res.push(level);
    leftToRight = !leftToRight;
  }
  return res;
}
```

**Complexity:** Time **O(n)**, Space **O(n)**.

**💡 Interview tip:** Use `unshift` (or reverse) rather than reversing the traversal direction — keeps the
BFS logic intact.

---

### 7.3 Minimum Depth of a Binary Tree

**Problem:** Number of nodes on the shortest root-to-leaf path.

**Company tags:** `Amazon` `Microsoft` `Facebook`

**Why this is a Tree BFS problem:** BFS reaches the closest leaf first, allowing an early return.

**Approach:** BFS with depth; return at the first leaf.

```js
function minDepth(root) {
  if (!root) return 0;
  const queue = [{ node: root, depth: 1 }];
  while (queue.length) {
    const { node, depth } = queue.shift();
    if (!node.left && !node.right) return depth;
    if (node.left) queue.push({ node: node.left, depth: depth + 1 });
    if (node.right) queue.push({ node: node.right, depth: depth + 1 });
  }
  return 0;
}
```

**Complexity:** Time **O(n)** worst case, Space **O(n)**.

**💡 Interview tip:** For *min* depth BFS beats DFS due to early exit; a DFS bug is treating a one-child node
as a leaf.

---

### 7.4 Binary Tree Right Side View

**Problem:** Return the values visible from the right side, top to bottom.

**Company tags:** `Amazon` `Meta` `Microsoft` `Bloomberg`

**Why this is a Tree BFS problem:** The last node of each level is the rightmost visible one.

**Approach:** BFS; record the last node processed in each level.

```js
function rightSideView(root) {
  const res = [];
  if (!root) return res;
  const queue = [root];
  while (queue.length) {
    const size = queue.length;
    for (let i = 0; i < size; i++) {
      const node = queue.shift();
      if (i === size - 1) res.push(node.val); // rightmost of the level
      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }
  }
  return res;
}
```

**Complexity:** Time **O(n)**, Space **O(n)**.

**💡 Interview tip:** "Last node per level" generalizes to left-side view (first node) — note the symmetry.

---

### 7.5 Average of Levels

**Problem:** Return the average value of nodes on each level.

**Company tags:** `Amazon` `Facebook` `Adobe`

**Why this is a Tree BFS problem:** Per-level aggregation is natural with level-order BFS.

**Approach:** BFS; sum each level and divide by its size.

```js
function averageOfLevels(root) {
  const res = [];
  if (!root) return res;
  const queue = [root];
  while (queue.length) {
    const size = queue.length;
    let sum = 0;
    for (let i = 0; i < size; i++) {
      const node = queue.shift();
      sum += node.val;
      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }
    res.push(sum / size);
  }
  return res;
}
```

**Complexity:** Time **O(n)**, Space **O(n)**.

**💡 Interview tip:** Watch for large sums overflowing in other languages; in JS use care with precision but
it's generally fine.

---

### 7.6 Connect Level-Order Siblings

**Problem:** Populate each node's `next` pointer to its right neighbor on the same level (null at level
end).

**Company tags:** `Amazon` `Microsoft` `Meta`

**Why this is a Tree BFS problem:** Linking siblings is inherently a level-by-level operation.

**Approach:** BFS; within each level, set the previous node's `next` to the current node.

```js
function connect(root) {
  if (!root) return root;
  const queue = [root];
  while (queue.length) {
    const size = queue.length;
    let prev = null;
    for (let i = 0; i < size; i++) {
      const node = queue.shift();
      if (prev) prev.next = node;
      prev = node;
      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }
    prev.next = null; // end of level
  }
  return root;
}
```

**Complexity:** Time **O(n)**, Space **O(n)**.

**💡 Interview tip:** For perfect binary trees there's an elegant **O(1) space** version using the existing
`next` pointers — mention it as the optimal follow-up.

---


## 8. Tree DFS

### 8.1 Path Sum (Root-to-Leaf)

**Problem:** Return true if a root-to-leaf path sums to a target.

**Company tags:** `Amazon` `Microsoft` `Meta` `Adobe`

**Why this is a Tree DFS problem:** It concerns a vertical root-to-leaf path; recurse downward carrying the
remaining sum.

**Approach:** Subtract node value while descending; at a leaf, check the remainder.

```js
function hasPathSum(root, target) {
  if (!root) return false;
  if (!root.left && !root.right) return target === root.val;
  const rem = target - root.val;
  return hasPathSum(root.left, rem) || hasPathSum(root.right, rem);
}
```

**Complexity:** Time **O(n)**, Space **O(h)**.

**💡 Interview tip:** Define the leaf condition precisely (both children null) — a frequent bug source.

---

### 8.2 All Root-to-Leaf Paths with Sum

**Problem:** Return all root-to-leaf paths whose values sum to a target.

**Company tags:** `Amazon` `Meta` `Microsoft`

**Why this is a Tree DFS problem:** Collecting full paths requires DFS with backtracking of the current
path.

**Approach:** DFS carrying the path; on a matching leaf, record a copy; backtrack on return.

```js
function pathSumII(root, target) {
  const res = [];
  function dfs(node, rem, path) {
    if (!node) return;
    path.push(node.val);
    if (!node.left && !node.right && rem === node.val) res.push([...path]);
    else {
      dfs(node.left, rem - node.val, path);
      dfs(node.right, rem - node.val, path);
    }
    path.pop(); // backtrack
  }
  dfs(root, target, []);
  return res;
}
```

**Complexity:** Time **O(n)** to visit, up to **O(n²)** to copy paths. Space **O(h)**.

**💡 Interview tip:** Push a **copy** (`[...path]`) into results and `pop()` to backtrack — the standard
DFS-path idiom.

---

### 8.3 Count Paths for a Sum

**Problem:** Count paths (downward, not necessarily starting at root) summing to a target.

**Company tags:** `Amazon` `Google` `Meta`

**Why this is a Tree DFS problem:** Combine DFS with running prefix sums to count any downward segment with
the target sum.

**Approach:** Track cumulative sum from root; a hash map of prefix-sum counts gives matches in O(n).

```js
function pathSumIII(root, target) {
  const prefix = new Map([[0, 1]]);
  let count = 0;
  function dfs(node, curr) {
    if (!node) return;
    curr += node.val;
    count += prefix.get(curr - target) || 0;
    prefix.set(curr, (prefix.get(curr) || 0) + 1);
    dfs(node.left, curr);
    dfs(node.right, curr);
    prefix.set(curr, prefix.get(curr) - 1); // backtrack the prefix count
  }
  dfs(root, 0);
  return count;
}
```

**Complexity:** Time **O(n)**, Space **O(n)**.

**💡 Interview tip:** This is "subarray sum equals K" applied to a tree path — naming that connection
impresses.

---

### 8.4 Diameter of a Binary Tree

**Problem:** Length (in edges) of the longest path between any two nodes.

**Company tags:** `Amazon` `Google` `Meta` `Bloomberg`

**Why this is a Tree DFS problem:** Longest path through a node = left height + right height; compute
heights bottom-up.

**Approach:** Post-order DFS returning height while updating a global max.

```js
function diameterOfBinaryTree(root) {
  let diameter = 0;
  function height(node) {
    if (!node) return 0;
    const l = height(node.left), r = height(node.right);
    diameter = Math.max(diameter, l + r);
    return 1 + Math.max(l, r);
  }
  height(root);
  return diameter;
}
```

**Complexity:** Time **O(n)**, Space **O(h)**.

**💡 Interview tip:** Compute height and update diameter in one pass; recomputing height per node is O(n²).

---

### 8.5 Maximum Path Sum

**Problem:** Find the maximum path sum where a path is any node sequence connected by edges (need not pass
through root).

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Bloomberg`

**Why this is a Tree DFS problem:** At each node, the best "through" path = node + max(0, left gain) +
max(0, right gain); compute gains bottom-up.

**Approach:** DFS returning the max downward gain; update a global max with the through-node path.

```js
function maxPathSum(root) {
  let maxSum = -Infinity;
  function gain(node) {
    if (!node) return 0;
    const left = Math.max(gain(node.left), 0);   // ignore negative gains
    const right = Math.max(gain(node.right), 0);
    maxSum = Math.max(maxSum, node.val + left + right);
    return node.val + Math.max(left, right);     // can only extend one side upward
  }
  gain(root);
  return maxSum;
}
```

**Complexity:** Time **O(n)**, Space **O(h)**.

**💡 Interview tip:** Two key ideas: clamp negative gains to 0, and return only one branch upward (a path
can't fork at the parent).

---

### 8.6 Lowest Common Ancestor

**Problem:** Find the lowest common ancestor of two nodes in a binary tree.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `LinkedIn`

**Why this is a Tree DFS problem:** Recursively search both subtrees; the node where the two targets split
is the LCA.

**Approach:** DFS; if a subtree contains one target each (or the node itself is a target), it's the LCA.

```js
function lowestCommonAncestor(root, p, q) {
  if (!root || root === p || root === q) return root;
  const left = lowestCommonAncestor(root.left, p, q);
  const right = lowestCommonAncestor(root.right, p, q);
  if (left && right) return root; // p and q split here
  return left || right;
}
```

**Complexity:** Time **O(n)**, Space **O(h)**.

**💡 Interview tip:** For a **BST**, use the ordering for an O(h) solution without scanning both subtrees —
mention it if they specify a BST.

---

### 8.7 Validate a Binary Search Tree

**Problem:** Determine whether a binary tree is a valid BST.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Bloomberg`

**Why this is a Tree DFS problem:** Validity depends on value ranges propagated down each path — a DFS
carrying (min, max) bounds.

**Approach:** DFS passing allowed `(low, high)` bounds; each node must lie strictly within them.

```js
function isValidBST(root, low = -Infinity, high = Infinity) {
  if (!root) return true;
  if (root.val <= low || root.val >= high) return false;
  return isValidBST(root.left, low, root.val) &&
         isValidBST(root.right, root.val, high);
}
```

**Complexity:** Time **O(n)**, Space **O(h)**.

**💡 Interview tip:** Checking only `left < node < right` locally is wrong — you must propagate **ancestor
bounds**. An in-order traversal (must be strictly increasing) is an equally valid approach.

---

## 9. Graph Traversal

### 9.1 Number of Islands

**Problem:** Count connected groups of `'1'` (land) in a grid (4-directional).

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Uber` `Bloomberg`

**Why this is a Graph Traversal problem:** The grid is an implicit graph; counting components = flood-fill
from each unvisited land cell.

**Approach:** Scan cells; on land, increment count and DFS-sink the whole island.

```js
function numIslands(grid) {
  if (!grid.length) return 0;
  const rows = grid.length, cols = grid[0].length;
  let count = 0;
  function dfs(r, c) {
    if (r < 0 || c < 0 || r >= rows || c >= cols || grid[r][c] === '0') return;
    grid[r][c] = '0';
    dfs(r + 1, c); dfs(r - 1, c); dfs(r, c + 1); dfs(r, c - 1);
  }
  for (let r = 0; r < rows; r++)
    for (let c = 0; c < cols; c++)
      if (grid[r][c] === '1') { count++; dfs(r, c); }
  return count;
}
```

**Complexity:** Time **O(rows·cols)**, Space **O(rows·cols)**.

**💡 Interview tip:** Ask if mutating the grid is allowed; otherwise keep a `visited` set. BFS avoids deep
recursion on huge grids.

---

### 9.2 Clone Graph

**Problem:** Deep-copy a connected undirected graph given a node reference.

**Company tags:** `Amazon` `Google` `Meta` `Microsoft` `Uber`

**Why this is a Graph Traversal problem:** Visit every node/edge once while handling cycles via a
visited→clone map.

**Approach:** DFS; clone on first visit, register before recursing, link neighbors.

```js
function cloneGraph(node) {
  if (!node) return null;
  const cloned = new Map();
  function dfs(curr) {
    if (cloned.has(curr)) return cloned.get(curr);
    const copy = { val: curr.val, neighbors: [] };
    cloned.set(curr, copy);
    for (const nb of curr.neighbors) copy.neighbors.push(dfs(nb));
    return copy;
  }
  return dfs(node);
}
```

**Complexity:** Time **O(V + E)**, Space **O(V)**.

**💡 Interview tip:** Register the clone in the map **before** recursing — otherwise cycles cause infinite
recursion.

---

### 9.3 Flood Fill

**Problem:** Given an image grid, a start pixel, and a new color, fill the connected region of the same
color.

**Company tags:** `Amazon` `Microsoft` `Adobe`

**Why this is a Graph Traversal problem:** Connected same-color pixels form a component to traverse and
recolor.

**Approach:** DFS/BFS from the start, recoloring matching neighbors; guard against the no-op case.

```js
function floodFill(image, sr, sc, newColor) {
  const start = image[sr][sc];
  if (start === newColor) return image;
  function dfs(r, c) {
    if (r < 0 || c < 0 || r >= image.length || c >= image[0].length || image[r][c] !== start) return;
    image[r][c] = newColor;
    dfs(r + 1, c); dfs(r - 1, c); dfs(r, c + 1); dfs(r, c - 1);
  }
  dfs(sr, sc);
  return image;
}
```

**Complexity:** Time **O(n)** pixels, Space **O(n)**.

**💡 Interview tip:** The `start === newColor` guard prevents infinite recursion — call it out.

---

### 9.4 Rotting Oranges

**Problem:** Each minute, rotten oranges (2) rot adjacent fresh ones (1). Return minutes until none are
fresh, or -1 if impossible.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta`

**Why this is a Graph Traversal problem:** Simultaneous spread from multiple sources = **multi-source BFS**,
where BFS levels are minutes.

**Approach:** Enqueue all rotten cells; BFS level by level rotting neighbors; count minutes; verify no
fresh remain.

```js
function orangesRotting(grid) {
  const rows = grid.length, cols = grid[0].length;
  const queue = [];
  let fresh = 0;
  for (let r = 0; r < rows; r++)
    for (let c = 0; c < cols; c++) {
      if (grid[r][c] === 2) queue.push([r, c]);
      else if (grid[r][c] === 1) fresh++;
    }
  let minutes = 0;
  const dirs = [[1,0],[-1,0],[0,1],[0,-1]];
  while (queue.length && fresh > 0) {
    const size = queue.length;
    for (let i = 0; i < size; i++) {
      const [r, c] = queue.shift();
      for (const [dr, dc] of dirs) {
        const nr = r + dr, nc = c + dc;
        if (nr >= 0 && nc >= 0 && nr < rows && nc < cols && grid[nr][nc] === 1) {
          grid[nr][nc] = 2; fresh--; queue.push([nr, nc]);
        }
      }
    }
    minutes++;
  }
  return fresh === 0 ? minutes : -1;
}
```

**Complexity:** Time **O(rows·cols)**, Space **O(rows·cols)**.

**💡 Interview tip:** Emphasize **multi-source BFS** (seed the queue with all rotten cells). Track `fresh` to
detect the impossible case.

---

### 9.5 Word Ladder (Shortest Transformation)

**Problem:** Given `beginWord`, `endWord`, and a word list, return the length of the shortest transformation
sequence changing one letter at a time (each intermediate must be in the list).

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `LinkedIn`

**Why this is a Graph Traversal problem:** Words are nodes; edges connect words differing by one letter.
Shortest path in an unweighted graph → BFS.

**Approach:** BFS from `beginWord`, generating one-letter mutations; the first time you reach `endWord`,
return the level.

```js
function ladderLength(beginWord, endWord, wordList) {
  const words = new Set(wordList);
  if (!words.has(endWord)) return 0;
  const queue = [[beginWord, 1]];
  while (queue.length) {
    const [word, steps] = queue.shift();
    if (word === endWord) return steps;
    for (let i = 0; i < word.length; i++) {
      for (let c = 97; c <= 122; c++) {
        const next = word.slice(0, i) + String.fromCharCode(c) + word.slice(i + 1);
        if (words.has(next)) {
          words.delete(next);         // mark visited
          queue.push([next, steps + 1]);
        }
      }
    }
  }
  return 0;
}
```

**Complexity:** Time **O(N · L · 26)** (N words, L length), Space **O(N)**.

**💡 Interview tip:** Deleting visited words from the set avoids revisits. Bidirectional BFS is the optimal
follow-up for large inputs.

---

### 9.6 Pacific Atlantic Water Flow

**Problem:** In a height grid, water flows to lower/equal neighbors. Return cells from which water can reach
**both** the Pacific (top/left) and Atlantic (bottom/right) edges.

**Company tags:** `Amazon` `Google` `Meta`

**Why this is a Graph Traversal problem:** Reverse the flow — DFS **inland** from each ocean's borders;
cells reachable from both oceans are the answer.

**Approach:** DFS from Pacific borders and Atlantic borders separately (climbing to ≥ heights); intersect
the two reachable sets.

```js
function pacificAtlantic(heights) {
  if (!heights.length) return [];
  const rows = heights.length, cols = heights[0].length;
  const pac = Array.from({ length: rows }, () => new Array(cols).fill(false));
  const atl = Array.from({ length: rows }, () => new Array(cols).fill(false));
  const dirs = [[1,0],[-1,0],[0,1],[0,-1]];
  function dfs(r, c, visited, prev) {
    if (r < 0 || c < 0 || r >= rows || c >= cols || visited[r][c] || heights[r][c] < prev) return;
    visited[r][c] = true;
    for (const [dr, dc] of dirs) dfs(r + dr, c + dc, visited, heights[r][c]);
  }
  for (let r = 0; r < rows; r++) { dfs(r, 0, pac, -Infinity); dfs(r, cols - 1, atl, -Infinity); }
  for (let c = 0; c < cols; c++) { dfs(0, c, pac, -Infinity); dfs(rows - 1, c, atl, -Infinity); }
  const res = [];
  for (let r = 0; r < rows; r++)
    for (let c = 0; c < cols; c++)
      if (pac[r][c] && atl[r][c]) res.push([r, c]);
  return res;
}
```

**Complexity:** Time **O(rows·cols)**, Space **O(rows·cols)**.

**💡 Interview tip:** The key trick is **reversing the flow** (DFS uphill from the oceans) — far cheaper than
testing every cell's downhill path.

---

## 10. Topological Sort

### 10.1 Course Schedule (Can Finish?)

**Problem:** Given prerequisites, determine if all courses can be finished (no cyclic dependency).

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Uber`

**Why this is a Topological Sort problem:** Dependency ordering on a directed graph; a valid order exists iff
the graph is a DAG.

**Approach (Kahn's BFS):** Build in-degrees; process zero-in-degree nodes, decrementing neighbors; if all
processed, no cycle.

```js
function canFinish(numCourses, prerequisites) {
  const adj = Array.from({ length: numCourses }, () => []);
  const indeg = new Array(numCourses).fill(0);
  for (const [c, p] of prerequisites) { adj[p].push(c); indeg[c]++; }
  const queue = [];
  for (let i = 0; i < numCourses; i++) if (indeg[i] === 0) queue.push(i);
  let done = 0;
  while (queue.length) {
    const node = queue.shift(); done++;
    for (const nxt of adj[node]) if (--indeg[nxt] === 0) queue.push(nxt);
  }
  return done === numCourses;
}
```

**Complexity:** Time **O(V + E)**, Space **O(V + E)**.

**💡 Interview tip:** A cycle = impossible ordering. Mention DFS-with-cycle-detection as the alternative.

---

### 10.2 Course Schedule II (Order)

**Problem:** Return a valid order to take all courses, or an empty array if impossible.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Uber`

**Why this is a Topological Sort problem:** It explicitly asks for a topological ordering of a dependency
DAG.

**Approach:** Kahn's BFS, recording the processing order.

```js
function findOrder(numCourses, prerequisites) {
  const adj = Array.from({ length: numCourses }, () => []);
  const indeg = new Array(numCourses).fill(0);
  for (const [c, p] of prerequisites) { adj[p].push(c); indeg[c]++; }
  const queue = [], order = [];
  for (let i = 0; i < numCourses; i++) if (indeg[i] === 0) queue.push(i);
  while (queue.length) {
    const node = queue.shift(); order.push(node);
    for (const nxt of adj[node]) if (--indeg[nxt] === 0) queue.push(nxt);
  }
  return order.length === numCourses ? order : [];
}
```

**Complexity:** Time **O(V + E)**, Space **O(V + E)**.

**💡 Interview tip:** Kahn's naturally yields the order; return `[]` when a cycle prevents completion.

---

### 10.3 Alien Dictionary

**Problem:** Given words sorted in an alien language, derive a valid character order.

**Company tags:** `Amazon` `Google` `Meta` `Airbnb`

**Why this is a Topological Sort problem:** Adjacent word comparisons yield "char A before char B" edges; a
topological order of those edges is the alphabet.

**Approach:** Build edges from adjacent word pairs (first differing char), then Kahn's topo sort; detect
invalid prefixes and cycles.

```js
function alienOrder(words) {
  const adj = new Map(), indeg = new Map();
  for (const w of words) for (const ch of w) { adj.set(ch, adj.get(ch) || new Set()); indeg.set(ch, 0); }
  for (let i = 0; i < words.length - 1; i++) {
    const a = words[i], b = words[i + 1];
    const len = Math.min(a.length, b.length);
    if (a.length > b.length && a.startsWith(b)) return ""; // invalid prefix order
    for (let j = 0; j < len; j++) {
      if (a[j] !== b[j]) {
        if (!adj.get(a[j]).has(b[j])) { adj.get(a[j]).add(b[j]); indeg.set(b[j], indeg.get(b[j]) + 1); }
        break;
      }
    }
  }
  const queue = [];
  for (const [ch, d] of indeg) if (d === 0) queue.push(ch);
  let res = "";
  while (queue.length) {
    const ch = queue.shift(); res += ch;
    for (const nxt of adj.get(ch)) { indeg.set(nxt, indeg.get(nxt) - 1); if (indeg.get(nxt) === 0) queue.push(nxt); }
  }
  return res.length === indeg.size ? res : ""; // cycle -> invalid
}
```

**Complexity:** Time **O(C)** (total chars), Space **O(1)** (bounded alphabet).

**💡 Interview tip:** Two edge cases distinguish strong answers: the invalid-prefix case (`"abc"` before
`"ab"`) and cycle detection.

---

### 10.4 Minimum Height Trees

**Problem:** In an undirected tree (n nodes), find all roots that minimize the tree's height.

**Company tags:** `Amazon` `Google` `Meta`

**Why this is a Topological Sort (peeling) problem:** Repeatedly trim leaves layer by layer (like Kahn's on
degree-1 nodes); the last 1–2 remaining are the centroids.

**Approach:** Build degrees; iteratively remove current leaves until ≤2 nodes remain.

```js
function findMinHeightTrees(n, edges) {
  if (n === 1) return [0];
  const adj = Array.from({ length: n }, () => new Set());
  for (const [a, b] of edges) { adj[a].add(b); adj[b].add(a); }
  let leaves = [];
  for (let i = 0; i < n; i++) if (adj[i].size === 1) leaves.push(i);
  let remaining = n;
  while (remaining > 2) {
    remaining -= leaves.length;
    const next = [];
    for (const leaf of leaves) {
      const nb = [...adj[leaf]][0];
      adj[nb].delete(leaf);
      if (adj[nb].size === 1) next.push(nb);
    }
    leaves = next;
  }
  return leaves;
}
```

**Complexity:** Time **O(V + E)**, Space **O(V + E)**.

**💡 Interview tip:** Frame it as "peel leaves toward the center" — there are at most two centroids in a
tree.

---

### 10.5 Task Scheduling Order

**Problem:** Given tasks and dependency pairs `[a, b]` (b before a), return any valid execution order, or
empty if impossible.

**Company tags:** `Amazon` `Microsoft` `Uber`

**Why this is a Topological Sort problem:** It's the generic dependency-ordering problem — identical
structure to Course Schedule II.

**Approach:** Kahn's BFS over the dependency graph, recording order.

```js
function taskOrder(tasks, dependencies) {
  const adj = Array.from({ length: tasks }, () => []);
  const indeg = new Array(tasks).fill(0);
  for (const [a, b] of dependencies) { adj[b].push(a); indeg[a]++; }
  const queue = [], order = [];
  for (let i = 0; i < tasks; i++) if (indeg[i] === 0) queue.push(i);
  while (queue.length) {
    const t = queue.shift(); order.push(t);
    for (const nxt of adj[t]) if (--indeg[nxt] === 0) queue.push(nxt);
  }
  return order.length === tasks ? order : [];
}
```

**Complexity:** Time **O(V + E)**, Space **O(V + E)**.

**💡 Interview tip:** Recognizing this as the *same* pattern as Course Schedule shows pattern transfer — the
real interview skill.

---

## 11. Two Heaps

> These problems use the `Heap` class shown near the top of this file.

### 11.1 Find Median from a Data Stream

**Problem:** Support adding numbers and querying the running median efficiently.

**Company tags:** `Amazon` `Google` `Microsoft` `Bloomberg`

**Why this is a Two Heaps problem:** The median sits between the smaller half (max-heap) and larger half
(min-heap); balancing them gives O(1) median.

**Approach:** Push to max-heap, shift its top to min-heap, rebalance sizes; median is the larger heap's top
or the average of both tops.

```js
class MedianFinder {
  constructor() {
    this.lo = new Heap((a, b) => b - a); // max-heap (smaller half)
    this.hi = new Heap((a, b) => a - b); // min-heap (larger half)
  }
  addNum(num) {
    this.lo.push(num);
    this.hi.push(this.lo.pop());
    if (this.hi.size() > this.lo.size()) this.lo.push(this.hi.pop());
  }
  findMedian() {
    if (this.lo.size() > this.hi.size()) return this.lo.peek();
    return (this.lo.peek() + this.hi.peek()) / 2;
  }
}
```

**Complexity:** `addNum` **O(log n)**, `findMedian` **O(1)**, Space **O(n)**.

**💡 Interview tip:** The "push-then-transfer" balancing keeps both halves valid; state that JS lacks a
built-in heap so you'd supply one.

---

### 11.2 Sliding Window Median

**Problem:** Return the median of each window of size `k` as it slides across the array.

**Company tags:** `Amazon` `Google` `Bloomberg`

**Why this is a Two Heaps problem:** Same two-heap median structure, extended with removal of the
out-of-window element each step.

**Approach:** Maintain two heaps with lazy deletion (or rebalance); for each step add the new element and
remove the one leaving the window, then read the median.

```js
// Simplified O(n*k) version for clarity (sorted-insert window).
function medianSlidingWindow(nums, k) {
  const window = [];
  const res = [];
  const insertSorted = (arr, val) => {
    let lo = 0, hi = arr.length;
    while (lo < hi) { const mid = (lo + hi) >> 1; arr[mid] < val ? lo = mid + 1 : hi = mid; }
    arr.splice(lo, 0, val);
  };
  for (let i = 0; i < nums.length; i++) {
    insertSorted(window, nums[i]);
    if (window.length > k) {
      const idx = window.indexOf(nums[i - k]);
      window.splice(idx, 1);
    }
    if (window.length === k) {
      const mid = k >> 1;
      res.push(k % 2 ? window[mid] : (window[mid - 1] + window[mid]) / 2);
    }
  }
  return res;
}
```

**Complexity:** Sorted-window version **O(n·k)**; the optimal two-heaps-with-lazy-deletion is **O(n log k)**.

**💡 Interview tip:** State the two-heaps + lazy-deletion approach for O(n log k); the sorted-window version
is a clean fallback that's easy to get right under pressure.

---

### 11.3 Maximize Capital (IPO)

**Problem:** With starting capital `w` and at most `k` projects (each with capital requirement and profit),
maximize final capital.

**Company tags:** `Amazon` `Google` `Bloomberg`

**Why this is a Two Heaps problem:** A min-heap by capital reveals affordable projects; a max-heap by profit
picks the most profitable affordable one — two heaps cooperating.

**Approach:** Push affordable projects (capital ≤ w) into a profit max-heap; take the best, add its profit,
repeat up to `k` times.

```js
function findMaximizedCapital(k, w, profits, capital) {
  const byCapital = new Heap((a, b) => a.cap - b.cap);
  const byProfit = new Heap((a, b) => b.profit - a.profit);
  for (let i = 0; i < profits.length; i++) byCapital.push({ cap: capital[i], profit: profits[i] });
  for (let i = 0; i < k; i++) {
    while (byCapital.size() && byCapital.peek().cap <= w) byProfit.push(byCapital.pop());
    if (!byProfit.size()) break;          // nothing affordable
    w += byProfit.pop().profit;
  }
  return w;
}
```

**Complexity:** Time **O(n log n)**, Space **O(n)**.

**💡 Interview tip:** The greedy insight (always take the most profitable currently-affordable project) plus
two heaps is what makes this efficient.

---

### 11.4 Next Interval

**Problem:** For each interval, find the index of the interval with the smallest start ≥ this interval's
end (-1 if none).

**Company tags:** `Amazon` `Google`

**Why this is a Two Heaps problem:** Two max-heaps (by start and by end) let you match each end to the
nearest qualifying start.

**Approach:** Heaps keyed by start and by end; pop the largest end and find the smallest start ≥ it by
draining the start-heap.

```js
function findRightInterval(intervals) {
  const res = new Array(intervals.length).fill(-1);
  const startHeap = new Heap((a, b) => b.val - a.val); // max by start
  const endHeap = new Heap((a, b) => b.val - a.val);   // max by end
  intervals.forEach((iv, i) => { startHeap.push({ val: iv[0], i }); endHeap.push({ val: iv[1], i }); });
  while (endHeap.size()) {
    const { val: end, i } = endHeap.pop();
    if (startHeap.peek().val >= end) {
      let candidate = startHeap.pop();
      while (startHeap.size() && startHeap.peek().val >= end) candidate = startHeap.pop();
      res[i] = candidate.i;
      startHeap.push(candidate); // put back the best match for reuse
    }
  }
  return res;
}
```

**Complexity:** Time **O(n log n)**, Space **O(n)**.

**💡 Interview tip:** A simpler approach sorts starts and binary-searches each end — mention it; the
two-heap version demonstrates the pattern explicitly.

---


## 12. Top-K Elements

> These problems use the `Heap` class shown near the top of this file.

### 12.1 Kth Largest Element in an Array

**Problem:** Find the `k`th largest element in an unsorted array.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Bloomberg`

**Why this is a Top-K problem:** A min-heap of size `k` keeps the k largest seen, giving O(n log k).

**Approach:** Push each value; pop the smallest when size exceeds `k`; the top is the answer.

```js
function findKthLargest(nums, k) {
  const minHeap = new Heap((a, b) => a - b);
  for (const num of nums) {
    minHeap.push(num);
    if (minHeap.size() > k) minHeap.pop();
  }
  return minHeap.peek();
}
// findKthLargest([3,2,1,5,6,4], 2) -> 5
```

**Complexity:** Time **O(n log k)**, Space **O(k)**.

**💡 Interview tip:** Spectrum: sort O(n log n), heap O(n log k), **Quickselect** average O(n). Heap is the
clean default; mention Quickselect for optimal average.

---

### 12.2 Top K Frequent Elements

**Problem:** Return the `k` most frequent elements.

**Company tags:** `Amazon` `Google` `Meta` `Uber` `Flipkart`

**Why this is a Top-K problem:** Count frequencies, then select the top K — bucket sort by frequency gives
O(n).

**Approach:** Frequency map → buckets indexed by frequency → read from the highest frequency down.

```js
function topKFrequent(nums, k) {
  const freq = new Map();
  for (const num of nums) freq.set(num, (freq.get(num) || 0) + 1);
  const buckets = Array.from({ length: nums.length + 1 }, () => []);
  for (const [num, c] of freq) buckets[c].push(num);
  const res = [];
  for (let f = buckets.length - 1; f >= 0 && res.length < k; f--) {
    for (const num of buckets[f]) { res.push(num); if (res.length === k) break; }
  }
  return res;
}
// topKFrequent([1,1,1,2,2,3], 2) -> [1,2]
```

**Complexity:** Time **O(n)**, Space **O(n)**.

**💡 Interview tip:** Heap gives O(n log k); bucket sort achieves O(n) since frequencies ≤ n. Offering O(n)
stands out.

---

### 12.3 K Closest Points to Origin

**Problem:** Return the `k` points closest to the origin.

**Company tags:** `Amazon` `Google` `Meta` `Uber`

**Why this is a Top-K problem:** "Closest K" by distance → a max-heap of size `k` keyed by squared distance.

**Approach:** Push each point; when size exceeds `k`, pop the farthest; return what remains.

```js
function kClosest(points, k) {
  const maxHeap = new Heap((a, b) => b.d - a.d); // farthest on top
  for (const [x, y] of points) {
    maxHeap.push({ d: x * x + y * y, point: [x, y] });
    if (maxHeap.size() > k) maxHeap.pop();
  }
  return maxHeap.data.map(e => e.point);
}
// kClosest([[1,3],[-2,2]], 1) -> [[-2,2]]
```

**Complexity:** Time **O(n log k)**, Space **O(k)**.

**💡 Interview tip:** Use **squared** distance to avoid `Math.sqrt` — it doesn't change ordering and is
faster/exact.

---

### 12.4 Sort Characters by Frequency

**Problem:** Sort a string so characters appear in decreasing frequency order.

**Company tags:** `Amazon` `Google` `Bloomberg`

**Why this is a Top-K problem:** Order by frequency = repeatedly take the most frequent — a max-heap (or
bucket sort) by count.

**Approach:** Count chars; bucket by frequency; build the result from highest frequency down.

```js
function frequencySort(s) {
  const freq = new Map();
  for (const c of s) freq.set(c, (freq.get(c) || 0) + 1);
  const buckets = Array.from({ length: s.length + 1 }, () => []);
  for (const [c, count] of freq) buckets[count].push(c);
  let res = "";
  for (let f = buckets.length - 1; f >= 0; f--) {
    for (const c of buckets[f]) res += c.repeat(f);
  }
  return res;
}
// frequencySort("tree") -> "eert" (or "eetr")
```

**Complexity:** Time **O(n)**, Space **O(n)**.

**💡 Interview tip:** Bucket sort beats a heap here for O(n); note multiple valid outputs exist for ties.

---

### 12.5 Reorganize String

**Problem:** Rearrange a string so no two adjacent characters are the same (or return "" if impossible).

**Company tags:** `Amazon` `Google` `Meta`

**Why this is a Top-K problem:** Always place the **most frequent remaining** character that isn't the one
just used — a greedy max-heap by frequency.

**Approach:** Max-heap by count; pop the top, hold it back one step so it can't be placed consecutively.

```js
function reorganizeString(s) {
  const freq = new Map();
  for (const c of s) freq.set(c, (freq.get(c) || 0) + 1);
  const maxHeap = new Heap((a, b) => b.count - a.count);
  for (const [ch, count] of freq) maxHeap.push({ ch, count });
  let res = "", prev = null;
  while (maxHeap.size()) {
    const cur = maxHeap.pop();
    res += cur.ch;
    cur.count--;
    if (prev && prev.count > 0) maxHeap.push(prev); // re-add the previous char
    prev = cur;
  }
  return res.length === s.length ? res : "";
}
// reorganizeString("aab") -> "aba"
```

**Complexity:** Time **O(n log k)**, Space **O(k)**.

**💡 Interview tip:** Holding the previous char back by one iteration enforces the no-adjacent rule. If the
max count exceeds `(n+1)/2`, it's impossible.

---

### 12.6 K Closest Numbers

**Problem:** In a sorted array, find the `k` numbers closest to a target `x` (return sorted).

**Company tags:** `Amazon` `Google`

**Why this is a Top-K problem:** "Closest K" in sorted data — best solved by binary-searching the window
start, but a heap also works.

**Approach (optimal):** Binary search for the left bound of the best length-`k` window by comparing the gap
to elements at both ends.

```js
function findClosestElements(arr, k, x) {
  let lo = 0, hi = arr.length - k;
  while (lo < hi) {
    const mid = (lo + hi) >> 1;
    // compare distance of the window edges to x
    if (x - arr[mid] > arr[mid + k] - x) lo = mid + 1;
    else hi = mid;
  }
  return arr.slice(lo, lo + k);
}
// findClosestElements([1,2,3,4,5], 4, 3) -> [1,2,3,4]
```

**Complexity:** Time **O(log(n−k) + k)**, Space **O(k)**.

**💡 Interview tip:** The heap solution is O(n log k); the **binary-search-the-window** answer is O(log n +
k) and is the standout for sorted input.

---

## 13. K-way Merge

> These problems use the `Heap` class shown near the top of this file.

### 13.1 Merge K Sorted Lists

**Problem:** Merge `k` sorted linked lists into one sorted list.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Bloomberg`

**Why this is a K-way Merge problem:** Multiple sorted sequences combined; a min-heap over current heads
always yields the global minimum next.

**Approach:** Push all heads; pop the smallest, append, push its `next`.

```js
function mergeKLists(lists) {
  const minHeap = new Heap((a, b) => a.val - b.val);
  for (const node of lists) if (node) minHeap.push(node);
  const dummy = { val: 0, next: null };
  let tail = dummy;
  while (minHeap.size()) {
    const node = minHeap.pop();
    tail.next = node; tail = node;
    if (node.next) minHeap.push(node.next);
  }
  return dummy.next;
}
```

**Complexity:** Time **O(N log k)**, Space **O(k)**.

**💡 Interview tip:** Mention the divide-and-conquer pairwise-merge alternative — also O(N log k) with O(1)
extra.

---

### 13.2 Kth Smallest in a Sorted Matrix

**Problem:** Given an `n×n` matrix with sorted rows and columns, find the `k`th smallest element.

**Company tags:** `Amazon` `Google` `Bloomberg`

**Why this is a K-way Merge problem:** Each row is a sorted list; a min-heap merges across rows to extract
the `k`th smallest.

**Approach:** Seed the heap with the first element of each row; pop `k` times, pushing the next element in
the popped element's row.

```js
function kthSmallest(matrix, k) {
  const n = matrix.length;
  const minHeap = new Heap((a, b) => a.val - b.val);
  for (let r = 0; r < Math.min(n, k); r++) minHeap.push({ val: matrix[r][0], r, c: 0 });
  let result = 0;
  for (let i = 0; i < k; i++) {
    const { val, r, c } = minHeap.pop();
    result = val;
    if (c + 1 < n) minHeap.push({ val: matrix[r][c + 1], r, c: c + 1 });
  }
  return result;
}
// kthSmallest([[1,5,9],[10,11,13],[12,13,15]], 8) -> 13
```

**Complexity:** Time **O(k log n)**, Space **O(n)**.

**💡 Interview tip:** The optimal **binary search on the value range** is O(n log(max−min)); mention it for
huge matrices.

---

### 13.3 Smallest Range Covering K Lists

**Problem:** Given `k` sorted lists, find the smallest range that includes at least one number from each.

**Company tags:** `Amazon` `Google` `Bloomberg`

**Why this is a K-way Merge problem:** Track the current minimum across lists (min-heap) and the running
maximum; the range spans them, advancing the list with the minimum.

**Approach:** Heap of one element per list; range = `[heapMin, currentMax]`; pop the min and push the next
from its list; stop when a list is exhausted.

```js
function smallestRange(nums) {
  const minHeap = new Heap((a, b) => a.val - b.val);
  let currentMax = -Infinity;
  nums.forEach((list, i) => { minHeap.push({ val: list[0], list: i, idx: 0 }); currentMax = Math.max(currentMax, list[0]); });
  let best = [-Infinity, Infinity];
  while (minHeap.size() === nums.length) {
    const { val, list, idx } = minHeap.pop();
    if (currentMax - val < best[1] - best[0]) best = [val, currentMax];
    if (idx + 1 < nums[list].length) {
      const next = nums[list][idx + 1];
      minHeap.push({ val: next, list, idx: idx + 1 });
      currentMax = Math.max(currentMax, next);
    }
  }
  return best;
}
// smallestRange([[4,10,15,24,26],[0,9,12,20],[5,18,22,30]]) -> [20,24]
```

**Complexity:** Time **O(N log k)**, Space **O(k)**.

**💡 Interview tip:** The loop must stop the moment one list runs out — you can no longer cover all lists.

---

### 13.4 Find K Pairs with Smallest Sums

**Problem:** Given two sorted arrays, find the `k` pairs `(a, b)` with the smallest sums.

**Company tags:** `Amazon` `Google` `LinkedIn`

**Why this is a K-way Merge problem:** Each element of the first array forms a sorted "list" of pair sums
with the second array; merge these k-ways via a min-heap.

**Approach:** Seed pairs `(nums1[i], nums2[0])`; pop the smallest sum, push the next pair in that row.

```js
function kSmallestPairs(nums1, nums2, k) {
  const res = [];
  if (!nums1.length || !nums2.length) return res;
  const minHeap = new Heap((a, b) => a.sum - b.sum);
  for (let i = 0; i < Math.min(nums1.length, k); i++) {
    minHeap.push({ sum: nums1[i] + nums2[0], i, j: 0 });
  }
  while (minHeap.size() && res.length < k) {
    const { i, j } = minHeap.pop();
    res.push([nums1[i], nums2[j]]);
    if (j + 1 < nums2.length) minHeap.push({ sum: nums1[i] + nums2[j + 1], i, j: j + 1 });
  }
  return res;
}
// kSmallestPairs([1,7,11], [2,4,6], 3) -> [[1,2],[1,4],[1,6]]
```

**Complexity:** Time **O(k log k)**, Space **O(k)**.

**💡 Interview tip:** Only seed the first column (`j = 0`) and expand rightward — seeding all pairs defeats
the efficiency.

---

## 14. Modified Binary Search

### 14.1 Search in Rotated Sorted Array

**Problem:** Find a target's index in a rotated sorted array, or -1. Expected O(log n).

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Bloomberg` `Adobe`

**Why this is a Modified Binary Search problem:** One half is always sorted; decide which half can contain
the target and discard the other.

**Approach:** Determine the sorted half; if the target lies in its range, search there, else the other.

```js
function search(nums, target) {
  let lo = 0, hi = nums.length - 1;
  while (lo <= hi) {
    const mid = (lo + hi) >> 1;
    if (nums[mid] === target) return mid;
    if (nums[lo] <= nums[mid]) {                 // left sorted
      if (target >= nums[lo] && target < nums[mid]) hi = mid - 1; else lo = mid + 1;
    } else {                                     // right sorted
      if (target > nums[mid] && target <= nums[hi]) lo = mid + 1; else hi = mid - 1;
    }
  }
  return -1;
}
// search([4,5,6,7,0,1,2], 0) -> 4
```

**Complexity:** Time **O(log n)**, Space **O(1)**.

**💡 Interview tip:** Verbalize the invariant "which half is sorted, is target inside it?". Duplicates
degrade the worst case to O(n).

---

### 14.2 Find First and Last Position

**Problem:** Find the first and last index of a target in a sorted array; `[-1,-1]` if absent.

**Company tags:** `Amazon` `Google` `Microsoft` `Adobe`

**Why this is a Modified Binary Search problem:** Locating value boundaries = binary-search-for-the-edge,
done twice.

**Approach:** Two biased binary searches — one keeps going left on a match, the other right.

```js
function searchRange(nums, target) {
  const bound = (isFirst) => {
    let lo = 0, hi = nums.length - 1, res = -1;
    while (lo <= hi) {
      const mid = (lo + hi) >> 1;
      if (nums[mid] === target) { res = mid; isFirst ? hi = mid - 1 : lo = mid + 1; }
      else if (nums[mid] < target) lo = mid + 1;
      else hi = mid - 1;
    }
    return res;
  };
  return [bound(true), bound(false)];
}
// searchRange([5,7,7,8,8,10], 8) -> [3,4]
```

**Complexity:** Time **O(log n)**, Space **O(1)**.

**💡 Interview tip:** Don't stop at the first match — keep narrowing toward the boundary.

---

### 14.3 Find Minimum in Rotated Sorted Array

**Problem:** Find the minimum element of a rotated sorted array (distinct values).

**Company tags:** `Amazon` `Google` `Microsoft` `Bloomberg`

**Why this is a Modified Binary Search problem:** Compare `mid` to `hi` to decide which half holds the
rotation point (the minimum).

**Approach:** If `nums[mid] > nums[hi]`, the min is to the right; else it's at `mid` or left.

```js
function findMin(nums) {
  let lo = 0, hi = nums.length - 1;
  while (lo < hi) {
    const mid = (lo + hi) >> 1;
    if (nums[mid] > nums[hi]) lo = mid + 1;
    else hi = mid;
  }
  return nums[lo];
}
// findMin([4,5,6,7,0,1,2]) -> 0
```

**Complexity:** Time **O(log n)**, Space **O(1)**.

**💡 Interview tip:** Compare to `hi` (not `lo`) — comparing to `lo` fails on already-sorted inputs.

---

### 14.4 Find Peak Element

**Problem:** Find any peak (an element greater than its neighbors); return its index. O(log n).

**Company tags:** `Amazon` `Google` `Meta` `Bloomberg`

**Why this is a Modified Binary Search problem:** Even unsorted, comparing `mid` with `mid+1` tells you
which side must contain a peak — so you halve the search.

**Approach:** If `nums[mid] < nums[mid+1]`, a peak lies to the right; else at `mid` or left.

```js
function findPeakElement(nums) {
  let lo = 0, hi = nums.length - 1;
  while (lo < hi) {
    const mid = (lo + hi) >> 1;
    if (nums[mid] < nums[mid + 1]) lo = mid + 1;
    else hi = mid;
  }
  return lo;
}
// findPeakElement([1,2,3,1]) -> 2
```

**Complexity:** Time **O(log n)**, Space **O(1)**.

**💡 Interview tip:** This shows binary search applies beyond sorted arrays — explain why a peak must exist
in the chosen half.

---

### 14.5 Koko Eating Bananas (Search the Answer)

**Problem:** Koko eats `k` bananas/hour from piles. Find the minimum `k` so she finishes all piles within
`h` hours.

**Company tags:** `Amazon` `Google` `Meta`

**Why this is a Modified Binary Search problem:** The answer space (eating speed) is monotonic — higher
speed never needs more hours — so binary-search the **answer**.

**Approach:** Binary search `k` in `[1, max(piles)]`; feasibility = total hours at speed `k` ≤ `h`.

```js
function minEatingSpeed(piles, h) {
  const hoursNeeded = (k) => piles.reduce((sum, p) => sum + Math.ceil(p / k), 0);
  let lo = 1, hi = Math.max(...piles);
  while (lo < hi) {
    const mid = (lo + hi) >> 1;
    if (hoursNeeded(mid) <= h) hi = mid;   // feasible -> try slower
    else lo = mid + 1;                     // too slow -> faster
  }
  return lo;
}
// minEatingSpeed([3,6,7,11], 8) -> 4
```

**Complexity:** Time **O(n log(maxPile))**, Space **O(1)**.

**💡 Interview tip:** Recognizing "binary search on the answer" (monotonic feasibility) is the key insight —
it generalizes to capacity/threshold problems.

---

### 14.6 Search a 2D Matrix

**Problem:** Search a target in a matrix where each row is sorted and the first integer of each row exceeds
the last of the previous row. O(log(m·n)).

**Company tags:** `Amazon` `Google` `Microsoft`

**Why this is a Modified Binary Search problem:** The matrix behaves like one sorted array of length `m·n`;
binary-search with index→(row,col) mapping.

**Approach:** Binary search over `[0, m·n−1]`, mapping `mid` to `(mid / cols, mid % cols)`.

```js
function searchMatrix(matrix, target) {
  const rows = matrix.length, cols = matrix[0].length;
  let lo = 0, hi = rows * cols - 1;
  while (lo <= hi) {
    const mid = (lo + hi) >> 1;
    const val = matrix[Math.floor(mid / cols)][mid % cols];
    if (val === target) return true;
    val < target ? lo = mid + 1 : hi = mid - 1;
  }
  return false;
}
// searchMatrix([[1,3,5,7],[10,11,16,20],[23,30,34,60]], 3) -> true
```

**Complexity:** Time **O(log(m·n))**, Space **O(1)**.

**💡 Interview tip:** The index→coordinate mapping is the trick. If only rows (not the whole matrix) are
sorted, use the staircase O(m+n) search instead.

---

## 15. Subsets / Backtracking

### 15.1 Generate All Subsets

**Problem:** Return all subsets (the power set) of distinct integers.

**Company tags:** `Amazon` `Google` `Meta` `Microsoft` `Adobe`

**Why this is a Backtracking problem:** Explore an include/exclude decision tree, recording every node.

**Approach:** Recurse with a start index; record the current subset, extend, recurse, undo.

```js
function subsets(nums) {
  const res = [];
  function backtrack(start, current) {
    res.push([...current]);
    for (let i = start; i < nums.length; i++) {
      current.push(nums[i]);
      backtrack(i + 1, current);
      current.pop();
    }
  }
  backtrack(0, []);
  return res;
}
// subsets([1,2,3]) -> 8 subsets
```

**Complexity:** Time **O(n·2ⁿ)**, Space **O(n)** recursion.

**💡 Interview tip:** Master the choose → explore → un-choose template; push a copy, not the reference.

---

### 15.2 Permutations

**Problem:** Return all permutations of distinct integers.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Uber`

**Why this is a Backtracking problem:** All orderings = place each unused element at each position,
backtracking after.

**Approach:** Track used elements; add unused, recurse, undo.

```js
function permute(nums) {
  const res = [], used = new Array(nums.length).fill(false);
  function backtrack(current) {
    if (current.length === nums.length) { res.push([...current]); return; }
    for (let i = 0; i < nums.length; i++) {
      if (used[i]) continue;
      used[i] = true; current.push(nums[i]);
      backtrack(current);
      current.pop(); used[i] = false;
    }
  }
  backtrack([]);
  return res;
}
// permute([1,2,3]) -> 6 permutations
```

**Complexity:** Time **O(n·n!)**, Space **O(n)**.

**💡 Interview tip:** For duplicates, sort and skip equal siblings to avoid repeats.

---

### 15.3 Combination Sum

**Problem:** Given distinct candidates and a target, return all unique combinations summing to the target
(each number reusable).

**Company tags:** `Amazon` `Google` `Meta` `Adobe`

**Why this is a Backtracking problem:** Build combinations by repeatedly choosing candidates and pruning
when the running sum exceeds the target.

**Approach:** Recurse with a start index (allow reuse via same `i`); prune when remaining < 0.

```js
function combinationSum(candidates, target) {
  const res = [];
  function backtrack(start, remaining, current) {
    if (remaining === 0) { res.push([...current]); return; }
    if (remaining < 0) return;
    for (let i = start; i < candidates.length; i++) {
      current.push(candidates[i]);
      backtrack(i, remaining - candidates[i], current); // i (not i+1) -> reuse allowed
      current.pop();
    }
  }
  backtrack(0, target, []);
  return res;
}
// combinationSum([2,3,6,7], 7) -> [[2,2,3],[7]]
```

**Complexity:** Exponential in the worst case; bounded by the target/candidates. Space **O(target)** depth.

**💡 Interview tip:** Passing `i` (not `i+1`) enables reuse; for "each used once," pass `i+1` and dedupe.

---

### 15.4 Letter Combinations of a Phone Number

**Problem:** Given digits 2–9, return all letter combinations they could spell (phone keypad).

**Company tags:** `Amazon` `Google` `Meta` `Microsoft`

**Why this is a Backtracking problem:** Each digit multiplies the branching; build strings one digit at a
time.

**Approach:** Map digits to letters; recurse appending each letter for the current digit.

```js
function letterCombinations(digits) {
  if (!digits.length) return [];
  const map = { '2':'abc','3':'def','4':'ghi','5':'jkl','6':'mno','7':'pqrs','8':'tuv','9':'wxyz' };
  const res = [];
  function backtrack(index, current) {
    if (index === digits.length) { res.push(current); return; }
    for (const ch of map[digits[index]]) backtrack(index + 1, current + ch);
  }
  backtrack(0, "");
  return res;
}
// letterCombinations("23") -> ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

**Complexity:** Time **O(4ⁿ·n)**, Space **O(n)** recursion.

**💡 Interview tip:** Handle the empty-input edge case up front; the branching factor is 3–4 per digit.

---

### 15.5 Generate Parentheses

**Problem:** Generate all valid combinations of `n` pairs of parentheses.

**Company tags:** `Amazon` `Google` `Meta` `Uber`

**Why this is a Backtracking problem:** Build strings while pruning invalid prefixes (never more `)` than
`(`).

**Approach:** Track open/close counts; add `(` while `open < n`, add `)` while `close < open`.

```js
function generateParenthesis(n) {
  const res = [];
  function backtrack(current, open, close) {
    if (current.length === 2 * n) { res.push(current); return; }
    if (open < n) backtrack(current + "(", open + 1, close);
    if (close < open) backtrack(current + ")", open, close + 1);
  }
  backtrack("", 0, 0);
  return res;
}
// generateParenthesis(3) -> 5 combinations
```

**Complexity:** Time **O(4ⁿ/√n)** (Catalan number), Space **O(n)**.

**💡 Interview tip:** The constraints (`open < n`, `close < open`) prune invalid branches early — far better
than generating all and filtering.

---

### 15.6 Word Search

**Problem:** Given a grid of letters and a word, return true if the word exists via adjacent cells (no
reuse).

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Bloomberg`

**Why this is a Backtracking problem:** DFS from each cell, marking visited and backtracking when a path
fails.

**Approach:** DFS matching characters; temporarily mark the cell visited, recurse 4 directions, restore.

```js
function exist(board, word) {
  const rows = board.length, cols = board[0].length;
  function dfs(r, c, i) {
    if (i === word.length) return true;
    if (r < 0 || c < 0 || r >= rows || c >= cols || board[r][c] !== word[i]) return false;
    const tmp = board[r][c];
    board[r][c] = '#'; // mark visited
    const found = dfs(r+1,c,i+1) || dfs(r-1,c,i+1) || dfs(r,c+1,i+1) || dfs(r,c-1,i+1);
    board[r][c] = tmp; // restore (backtrack)
    return found;
  }
  for (let r = 0; r < rows; r++)
    for (let c = 0; c < cols; c++)
      if (dfs(r, c, 0)) return true;
  return false;
}
// exist([["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], "ABCCED") -> true
```

**Complexity:** Time **O(rows·cols·4^L)**, Space **O(L)** recursion.

**💡 Interview tip:** Restoring the cell after recursion (backtracking) is essential so other paths can
reuse it.

---

### 15.7 N-Queens

**Problem:** Place `n` queens on an `n×n` board so none attack each other; return the number of distinct
solutions (or the boards).

**Company tags:** `Amazon` `Google` `Meta`

**Why this is a Backtracking problem:** Place queens row by row, pruning columns/diagonals already
attacked, backtracking on dead ends.

**Approach:** Track used columns and both diagonals (by `r+c` and `r-c`); recurse row by row.

```js
function totalNQueens(n) {
  let count = 0;
  const cols = new Set(), diag1 = new Set(), diag2 = new Set();
  function backtrack(row) {
    if (row === n) { count++; return; }
    for (let col = 0; col < n; col++) {
      if (cols.has(col) || diag1.has(row - col) || diag2.has(row + col)) continue;
      cols.add(col); diag1.add(row - col); diag2.add(row + col);
      backtrack(row + 1);
      cols.delete(col); diag1.delete(row - col); diag2.delete(row + col);
    }
  }
  backtrack(0);
  return count;
}
// totalNQueens(4) -> 2
```

**Complexity:** Time roughly **O(n!)**, Space **O(n)**.

**💡 Interview tip:** Representing diagonals as `row−col` and `row+col` makes attack checks O(1) — the
elegant detail interviewers look for.

---

## 16. Dynamic Programming

### 16.1 Climbing Stairs

**Problem:** Climb 1 or 2 steps at a time; count the ways to reach step `n`.

**Company tags:** `Amazon` `Microsoft` `Adobe` `Goldman Sachs`

**Why this is a DP problem:** `ways(n) = ways(n-1) + ways(n-2)` — overlapping subproblems (Fibonacci).

**Approach:** Iterate keeping only the last two values.

```js
function climbStairs(n) {
  if (n <= 2) return n;
  let a = 1, b = 2;
  for (let i = 3; i <= n; i++) { [a, b] = [b, a + b]; }
  return b;
}
// climbStairs(5) -> 8
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Show the progression: naive recursion O(2ⁿ) → memo O(n) → rolling O(1) space.

---

### 16.2 House Robber

**Problem:** Maximize the sum from non-adjacent houses (can't rob two in a row).

**Company tags:** `Amazon` `Microsoft` `Google`

**Why this is a DP problem:** `best(i) = max(best(i-1), best(i-2) + nums[i])` — optimal substructure with
overlapping subproblems.

**Approach:** Track the best including vs. excluding the current house with two rolling variables.

```js
function rob(nums) {
  let prev = 0, curr = 0;
  for (const num of nums) {
    const temp = Math.max(curr, prev + num);
    prev = curr;
    curr = temp;
  }
  return curr;
}
// rob([2,7,9,3,1]) -> 12
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Follow-ups: houses in a circle (House Robber II) and a binary tree (House Robber III) —
note they reuse this recurrence.

---

### 16.3 Coin Change (Minimum Coins)

**Problem:** Fewest coins to make an amount (unlimited coins), or -1.

**Company tags:** `Amazon` `Google` `Microsoft` `Uber` `Bloomberg`

**Why this is a DP problem:** `min(amount)` depends on `min(amount - coin)`; greedy fails for arbitrary
denominations.

**Approach:** Bottom-up table; `dp[a] = min over coins of dp[a-coin] + 1`.

```js
function coinChange(coins, amount) {
  const dp = new Array(amount + 1).fill(Infinity);
  dp[0] = 0;
  for (let a = 1; a <= amount; a++)
    for (const coin of coins)
      if (coin <= a) dp[a] = Math.min(dp[a], dp[a - coin] + 1);
  return dp[amount] === Infinity ? -1 : dp[amount];
}
// coinChange([1,2,5], 11) -> 3
```

**Complexity:** Time **O(amount·coins)**, Space **O(amount)**.

**💡 Interview tip:** Explain *why greedy fails* (coins `[1,3,4]`, amount 6 → greedy 4+1+1, optimal 3+3).

---

### 16.4 Longest Common Subsequence

**Problem:** Length of the longest common subsequence of two strings.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Goldman Sachs`

**Why this is a DP problem:** Prefix answers depend on smaller prefixes — a 2D overlapping subproblem grid.

**Approach:** `dp[i][j] = dp[i-1][j-1]+1` if chars match, else `max(dp[i-1][j], dp[i][j-1])`.

```js
function longestCommonSubsequence(a, b) {
  const m = a.length, n = b.length;
  const dp = Array.from({ length: m + 1 }, () => new Array(n + 1).fill(0));
  for (let i = 1; i <= m; i++)
    for (let j = 1; j <= n; j++)
      dp[i][j] = a[i-1] === b[j-1] ? dp[i-1][j-1] + 1 : Math.max(dp[i-1][j], dp[i][j-1]);
  return dp[m][n];
}
// longestCommonSubsequence("abcde", "ace") -> 3
```

**Complexity:** Time **O(m·n)**, Space **O(m·n)** (reducible to O(n)).

**💡 Interview tip:** Offer the **O(n) space** optimization (keep only the previous row).

---

### 16.5 Longest Increasing Subsequence

**Problem:** Length of the longest strictly increasing subsequence.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta`

**Why this is a DP problem:** `dp[i]` (LIS ending at `i`) depends on all smaller `dp[j]` with `nums[j] <
nums[i]`.

**Approach (O(n log n)):** Maintain a `tails` array; binary-search the position to replace/extend.

```js
function lengthOfLIS(nums) {
  const tails = [];
  for (const num of nums) {
    let lo = 0, hi = tails.length;
    while (lo < hi) { const mid = (lo + hi) >> 1; tails[mid] < num ? lo = mid + 1 : hi = mid; }
    tails[lo] = num;            // replace or extend
    if (lo === tails.length) tails.push(num);
  }
  return tails.length;
}
// lengthOfLIS([10,9,2,5,3,7,101,18]) -> 4
```

**Complexity:** Time **O(n log n)**, Space **O(n)**.

**💡 Interview tip:** Start with the O(n²) DP, then upgrade to the patience-sorting O(n log n) — `tails`
isn't the LIS itself but its length is correct.

---

### 16.6 0/1 Knapsack

**Problem:** Given item weights/values and capacity `W`, maximize value without exceeding `W` (each item
used at most once).

**Company tags:** `Amazon` `Google` `Microsoft` `Flipkart`

**Why this is a DP problem:** Each item is an include/exclude choice with overlapping subproblems over
remaining capacity.

**Approach:** 1D DP over capacity, iterating capacity **backward** so each item is used once.

```js
function knapsack(weights, values, W) {
  const dp = new Array(W + 1).fill(0);
  for (let i = 0; i < weights.length; i++)
    for (let c = W; c >= weights[i]; c--)        // backward -> 0/1 (no reuse)
      dp[c] = Math.max(dp[c], dp[c - weights[i]] + values[i]);
  return dp[W];
}
// knapsack([1,3,4,5], [1,4,5,7], 7) -> 9
```

**Complexity:** Time **O(n·W)**, Space **O(W)**.

**💡 Interview tip:** Iterating capacity **backward** is the trick that prevents reusing an item — for the
unbounded variant, iterate forward.

---

### 16.7 Edit Distance

**Problem:** Minimum insert/delete/replace operations to convert one string into another.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta`

**Why this is a DP problem:** Transforming prefixes depends on smaller prefix transforms — a 2D grid of
subproblems.

**Approach:** `dp[i][j]` = edits for first `i`/`j` chars; if equal, carry diagonal; else 1 + min(insert,
delete, replace).

```js
function minDistance(word1, word2) {
  const m = word1.length, n = word2.length;
  const dp = Array.from({ length: m + 1 }, () => new Array(n + 1).fill(0));
  for (let i = 0; i <= m; i++) dp[i][0] = i;
  for (let j = 0; j <= n; j++) dp[0][j] = j;
  for (let i = 1; i <= m; i++)
    for (let j = 1; j <= n; j++)
      dp[i][j] = word1[i-1] === word2[j-1]
        ? dp[i-1][j-1]
        : 1 + Math.min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]);
  return dp[m][n];
}
// minDistance("horse", "ros") -> 3
```

**Complexity:** Time **O(m·n)**, Space **O(m·n)**.

**💡 Interview tip:** Map each `min` term to its operation (delete / insert / replace) when explaining — it
makes the recurrence click.

---

### 16.8 Word Break

**Problem:** Given a string and a dictionary, can the string be segmented into dictionary words?

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Bloomberg`

**Why this is a DP problem:** `canBreak(i)` depends on some `canBreak(j)` with `s[j..i]` a word — overlapping
subproblems.

**Approach:** `dp[i]` = is `s[0..i)` segmentable; `dp[i]` true if some `dp[j]` true and `s[j..i)` in the
dictionary.

```js
function wordBreak(s, wordDict) {
  const words = new Set(wordDict);
  const dp = new Array(s.length + 1).fill(false);
  dp[0] = true;
  for (let i = 1; i <= s.length; i++)
    for (let j = 0; j < i; j++)
      if (dp[j] && words.has(s.slice(j, i))) { dp[i] = true; break; }
  return dp[s.length];
}
// wordBreak("leetcode", ["leet","code"]) -> true
```

**Complexity:** Time **O(n²·L)** (substring/lookup), Space **O(n)**.

**💡 Interview tip:** `dp[0] = true` (empty prefix) seeds the recurrence. A Trie can speed up the inner
substring checks.

---


## 17. Greedy

### 17.1 Jump Game

**Problem:** Each element is the max jump length from that index. Can you reach the last index?

**Company tags:** `Amazon` `Google` `Microsoft` `Meta`

**Why this is a Greedy problem:** Track the farthest reachable index; a local "best reach" yields the global
answer.

**Approach:** Scan; if an index is beyond the current reach, fail; else extend the reach.

```js
function canJump(nums) {
  let reach = 0;
  for (let i = 0; i < nums.length; i++) {
    if (i > reach) return false;
    reach = Math.max(reach, i + nums[i]);
  }
  return true;
}
// canJump([2,3,1,1,4]) -> true ; canJump([3,2,1,0,4]) -> false
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Contrast with the O(n²) DP; tracking only the max reach is the greedy upgrade.

---

### 17.2 Jump Game II (Min Jumps)

**Problem:** Return the minimum number of jumps to reach the last index (assume reachable).

**Company tags:** `Amazon` `Google` `Meta`

**Why this is a Greedy problem:** A BFS-like greedy: within the current jump's reach, extend to the farthest
you can next, incrementing jumps at the boundary.

**Approach:** Track the current jump's end and the farthest reachable; bump jumps when you hit the boundary.

```js
function jump(nums) {
  let jumps = 0, currentEnd = 0, farthest = 0;
  for (let i = 0; i < nums.length - 1; i++) {
    farthest = Math.max(farthest, i + nums[i]);
    if (i === currentEnd) { jumps++; currentEnd = farthest; }
  }
  return jumps;
}
// jump([2,3,1,1,4]) -> 2
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Frame it as implicit BFS layers — each "jump" is a level. Stop before the last index to
avoid an extra count.

---

### 17.3 Gas Station

**Problem:** Given `gas[i]` and `cost[i]` around a circular route, return the start index to complete the
circuit, or -1.

**Company tags:** `Amazon` `Google` `Microsoft`

**Why this is a Greedy problem:** If total gas ≥ total cost a solution exists; the start is just after the
point where the running tank dips negative.

**Approach:** Track total and current tank; reset start when the tank goes negative.

```js
function canCompleteCircuit(gas, cost) {
  let total = 0, tank = 0, start = 0;
  for (let i = 0; i < gas.length; i++) {
    const diff = gas[i] - cost[i];
    total += diff;
    tank += diff;
    if (tank < 0) { start = i + 1; tank = 0; } // can't start before i+1
  }
  return total >= 0 ? start : -1;
}
// canCompleteCircuit([1,2,3,4,5], [3,4,5,1,2]) -> 3
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Two facts make it greedy: feasibility iff `sum(gas) >= sum(cost)`, and any prefix that
fails can't contain a valid start.

---

### 17.4 Task Scheduler

**Problem:** Given tasks and a cooldown `n` between identical tasks, return the minimum total time
(including idles).

**Company tags:** `Amazon` `Google` `Meta` `Microsoft`

**Why this is a Greedy problem:** Schedule the **most frequent** task first to minimize idle gaps — a greedy
arrangement around the busiest task.

**Approach:** Compute the frame from the max-frequency task; idle slots are filled by other tasks; answer is
`max(len, frameSize)`.

```js
function leastInterval(tasks, n) {
  const freq = new Array(26).fill(0);
  for (const t of tasks) freq[t.charCodeAt(0) - 65]++;
  const maxFreq = Math.max(...freq);
  const maxCount = freq.filter(f => f === maxFreq).length; // tasks sharing the max
  const frame = (maxFreq - 1) * (n + 1) + maxCount;
  return Math.max(tasks.length, frame);
}
// leastInterval(["A","A","A","B","B","B"], 2) -> 8
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** The frame formula is the elegant closed-form; a max-heap simulation is the alternative
if they want you to *show* the schedule.

---

### 17.5 Partition Labels

**Problem:** Partition a string into as many parts as possible so each letter appears in at most one part;
return the part sizes.

**Company tags:** `Amazon` `Google` `Meta`

**Why this is a Greedy problem:** Greedily extend the current partition to the last occurrence of any letter
seen so far; cut when the window closes.

**Approach:** Record each letter's last index; expand the partition end to the max last-index; cut at the
boundary.

```js
function partitionLabels(s) {
  const last = {};
  for (let i = 0; i < s.length; i++) last[s[i]] = i;
  const res = [];
  let start = 0, end = 0;
  for (let i = 0; i < s.length; i++) {
    end = Math.max(end, last[s[i]]);
    if (i === end) { res.push(end - start + 1); start = i + 1; }
  }
  return res;
}
// partitionLabels("ababcbacadefegdehijhklij") -> [9,7,8]
```

**Complexity:** Time **O(n)**, Space **O(1)** (bounded alphabet).

**💡 Interview tip:** Precomputing last occurrences then expanding the window is the clean two-pass greedy.

---

### 17.6 Assign Cookies

**Problem:** Each child has a greed factor; each cookie a size. Maximize the number of content children
(a child is content if cookie size ≥ greed).

**Company tags:** `Amazon` `Microsoft`

**Why this is a Greedy problem:** Sort both; give the smallest sufficient cookie to the least greedy child —
a greedy match.

**Approach:** Sort greed and sizes; two pointers assigning the smallest adequate cookie.

```js
function findContentChildren(g, s) {
  g.sort((a, b) => a - b);
  s.sort((a, b) => a - b);
  let child = 0, cookie = 0;
  while (child < g.length && cookie < s.length) {
    if (s[cookie] >= g[child]) child++; // satisfied
    cookie++;
  }
  return child;
}
// findContentChildren([1,2,3], [1,1]) -> 1
```

**Complexity:** Time **O(n log n)**, Space **O(1)**.

**💡 Interview tip:** Justify the greedy: using the smallest sufficient cookie never wastes a larger one
needed elsewhere.

---

## 18. Monotonic Stack

### 18.1 Next Greater Element

**Problem:** For each element, find the next greater element to its right (-1 if none).

**Company tags:** `Amazon` `Google` `Bloomberg`

**Why this is a Monotonic Stack problem:** A decreasing stack of indices "waits" for a larger value that
resolves them — the defining setup.

**Approach:** Iterate; while the current value exceeds the stack top, pop and record the answer.

```js
function nextGreaterElements(nums) {
  const res = new Array(nums.length).fill(-1);
  const stack = []; // indices, decreasing values
  for (let i = 0; i < nums.length; i++) {
    while (stack.length && nums[i] > nums[stack[stack.length - 1]]) {
      res[stack.pop()] = nums[i];
    }
    stack.push(i);
  }
  return res;
}
// nextGreaterElements([2,1,2,4,3]) -> [4,2,4,-1,-1]
```

**Complexity:** Time **O(n)**, Space **O(n)**.

**💡 Interview tip:** Each index is pushed/popped once → O(n), versus O(n²) brute force.

---

### 18.2 Daily Temperatures

**Problem:** For each day, how many days until a warmer temperature (0 if none).

**Company tags:** `Amazon` `Google` `Meta` `Bloomberg`

**Why this is a Monotonic Stack problem:** "Next greater" with index distances — a decreasing stack of
indices.

**Approach:** Pop colder days when a warmer day arrives, recording the day gap.

```js
function dailyTemperatures(temps) {
  const res = new Array(temps.length).fill(0);
  const stack = [];
  for (let i = 0; i < temps.length; i++) {
    while (stack.length && temps[i] > temps[stack[stack.length - 1]]) {
      const prev = stack.pop();
      res[prev] = i - prev;
    }
    stack.push(i);
  }
  return res;
}
// dailyTemperatures([73,74,75,71,69,72,76,73]) -> [1,1,4,2,1,1,0,0]
```

**Complexity:** Time **O(n)**, Space **O(n)**.

**💡 Interview tip:** Store **indices** (not values) so you can compute the distance.

---

### 18.3 Next Greater Element II (Circular)

**Problem:** Like next-greater, but the array is circular (wraps around).

**Company tags:** `Amazon` `Google`

**Why this is a Monotonic Stack problem:** Same decreasing stack; simulate the wrap by iterating twice over
the indices.

**Approach:** Loop `2n` times using `i % n`; only push during the first pass conceptually (use modulo
indexing).

```js
function nextGreaterElementsCircular(nums) {
  const n = nums.length;
  const res = new Array(n).fill(-1);
  const stack = [];
  for (let i = 0; i < 2 * n; i++) {
    const num = nums[i % n];
    while (stack.length && num > nums[stack[stack.length - 1]]) {
      res[stack.pop()] = num;
    }
    if (i < n) stack.push(i);
  }
  return res;
}
// nextGreaterElementsCircular([1,2,1]) -> [2,-1,2]
```

**Complexity:** Time **O(n)**, Space **O(n)**.

**💡 Interview tip:** The `2n` loop with `% n` is the standard "circular array" trick — only push real
indices once.

---

### 18.4 Largest Rectangle in Histogram

**Problem:** Find the largest rectangle area in a histogram of bar heights.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Bloomberg`

**Why this is a Monotonic Stack problem:** For each bar we need the nearest shorter bars on both sides; an
increasing stack resolves them in one pass.

**Approach:** Increasing stack of indices; when a shorter bar appears, pop and compute area with the popped
height; a trailing sentinel flushes the stack.

```js
function largestRectangleArea(heights) {
  const stack = [];
  let maxArea = 0;
  const bars = [...heights, 0]; // sentinel flushes remaining bars
  for (let i = 0; i < bars.length; i++) {
    while (stack.length && bars[i] < bars[stack[stack.length - 1]]) {
      const h = bars[stack.pop()];
      const w = stack.length ? i - stack[stack.length - 1] - 1 : i;
      maxArea = Math.max(maxArea, h * w);
    }
    stack.push(i);
  }
  return maxArea;
}
// largestRectangleArea([2,1,5,6,2,3]) -> 10
```

**Complexity:** Time **O(n)**, Space **O(n)**.

**💡 Interview tip:** The sentinel `0` and width formula `i - newTop - 1` are the two details people miss —
explain with an example.

---

### 18.5 Trapping Rain Water

**Problem:** Given bar heights, compute how much rain water is trapped.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Bloomberg`

**Why this is a Monotonic Stack (or two-pointer) problem:** Water above a bar depends on the higher bars on
both sides; a decreasing stack pairs valleys with their bounding walls.

**Approach (two-pointer, optimal):** Move the side with the smaller wall inward, accumulating water from the
running max on that side.

```js
function trap(height) {
  let left = 0, right = height.length - 1;
  let leftMax = 0, rightMax = 0, water = 0;
  while (left < right) {
    if (height[left] < height[right]) {
      leftMax = Math.max(leftMax, height[left]);
      water += leftMax - height[left];
      left++;
    } else {
      rightMax = Math.max(rightMax, height[right]);
      water += rightMax - height[right];
      right--;
    }
  }
  return water;
}
// trap([0,1,0,2,1,0,1,3,2,1,2,1]) -> 6
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** The two-pointer version is O(1) space vs. the stack/prefix-array versions at O(n).
Justify moving the smaller side: that side's water is bounded by its own max.

---

### 18.6 Remove K Digits

**Problem:** Remove `k` digits from a number string to make the smallest possible number.

**Company tags:** `Amazon` `Google` `Bloomberg`

**Why this is a Monotonic Stack problem:** Greedily remove a digit when it's larger than the next — keeping
the stack increasing yields the smallest number.

**Approach:** Build an increasing stack, popping while the top exceeds the current digit and `k` remains;
trim leftover, strip leading zeros.

```js
function removeKdigits(num, k) {
  const stack = [];
  for (const d of num) {
    while (k > 0 && stack.length && stack[stack.length - 1] > d) { stack.pop(); k--; }
    stack.push(d);
  }
  while (k-- > 0) stack.pop();            // remove from the end if any left
  const res = stack.join("").replace(/^0+/, "");
  return res === "" ? "0" : res;
}
// removeKdigits("1432219", 3) -> "1219"
```

**Complexity:** Time **O(n)**, Space **O(n)**.

**💡 Interview tip:** Don't forget the leftover-`k` trim (already-increasing input) and leading-zero
stripping — common edge-case misses.

---

## 19. Prefix Sum

### 19.1 Subarray Sum Equals K

**Problem:** Count contiguous subarrays summing to `k` (values may be negative).

**Company tags:** `Amazon` `Google` `Meta` `Microsoft` `Bloomberg`

**Why this is a Prefix Sum problem:** A subarray sum = difference of two prefix sums; a frequency map of
prefix sums counts matches in one pass.

**Approach:** Running prefix sum + map of seen prefix-sum counts; add `count[prefix - k]` each step.

```js
function subarraySum(nums, k) {
  const seen = new Map([[0, 1]]);
  let sum = 0, count = 0;
  for (const num of nums) {
    sum += num;
    count += seen.get(sum - k) || 0;
    seen.set(sum, (seen.get(sum) || 0) + 1);
  }
  return count;
}
// subarraySum([1,1,1], 2) -> 2
```

**Complexity:** Time **O(n)**, Space **O(n)**.

**💡 Interview tip:** Explain why sliding window fails with negatives, and why `seen.set(0,1)` seeds
subarrays starting at index 0.

---

### 19.2 Product of Array Except Self

**Problem:** Return an array where each element is the product of all others, no division, O(n).

**Company tags:** `Amazon` `Google` `Meta` `Microsoft` `Apple`

**Why this is a Prefix Sum (prefix-product) problem:** Prefix products from the left and suffix products
from the right combine per index.

**Approach:** Fill with left products, then multiply by running right products.

```js
function productExceptSelf(nums) {
  const n = nums.length, res = new Array(n).fill(1);
  let left = 1;
  for (let i = 0; i < n; i++) { res[i] = left; left *= nums[i]; }
  let right = 1;
  for (let i = n - 1; i >= 0; i--) { res[i] *= right; right *= nums[i]; }
  return res;
}
// productExceptSelf([1,2,3,4]) -> [24,12,8,6]
```

**Complexity:** Time **O(n)**, Space **O(1)** extra.

**💡 Interview tip:** Division is banned to handle zeros and test the prefix/suffix idea; the output array
doubles as scratch space.

---

### 19.3 Range Sum Query (Immutable)

**Problem:** Given an immutable array, answer many `sumRange(i, j)` queries efficiently.

**Company tags:** `Amazon` `Google` `Microsoft`

**Why this is a Prefix Sum problem:** Precompute cumulative sums so each query is an O(1) difference.

**Approach:** Build `prefix[i] = sum of first i elements`; `sumRange(i,j) = prefix[j+1] - prefix[i]`.

```js
class NumArray {
  constructor(nums) {
    this.prefix = new Array(nums.length + 1).fill(0);
    for (let i = 0; i < nums.length; i++) this.prefix[i + 1] = this.prefix[i] + nums[i];
  }
  sumRange(i, j) {
    return this.prefix[j + 1] - this.prefix[i];
  }
}
// new NumArray([-2,0,3,-5,2,-1]).sumRange(0,2) -> 1
```

**Complexity:** Build **O(n)**, each query **O(1)**, Space **O(n)**.

**💡 Interview tip:** The size-`n+1` prefix array avoids special-casing `i = 0`. For *mutable* arrays,
mention a Fenwick/segment tree.

---

### 19.4 Find Pivot Index

**Problem:** Find the index where the sum of the left elements equals the sum of the right elements.

**Company tags:** `Amazon` `Google` `Microsoft`

**Why this is a Prefix Sum problem:** Left sum is a prefix; right sum = total − left − current — a single
pass with running sums.

**Approach:** Precompute total; iterate maintaining the left sum; check `left === total - left - nums[i]`.

```js
function pivotIndex(nums) {
  const total = nums.reduce((a, b) => a + b, 0);
  let left = 0;
  for (let i = 0; i < nums.length; i++) {
    if (left === total - left - nums[i]) return i;
    left += nums[i];
  }
  return -1;
}
// pivotIndex([1,7,3,6,5,6]) -> 3
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Expressing the right sum as `total - left - nums[i]` avoids a second prefix array.

---

### 19.5 Contiguous Array (Equal 0s and 1s)

**Problem:** Find the longest contiguous subarray with an equal number of 0s and 1s.

**Company tags:** `Amazon` `Google` `Meta`

**Why this is a Prefix Sum problem:** Treat 0 as −1; a subarray with equal counts has prefix-sum difference
0, so two equal prefix sums bound it.

**Approach:** Map each prefix sum to its first index; when a sum repeats, the span between is balanced.

```js
function findMaxLength(nums) {
  const firstIndex = new Map([[0, -1]]);
  let sum = 0, maxLen = 0;
  for (let i = 0; i < nums.length; i++) {
    sum += nums[i] === 1 ? 1 : -1;
    if (firstIndex.has(sum)) maxLen = Math.max(maxLen, i - firstIndex.get(sum));
    else firstIndex.set(sum, i);
  }
  return maxLen;
}
// findMaxLength([0,1,0]) -> 2
```

**Complexity:** Time **O(n)**, Space **O(n)**.

**💡 Interview tip:** The 0→−1 remap turning "equal counts" into "prefix sum 0" is the key trick; store the
**first** occurrence only.

---

### 19.6 Subarray Sums Divisible by K

**Problem:** Count contiguous subarrays whose sum is divisible by `k`.

**Company tags:** `Amazon` `Google` `Bloomberg`

**Why this is a Prefix Sum problem:** Two prefix sums with the same remainder mod `k` bound a divisible
subarray; count by remainder frequency.

**Approach:** Track prefix-sum remainders (normalized positive); add the count of each remainder seen.

```js
function subarraysDivByK(nums, k) {
  const count = new Map([[0, 1]]);
  let sum = 0, result = 0;
  for (const num of nums) {
    sum += num;
    let mod = ((sum % k) + k) % k;          // normalize negatives
    result += count.get(mod) || 0;
    count.set(mod, (count.get(mod) || 0) + 1);
  }
  return result;
}
// subarraysDivByK([4,5,0,-2,-3,1], 5) -> 7
```

**Complexity:** Time **O(n)**, Space **O(k)**.

**💡 Interview tip:** Normalizing the remainder (`((x%k)+k)%k`) is essential for negative sums in JS — a
common bug.

---

## 20. Trie

### 20.1 Implement a Trie

**Problem:** Implement `insert`, `search`, and `startsWith`.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Uber`

**Why this is a Trie problem:** Efficient prefix operations over a word set — each node is a character.

**Approach:** Nodes hold a children map and an `isEnd` flag; walk char by char.

```js
class TrieNode { constructor() { this.children = new Map(); this.isEnd = false; } }
class Trie {
  constructor() { this.root = new TrieNode(); }
  insert(word) {
    let node = this.root;
    for (const ch of word) {
      if (!node.children.has(ch)) node.children.set(ch, new TrieNode());
      node = node.children.get(ch);
    }
    node.isEnd = true;
  }
  _walk(str) {
    let node = this.root;
    for (const ch of str) { if (!node.children.has(ch)) return null; node = node.children.get(ch); }
    return node;
  }
  search(word) { const n = this._walk(word); return !!n && n.isEnd; }
  startsWith(prefix) { return this._walk(prefix) !== null; }
}
```

**Complexity:** Each op **O(L)**, Space **O(total chars)**.

**💡 Interview tip:** `search` needs `isEnd`; `startsWith` just needs the path. A trie beats a hash set when
prefix queries matter.

---

### 20.2 Add and Search Word (Wildcard)

**Problem:** Support `addWord` and `search`, where `search` may contain `.` matching any single character.

**Company tags:** `Amazon` `Google` `Meta` `Bloomberg`

**Why this is a Trie problem:** A trie with DFS handles wildcards by branching into all children on `.`.

**Approach:** Insert normally; for search, DFS the trie, trying all children when the char is `.`.

```js
class WordDictionary {
  constructor() { this.root = new TrieNode(); }
  addWord(word) {
    let node = this.root;
    for (const ch of word) {
      if (!node.children.has(ch)) node.children.set(ch, new TrieNode());
      node = node.children.get(ch);
    }
    node.isEnd = true;
  }
  search(word) {
    const dfs = (node, i) => {
      if (i === word.length) return node.isEnd;
      const ch = word[i];
      if (ch === '.') {
        for (const child of node.children.values()) if (dfs(child, i + 1)) return true;
        return false;
      }
      return node.children.has(ch) && dfs(node.children.get(ch), i + 1);
    };
    return dfs(this.root, 0);
  }
}
```

**Complexity:** add **O(L)**; search **O(L)** typical, up to **O(26^L)** with many wildcards. Space **O(total
chars)**.

**💡 Interview tip:** The `.` case is exactly why a trie + DFS beats a flat hash map — you can branch
mid-word.

---

### 20.3 Word Search II

**Problem:** Given a board and a list of words, return all words found on the board (adjacent cells, no
reuse).

**Company tags:** `Amazon` `Google` `Microsoft` `Meta`

**Why this is a Trie problem:** Build a trie of the words so a single DFS over the board can match **all**
words simultaneously, pruning dead prefixes.

**Approach:** Insert words into a trie; DFS each cell following trie edges; collect words at `isEnd` nodes.

```js
function findWords(board, words) {
  const root = new TrieNode();
  for (const w of words) {
    let node = root;
    for (const ch of w) {
      if (!node.children.has(ch)) node.children.set(ch, new TrieNode());
      node = node.children.get(ch);
    }
    node.word = w; // store the full word at the end
  }
  const rows = board.length, cols = board[0].length, res = [];
  function dfs(r, c, node) {
    if (r < 0 || c < 0 || r >= rows || c >= cols) return;
    const ch = board[r][c];
    if (ch === '#' || !node.children.has(ch)) return;
    const next = node.children.get(ch);
    if (next.word) { res.push(next.word); next.word = null; } // avoid duplicates
    board[r][c] = '#';
    dfs(r+1,c,next); dfs(r-1,c,next); dfs(r,c+1,next); dfs(r,c-1,next);
    board[r][c] = ch;
  }
  for (let r = 0; r < rows; r++) for (let c = 0; c < cols; c++) dfs(r, c, root);
  return res;
}
```

**Complexity:** Time ~**O(rows·cols·4^L)** worst case, Space **O(total chars)**.

**💡 Interview tip:** Searching each word separately is wasteful; the trie lets one board traversal match all
words and prune branches early.

---

### 20.4 Replace Words

**Problem:** Given dictionary roots and a sentence, replace each word with the shortest root that is its
prefix.

**Company tags:** `Amazon` `Google`

**Why this is a Trie problem:** Finding the shortest matching prefix per word is a natural trie walk.

**Approach:** Insert roots into a trie; for each word, walk until an `isEnd` (shortest root) or mismatch.

```js
function replaceWords(dictionary, sentence) {
  const root = new TrieNode();
  for (const w of dictionary) {
    let node = root;
    for (const ch of w) {
      if (!node.children.has(ch)) node.children.set(ch, new TrieNode());
      node = node.children.get(ch);
    }
    node.isEnd = true;
  }
  const shortestRoot = (word) => {
    let node = root, prefix = "";
    for (const ch of word) {
      if (!node.children.has(ch)) return word;
      prefix += ch;
      node = node.children.get(ch);
      if (node.isEnd) return prefix;
    }
    return word;
  };
  return sentence.split(" ").map(shortestRoot).join(" ");
}
// replaceWords(["cat","bat","rat"], "the cattle was rattled by the battery")
//   -> "the cat was rat by the bat"
```

**Complexity:** Time **O(total chars)**, Space **O(total chars)**.

**💡 Interview tip:** Return at the **first** `isEnd` to guarantee the shortest root.

---

### 20.5 Longest Word in Dictionary

**Problem:** Find the longest word buildable one character at a time, where every prefix is also a word
(ties → lexicographically smallest).

**Company tags:** `Amazon` `Google`

**Why this is a Trie problem:** "Every prefix is also a word" is naturally checked by walking a trie where
each node along the path is an `isEnd`.

**Approach:** Insert all words; DFS only through nodes that are word-ends, tracking the longest/smallest.

```js
function longestWord(words) {
  const root = new TrieNode();
  for (const w of words) {
    let node = root;
    for (const ch of w) {
      if (!node.children.has(ch)) node.children.set(ch, new TrieNode());
      node = node.children.get(ch);
    }
    node.isEnd = true;
  }
  let best = "";
  function dfs(node, current) {
    if (current.length > best.length || (current.length === best.length && current < best)) {
      if (current !== "") best = current;
    }
    for (const [ch, child] of [...node.children.entries()].sort()) {
      if (child.isEnd) dfs(child, current + ch); // only continue through valid words
    }
  }
  dfs(root, "");
  return best;
}
// longestWord(["w","wo","wor","worl","world"]) -> "world"
```

**Complexity:** Time **O(total chars)**, Space **O(total chars)**.

**💡 Interview tip:** Only recurse into children that are themselves word-ends — that enforces the
"every prefix is a word" rule.

---

## 21. Union-Find

> A reusable Disjoint Set with path compression + union by rank:
>
> ```js
> class DSU {
>   constructor(n) { this.parent = Array.from({length: n}, (_, i) => i); this.rank = new Array(n).fill(0); }
>   find(x) { while (this.parent[x] !== x) { this.parent[x] = this.parent[this.parent[x]]; x = this.parent[x]; } return x; }
>   union(a, b) {
>     const ra = this.find(a), rb = this.find(b);
>     if (ra === rb) return false;
>     if (this.rank[ra] < this.rank[rb]) this.parent[ra] = rb;
>     else if (this.rank[ra] > this.rank[rb]) this.parent[rb] = ra;
>     else { this.parent[rb] = ra; this.rank[ra]++; }
>     return true;
>   }
> }
> ```

### 21.1 Number of Connected Components

**Problem:** Count connected components in an undirected graph of `n` nodes with given edges.

**Company tags:** `Amazon` `Google` `Microsoft` `Uber`

**Why this is a Union-Find problem:** Grouping by connectivity with incremental unions is exactly DSU's job.

**Approach:** Start with `n` components; each successful union reduces the count.

```js
function countComponents(n, edges) {
  const dsu = new DSU(n);
  let components = n;
  for (const [a, b] of edges) if (dsu.union(a, b)) components--;
  return components;
}
// countComponents(5, [[0,1],[1,2],[3,4]]) -> 2
```

**Complexity:** Time **O(E·α(n))**, Space **O(n)**.

**💡 Interview tip:** DFS/BFS also works in O(V+E); DSU shines for dynamic edges or repeated connectivity
queries.

---

### 21.2 Redundant Connection

**Problem:** In a graph that was a tree plus one extra edge, return the edge that creates a cycle (the last
such one).

**Company tags:** `Amazon` `Google` `Microsoft`

**Why this is a Union-Find problem:** The first edge whose endpoints already share a root closes a cycle —
DSU detects it directly.

**Approach:** Union each edge; the edge where `union` fails (already connected) is the answer.

```js
function findRedundantConnection(edges) {
  const dsu = new DSU(edges.length + 1);
  for (const [a, b] of edges) if (!dsu.union(a, b)) return [a, b];
  return [];
}
// findRedundantConnection([[1,2],[1,3],[2,3]]) -> [2,3]
```

**Complexity:** Time **O(E·α(n))**, Space **O(n)**.

**💡 Interview tip:** `union` returning false (same root) is the cycle signal — clean and O(α).

---

### 21.3 Number of Provinces

**Problem:** Given an adjacency matrix of cities, count the provinces (connected groups).

**Company tags:** `Amazon` `Microsoft` `Google`

**Why this is a Union-Find problem:** It's connected components from a matrix — union connected pairs and
count roots.

**Approach:** Union `i`/`j` where `isConnected[i][j] === 1`; count distinct roots.

```js
function findCircleNum(isConnected) {
  const n = isConnected.length;
  const dsu = new DSU(n);
  let provinces = n;
  for (let i = 0; i < n; i++)
    for (let j = i + 1; j < n; j++)
      if (isConnected[i][j] === 1 && dsu.union(i, j)) provinces--;
  return provinces;
}
// findCircleNum([[1,1,0],[1,1,0],[0,0,1]]) -> 2
```

**Complexity:** Time **O(n²·α(n))**, Space **O(n)**.

**💡 Interview tip:** Only scan the upper triangle (`j > i`) — the matrix is symmetric.

---

### 21.4 Accounts Merge

**Problem:** Merge accounts that share any email (same person), returning each person's sorted emails with
their name.

**Company tags:** `Amazon` `Google` `Meta`

**Why this is a Union-Find problem:** Emails belonging to the same person form connected groups; union
emails that co-occur in an account.

**Approach:** Map emails to ids, union emails within each account, then group emails by root.

```js
function accountsMerge(accounts) {
  const emailToId = new Map(), emailToName = new Map();
  let id = 0;
  for (const [name, ...emails] of accounts)
    for (const email of emails) {
      if (!emailToId.has(email)) emailToId.set(email, id++);
      emailToName.set(email, name);
    }
  const dsu = new DSU(id);
  for (const [, ...emails] of accounts)
    for (let i = 1; i < emails.length; i++)
      dsu.union(emailToId.get(emails[0]), emailToId.get(emails[i]));

  const groups = new Map();
  for (const [email, eid] of emailToId) {
    const root = dsu.find(eid);
    if (!groups.has(root)) groups.set(root, []);
    groups.get(root).push(email);
  }
  const res = [];
  for (const emails of groups.values()) {
    emails.sort();
    res.push([emailToName.get(emails[0]), ...emails]);
  }
  return res;
}
```

**Complexity:** Time **O(N·α + N log N)** for sorting emails, Space **O(N)**.

**💡 Interview tip:** Union emails *within* each account (link the first to the rest); then bucket by root.
This is a great "DSU on strings" showcase.

---

### 21.5 Graph Valid Tree

**Problem:** Given `n` nodes and edges, determine if they form a valid tree (connected and acyclic).

**Company tags:** `Amazon` `Google` `Meta`

**Why this is a Union-Find problem:** A valid tree has exactly `n-1` edges and no cycle — DSU detects cycles
and unions count connectivity.

**Approach:** Require `edges.length === n-1`; union all edges, failing if any edge closes a cycle.

```js
function validTree(n, edges) {
  if (edges.length !== n - 1) return false; // tree must have exactly n-1 edges
  const dsu = new DSU(n);
  for (const [a, b] of edges) if (!dsu.union(a, b)) return false; // cycle
  return true;
}
// validTree(5, [[0,1],[0,2],[0,3],[1,4]]) -> true
```

**Complexity:** Time **O(E·α(n))**, Space **O(n)**.

**💡 Interview tip:** The `n-1` edge check plus "no cycle" together imply connectivity — a neat shortcut to
explain.

---

## 22. Bitwise XOR

### 22.1 Single Number

**Problem:** Every element appears twice except one; find it. O(n) time, O(1) space.

**Company tags:** `Amazon` `Microsoft` `Adobe` `Cisco`

**Why this is a Bitwise XOR problem:** XOR cancels equal pairs (`a^a=0`) and keeps the lone value (`a^0=a`).

**Approach:** XOR everything together.

```js
function singleNumber(nums) {
  let res = 0;
  for (const num of nums) res ^= num;
  return res;
}
// singleNumber([4,1,2,1,2]) -> 4
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** State the two XOR identities; a hash map works but uses O(n) space.

---

### 22.2 Single Number III (Two Uniques)

**Problem:** Exactly two elements appear once; all others twice. Return the two unique numbers.

**Company tags:** `Amazon` `Google` `Bloomberg`

**Why this is a Bitwise XOR problem:** XOR of all gives `a^b`; a set bit in it distinguishes `a` from `b`,
splitting the array into two XOR groups.

**Approach:** XOR all → `xorAll`; pick a set bit; partition by that bit and XOR each group.

```js
function singleNumberIII(nums) {
  let xorAll = 0;
  for (const num of nums) xorAll ^= num;
  const diffBit = xorAll & (-xorAll);  // lowest set bit
  let a = 0, b = 0;
  for (const num of nums) {
    if (num & diffBit) a ^= num;
    else b ^= num;
  }
  return [a, b];
}
// singleNumberIII([1,2,1,3,2,5]) -> [3,5] (order may vary)
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** `x & (-x)` isolating the lowest set bit is the elegant partition trick — explain why
that bit differs between `a` and `b`.

---

### 22.3 Missing Number (XOR)

**Problem:** Array of `n` distinct numbers from `0..n` with one missing; find it using XOR.

**Company tags:** `Amazon` `Microsoft`

**Why this is a Bitwise XOR problem:** XOR-ing all indices `0..n` with all values cancels present pairs,
leaving the missing number.

**Approach:** XOR all indices and values together.

```js
function missingNumber(nums) {
  let res = nums.length;
  for (let i = 0; i < nums.length; i++) res ^= i ^ nums[i];
  return res;
}
// missingNumber([3,0,1]) -> 2
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** XOR avoids the potential overflow of the sum formula in other languages — a nice point
to raise.

---

### 22.4 Find the Difference

**Problem:** String `t` is `s` shuffled with one extra character added. Find the extra character.

**Company tags:** `Amazon` `Google`

**Why this is a Bitwise XOR problem:** XOR all char codes of `s` and `t`; matching characters cancel,
leaving the added one.

**Approach:** XOR every char code in both strings; convert back to a character.

```js
function findTheDifference(s, t) {
  let code = 0;
  for (const ch of s) code ^= ch.charCodeAt(0);
  for (const ch of t) code ^= ch.charCodeAt(0);
  return String.fromCharCode(code);
}
// findTheDifference("abcd", "abcde") -> "e"
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** XOR over char codes generalizes the single-number idea to characters — mention the
frequency-count alternative.

---

### 22.5 Counting Bits

**Problem:** For every number `0..n`, return the count of set bits.

**Company tags:** `Amazon` `Google` `Microsoft`

**Why this is a Bitwise problem:** `bits[i] = bits[i >> 1] + (i & 1)` — a DP recurrence over bit shifts.

**Approach:** Build the table using the relation between `i` and `i/2`.

```js
function countBits(n) {
  const bits = new Array(n + 1).fill(0);
  for (let i = 1; i <= n; i++) bits[i] = bits[i >> 1] + (i & 1);
  return bits;
}
// countBits(5) -> [0,1,1,2,1,2]
```

**Complexity:** Time **O(n)**, Space **O(n)**.

**💡 Interview tip:** The `i >> 1` relation (dropping the last bit) turns an O(n·log n) popcount loop into
O(n) — a tidy bit-DP.

---

## Final Advice for the Interview

1. **Name the pattern first.** Use the clue words in [`dsa-pattern.md`](./dsa-pattern.md) before coding.
2. **Brute force → optimal.** State the naive idea and its complexity, then improve it out loud.
3. **Always give time & space complexity**, unprompted.
4. **Call out edge cases** — empty input, single element, duplicates, negatives, cycles, overflow.
5. **Mention the best alternative** even if you code the simpler one (Quickselect vs. heap, O(n) DP space
   reduction, two-pointer vs. stack for rain water).
6. **Dry-run a small example** to validate before declaring done.

### How many questions to practice per pattern
- ⭐⭐⭐⭐⭐ patterns (Sliding Window, Two Pointers, Tree BFS/DFS, Graph, Binary Search, Backtracking, DP,
  Top-K): aim for **8–10** each.
- ⭐⭐⭐⭐ patterns: **5–7** each.
- ⭐⭐⭐ patterns: **4–5** each.

---

*Contributions welcome. Add problems following the same structure: Problem → Company tags → Why this
pattern → Approach → Solution → Complexity → Interview tip.*
