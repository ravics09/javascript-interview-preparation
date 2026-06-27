# DSA Interview Problems by Pattern (JavaScript)

A companion to [`dsa-pattern.md`](./dsa-pattern.md). Where that file teaches you to *recognize* patterns,
this file gives you **worked interview problems** for each pattern — with full JavaScript solutions and
detailed reasoning.

Every problem follows the same structure:

- **Problem** — the question statement.
- **Company tags** — where this question has been commonly reported.
- **Why this is a `<pattern>` problem** — the signals that map it to the pattern.
- **Approach** — the idea, step by step.
- **Solution (JavaScript)** — clean, commented code.
- **Complexity** — time and space.
- **💡 Interview tip** — what the strongest answer looks like (what to say/do to stand out).

> **Note on company tags:** Tags are *indicative*, compiled from widely shared interview experiences. They
> mean "this kind of company asks this kind of question," not a guarantee.

## Table of Contents

1. [Sliding Window](#1-sliding-window)
2. [Two Pointers](#2-two-pointers)
3. [Fast & Slow Pointers](#3-fast--slow-pointers)
4. [Merge Intervals](#4-merge-intervals)
5. [Cyclic Sort](#5-cyclic-sort)
6. [In-place Linked List Reversal](#6-in-place-linked-list-reversal)
7. [Tree BFS](#7-tree-bfs)
8. [Tree DFS](#8-tree-dfs)
9. [Graph Traversal](#9-graph-traversal)
10. [Topological Sort](#10-topological-sort)
11. [Two Heaps](#11-two-heaps)
12. [Top-K Elements](#12-top-k-elements)
13. [K-way Merge](#13-k-way-merge)
14. [Modified Binary Search](#14-modified-binary-search)
15. [Subsets / Backtracking](#15-subsets--backtracking)
16. [Dynamic Programming](#16-dynamic-programming)
17. [Greedy](#17-greedy)
18. [Monotonic Stack](#18-monotonic-stack)
19. [Prefix Sum](#19-prefix-sum)
20. [Trie](#20-trie)
21. [Union-Find](#21-union-find)
22. [Bitwise XOR](#22-bitwise-xor)

---

## 1. Sliding Window

### 1.1 Maximum Sum Subarray of Size K

**Problem:** Given an array of positive integers and a number `k`, find the maximum sum of any contiguous
subarray of size `k`.

**Company tags:** `Amazon` `Microsoft` `Goldman Sachs`

**Why this is a Sliding Window problem:** It asks for an optimal value over a **contiguous, fixed-size**
range. Recomputing each window's sum is wasteful because adjacent windows overlap by `k-1` elements — the
hallmark signal for sliding window.

**Approach:**
1. Sum the first `k` elements to seed the window.
2. Slide the window one step at a time: add the incoming element, subtract the outgoing one.
3. Track the maximum window sum seen.

**Solution (JavaScript):**
```js
function maxSumSubarray(arr, k) {
  let windowSum = 0;
  let maxSum = 0;

  // Seed the first window
  for (let i = 0; i < k; i++) windowSum += arr[i];
  maxSum = windowSum;

  // Slide: add the new element, remove the one leaving the window
  for (let end = k; end < arr.length; end++) {
    windowSum += arr[end] - arr[end - k];
    maxSum = Math.max(maxSum, windowSum);
  }
  return maxSum;
}

// maxSumSubarray([2, 1, 5, 1, 3, 2], 3) -> 9  (subarray [5,1,3])
```

**Complexity:** Time **O(n)** — each element enters/leaves the window once. Space **O(1)**.

**💡 Interview tip:** Start by stating the brute force (O(n·k)), then improve to O(n) with the sliding
window. Mentioning the "add new − remove old" trick shows you understand *why* the window is efficient.

---

### 1.2 Longest Substring Without Repeating Characters

**Problem:** Given a string, find the length of the longest substring without repeating characters.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Adobe` `Bloomberg`

**Why this is a Sliding Window problem:** It asks for the **longest contiguous** substring satisfying a
constraint ("no repeats"). The window grows while valid and shrinks when the constraint breaks — a
**dynamic-size** sliding window.

**Approach:**
1. Expand the window by moving `end`, storing each char's latest index in a map.
2. If a char repeats inside the current window, jump `start` to just past its previous occurrence.
3. Track the max window length.

**Solution (JavaScript):**
```js
function lengthOfLongestSubstring(s) {
  const lastIndex = new Map();
  let start = 0;
  let maxLen = 0;

  for (let end = 0; end < s.length; end++) {
    const ch = s[end];
    // If we've seen ch within the current window, move start past it
    if (lastIndex.has(ch) && lastIndex.get(ch) >= start) {
      start = lastIndex.get(ch) + 1;
    }
    lastIndex.set(ch, end);
    maxLen = Math.max(maxLen, end - start + 1);
  }
  return maxLen;
}

// lengthOfLongestSubstring("abcabcbb") -> 3 ("abc")
```

**Complexity:** Time **O(n)** — single pass. Space **O(min(n, charset))** for the map.

**💡 Interview tip:** The subtlety is the `>= start` check — without it you'd wrongly move `start`
backward for characters that fell out of the window. Call this out explicitly.

---

### 1.3 Longest Substring with At Most K Distinct Characters

**Problem:** Given a string, find the length of the longest substring containing **at most `k` distinct**
characters.

**Company tags:** `Amazon` `Google` `Uber` `Facebook`

**Why this is a Sliding Window problem:** "Longest contiguous substring under a frequency constraint" =
variable-size sliding window with a frequency map that triggers shrinking when distinct count exceeds `k`.

**Approach:**
1. Expand `end`, incrementing the char's count in a map.
2. While the map has more than `k` keys, shrink from `start` and remove counts that hit zero.
3. Track the max valid window length.

**Solution (JavaScript):**
```js
function longestSubstringKDistinct(s, k) {
  if (k === 0) return 0;
  const freq = new Map();
  let start = 0;
  let maxLen = 0;

  for (let end = 0; end < s.length; end++) {
    freq.set(s[end], (freq.get(s[end]) || 0) + 1);

    while (freq.size > k) {
      const left = s[start];
      freq.set(left, freq.get(left) - 1);
      if (freq.get(left) === 0) freq.delete(left);
      start++;
    }
    maxLen = Math.max(maxLen, end - start + 1);
  }
  return maxLen;
}

// longestSubstringKDistinct("araaci", 2) -> 4 ("araa")
```

**Complexity:** Time **O(n)** — each char is added and removed at most once. Space **O(k)**.

**💡 Interview tip:** This is the *template* for many window problems ("at most K …"). Master it, then note
that "exactly K distinct" can be derived as `atMost(K) - atMost(K-1)`.

---

## 2. Two Pointers

### 2.1 Pair with Target Sum (Sorted Array)

**Problem:** Given a **sorted** array, find indices of two numbers that add up to a target.

**Company tags:** `Amazon` `Microsoft` `Adobe`

**Why this is a Two Pointers problem:** The array is **sorted**, so moving a pointer predictably increases
or decreases the sum — letting us converge on the answer in one pass instead of using nested loops.

**Approach:**
1. Put one pointer at the start, one at the end.
2. If the sum is too small, move `left` right; if too big, move `right` left; if equal, return.

**Solution (JavaScript):**
```js
function pairWithTargetSum(arr, target) {
  let left = 0;
  let right = arr.length - 1;

  while (left < right) {
    const sum = arr[left] + arr[right];
    if (sum === target) return [left, right];
    if (sum < target) left++;   // need a bigger sum
    else right--;               // need a smaller sum
  }
  return [-1, -1];
}

// pairWithTargetSum([1, 2, 3, 4, 6], 6) -> [1, 3]
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** If the array is **unsorted**, a hash map gives O(n) time without sorting — mention
both, and pick based on whether sorting is allowed / extra space is constrained.

---

### 2.2 Three Sum (Triplets That Sum to Zero)

**Problem:** Given an array, find all **unique** triplets `[a, b, c]` such that `a + b + c = 0`.

**Company tags:** `Amazon` `Google` `Meta` `Microsoft` `Bloomberg`

**Why this is a Two Pointers problem:** After sorting, fix one element and reduce the rest to a classic
**two-pointer pair search** on the remaining sorted subarray.

**Approach:**
1. Sort the array.
2. For each index `i`, run two pointers on `i+1..end` looking for `-arr[i]`.
3. Skip duplicates for both the fixed element and the moving pointers.

**Solution (JavaScript):**
```js
function threeSum(nums) {
  nums.sort((a, b) => a - b); // sorting is allowed; enables two-pointer + dedup
  const result = [];

  for (let i = 0; i < nums.length - 2; i++) {
    if (i > 0 && nums[i] === nums[i - 1]) continue; // skip duplicate anchors
    let left = i + 1;
    let right = nums.length - 1;

    while (left < right) {
      const sum = nums[i] + nums[left] + nums[right];
      if (sum === 0) {
        result.push([nums[i], nums[left], nums[right]]);
        while (left < right && nums[left] === nums[left + 1]) left++;   // skip dups
        while (left < right && nums[right] === nums[right - 1]) right--;
        left++;
        right--;
      } else if (sum < 0) {
        left++;
      } else {
        right--;
      }
    }
  }
  return result;
}

// threeSum([-1, 0, 1, 2, -1, -4]) -> [[-1, -1, 2], [-1, 0, 1]]
```

**Complexity:** Time **O(n²)** (sort O(n log n) + nested two-pointer O(n²)). Space **O(1)** or O(n)
depending on the sort.

**💡 Interview tip:** The bug interviewers look for is **duplicate handling**. Walk through your dedup
logic explicitly. Note the lower bound: 3Sum can't beat O(n²) in general.

---

### 2.3 Remove Duplicates from a Sorted Array (In Place)

**Problem:** Given a sorted array, remove duplicates in place so each element appears once; return the new
length.

**Company tags:** `Amazon` `Microsoft` `Adobe`

**Why this is a Two Pointers problem:** A **slow** pointer marks the position of the last unique element
while a **fast** pointer scans ahead — the same-direction two-pointer variant for in-place rewriting.

**Approach:**
1. `slow` starts at 0. Move `fast` from 1.
2. When `arr[fast]` differs from `arr[slow]`, advance `slow` and copy the new value.

**Solution (JavaScript):**
```js
function removeDuplicates(arr) {
  if (arr.length === 0) return 0;
  let slow = 0;
  for (let fast = 1; fast < arr.length; fast++) {
    if (arr[fast] !== arr[slow]) {
      slow++;
      arr[slow] = arr[fast];
    }
  }
  return slow + 1; // count of unique elements
}

// removeDuplicates([2, 3, 3, 3, 6, 9, 9]) -> 4, arr begins with [2, 3, 6, 9]
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Emphasize the **O(1) space, in-place** requirement — interviewers often reject
solutions that allocate a new array here.

---

## 3. Fast & Slow Pointers

### 3.1 Linked List Cycle Detection

**Problem:** Determine whether a singly linked list has a cycle.

**Company tags:** `Amazon` `Microsoft` `Meta` `Bloomberg`

**Why this is a Fast & Slow Pointers problem:** A fast pointer (2 steps) and a slow pointer (1 step) will
**meet inside a cycle** but never meet if the list ends — the canonical Floyd's algorithm signal.

**Approach:**
1. Move `slow` by 1 and `fast` by 2 each iteration.
2. If they ever point to the same node, there's a cycle; if `fast` hits null, there isn't.

**Solution (JavaScript):**
```js
function hasCycle(head) {
  let slow = head;
  let fast = head;

  while (fast && fast.next) {
    slow = slow.next;        // 1 step
    fast = fast.next.next;   // 2 steps
    if (slow === fast) return true; // pointers met -> cycle
  }
  return false;
}
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Contrast with the hash-set approach (O(n) space). The two-pointer method's **O(1)
space** is why it's preferred. Be ready for the follow-up: "find the cycle's start node" (reset one pointer
to head, then advance both by 1 until they meet).

---

### 3.2 Happy Number

**Problem:** A number is "happy" if repeatedly replacing it with the sum of the squares of its digits
eventually reaches 1. Numbers that loop forever are not happy. Determine if a number is happy.

**Company tags:** `Amazon` `Google` `Uber` `Twitter`

**Why this is a Fast & Slow Pointers problem:** The sequence of digit-square-sums either reaches 1 or
**enters a cycle**. Cycle detection without extra memory is exactly fast & slow pointers.

**Approach:**
1. `slow` advances one step (one transform), `fast` advances two.
2. If `fast` reaches 1, it's happy; if `slow === fast` (and not 1), there's a cycle → not happy.

**Solution (JavaScript):**
```js
function isHappy(n) {
  const squareDigits = (num) => {
    let sum = 0;
    while (num > 0) {
      const d = num % 10;
      sum += d * d;
      num = Math.floor(num / 10);
    }
    return sum;
  };

  let slow = n;
  let fast = n;
  do {
    slow = squareDigits(slow);
    fast = squareDigits(squareDigits(fast));
  } while (slow !== fast);

  return slow === 1;
}

// isHappy(19) -> true ; isHappy(2) -> false
```

**Complexity:** Time **O(log n)** per transform step, overall effectively **O(log n)**. Space **O(1)**.

**💡 Interview tip:** Many candidates use a `Set` to detect the loop (O(n) space). Showing the fast/slow
approach for **O(1) space** demonstrates pattern fluency.

---

## 4. Merge Intervals

### 4.1 Merge Overlapping Intervals

**Problem:** Given a list of intervals, merge all overlapping intervals.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Salesforce`

**Why this is a Merge Intervals problem:** It operates on `[start, end]` ranges and asks to combine
overlaps — the defining setup. Sorting by start makes overlaps adjacent.

**Approach:**
1. Sort intervals by start.
2. Iterate; if the current interval overlaps the last merged one (`current.start <= last.end`), extend the
   end; otherwise push it as new.

**Solution (JavaScript):**
```js
function mergeIntervals(intervals) {
  if (intervals.length <= 1) return intervals;
  intervals.sort((a, b) => a[0] - b[0]); // sort by start

  const merged = [intervals[0]];
  for (let i = 1; i < intervals.length; i++) {
    const last = merged[merged.length - 1];
    const curr = intervals[i];
    if (curr[0] <= last[1]) {
      last[1] = Math.max(last[1], curr[1]); // overlap -> extend
    } else {
      merged.push(curr);                    // disjoint -> add
    }
  }
  return merged;
}

// mergeIntervals([[1,3],[2,6],[8,10],[15,18]]) -> [[1,6],[8,10],[15,18]]
```

**Complexity:** Time **O(n log n)** (sorting dominates). Space **O(n)** for the output.

**💡 Interview tip:** Always state "sort by start first" — it's the key insight. Mention the `Math.max` for
the end, since a contained interval (`[2,6]` inside `[1,8]`) shouldn't shrink the merged end.

---

### 4.2 Minimum Meeting Rooms

**Problem:** Given meeting time intervals, find the minimum number of rooms required so no meetings
overlap in the same room.

**Company tags:** `Amazon` `Google` `Meta` `Uber` `Bloomberg`

**Why this is a Merge Intervals problem:** It's about **overlap counting** across intervals. The peak
number of simultaneous overlaps equals the rooms needed.

**Approach (sweep line):**
1. Separate and sort all start times and end times.
2. Sweep through starts; if a meeting starts before the earliest end, allocate a room; otherwise reuse one
   (advance the end pointer).
3. Track the peak concurrent rooms.

**Solution (JavaScript):**
```js
function minMeetingRooms(intervals) {
  if (intervals.length === 0) return 0;
  const starts = intervals.map((i) => i[0]).sort((a, b) => a - b);
  const ends = intervals.map((i) => i[1]).sort((a, b) => a - b);

  let rooms = 0, maxRooms = 0;
  let s = 0, e = 0;

  while (s < starts.length) {
    if (starts[s] < ends[e]) {
      rooms++;          // a meeting starts before the earliest one ends
      s++;
    } else {
      rooms--;          // a meeting ended; free a room
      e++;
    }
    maxRooms = Math.max(maxRooms, rooms);
  }
  return maxRooms;
}

// minMeetingRooms([[0,30],[5,10],[15,20]]) -> 2
```

**Complexity:** Time **O(n log n)**, Space **O(n)**.

**💡 Interview tip:** Two strong approaches exist — the sweep line above and a **min-heap of end times**.
Mention both; the heap version generalizes well if asked to also return *which* meetings share rooms.

---

## 5. Cyclic Sort

### 5.1 Find the Missing Number

**Problem:** Given an array of `n` distinct numbers taken from `0..n` (one is missing), find the missing
number.

**Company tags:** `Amazon` `Microsoft` `Adobe` `Apple`

**Why this is a Cyclic Sort problem:** Values map directly to indices in a bounded range `0..n`. Placing
each number at its index reveals the gap — the cyclic-sort hallmark.

**Approach:**
1. Place each number `v` at index `v` via swaps (skip `v === n`, which has no slot).
2. The first index whose value ≠ index is the missing number; if all match, it's `n`.

**Solution (JavaScript):**
```js
function findMissingNumber(nums) {
  let i = 0;
  const n = nums.length;
  while (i < n) {
    const correct = nums[i];
    if (nums[i] < n && nums[i] !== nums[correct]) {
      [nums[i], nums[correct]] = [nums[correct], nums[i]]; // place at its index
    } else {
      i++;
    }
  }
  for (let j = 0; j < n; j++) {
    if (nums[j] !== j) return j;
  }
  return n;
}

// findMissingNumber([4, 0, 3, 1]) -> 2
```

**Complexity:** Time **O(n)** (each number is placed at most once). Space **O(1)**.

**💡 Interview tip:** Interviewers also accept the **XOR** or **sum formula** (`n(n+1)/2 - sum`) solutions.
Mention cyclic sort generalizes better to "find all missing/duplicates" follow-ups where formulas don't.

---

### 5.2 Find All Duplicates in an Array

**Problem:** Given an array of `n` integers where each is in `1..n` and some appear twice, return all
elements that appear twice. Aim for O(n) time, O(1) extra space.

**Company tags:** `Amazon` `Google` `Microsoft`

**Why this is a Cyclic Sort problem:** Bounded range `1..n` mapping to indices — after cyclic placement,
any index holding a "wrong" value exposes a duplicate.

**Approach:**
1. Cyclically place each value `v` at index `v-1`.
2. Any index `i` where `nums[i] !== i+1` holds a duplicate (`nums[i]`).

**Solution (JavaScript):**
```js
function findAllDuplicates(nums) {
  let i = 0;
  while (i < nums.length) {
    const correct = nums[i] - 1;
    if (nums[i] !== nums[correct]) {
      [nums[i], nums[correct]] = [nums[correct], nums[i]];
    } else {
      i++;
    }
  }
  const duplicates = [];
  for (let j = 0; j < nums.length; j++) {
    if (nums[j] !== j + 1) duplicates.push(nums[j]);
  }
  return duplicates;
}

// findAllDuplicates([3, 4, 4, 5, 5]) -> [4, 5]
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** There's also a neat **index-negation** trick (mark `nums[abs(v)-1]` negative). Both
are valid; cyclic sort is easier to explain and extend.

---

## 6. In-place Linked List Reversal

### 6.1 Reverse a Linked List

**Problem:** Reverse a singly linked list and return the new head.

**Company tags:** `Amazon` `Microsoft` `Meta` `Google` `Adobe`

**Why this is an In-place Reversal problem:** You re-point each node's `next` to its predecessor using a
few pointers and **no extra data structure** — the defining technique.

**Approach:**
1. Track `prev` (initially null) and `curr` (head).
2. For each node, save `next`, point `curr.next` to `prev`, then advance `prev` and `curr`.

**Solution (JavaScript):**
```js
function reverseList(head) {
  let prev = null;
  let curr = head;
  while (curr) {
    const next = curr.next; // save the rest of the list
    curr.next = prev;       // reverse the link
    prev = curr;            // advance prev
    curr = next;            // advance curr
  }
  return prev; // new head
}
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Be ready to also give the **recursive** version, and to explain the pointer dance
clearly (the most common mistake is losing the rest of the list by not saving `next` first).

---

### 6.2 Reverse Nodes in K-Group

**Problem:** Reverse the nodes of a linked list `k` at a time and return the modified list. Nodes left over
(fewer than `k`) stay as-is.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Bloomberg`

**Why this is an In-place Reversal problem:** It's repeated **sub-list reversal** with careful re-linking
between groups — an advanced variant of the basic reversal.

**Approach:**
1. Check there are at least `k` nodes ahead; if not, stop.
2. Reverse the next `k` nodes in place, then connect the previous group's tail to the new sub-head and the
   current sub-tail to the remainder.

**Solution (JavaScript):**
```js
function reverseKGroup(head, k) {
  // Verify k nodes remain
  let node = head;
  for (let i = 0; i < k; i++) {
    if (!node) return head; // fewer than k -> leave as is
    node = node.next;
  }

  // Reverse first k nodes
  let prev = null;
  let curr = head;
  for (let i = 0; i < k; i++) {
    const next = curr.next;
    curr.next = prev;
    prev = curr;
    curr = next;
  }

  // head is now the tail of this group; connect to the recursively reversed rest
  head.next = reverseKGroup(curr, k);
  return prev; // new head of this group
}
```

**Complexity:** Time **O(n)** (each node reversed once). Space **O(n/k)** recursion stack (or O(1) with an
iterative version).

**💡 Interview tip:** Clarify the edge rule up front ("what about a leftover tail < k?"). Offer the
iterative O(1)-space version if they push on space.

---


## 7. Tree BFS

### 7.1 Binary Tree Level Order Traversal

**Problem:** Return the node values of a binary tree, grouped level by level (top to bottom).

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Flipkart`

**Why this is a Tree BFS problem:** "Level by level" output is the textbook signal for breadth-first
traversal using a queue.

**Approach:**
1. Enqueue the root.
2. For each level, record the current queue size, dequeue exactly that many nodes, collect their values,
   and enqueue their children.

**Solution (JavaScript):**
```js
function levelOrder(root) {
  const result = [];
  if (!root) return result;

  const queue = [root];
  while (queue.length) {
    const levelSize = queue.length;   // freeze the count for this level
    const level = [];
    for (let i = 0; i < levelSize; i++) {
      const node = queue.shift();
      level.push(node.val);
      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }
    result.push(level);
  }
  return result;
}
```

**Complexity:** Time **O(n)**, Space **O(n)** (queue can hold up to a full level).

**💡 Interview tip:** The key trick is snapshotting `levelSize` before the inner loop — that's what
separates levels. `shift()` is O(n); for large inputs mention using a head index or a real queue for true
O(1) dequeues.

---

### 7.2 Minimum Depth of a Binary Tree

**Problem:** Find the minimum depth — the number of nodes along the shortest path from root to the nearest
leaf.

**Company tags:** `Amazon` `Microsoft` `Facebook`

**Why this is a Tree BFS problem:** BFS reaches the **closest leaf first**, so we can return as soon as we
hit any leaf — more efficient than exploring the whole tree with DFS.

**Approach:**
1. BFS level by level, tracking depth.
2. The first node with no children encountered is the shallowest leaf — return its depth.

**Solution (JavaScript):**
```js
function minDepth(root) {
  if (!root) return 0;
  const queue = [{ node: root, depth: 1 }];
  while (queue.length) {
    const { node, depth } = queue.shift();
    if (!node.left && !node.right) return depth; // first leaf found
    if (node.left) queue.push({ node: node.left, depth: depth + 1 });
    if (node.right) queue.push({ node: node.right, depth: depth + 1 });
  }
  return 0;
}
```

**Complexity:** Time **O(n)** worst case, Space **O(n)**.

**💡 Interview tip:** Contrast with **max depth**, where DFS is natural. For *min* depth, BFS's early exit
is the differentiator — and a subtle DFS bug is treating a node with one child as a leaf.

---

## 8. Tree DFS

### 8.1 Path Sum (Root-to-Leaf)

**Problem:** Given a binary tree and a target, return true if there's a root-to-leaf path whose values sum
to the target.

**Company tags:** `Amazon` `Microsoft` `Meta` `Adobe`

**Why this is a Tree DFS problem:** It asks about a **vertical root-to-leaf path**, so we recurse downward
carrying the remaining sum — classic depth-first traversal.

**Approach:**
1. Subtract the node value from the target as you descend.
2. At a leaf, check whether the remaining target equals the leaf value.

**Solution (JavaScript):**
```js
function hasPathSum(root, target) {
  if (!root) return false;
  // Leaf node: does the path complete the target?
  if (!root.left && !root.right) return target === root.val;

  const remaining = target - root.val;
  return hasPathSum(root.left, remaining) || hasPathSum(root.right, remaining);
}
```

**Complexity:** Time **O(n)**, Space **O(h)** where `h` is tree height (recursion stack).

**💡 Interview tip:** Be precise about the **leaf condition** (both children null). A common bug allows
paths ending mid-tree. Mention space is O(h) — O(log n) balanced, O(n) skewed.

---

### 8.2 Diameter of a Binary Tree

**Problem:** Find the length (in edges) of the longest path between any two nodes. The path may or may not
pass through the root.

**Company tags:** `Amazon` `Google` `Meta` `Bloomberg`

**Why this is a Tree DFS problem:** The longest path through any node = left subtree height + right subtree
height. We need per-node heights computed bottom-up — a post-order DFS.

**Approach:**
1. Recurse to compute each subtree's height.
2. At each node, update a global max with `leftHeight + rightHeight`.

**Solution (JavaScript):**
```js
function diameterOfBinaryTree(root) {
  let diameter = 0;

  function height(node) {
    if (!node) return 0;
    const left = height(node.left);
    const right = height(node.right);
    diameter = Math.max(diameter, left + right); // path through this node
    return 1 + Math.max(left, right);            // height to parent
  }

  height(root);
  return diameter;
}
```

**Complexity:** Time **O(n)**, Space **O(h)**.

**💡 Interview tip:** The insight is computing height and updating the diameter **in the same pass**. A
naive solution recomputes height at every node → O(n²); calling that out shows optimization awareness.

---

## 9. Graph Traversal

### 9.1 Number of Islands

**Problem:** Given a 2D grid of `'1'` (land) and `'0'` (water), count the number of islands (connected
groups of land, 4-directionally).

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Uber` `Bloomberg`

**Why this is a Graph Traversal problem:** The grid is an implicit graph (each cell is a node, edges to its
4 neighbors). Counting connected components = traverse from each unvisited land cell and sink it.

**Approach:**
1. Scan each cell. On finding unvisited land, increment the count and flood-fill (DFS/BFS) all connected
   land, marking it visited.

**Solution (JavaScript):**
```js
function numIslands(grid) {
  if (!grid || grid.length === 0) return 0;
  const rows = grid.length, cols = grid[0].length;
  let count = 0;

  function dfs(r, c) {
    if (r < 0 || c < 0 || r >= rows || c >= cols || grid[r][c] === '0') return;
    grid[r][c] = '0';      // mark visited (sink the land)
    dfs(r + 1, c);
    dfs(r - 1, c);
    dfs(r, c + 1);
    dfs(r, c - 1);
  }

  for (let r = 0; r < rows; r++) {
    for (let c = 0; c < cols; c++) {
      if (grid[r][c] === '1') {
        count++;
        dfs(r, c);
      }
    }
  }
  return count;
}
```

**Complexity:** Time **O(rows × cols)** — each cell visited once. Space **O(rows × cols)** worst case
(recursion/stack).

**💡 Interview tip:** Ask whether mutating the input grid is allowed; if not, keep a separate `visited`
set. Mention BFS as an alternative to avoid deep recursion stack overflow on huge grids.

---

### 9.2 Clone Graph

**Problem:** Given a reference to a node in a connected undirected graph, return a deep copy of the graph.

**Company tags:** `Amazon` `Google` `Meta` `Microsoft` `Uber`

**Why this is a Graph Traversal problem:** You must visit every node and edge exactly once while avoiding
infinite loops on cycles — DFS/BFS with a visited map mapping originals to clones.

**Approach:**
1. Use a hash map `original → clone`.
2. DFS: clone the node if unseen, then recursively clone/link each neighbor.

**Solution (JavaScript):**
```js
function cloneGraph(node) {
  if (!node) return null;
  const cloned = new Map(); // original -> clone

  function dfs(curr) {
    if (cloned.has(curr)) return cloned.get(curr);
    const copy = { val: curr.val, neighbors: [] };
    cloned.set(curr, copy);               // record BEFORE recursing (handles cycles)
    for (const neighbor of curr.neighbors) {
      copy.neighbors.push(dfs(neighbor));
    }
    return copy;
  }

  return dfs(node);
}
```

**Complexity:** Time **O(V + E)**, Space **O(V)**.

**💡 Interview tip:** The crucial detail is registering the clone in the map **before** recursing into
neighbors — otherwise cycles cause infinite recursion. State this explicitly.

---

## 10. Topological Sort

### 10.1 Course Schedule (Can Finish All Courses?)

**Problem:** Given `numCourses` and prerequisite pairs `[a, b]` (take `b` before `a`), determine if you can
finish all courses (i.e., no cyclic dependency).

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Uber`

**Why this is a Topological Sort problem:** It's a **dependency ordering** question on a directed graph; a
valid topological order exists iff the graph is a DAG (no cycle).

**Approach (Kahn's BFS):**
1. Build an adjacency list and in-degree count.
2. Start from courses with in-degree 0; repeatedly remove them and decrement neighbors' in-degrees.
3. If all courses get processed, there's no cycle.

**Solution (JavaScript):**
```js
function canFinish(numCourses, prerequisites) {
  const adj = Array.from({ length: numCourses }, () => []);
  const inDegree = new Array(numCourses).fill(0);

  for (const [course, prereq] of prerequisites) {
    adj[prereq].push(course);
    inDegree[course]++;
  }

  const queue = [];
  for (let i = 0; i < numCourses; i++) {
    if (inDegree[i] === 0) queue.push(i);
  }

  let processed = 0;
  while (queue.length) {
    const node = queue.shift();
    processed++;
    for (const next of adj[node]) {
      if (--inDegree[next] === 0) queue.push(next);
    }
  }
  return processed === numCourses; // all processed -> no cycle
}

// canFinish(2, [[1,0]]) -> true ; canFinish(2, [[1,0],[0,1]]) -> false
```

**Complexity:** Time **O(V + E)**, Space **O(V + E)**.

**💡 Interview tip:** Mention both flavors: **Kahn's (BFS, in-degrees)** and **DFS with cycle detection**.
For the follow-up "return the order", Kahn's naturally yields it. State that a cycle = impossible ordering.

---

## 11. Two Heaps

### 11.1 Find Median from a Data Stream

**Problem:** Design a structure that supports adding numbers and returning the median of all numbers so
far, efficiently.

**Company tags:** `Amazon` `Google` `Microsoft` `Bloomberg`

**Why this is a Two Heaps problem:** The median depends on the **middle** of the data. Keeping the smaller
half in a max-heap and the larger half in a min-heap gives O(1) median and O(log n) inserts.

**Approach:**
1. `maxHeap` holds the smaller half; `minHeap` holds the larger half.
2. On insert, push to the appropriate heap and rebalance so sizes differ by at most 1.
3. Median = top of the larger heap, or the average of both tops.

**Solution (JavaScript):** *(using a minimal binary heap)*
```js
class Heap {
  constructor(compare) { this.data = []; this.compare = compare; }
  size() { return this.data.length; }
  peek() { return this.data[0]; }
  push(val) {
    this.data.push(val);
    let i = this.data.length - 1;
    while (i > 0) {
      const parent = (i - 1) >> 1;
      if (this.compare(this.data[i], this.data[parent]) >= 0) break;
      [this.data[i], this.data[parent]] = [this.data[parent], this.data[i]];
      i = parent;
    }
  }
  pop() {
    const top = this.data[0];
    const last = this.data.pop();
    if (this.data.length) {
      this.data[0] = last;
      let i = 0;
      const n = this.data.length;
      while (true) {
        let smallest = i, l = 2 * i + 1, r = 2 * i + 2;
        if (l < n && this.compare(this.data[l], this.data[smallest]) < 0) smallest = l;
        if (r < n && this.compare(this.data[r], this.data[smallest]) < 0) smallest = r;
        if (smallest === i) break;
        [this.data[i], this.data[smallest]] = [this.data[smallest], this.data[i]];
        i = smallest;
      }
    }
    return top;
  }
}

class MedianFinder {
  constructor() {
    this.maxHeap = new Heap((a, b) => b - a); // smaller half (max on top)
    this.minHeap = new Heap((a, b) => a - b); // larger half (min on top)
  }
  addNum(num) {
    this.maxHeap.push(num);
    this.minHeap.push(this.maxHeap.pop());     // balance values across heaps
    if (this.minHeap.size() > this.maxHeap.size()) {
      this.maxHeap.push(this.minHeap.pop());   // keep sizes balanced
    }
  }
  findMedian() {
    if (this.maxHeap.size() > this.minHeap.size()) return this.maxHeap.peek();
    return (this.maxHeap.peek() + this.minHeap.peek()) / 2;
  }
}
```

**Complexity:** `addNum` **O(log n)**, `findMedian` **O(1)**. Space **O(n)**.

**💡 Interview tip:** JavaScript has no built-in heap — mention this and either bring a small heap class
(as above) or state you'd use one. The rebalancing "push-then-transfer" trick keeps the two halves valid.

---

## 12. Top-K Elements

### 12.1 Kth Largest Element in an Array

**Problem:** Find the `k`th largest element in an unsorted array.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Bloomberg`

**Why this is a Top-K problem:** We want the K-th extreme element. A **min-heap of size K** tracks the K
largest seen, giving O(n log K) — better than fully sorting.

**Approach:**
1. Maintain a min-heap of size `k`.
2. Push each element; if the heap exceeds `k`, pop the smallest. The heap's top is the answer.

**Solution (JavaScript):** *(reusing the `Heap` class from 11.1)*
```js
function findKthLargest(nums, k) {
  const minHeap = new Heap((a, b) => a - b);
  for (const num of nums) {
    minHeap.push(num);
    if (minHeap.size() > k) minHeap.pop(); // drop the smallest -> keep top k
  }
  return minHeap.peek(); // smallest among the k largest = kth largest
}

// findKthLargest([3, 2, 1, 5, 6, 4], 2) -> 5
```

**Complexity:** Time **O(n log k)**, Space **O(k)**.

**💡 Interview tip:** Discuss the spectrum: sorting O(n log n), heap O(n log k), and **Quickselect** with an
average **O(n)**. The heap is the cleanest "good enough" answer; mention Quickselect if they want optimal
average time.

---

### 12.2 Top K Frequent Elements

**Problem:** Given an array, return the `k` most frequent elements.

**Company tags:** `Amazon` `Google` `Meta` `Uber` `Flipkart`

**Why this is a Top-K problem:** "Most frequent K" → count frequencies, then select the top K by
frequency, ideally without sorting everything.

**Approach:**
1. Build a frequency map.
2. Use **bucket sort by frequency** (index = frequency) for O(n), then read buckets from the top until you
   have K elements.

**Solution (JavaScript):**
```js
function topKFrequent(nums, k) {
  const freq = new Map();
  for (const num of nums) freq.set(num, (freq.get(num) || 0) + 1);

  // buckets[f] = list of numbers occurring exactly f times
  const buckets = Array.from({ length: nums.length + 1 }, () => []);
  for (const [num, count] of freq) buckets[count].push(num);

  const result = [];
  for (let f = buckets.length - 1; f >= 0 && result.length < k; f--) {
    for (const num of buckets[f]) {
      result.push(num);
      if (result.length === k) break;
    }
  }
  return result;
}

// topKFrequent([1,1,1,2,2,3], 2) -> [1, 2]
```

**Complexity:** Time **O(n)** (bucket sort), Space **O(n)**.

**💡 Interview tip:** Heap gives O(n log k); the **bucket-sort** trick achieves O(n) because frequencies are
bounded by `n`. Offering the O(n) solution stands out.

---

## 13. K-way Merge

### 13.1 Merge K Sorted Lists

**Problem:** Merge `k` sorted linked lists into one sorted list.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Bloomberg`

**Why this is a K-way Merge problem:** Multiple **already-sorted** sequences combined into one — a min-heap
over the current heads efficiently always picks the global minimum next.

**Approach:**
1. Push the head of each list into a min-heap keyed by node value.
2. Pop the smallest, append it to the result, and push that node's `next`.

**Solution (JavaScript):** *(reusing the `Heap` class from 11.1)*
```js
function mergeKLists(lists) {
  const minHeap = new Heap((a, b) => a.val - b.val);
  for (const node of lists) {
    if (node) minHeap.push(node);
  }

  const dummy = { val: 0, next: null };
  let tail = dummy;

  while (minHeap.size()) {
    const smallest = minHeap.pop();
    tail.next = smallest;
    tail = tail.next;
    if (smallest.next) minHeap.push(smallest.next);
  }
  return dummy.next;
}
```

**Complexity:** Time **O(N log k)** where N = total nodes. Space **O(k)** for the heap.

**💡 Interview tip:** Note the alternative **divide-and-conquer** merge (pair up lists, merge two at a
time), also O(N log k) but O(1) extra. The heap is the more intuitive explanation under time pressure.

---

## 14. Modified Binary Search

### 14.1 Search in Rotated Sorted Array

**Problem:** A sorted array is rotated at an unknown pivot. Find the index of a target, or -1. Expected
O(log n).

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Bloomberg` `Adobe`

**Why this is a Modified Binary Search problem:** Sorted-ish input + an O(log n) expectation. At each step
one half is still sorted, so we can decide which half to keep — a binary search variant.

**Approach:**
1. Compute `mid`. Determine which half is sorted (compare `arr[low]` with `arr[mid]`).
2. If the target lies within the sorted half's range, search there; otherwise search the other half.

**Solution (JavaScript):**
```js
function searchRotated(nums, target) {
  let low = 0, high = nums.length - 1;
  while (low <= high) {
    const mid = Math.floor((low + high) / 2);
    if (nums[mid] === target) return mid;

    if (nums[low] <= nums[mid]) {            // left half is sorted
      if (target >= nums[low] && target < nums[mid]) high = mid - 1;
      else low = mid + 1;
    } else {                                 // right half is sorted
      if (target > nums[mid] && target <= nums[high]) low = mid + 1;
      else high = mid - 1;
    }
  }
  return -1;
}

// searchRotated([4,5,6,7,0,1,2], 0) -> 4
```

**Complexity:** Time **O(log n)**, Space **O(1)**.

**💡 Interview tip:** The crux is "which half is sorted, and is the target in it?" Verbalize that invariant.
A follow-up adds duplicates, which degrades the worst case to O(n) — mention it.

---

### 14.2 Find First and Last Position of an Element

**Problem:** Given a sorted array, find the starting and ending index of a target. Return `[-1, -1]` if not
found. Expected O(log n).

**Company tags:** `Amazon` `Google` `Microsoft` `Adobe`

**Why this is a Modified Binary Search problem:** Locating **boundaries** of a value in sorted data is a
binary-search-for-the-edge variant (find leftmost and rightmost occurrence separately).

**Approach:**
1. Binary search biased left to find the first occurrence.
2. Binary search biased right to find the last occurrence.

**Solution (JavaScript):**
```js
function searchRange(nums, target) {
  const findBound = (isFirst) => {
    let low = 0, high = nums.length - 1, result = -1;
    while (low <= high) {
      const mid = Math.floor((low + high) / 2);
      if (nums[mid] === target) {
        result = mid;
        if (isFirst) high = mid - 1; // keep searching left
        else low = mid + 1;          // keep searching right
      } else if (nums[mid] < target) {
        low = mid + 1;
      } else {
        high = mid - 1;
      }
    }
    return result;
  };

  return [findBound(true), findBound(false)];
}

// searchRange([5,7,7,8,8,10], 8) -> [3, 4]
```

**Complexity:** Time **O(log n)** (two binary searches), Space **O(1)**.

**💡 Interview tip:** Emphasize that you **don't stop** on the first match — you keep narrowing toward the
boundary. This "find the edge" idea generalizes to many binary-search-on-boundary questions.

---


## 15. Subsets / Backtracking

### 15.1 Generate All Subsets (Power Set)

**Problem:** Given a set of distinct integers, return all possible subsets (the power set).

**Company tags:** `Amazon` `Google` `Meta` `Microsoft` `Adobe`

**Why this is a Backtracking problem:** We explore a decision tree — for each element, "include or exclude"
— building every combination. Generating *all* arrangements is the backtracking signal.

**Approach:**
1. Recurse with a `start` index and a `current` subset.
2. Record the current subset, then try adding each remaining element, recursing, and removing it (undo).

**Solution (JavaScript):**
```js
function subsets(nums) {
  const result = [];

  function backtrack(start, current) {
    result.push([...current]);          // every node is a valid subset
    for (let i = start; i < nums.length; i++) {
      current.push(nums[i]);            // choose
      backtrack(i + 1, current);        // explore
      current.pop();                    // un-choose (backtrack)
    }
  }

  backtrack(0, []);
  return result;
}

// subsets([1, 2, 3]) -> [[],[1],[1,2],[1,2,3],[1,3],[2],[2,3],[3]]
```

**Complexity:** Time **O(n · 2ⁿ)** (2ⁿ subsets, each up to length n to copy). Space **O(n)** recursion depth
(plus output).

**💡 Interview tip:** Stress the **choose → explore → un-choose** template — it transfers directly to
permutations, combinations, and combination-sum. Push `[...current]` (a copy), not the reference.

---

### 15.2 Permutations

**Problem:** Given an array of distinct integers, return all possible permutations.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Uber`

**Why this is a Backtracking problem:** All orderings = explore every position with every unused element,
backtracking after each placement.

**Approach:**
1. Track used elements (or swap in place).
2. Add an unused element, recurse, then remove it.

**Solution (JavaScript):**
```js
function permute(nums) {
  const result = [];
  const used = new Array(nums.length).fill(false);

  function backtrack(current) {
    if (current.length === nums.length) {
      result.push([...current]);
      return;
    }
    for (let i = 0; i < nums.length; i++) {
      if (used[i]) continue;
      used[i] = true;
      current.push(nums[i]);
      backtrack(current);
      current.pop();          // undo
      used[i] = false;        // undo
    }
  }

  backtrack([]);
  return result;
}

// permute([1, 2, 3]) -> 6 permutations
```

**Complexity:** Time **O(n · n!)**, Space **O(n)** recursion (plus output).

**💡 Interview tip:** Mention the **swap-based** variant (O(1) extra besides recursion). For inputs with
duplicates, sort first and skip equal siblings to avoid repeated permutations.

---

## 16. Dynamic Programming

### 16.1 Climbing Stairs (Intro DP)

**Problem:** You can climb 1 or 2 steps at a time. In how many distinct ways can you reach the top of `n`
stairs?

**Company tags:** `Amazon` `Microsoft` `Adobe` `Goldman Sachs`

**Why this is a DP problem:** `ways(n) = ways(n-1) + ways(n-2)` — overlapping subproblems with optimal
substructure (it's Fibonacci in disguise).

**Approach:**
1. Base cases: `ways(1)=1`, `ways(2)=2`.
2. Build up iteratively, keeping only the last two values (space-optimized).

**Solution (JavaScript):**
```js
function climbStairs(n) {
  if (n <= 2) return n;
  let oneStepBack = 2; // ways(2)
  let twoStepsBack = 1; // ways(1)
  for (let i = 3; i <= n; i++) {
    const current = oneStepBack + twoStepsBack;
    twoStepsBack = oneStepBack;
    oneStepBack = current;
  }
  return oneStepBack;
}

// climbStairs(5) -> 8
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Start from naive recursion (O(2ⁿ)), add memoization (O(n)), then the **rolling-variable
O(1) space** version. Showing that progression is exactly what interviewers want to see in DP.

---

### 16.2 Coin Change (Minimum Coins)

**Problem:** Given coin denominations and an amount, return the fewest coins needed to make the amount, or
-1 if impossible. Unlimited coins of each type.

**Company tags:** `Amazon` `Google` `Microsoft` `Uber` `Bloomberg`

**Why this is a DP problem:** `minCoins(amount)` depends on `minCoins(amount - coin)` for each coin —
overlapping subproblems; greedy fails for arbitrary denominations.

**Approach (bottom-up tabulation):**
1. `dp[a]` = fewest coins to make amount `a`; init to Infinity, `dp[0] = 0`.
2. For each amount, try each coin: `dp[a] = min(dp[a], dp[a-coin] + 1)`.

**Solution (JavaScript):**
```js
function coinChange(coins, amount) {
  const dp = new Array(amount + 1).fill(Infinity);
  dp[0] = 0;

  for (let a = 1; a <= amount; a++) {
    for (const coin of coins) {
      if (coin <= a) dp[a] = Math.min(dp[a], dp[a - coin] + 1);
    }
  }
  return dp[amount] === Infinity ? -1 : dp[amount];
}

// coinChange([1, 2, 5], 11) -> 3  (5 + 5 + 1)
```

**Complexity:** Time **O(amount × coins)**, Space **O(amount)**.

**💡 Interview tip:** Explicitly say **why greedy is wrong** here (e.g., coins `[1,3,4]`, amount `6` →
greedy gives `4+1+1`, optimal is `3+3`). That insight is often the real test.

---

### 16.3 Longest Common Subsequence

**Problem:** Given two strings, find the length of their longest common subsequence (not necessarily
contiguous).

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Goldman Sachs`

**Why this is a DP problem:** The answer for prefixes depends on smaller prefixes — a 2D overlapping
subproblem grid.

**Approach:**
1. `dp[i][j]` = LCS of `text1[0..i-1]` and `text2[0..j-1]`.
2. If characters match, `dp[i][j] = dp[i-1][j-1] + 1`; else `max(dp[i-1][j], dp[i][j-1])`.

**Solution (JavaScript):**
```js
function longestCommonSubsequence(text1, text2) {
  const m = text1.length, n = text2.length;
  const dp = Array.from({ length: m + 1 }, () => new Array(n + 1).fill(0));

  for (let i = 1; i <= m; i++) {
    for (let j = 1; j <= n; j++) {
      if (text1[i - 1] === text2[j - 1]) {
        dp[i][j] = dp[i - 1][j - 1] + 1;
      } else {
        dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
      }
    }
  }
  return dp[m][n];
}

// longestCommonSubsequence("abcde", "ace") -> 3
```

**Complexity:** Time **O(m × n)**, Space **O(m × n)** (reducible to O(min(m, n))).

**💡 Interview tip:** Draw the grid and explain the match vs. no-match transition. Mention you can **shrink
space to O(n)** by keeping only the previous row — a great optimization to offer.

---

## 17. Greedy

### 17.1 Jump Game (Can You Reach the End?)

**Problem:** Each element is the max jump length from that position. Determine if you can reach the last
index from the first.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta`

**Why this is a Greedy problem:** Track the **farthest reachable** index as you go; a local "best reach"
choice yields the global answer without exploring every path (which DP/brute force would).

**Approach:**
1. Maintain `maxReach`. For each index `i`, if `i > maxReach`, you're stuck → false.
2. Update `maxReach = max(maxReach, i + nums[i])`.

**Solution (JavaScript):**
```js
function canJump(nums) {
  let maxReach = 0;
  for (let i = 0; i < nums.length; i++) {
    if (i > maxReach) return false;          // can't even get to i
    maxReach = Math.max(maxReach, i + nums[i]);
    if (maxReach >= nums.length - 1) return true;
  }
  return true;
}

// canJump([2,3,1,1,4]) -> true ; canJump([3,2,1,0,4]) -> false
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** Contrast with the DP solution (O(n²)). The greedy "farthest reach" insight is the
upgrade interviewers reward — justify *why* tracking only the max reach is sufficient.

---

## 18. Monotonic Stack

### 18.1 Daily Temperatures

**Problem:** Given daily temperatures, return an array where each entry is how many days until a warmer
temperature (0 if none).

**Company tags:** `Amazon` `Google` `Meta` `Bloomberg`

**Why this is a Monotonic Stack problem:** "Next greater element" queries are solved by a **decreasing
stack** of indices waiting for a larger value — the defining use case.

**Approach:**
1. Keep a stack of indices with decreasing temperatures.
2. For each day, pop all colder days (resolve their wait), then push the current index.

**Solution (JavaScript):**
```js
function dailyTemperatures(temps) {
  const result = new Array(temps.length).fill(0);
  const stack = []; // indices of days awaiting a warmer day (decreasing temps)

  for (let i = 0; i < temps.length; i++) {
    while (stack.length && temps[i] > temps[stack[stack.length - 1]]) {
      const prev = stack.pop();
      result[prev] = i - prev; // days until warmer
    }
    stack.push(i);
  }
  return result;
}

// dailyTemperatures([73,74,75,71,69,72,76,73]) -> [1,1,4,2,1,1,0,0]
```

**Complexity:** Time **O(n)** — each index pushed/popped once. Space **O(n)**.

**💡 Interview tip:** Naively scanning forward for each day is O(n²). Explain why the monotonic stack
achieves O(n): every index is pushed and popped at most once.

---

### 18.2 Largest Rectangle in Histogram

**Problem:** Given bar heights of a histogram (width 1 each), find the area of the largest rectangle.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Bloomberg`

**Why this is a Monotonic Stack problem:** For each bar we need the nearest shorter bars on both sides — an
increasing stack resolves these boundaries in one pass.

**Approach:**
1. Maintain an increasing stack of indices.
2. When the current bar is shorter than the stack top, pop and compute the area with the popped bar as the
   limiting height; width is bounded by the new top and current index.

**Solution (JavaScript):**
```js
function largestRectangleArea(heights) {
  const stack = []; // increasing heights (store indices)
  let maxArea = 0;
  const bars = [...heights, 0]; // sentinel 0 flushes the stack at the end

  for (let i = 0; i < bars.length; i++) {
    while (stack.length && bars[i] < bars[stack[stack.length - 1]]) {
      const height = bars[stack.pop()];
      const width = stack.length ? i - stack[stack.length - 1] - 1 : i;
      maxArea = Math.max(maxArea, height * width);
    }
    stack.push(i);
  }
  return maxArea;
}

// largestRectangleArea([2,1,5,6,2,3]) -> 10
```

**Complexity:** Time **O(n)**, Space **O(n)**.

**💡 Interview tip:** The trailing **sentinel 0** is the elegant trick to flush remaining bars — mention it.
Width computation (`i - newTop - 1`) trips people up; explain it with a quick example.

---

## 19. Prefix Sum

### 19.1 Subarray Sum Equals K

**Problem:** Given an array and an integer `k`, count the number of contiguous subarrays summing to `k`
(values can be negative).

**Company tags:** `Amazon` `Google` `Meta` `Microsoft` `Bloomberg`

**Why this is a Prefix Sum problem:** A subarray sum = difference of two prefix sums. Storing prefix-sum
frequencies lets us count matches in one pass — sliding window fails with negatives.

**Approach:**
1. Track a running prefix sum and a map of `prefixSum → count`.
2. For each index, the number of subarrays ending here with sum `k` is `count[prefix - k]`.

**Solution (JavaScript):**
```js
function subarraySum(nums, k) {
  const prefixCount = new Map();
  prefixCount.set(0, 1); // empty prefix
  let sum = 0, count = 0;

  for (const num of nums) {
    sum += num;
    if (prefixCount.has(sum - k)) count += prefixCount.get(sum - k);
    prefixCount.set(sum, (prefixCount.get(sum) || 0) + 1);
  }
  return count;
}

// subarraySum([1, 1, 1], 2) -> 2
```

**Complexity:** Time **O(n)**, Space **O(n)**.

**💡 Interview tip:** Explicitly explain why **sliding window doesn't work** here (negatives break the
monotonic window assumption). The `prefixCount.set(0, 1)` seed handles subarrays starting at index 0 —
call it out.

---

### 19.2 Product of Array Except Self

**Problem:** Return an array where each element is the product of all others, **without division** and in
O(n).

**Company tags:** `Amazon` `Google` `Meta` `Microsoft` `Apple`

**Why this is a Prefix Sum (prefix-product) problem:** It's the multiplicative analog — prefix products
from the left and suffix products from the right combine to give each answer.

**Approach:**
1. First pass: fill `result[i]` with the product of everything to its left.
2. Second pass (right to left): multiply by the running product of everything to its right.

**Solution (JavaScript):**
```js
function productExceptSelf(nums) {
  const n = nums.length;
  const result = new Array(n).fill(1);

  let leftProduct = 1;
  for (let i = 0; i < n; i++) {
    result[i] = leftProduct;   // product of all elements left of i
    leftProduct *= nums[i];
  }

  let rightProduct = 1;
  for (let i = n - 1; i >= 0; i--) {
    result[i] *= rightProduct; // multiply by product of all to the right
    rightProduct *= nums[i];
  }
  return result;
}

// productExceptSelf([1, 2, 3, 4]) -> [24, 12, 8, 6]
```

**Complexity:** Time **O(n)**, Space **O(1)** extra (output array aside).

**💡 Interview tip:** Interviewers explicitly forbid division (to handle zeros and test the prefix/suffix
idea). Highlight that the output array doubles as scratch space → O(1) extra space.

---

## 20. Trie

### 20.1 Implement a Trie (Prefix Tree)

**Problem:** Implement a Trie with `insert(word)`, `search(word)`, and `startsWith(prefix)`.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Uber`

**Why this is a Trie problem:** Efficient **prefix** operations over a word set are exactly what a trie is
built for — each node is a character, paths are words.

**Approach:**
1. Each node holds a map of children and an `isEnd` flag.
2. Insert/search walk the tree character by character; `startsWith` is search without requiring `isEnd`.

**Solution (JavaScript):**
```js
class TrieNode {
  constructor() {
    this.children = new Map();
    this.isEnd = false;
  }
}

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

  _traverse(str) {
    let node = this.root;
    for (const ch of str) {
      if (!node.children.has(ch)) return null;
      node = node.children.get(ch);
    }
    return node;
  }

  search(word) {
    const node = this._traverse(word);
    return node !== null && node.isEnd;
  }

  startsWith(prefix) {
    return this._traverse(prefix) !== null;
  }
}
```

**Complexity:** Insert/search/startsWith all **O(L)** where L = word length. Space **O(total characters)**.

**💡 Interview tip:** Distinguish `search` (needs `isEnd`) from `startsWith` (just needs the path). A trie
beats a hash set when you need **prefix** queries; say so to justify the structure.

---

## 21. Union-Find

### 21.1 Number of Connected Components

**Problem:** Given `n` nodes labeled `0..n-1` and a list of undirected edges, count the connected
components.

**Company tags:** `Amazon` `Google` `Microsoft` `Uber`

**Why this is a Union-Find problem:** It's about **grouping by connectivity** with incremental unions —
exactly what Disjoint Set Union (with path compression + union by rank) is optimized for.

**Approach:**
1. Initialize each node as its own parent; component count = `n`.
2. For each edge, union the two endpoints; each successful union reduces the count by 1.

**Solution (JavaScript):**
```js
function countComponents(n, edges) {
  const parent = Array.from({ length: n }, (_, i) => i);
  const rank = new Array(n).fill(0);
  let components = n;

  function find(x) {
    while (parent[x] !== x) {
      parent[x] = parent[parent[x]]; // path compression
      x = parent[x];
    }
    return x;
  }

  function union(a, b) {
    const rootA = find(a), rootB = find(b);
    if (rootA === rootB) return false; // already connected
    // union by rank
    if (rank[rootA] < rank[rootB]) parent[rootA] = rootB;
    else if (rank[rootA] > rank[rootB]) parent[rootB] = rootA;
    else { parent[rootB] = rootA; rank[rootA]++; }
    return true;
  }

  for (const [a, b] of edges) {
    if (union(a, b)) components--;
  }
  return components;
}

// countComponents(5, [[0,1],[1,2],[3,4]]) -> 2
```

**Complexity:** Time **O(E · α(n))** (near-constant α, the inverse Ackermann). Space **O(n)**.

**💡 Interview tip:** Mention DFS/BFS also solves this in O(V+E); Union-Find shines when edges arrive
**dynamically** or you need repeated connectivity queries. Always include **path compression + union by
rank** — without them it degrades.

---

## 22. Bitwise XOR

### 22.1 Single Number

**Problem:** Every element appears twice except one. Find the single one in O(n) time and O(1) space.

**Company tags:** `Amazon` `Microsoft` `Adobe` `Cisco`

**Why this is a Bitwise XOR problem:** XOR cancels equal pairs (`a ^ a = 0`) and preserves the lone value
(`a ^ 0 = a`) — so XOR-ing everything leaves exactly the unique number.

**Approach:**
1. XOR all elements together; duplicates cancel, leaving the single number.

**Solution (JavaScript):**
```js
function singleNumber(nums) {
  let result = 0;
  for (const num of nums) {
    result ^= num; // pairs cancel out
  }
  return result;
}

// singleNumber([4, 1, 2, 1, 2]) -> 4
```

**Complexity:** Time **O(n)**, Space **O(1)**.

**💡 Interview tip:** A hash map also works but uses O(n) space. The XOR trick is the "wow" answer here —
state the two XOR identities that make it work. Follow-ups: "every element appears 3× except one" needs bit
counting instead.

---

## Final Advice for the Interview

1. **Identify the pattern first.** Use the clue words in [`dsa-pattern.md`](./dsa-pattern.md) to name the
   pattern before coding.
2. **State brute force → optimal.** Show the naive idea, its complexity, then improve it. This narrates
   your problem-solving.
3. **Always give time & space complexity** — unprompted. It signals seniority.
4. **Call out edge cases** — empty input, single element, duplicates, negatives, cycles.
5. **Mention the "best" alternative** even if you code the simpler one (e.g., Quickselect vs. heap, O(n)
   space reduction in DP). Interviewers reward knowing the trade-offs.
6. **Test your code** by dry-running a small example out loud.

---

*Contributions welcome. Add problems following the same structure: Problem → Company tags → Why this
pattern → Approach → Solution → Complexity → Interview tip.*
