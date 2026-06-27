# DSA Patterns for Coding Interviews (JavaScript)

A pattern-first guide to cracking Data Structures & Algorithms interviews. Instead of memorizing hundreds
of problems, learn the **~20 recurring patterns** — once you recognize the pattern behind a question, the
approach follows naturally.

Each pattern includes:

- **What it is** — the core idea.
- **When to use it** — the signals/clues in a problem statement that point to this pattern.
- **How to use it** — the general approach/steps to apply it.
- **Importance** — a ⭐ rating (out of 5) reflecting how frequently it appears in interviews.
- **Company tags** — where this pattern's questions are commonly reported.
- **Example questions** — representative problems (statements only — **no answers, no code**).

> **No solutions on purpose.** This file is a *recognition & strategy* reference. Try to map each example
> question to its pattern and solve it yourself.

> **Note on company tags & stars:** Both are *indicative*, compiled from widely shared interview
> experiences (Glassdoor, LeetCode discuss, blogs, Grokking-style pattern lists). Treat them as guidance,
> not guarantees.

---

## Importance & Difficulty Matrix

| # | Pattern | Importance | Typical Difficulty | Core Data Structure |
|---|---------|:----------:|:------------------:|---------------------|
| 1 | Sliding Window | ⭐⭐⭐⭐⭐ | Easy–Medium | Array / String |
| 2 | Two Pointers | ⭐⭐⭐⭐⭐ | Easy–Medium | Array / String |
| 3 | Fast & Slow Pointers | ⭐⭐⭐⭐ | Easy–Medium | Linked List / Array |
| 4 | Merge Intervals | ⭐⭐⭐⭐ | Medium | Array of intervals |
| 5 | Cyclic Sort | ⭐⭐⭐ | Easy–Medium | Array (bounded range) |
| 6 | In-place Linked List Reversal | ⭐⭐⭐⭐ | Easy–Medium | Linked List |
| 7 | Tree BFS | ⭐⭐⭐⭐⭐ | Easy–Medium | Tree / Queue |
| 8 | Tree DFS | ⭐⭐⭐⭐⭐ | Medium | Tree / Recursion |
| 9 | Graph Traversal (BFS/DFS) | ⭐⭐⭐⭐⭐ | Medium | Graph |
| 10 | Topological Sort | ⭐⭐⭐⭐ | Medium | Graph (DAG) |
| 11 | Two Heaps | ⭐⭐⭐ | Medium–Hard | Heap |
| 12 | Top-K Elements | ⭐⭐⭐⭐⭐ | Medium | Heap |
| 13 | K-way Merge | ⭐⭐⭐ | Medium | Heap |
| 14 | Modified Binary Search | ⭐⭐⭐⭐⭐ | Easy–Medium | Sorted Array |
| 15 | Subsets / Backtracking | ⭐⭐⭐⭐⭐ | Medium–Hard | Recursion |
| 16 | Dynamic Programming | ⭐⭐⭐⭐⭐ | Medium–Hard | Table / Memo |
| 17 | Greedy | ⭐⭐⭐⭐ | Medium | Varies |
| 18 | Monotonic Stack | ⭐⭐⭐⭐ | Medium | Stack |
| 19 | Prefix Sum | ⭐⭐⭐⭐ | Easy–Medium | Array / HashMap |
| 20 | Trie (Prefix Tree) | ⭐⭐⭐ | Medium | Trie |
| 21 | Union-Find (DSU) | ⭐⭐⭐ | Medium | Disjoint Set |
| 22 | Bitwise XOR | ⭐⭐⭐ | Easy–Medium | Bits |

---

## Pattern → "Clue Words" Recognition Matrix

Use this to quickly map a problem statement to a pattern based on the words/constraints it contains.

| If the problem mentions… | Likely pattern |
|--------------------------|----------------|
| "contiguous subarray / substring", "window of size k", "longest/shortest substring" | Sliding Window |
| "sorted array", "pair/triplet that sums to", "remove duplicates in place" | Two Pointers |
| "linked list cycle", "find middle", "happy number" | Fast & Slow Pointers |
| "overlapping intervals", "meeting rooms", "merge ranges" | Merge Intervals |
| "array of 1..n", "missing/duplicate number", numbers in a fixed range | Cyclic Sort |
| "reverse a linked list", "reverse every k nodes" | In-place LL Reversal |
| "level by level", "level order", "minimum depth" | Tree BFS |
| "root-to-leaf path", "path sum", "tree diameter" | Tree DFS |
| "connected components", "islands", "shortest path in grid" | Graph Traversal |
| "course schedule", "build order", "dependencies/ordering" | Topological Sort |
| "median of a stream", "balance two halves" | Two Heaps |
| "top/largest/smallest/most frequent K" | Top-K Elements |
| "merge K sorted lists/arrays" | K-way Merge |
| "sorted input + find target / boundary", O(log n) expected | Modified Binary Search |
| "all combinations/permutations/subsets", "generate all" | Subsets / Backtracking |
| "min/max ways", "can you reach", "optimal value", overlapping subproblems | Dynamic Programming |
| "max/min while making local choices", "intervals/jobs scheduling" | Greedy |
| "next greater/smaller element", "largest rectangle" | Monotonic Stack |
| "range sum queries", "subarray sum equals k" | Prefix Sum |
| "search words by prefix", "autocomplete", "dictionary" | Trie |
| "are these connected", "number of groups/components" | Union-Find |
| "single number", "find missing with XOR", bit manipulation | Bitwise XOR |

---

## 1. Sliding Window

**Importance:** ⭐⭐⭐⭐⭐

**What it is:** A technique for problems involving a **contiguous range (subarray/substring)** where you
maintain a "window" and slide it across the data, expanding/shrinking it instead of recomputing from
scratch.

**When to use it:**
- The problem asks for the longest/shortest/optimal **contiguous** subarray or substring.
- There's a constraint like "window of size k", "at most K distinct", or "sum/product condition".
- A brute-force solution would recompute overlapping ranges (O(n²) or worse).

**How to use it:**
- Use two pointers (`start`, `end`) to define the window bounds.
- Expand the window by moving `end`; when a condition breaks, shrink by moving `start`.
- Track the running result (sum, count, frequency map) incrementally as the window moves.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Uber` `Adobe` `Flipkart`

**Example questions (no solutions):**
- Find the maximum sum of any contiguous subarray of size `k`.
- Longest substring with no more than `K` distinct characters.
- Longest substring without repeating characters.
- Smallest subarray with a sum greater than or equal to a target.
- Find all anagrams of a pattern within a string.

---

## 2. Two Pointers

**Importance:** ⭐⭐⭐⭐⭐

**What it is:** Use **two indices** moving through the data (toward each other, or in the same direction)
to reduce nested loops to a single pass.

**When to use it:**
- The input is **sorted** (or can be sorted) and you're looking for pairs/triplets meeting a condition.
- You need to compare elements from **both ends**, or partition/remove in place.

**How to use it:**
- Place pointers at the two ends (or one slow + one fast in the same direction).
- Move them based on a comparison with the target/condition until they meet or cross.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Bloomberg` `Goldman Sachs`

**Example questions (no solutions):**
- Given a sorted array, find a pair that sums to a target.
- Three numbers that sum to zero (3Sum).
- Remove duplicates from a sorted array in place.
- Container that holds the most water.
- Squaring a sorted array (including negatives).

---

## 3. Fast & Slow Pointers (Floyd's Cycle Detection)

**Importance:** ⭐⭐⭐⭐

**What it is:** Two pointers moving at **different speeds** (one moves 1 step, the other 2). They're great
for cycle detection and finding midpoints.

**When to use it:**
- Working with **linked lists** and you suspect a cycle or need the middle node.
- Problems that can be modeled as a sequence that may loop (e.g., "happy number").

**How to use it:**
- Advance `slow` by 1 and `fast` by 2 each step.
- If they meet, there's a cycle; the meeting point helps find cycle start/length.

**Company tags:** `Amazon` `Microsoft` `Meta` `Adobe` `Bloomberg`

**Example questions (no solutions):**
- Detect whether a linked list has a cycle.
- Find the start node of a cycle in a linked list.
- Find the middle of a linked list.
- Determine if a number is a "happy number".
- Check if a linked list is a palindrome.

---

## 4. Merge Intervals

**Importance:** ⭐⭐⭐⭐

**What it is:** A set of techniques for dealing with **overlapping intervals** — merging, inserting, or
finding intersections.

**When to use it:**
- The input is a list of intervals `[start, end]`.
- You need to merge overlaps, find conflicts, or compute free/busy times.

**How to use it:**
- Sort intervals by start time.
- Iterate and compare each interval's start with the previous end to decide merge vs. add.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Uber` `Salesforce`

**Example questions (no solutions):**
- Merge all overlapping intervals.
- Insert a new interval into a sorted, non-overlapping list and merge if needed.
- Find the intersection of two interval lists.
- Minimum number of meeting rooms required.
- Determine if a person can attend all meetings.

---

## 5. Cyclic Sort

**Importance:** ⭐⭐⭐

**What it is:** An in-place technique for arrays containing numbers in a **known, bounded range** (e.g.,
`1..n`), placing each number at its correct index.

**When to use it:**
- The array holds numbers in a fixed range `1..n` (or `0..n`).
- You need to find missing, duplicate, or misplaced numbers — ideally in O(n) time, O(1) space.

**How to use it:**
- Walk the array; if `nums[i]` isn't at its correct index, swap it there.
- After placing everything, scan for indices whose value doesn't match.

**Company tags:** `Amazon` `Microsoft` `Adobe` `Apple`

**Example questions (no solutions):**
- Find the missing number in an array containing `0..n`.
- Find all numbers that are missing from `1..n`.
- Find the single duplicate number.
- Find all duplicates in the array.
- Find the first missing positive integer.

---

## 6. In-place Linked List Reversal

**Importance:** ⭐⭐⭐⭐

**What it is:** Reverse the direction of pointers in a linked list (whole list or a sub-section) **without
extra memory**.

**When to use it:**
- You must reverse a linked list or part of it.
- Extra space is restricted (O(1) required).

**How to use it:**
- Maintain `prev`, `current`, `next` pointers and re-link nodes one at a time as you traverse.

**Company tags:** `Amazon` `Microsoft` `Meta` `Adobe` `Google`

**Example questions (no solutions):**
- Reverse a singly linked list.
- Reverse a sub-list between positions `m` and `n`.
- Reverse nodes in groups of `k`.
- Rotate a linked list by `k` places.

---

## 7. Tree Breadth-First Search (BFS)

**Importance:** ⭐⭐⭐⭐⭐

**What it is:** **Level-by-level** traversal of a tree using a queue.

**When to use it:**
- The problem requires processing nodes **level by level** or the **shortest path/min depth**.
- Output is grouped by depth.

**How to use it:**
- Push the root into a queue; repeatedly dequeue all nodes of the current level, process them, and enqueue
  their children.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Uber` `Flipkart`

**Example questions (no solutions):**
- Level-order traversal of a binary tree.
- Zigzag (spiral) level-order traversal.
- Find the minimum depth of a binary tree.
- Connect level-order siblings (next right pointers).
- Right-side view of a binary tree.

---

## 8. Tree Depth-First Search (DFS)

**Importance:** ⭐⭐⭐⭐⭐

**What it is:** Explore as deep as possible along each branch (pre/in/post-order) before backtracking,
usually via recursion.

**When to use it:**
- The problem deals with **root-to-leaf paths**, subtree properties, or path sums.
- You need to compare/aggregate values along a vertical path.

**How to use it:**
- Recurse into children, passing down running state (sum, path) and combining results on the way back up.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Bloomberg` `Adobe`

**Example questions (no solutions):**
- Does a root-to-leaf path with a given sum exist?
- Find all root-to-leaf paths that sum to a target.
- Count paths that sum to a value (paths need not start at root).
- Diameter of a binary tree.
- Maximum path sum in a binary tree.

---

## 9. Graph Traversal (BFS / DFS)

**Importance:** ⭐⭐⭐⭐⭐

**What it is:** Systematically visit all vertices/edges of a graph using a queue (BFS) or stack/recursion
(DFS), tracking visited nodes.

**When to use it:**
- Data is modeled as a **graph or grid**: connectivity, components, reachability, or shortest path
  (unweighted) questions.

**How to use it:**
- Build an adjacency list (or treat the grid as a graph).
- Traverse from each unvisited node, marking visited to avoid revisits/cycles.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Uber` `Goldman Sachs`

**Example questions (no solutions):**
- Number of islands in a 2D grid.
- Clone a graph.
- Flood fill an image.
- Shortest path in a binary maze/matrix.
- Detect a cycle in an undirected/directed graph.

---

## 10. Topological Sort

**Importance:** ⭐⭐⭐⭐

**What it is:** A linear ordering of vertices in a **Directed Acyclic Graph (DAG)** so every edge `u → v`
has `u` before `v`.

**When to use it:**
- There are **dependencies/ordering** constraints ("must do X before Y").
- You need a valid build/execution order, or to detect impossible (cyclic) ordering.

**How to use it:**
- Compute in-degrees, start from zero-in-degree nodes (Kahn's BFS), and peel off nodes; or use DFS with a
  finish-time stack.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Uber`

**Example questions (no solutions):**
- Course schedule — can all courses be finished given prerequisites?
- Return a valid course order.
- Alien dictionary — derive character order from sorted words.
- Build/task scheduling with dependencies.

---

## 11. Two Heaps

**Importance:** ⭐⭐⭐

**What it is:** Maintain a **max-heap** and a **min-heap** together to track the smaller and larger halves
of a dataset.

**When to use it:**
- You need the **median** of a stream, or to repeatedly balance two halves of data.

**How to use it:**
- Keep the smaller half in a max-heap and the larger half in a min-heap; rebalance after each insert so
  sizes differ by at most one.

**Company tags:** `Amazon` `Google` `Microsoft` `Bloomberg`

**Example questions (no solutions):**
- Find the median from a continuous data stream.
- Sliding window median.
- Maximize capital with at most K projects (IPO-style).

---

## 12. Top-K Elements

**Importance:** ⭐⭐⭐⭐⭐

**What it is:** Use a heap (size K) to efficiently track the K largest/smallest/most-frequent elements.

**When to use it:**
- The problem asks for the **top/smallest/most frequent K** items.
- You want better than full-sort O(n log n) — a K-sized heap gives O(n log K).

**How to use it:**
- Push elements into a heap; when it exceeds size K, pop the extreme element so only the K best remain.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Uber` `Flipkart`

**Example questions (no solutions):**
- Find the Kth largest element in an array.
- Top K frequent elements/words.
- K closest points to the origin.
- Sort a nearly-sorted (K-sorted) array.
- K closest numbers to a target in a sorted array.

---

## 13. K-way Merge

**Importance:** ⭐⭐⭐

**What it is:** Merge **K sorted** lists/arrays into one sorted output efficiently using a min-heap.

**When to use it:**
- You have multiple already-sorted inputs to combine.

**How to use it:**
- Push the first element of each list into a min-heap; pop the smallest, output it, and push the next
  element from that list.

**Company tags:** `Amazon` `Google` `Microsoft` `Bloomberg`

**Example questions (no solutions):**
- Merge K sorted linked lists.
- Find the Kth smallest element in a sorted matrix.
- Smallest range covering elements from K lists.

---

## 14. Modified Binary Search

**Importance:** ⭐⭐⭐⭐⭐

**What it is:** Variations of binary search applied to **sorted (or partially sorted)** data, or on an
"answer space".

**When to use it:**
- Input is sorted/rotated, or the expected complexity is **O(log n)**.
- You can frame the question as "find the boundary/threshold" and binary-search the answer.

**How to use it:**
- Maintain `low`/`high`, compute `mid`, and discard half each step based on a condition.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Adobe` `Goldman Sachs`

**Example questions (no solutions):**
- Search in a rotated sorted array.
- Find the first and last position of a target.
- Find the peak element in a mountain array.
- Search in an array of unknown/infinite size.
- Minimum capacity to ship packages within D days (binary search on the answer).

---

## 15. Subsets / Backtracking

**Importance:** ⭐⭐⭐⭐⭐

**What it is:** Systematically build all candidate solutions, **abandoning** ("pruning") partial paths that
can't lead to a valid result.

**When to use it:**
- The problem asks to **generate all** combinations, permutations, subsets, or arrangements.
- You need to explore a decision tree under constraints.

**How to use it:**
- Make a choice, recurse, then **undo the choice** (backtrack) to try the next option; prune invalid
  branches early.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Uber` `Adobe`

**Example questions (no solutions):**
- Generate all subsets of a set.
- All permutations of an array.
- Combination sum.
- Letter combinations of a phone number.
- N-Queens placement; word search in a grid.

---

## 16. Dynamic Programming

**Importance:** ⭐⭐⭐⭐⭐

**What it is:** Break a problem into **overlapping subproblems**, solve each once, and reuse results
(memoization / tabulation) to build the final answer.

**When to use it:**
- The problem has **optimal substructure** and **overlapping subproblems**.
- It asks for "number of ways", "min/max cost", "can you reach", or "longest/largest …".

**How to use it:**
- Define the state and recurrence, choose top-down (memo) or bottom-up (table), and handle base cases.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Bloomberg` `Uber` `Adobe`

**Example questions (no solutions):**
- 0/1 Knapsack — maximize value within a weight limit.
- Longest common subsequence / longest increasing subsequence.
- Coin change — fewest coins to make an amount.
- Edit distance between two strings.
- House robber; climbing stairs; unique grid paths.

---

## 17. Greedy

**Importance:** ⭐⭐⭐⭐

**What it is:** Build a solution by always making the **locally optimal** choice, hoping it yields a global
optimum (works when the problem has the greedy-choice property).

**When to use it:**
- Local optimal choices provably lead to a global optimum (often interval/scheduling/allocation problems).

**How to use it:**
- Sort or prioritize by the greedy criterion, then iterate making the best immediate choice.

**Company tags:** `Amazon` `Google` `Microsoft` `Uber` `Flipkart`

**Example questions (no solutions):**
- Activity selection / non-overlapping intervals to remove.
- Jump game — can you reach the last index?
- Gas station — find a valid starting point.
- Assign cookies to children; task scheduler.

---

## 18. Monotonic Stack

**Importance:** ⭐⭐⭐⭐

**What it is:** A stack kept in increasing or decreasing order, used to find the **next/previous
greater/smaller** element efficiently.

**When to use it:**
- The problem asks for the nearest larger/smaller element, or spans bounded by such elements.

**How to use it:**
- Iterate while popping elements that violate the monotonic order, recording answers as you pop.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Bloomberg`

**Example questions (no solutions):**
- Next greater element for each item.
- Daily temperatures — days until a warmer day.
- Largest rectangle in a histogram.
- Trapping rain water.
- Stock span problem.

---

## 19. Prefix Sum

**Importance:** ⭐⭐⭐⭐

**What it is:** Precompute cumulative sums so any **range sum** can be answered in O(1); often combined
with a hash map for subarray-sum problems.

**When to use it:**
- Many **range-sum queries**, or "count/find subarrays with sum = K".

**How to use it:**
- Build a running-sum array (or a map of prefix-sum → count) and use differences to get range results.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Adobe`

**Example questions (no solutions):**
- Subarray sum equals K (count of subarrays).
- Range sum query — immutable.
- Find the pivot index of an array.
- Contiguous array with equal 0s and 1s.
- Product of array except self.

---

## 20. Trie (Prefix Tree)

**Importance:** ⭐⭐⭐

**What it is:** A tree where each node represents a character, enabling fast **prefix-based** lookups.

**When to use it:**
- You need **prefix search**, autocomplete, or to store/query a dictionary of words efficiently.

**How to use it:**
- Insert words character by character; traverse the same way for search/prefix queries.

**Company tags:** `Amazon` `Google` `Microsoft` `Meta` `Uber`

**Example questions (no solutions):**
- Implement a Trie with insert/search/startsWith.
- Word search II (find many words in a grid).
- Design an autocomplete / search suggestions system.
- Replace words with their shortest root.

---

## 21. Union-Find (Disjoint Set Union)

**Importance:** ⭐⭐⭐

**What it is:** A structure that tracks elements partitioned into disjoint sets, supporting near-constant
**union** and **find** operations (with path compression + union by rank).

**When to use it:**
- Questions about **connectivity**, grouping, or counting components — especially with dynamic unions.

**How to use it:**
- Maintain a parent array; `find` returns a set's representative, `union` merges two sets.

**Company tags:** `Amazon` `Google` `Microsoft` `Uber`

**Example questions (no solutions):**
- Number of connected components in a graph.
- Redundant connection (find the edge creating a cycle).
- Accounts merge.
- Number of provinces; friend circles.

---

## 22. Bitwise XOR

**Importance:** ⭐⭐⭐

**What it is:** Exploit XOR properties (`a ^ a = 0`, `a ^ 0 = a`) to solve problems with O(1) space.

**When to use it:**
- Finding a unique/missing element among duplicates, or manipulating bits directly.

**How to use it:**
- XOR all elements; pairs cancel out, leaving the unique value(s).

**Company tags:** `Amazon` `Microsoft` `Adobe` `Cisco`

**Example questions (no solutions):**
- Single number — every element appears twice except one.
- Find the two numbers that appear only once.
- Find the missing number using XOR.
- Count the number of set bits / flip to make equal.

---

## How to Use This Guide

1. **Read a problem statement and guess the pattern first** using the "Clue Words" matrix above.
2. **Drill by pattern, not randomly** — solve 5–8 problems per pattern to internalize the approach.
3. **Prioritize by stars** — start with the ⭐⭐⭐⭐⭐ patterns; they cover the majority of interviews.
4. **Explain the "when & how"** out loud — interviewers value recognizing the pattern as much as coding it.
5. **Then implement** — solve the example questions yourself (code intentionally omitted here).

---

*Contributions welcome. Add new patterns following the same format: What → When to use → How to use →
Importance (stars) → Company tags → Example questions (statements only, no solutions).*
