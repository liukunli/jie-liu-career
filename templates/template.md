# Algorithm Templates — Master Reference

High-level templates, core algorithms, and quick-reference tables for every pattern. Detailed per-problem walkthroughs and side-by-side comparisons live in each category's own file (e.g. `dynamic_programming.md`, `graph.md`). A complete index of all reference problems by category is appended at the end.

---

## Two Pointers  &nbsp;`two_pointers.md`

Two patterns — pick based on whether pointers converge or march together.

### Quick Reference Table

| # | Name | Description | Intuition | Time | Space | Key Implementation |
|---|---|---|---|---|---|---|
| 167 | Two Sum II | Sorted array. Find two numbers summing to target. Return 1-based indices. | Squeeze from both ends; each comparison tells you which side is wrong, so one move eliminates a whole row/column of pairs. | O(n) | O(1) | Standard |
| 15 | 3Sum | Find all unique triplets summing to 0. No duplicate triplets in output. | Pin one number, then it becomes Two Sum on the rest — turning a triple search into a sweep. | O(n^2) | O(1) excluding output (O(n) sort stack) | Standard |
| 18 | 4Sum | Find all unique quadruplets summing to target. | Pin two numbers, then the inner search is Two Sum — same idea as 3Sum with one more fixed level. | O(n^3) | O(1) excluding output (O(n) sort stack) | Standard |
| 11 | Container With Most Water | Given heights of vertical lines, find two lines forming the container with most water. | Width shrinks every step, so only a taller boundary can ever help; abandon the shorter wall. | O(n) | O(1) | Standard |
| 42 | Trapping Rain Water | Given elevation heights, compute total water trapped after rain. | Water level at a cell is set by the shorter side's tallest wall, so always process from the lower side where that max is already known. | O(n) | O(1) | Standard |
| 27 | Remove Element | Remove all occurrences of `val` in-place. Return new length. | The writer only advances on keepers, so it always points at the next free slot for a kept value. | O(n) | O(1) | Standard |
| 26 | Remove Duplicates from Sorted Array | Remove duplicates in-place so each element appears at most once. Return new length. | Since the array is sorted, comparing against the last written value is enough to drop every duplicate run. | O(n) | O(1) | Standard |
| 80 | Remove Duplicates from Sorted Array II | Each element may appear at most twice in-place. Return new length. | Looking two slots back lets at most two copies through before the third is rejected. | O(n) | O(1) | Standard |
| 283 | Move Zeroes | Move all zeroes to end while preserving relative order of non-zero elements. | Compact the non-zeros to the front in order, then pad the leftover tail with zeros. | O(n) | O(1) | Standard |
| 75 | Sort Colors | Sort array of 0s, 1s, 2s in-place without library sort. | A single scan grows a "small" region from the left and a "large" region from the right, leaving mids in the middle. | O(n) | O(1) | Standard |
| 1 | Two Sum | Given an integer array and a target sum, return the indices of two numbers that add up to target. Exactly one solution exists. | Trade space for time — remember every value you've passed so the complement is a single lookup. | O(n) | O(n) | Standard |
| 16 | 3Sum Closest | Find three integers whose sum is closest to target. Return that sum. | Same pin-and-sweep as 3Sum, but instead of matching exactly you keep the running closest. | O(n^2) | O(1) | Standard |
| 31 | Next Permutation | Rearrange the array to its lexicographically next greater permutation in-place. If none, sort ascending. | The longest decreasing suffix is already maximal; bump the digit just before it up to the smallest larger value, then reset the suffix to ascending. | O(n) | O(1) | Standard |
| 41 | First Missing Positive | Find the smallest missing positive integer in an unsorted array. O(n) time, O(1) space. | Use the array itself as a hash table keyed by value, then scan for the first slot holding the wrong number. | O(n) | O(1) | Standard |
| 48 | Rotate Image | Rotate an n×n matrix 90 degrees clockwise in-place. | Transposing flips across the main diagonal; reversing each row then completes the clockwise turn. | O(n^2) | O(1) | Standard |
| 54 | Spiral Matrix | Return all elements of an m×n matrix in spiral order. | Peel the matrix like an onion, one boundary layer per loop. | O(m*n) | O(1) excluding output | Standard |
| 73 | Set Matrix Zeroes | If any element is 0, set its entire row and column to 0, in-place. | Reuse the first row and column as the bookkeeping space so no extra arrays are needed. | O(m*n) | O(1) | Standard |
| 128 | Longest Consecutive Sequence | Find the length of the longest run of consecutive integers in an unsorted array. O(n). | Each sequence is counted exactly once by starting only at its smallest member. | O(n) | O(n) | Standard |
| 164 | Maximum Gap | Find the maximum gap between successive elements in the sorted form of an array. O(n). | With buckets sized at the minimum possible gap, the answer never lies inside a bucket, only between bucket boundaries. | O(n) | O(n) | Standard |
| 169 | Majority Element | Find the element appearing more than n/2 times. | Pairing off different elements cancels them out; the majority element always survives. | O(n) | O(1) | Standard |
| 189 | Rotate Array | Rotate the array right by k positions, in-place. | Two partial reversals after a full reversal place each block in its rotated position without extra space. | O(n) | O(1) | Standard |
| 217 | Contains Duplicate | Return true if any value appears at least twice. | A set rejects repeats, so the first failed insert proves a duplicate. | O(n) | O(n) | Standard |
| 220 | Contains Duplicate III | Are there indices i, j with `\|nums[i]-nums[j]\| <= valueDiff` and `\|i-j\| <= indexDiff`? | Same-bucket means automatically within range; neighbor buckets need an explicit check. Slide a window of size indexDiff. | O(n) | O(min(n, indexDiff)) | Standard |
| 229 | Majority Element II | Find all elements appearing more than n/3 times. | At most two elements can each occur more than a third of the time, so track two running candidates. | O(n) | O(1) | Standard |
| 238 | Product of Array Except Self | Return output where `output[i]` is the product of all elements except `nums[i]`. No division. | Each position's answer is everything to its left times everything to its right. | O(n) | O(1) excluding output | Standard |
| 259 | 3Sum Smaller | Count triplets with sum strictly less than target in a sorted array. | Once the largest partner works, every smaller partner does too, so count them in bulk. | O(n^2) | O(1) | bulk-count all valid j for this i |
| 280 | Wiggle Sort | Reorder in-place so `nums[0] <= nums[1] >= nums[2] <= nums[3]...` | A greedy local swap is always safe — it never breaks the pair you already fixed. | O(n) | O(1) | Standard |
| 289 | Game of Life | Simulate one Game of Life step, updating all cells simultaneously, in-place. | Pack the new state into a spare bit so neighbor counts still read the old state during the pass. | O(m*n) | O(1) | Standard |
| 303 | Range Sum Query - Immutable | Answer many range-sum queries on a static array efficiently. | A range sum is the difference of two prefix sums, so each query is O(1) after one build pass. | O(n) build, O(1) query | O(n) | Standard |
| 304 | Range Sum Query 2D - Immutable | Answer many 2D region-sum queries on a static matrix efficiently. | Each region sum combines four corner prefix sums via inclusion-exclusion. | O(m*n) build, O(1) query | O(m*n) | Standard |
| 307 | Range Sum Query - Mutable | Support range-sum queries and point updates. | A Fenwick tree stores partial sums over power-of-two ranges so updates and queries each touch only log n nodes. | O(log n) update/query | O(n) | Standard |
| 311 | Sparse Matrix Multiplication | Multiply two sparse matrices, skipping zero elements. | A zero in A contributes nothing, so skip it entirely instead of doing a full triple loop. | O(m*k*n) worst case | O(m*n) excluding output | skip zero to exploit sparsity |
| 315 | Count of Smaller Numbers After Self | For each element, count elements to its right that are smaller. O(n log n). | During a merge, every time a right element is taken before a left one, it is a smaller-to-the-right for that left element. | O(n log n) | O(n) | Standard |
| 325 | Maximum Size Subarray Sum Equals k | Find the longest subarray with sum equal to k. O(n). | A subarray sums to k exactly when two prefix sums differ by k; keep the earliest index to maximize length. | O(n) | O(n) | Standard |
| 327 | Count of Range Sum | Count range sums that lie in [lower, upper]. O(n log n). | A range sum is a difference of two prefix sums; merge sort lets you count qualifying pairs across halves efficiently. | O(n log n) | O(n) | Standard |
| 334 | Increasing Triplet Subsequence | Return true if there exists `i < j < k` with `nums[i] < nums[j] < nums[k]`. | Maintaining the two smallest ascending values seen so far is enough to detect a third larger one. | O(n) | O(1) | Standard |
| 349 | Intersection of Two Arrays | Return the intersection of two arrays (unique elements only). | Set membership turns intersection into linear lookups. | O(n + m) | O(n) | Standard |
| 350 | Intersection of Two Arrays II | Return the intersection including duplicates (multiplicity is the min of counts). | A frequency map lets each shared occurrence be matched at most once. | O(n + m) | O(min(n, m)) | Standard |
| 370 | Range Addition | Apply range updates `[start, end] += inc` then return the final array. | Mark only the endpoints of each update; a single prefix pass materializes all increments. | O(n + updates) | O(n) | Standard |
| 384 | Shuffle an Array | Return a uniformly random permutation of the array; support reset to original. | Choosing each position's element uniformly from the remaining ones yields every permutation with equal probability. | O(n) per shuffle | O(n) | Standard |
| 414 | Third Maximum Number | Return the third distinct maximum; if it doesn't exist, return the maximum. | Keep a sorted top-three as you scan, skipping duplicates. | O(n) | O(1) | Standard |
| 419 | Battleships in a Board | Count battleships ('X' runs, horizontal or vertical, never adjacent). | Each ship has exactly one cell with no ship-neighbor above or to its left, so count those. | O(m*n) | O(1) | Standard |
| 442 | Find All Duplicates in an Array | Values in [1,n], each appears once or twice. Return the ones appearing twice. O(n) time, O(1) extra space. | Flip the sign at each value's home index; encountering an already-negative slot means that value repeated. | O(n) | O(1) | Standard |
| 448 | Find All Numbers Disappeared in an Array | Values in [1,n]. Return all numbers in [1,n] missing from the array. | Use sign marking; any home index never marked means that number was absent. | O(n) | O(1) | Standard |
| 454 | 4Sum II | Count quadruplets (i,j,k,l) with `A[i]+B[j]+C[k]+D[l] == 0`. | Split four arrays into two pairs so a hash of one pair's sums turns the search into O(n^2) lookups. | O(n^2) | O(n^2) | Standard |
| 457 | Circular Array Loop | Detect a cycle of length > 1 with consistent direction in a circular array of jumps. | Fast/slow pointers detect cycles; reject single-element self-loops and direction flips. | O(n) | O(1) | Standard |
| 485 | Max Consecutive Ones | Find the maximum number of consecutive 1s in a binary array. | Grow a streak while seeing 1s and reset at each 0. | O(n) | O(1) | Standard |
| 493 | Reverse Pairs | Count pairs (i,j) with `i < j` and `nums[i] > 2 * nums[j]`. | Sorted halves let you count `nums[i] > 2*nums[j]` pairs with a linear two-pointer sweep per merge. | O(n log n) | O(n) | Standard |
| 498 | Diagonal Traverse | Traverse an m×n matrix diagonally, alternating direction each diagonal. | Cells on the same diagonal share `r+c`; flip the read direction on alternating diagonals to zig-zag. | O(m*n) | O(1) excluding output | Standard |
| 517 | Super Washing Machines | Minimize the max number of moves to equalize dresses across machines (one dress to a neighbor per move). | A bottleneck is either a machine with too much surplus or a cut that must pass a large net flow. | O(n) | O(1) | Standard |
| 523 | Continuous Subarray Sum | Is there a subarray of length >= 2 whose sum is a multiple of k? | Two prefix sums with the same remainder mod k bound a subarray sum divisible by k. | O(n) | O(min(n, k)) | Standard |
| 525 | Contiguous Array | Find the longest subarray with equal numbers of 0s and 1s. | Equal counts means a running balance returns to a value seen before. | O(n) | O(n) | Standard |
| 532 | K-diff Pairs in an Array | Count unique pairs (i,j) where `nums[i] - nums[j] == k` (k >= 0). | Counting distinct values avoids duplicate pairs; the zero-diff case needs a repeated value. | O(n) | O(n) | Standard |
| 560 | Subarray Sum Equals K | Count subarrays summing to exactly k. | Each earlier prefix equal to `s-k` marks the start of a qualifying subarray ending here. | O(n) | O(n) | Standard |
| 566 | Reshape the Matrix | Reshape an m×n matrix into r×c keeping row-major order; return original if sizes mismatch. | Both shapes share a linear index, so map between them with division and modulo. | O(m*n) | O(r*c) excluding output | Standard |
| 581 | Shortest Unsorted Continuous Subarray | Find the shortest subarray that, if sorted, makes the whole array sorted. | The window starts where an element exceeds some later minimum and ends where an element falls below some earlier maximum. | O(n) | O(1) | Standard |
| 594 | Longest Harmonious Subsequence | Find the longest subsequence where max and min differ by exactly 1. | A harmonious subsequence uses exactly two adjacent values, so combine each pair's counts. | O(n) | O(n) | Standard |
| 599 | Minimum Index Sum of Two Lists | Find common strings between two lists with minimum index sum. | Index sum is minimized greedily as you scan; ties are collected together. | O(n + m) | O(n) | Standard |
| 611 | Valid Triangle Number | Count triplets from an array of side lengths that form a valid triangle. | Only the two smaller sides need to beat the largest, so fix the largest and bulk-count valid pairs. | O(n^2) | O(1) | bulk-count valid i for this j |
| 661 | Image Smoother | Replace each cell with the floor of the average of itself and its up-to-8 neighbors. | Average over the in-bounds 3×3 window centered on each cell. | O(m*n) | O(m*n) excluding output | Standard |
| 723 | Candy Crush | Repeatedly crush horizontal/vertical runs of 3+ same-positive candies and apply gravity, until stable. | Mark all matches in one pass before clearing so simultaneous crushes are handled, then let candies fall. | O((m*n)^2) worst case | O(1) | Standard |
| 724 | Find Pivot Index | Find the leftmost index where the sum to its left equals the sum to its right. | Track a running left sum and derive the right sum from the precomputed total. | O(n) | O(1) | Standard |
| 766 | Toeplitz Matrix | Check if every top-left to bottom-right diagonal has a single value. | Comparing each cell to its diagonal predecessor verifies all diagonals locally. | O(m*n) | O(1) | Standard |
| 769 | Max Chunks To Make Sorted | Array is a permutation of [0,n-1]. Max number of chunks that can be sorted independently to sort the whole. | When the largest value seen so far equals the index, everything up to here is a self-contained block. | O(n) | O(1) | Standard |
| 795 | Number of Subarrays with Bounded Maximum | Count subarrays whose maximum lies in [left, right]. | "Max in range" equals the difference of two "max at most X" counts, each computed in one pass. | O(n) | O(1) | Standard |
| 807 | Max Increase to Keep City Skyline | Increase building heights as much as possible without changing skylines viewed from any of 4 sides. | A building is capped by the smaller of its row and column maxima to preserve both silhouettes. | O(n^2) | O(n) | Standard |
| 825 | Friends Of Appropriate Ages | Count friend requests; x friends y unless `age[y] <= 0.5*age[x]+7`, `age[y] > age[x]`, or `age[y]>100 && age[x]<100`. | Ages are bounded, so counting per age-bucket pair collapses the problem to constant-size work. | O(n + 120^2) | O(1) | Standard |
| 838 | Push Dominoes | Simulate falling dominoes given a string of 'L', 'R', '.'. | Each cell's outcome is the balance of forces from the nearest pushers on either side. | O(n) | O(n) | Standard |
| 845 | Longest Mountain in Array | Find the length of the longest mountain (strictly up then strictly down). | Scan to a peak by rising, then descend; the span counts only when both directions occurred. | O(n) | O(1) | Standard |
| 896 | Monotonic Array | Return true if the array is entirely non-increasing or entirely non-decreasing. | A single pass noting direction changes detects non-monotonicity. | O(n) | O(1) | Standard |
| 912 | Sort an Array | Sort an integer array. Implement an O(n log n) sort. | Recursively split, sort halves, and merge — stable O(n log n) without library sort. | O(n log n) | O(n) | Standard |
| 974 | Subarray Sums Divisible by K | Count subarrays whose sum is divisible by k. | Two prefixes with the same remainder mod k bound a divisible subarray; count pairs per remainder. | O(n) | O(k) | Standard |
| 977 | Squares of a Sorted Array | Return the squares of a sorted array in sorted order. | The biggest squares sit at the extremes, so fill the result from the largest slot inward. | O(n) | O(1) excluding output | Standard |
| 1013 | Partition Array Into Three Parts With Equal Sum | Can the array be split into three contiguous parts with equal sums? | Greedily close off a part each time the running sum hits one-third; succeed if at least three parts form. | O(n) | O(1) | Standard |
| 1074 | Number of Submatrices That Sum to Target | Count submatrices summing to target. | Reduce 2D to 1D by fixing the top and bottom rows, then count target-sum subarrays. | O(m^2 * n) | O(n) | Standard |
| 1109 | Corporate Flight Bookings | Given bookings `[first, last, seats]`, return total seats booked per flight. | Range increments become two endpoint marks resolved by one prefix pass. | O(n + bookings) | O(n) | Standard |
| 1213 | Intersection of Three Sorted Arrays | Return the common elements of three sorted arrays. | Like merging — advance whichever pointer lags so all three meet at shared values. | O(n) | O(1) excluding output | Standard |
| 1275 | Find Winner on a Tic Tac Toe Game | Given alternating A/B moves, determine the winner, "Draw", or "Pending". | Signed counts per line reveal a win the moment any line reaches +3 or -3. | O(1) | O(1) | Standard |
| 1351 | Count Negative Numbers in a Sorted Matrix | Count negatives in a matrix sorted descending by row and column. | From the bottom-left, sorted order lets each step rule out a whole row or column of negatives. | O(m + n) | O(1) | Standard |
| 1424 | Diagonal Traverse II | Traverse a jagged 2D list diagonally from bottom-left to top-right. | Cells on a diagonal share `r+c`; emitting rows in descending order gives the bottom-left-up direction. | O(total) | O(total) | Standard |
| 1460 | Make Two Arrays Equal by Reversing Sub-arrays | Can target become arr after reversing any sub-arrays any number of times? | Any permutation is reachable through reversals, so only element counts matter. | O(n) | O(1) | Standard |
| 1480 | Running Sum of 1d Array | Return the running (prefix) sum of the array. | Each running sum is the prior running sum plus the current value. | O(n) | O(1) | Standard |
| 1498 | Number of Subsequences That Satisfy the Given Sum Condition | Count subsequences where min + max <= target. Answer mod 1e9+7. | After sorting, fixing the minimum lets every subset of the elements up to the max be chosen freely. | O(n log n) | O(n) | Standard |
| 1748 | Sum of Unique Elements | Sum all elements that appear exactly once. | Count occurrences, then sum only the singletons. | O(n) | O(1) | Standard |
| 1762 | Buildings With an Ocean View | Return indices of buildings with nothing taller to their right (ocean to the right). | Sweeping from the ocean side, only record buildings that exceed every taller one already passed. | O(n) | O(1) excluding output | Standard |
| 1868 | Product of Two Run-Length Encoded Arrays | Multiply two run-length-encoded arrays element-wise; return the RLE product. | March through both run lists together, consuming the shorter overlap and coalescing equal results. | O(n + m) | O(1) excluding output | Standard |
| 1877 | Minimize Maximum Pair Sum in Array | Pair up elements to minimize the maximum pair sum. | Pairing extremes balances the sums, keeping the largest pair as small as possible. | O(n log n) | O(1) | Standard |
| 1893 | Check if All the Integers in a Range Are Covered | Are all integers in [left, right] covered by at least one given interval? | Mark interval starts and ends, then a prefix sweep shows which points are covered. | O(n + 50) | O(1) | Standard |
| 1894 | Find the Student that Will Replace the Chalk | Students consume chalk in order cyclically; find who runs out. | Whole cycles repeat, so only the remainder after a full round determines the failing student. | O(n) | O(1) | Standard |
| 1920 | Build Array from Permutation | Return `result[i] = nums[nums[i]]`. | Each output is a double lookup into the permutation. | O(n) | O(n) excluding output | Standard |
| 1929 | Concatenation of Array | Return `nums` concatenated with itself. | Copy each element into position `i` and `i+n`. | O(n) | O(1) excluding output | Standard |

---

### Pattern 1 — Opposite Two Pointers

```java
// MENTAL MODEL: two ends close in on the answer; each comparison rules out one whole end of the range.
// WHY sorted: moving inward only safely eliminates half the space if the array is sorted
int i = 0, j = n - 1;
while (i < j) {
    if (condition == target) {
        /* record */ i++; j--;
    } else if (tooSmall) {
        i++;
    } else {
        j--;
    }
}
```

Sort first. `i` and `j` converge inward. Used when the array is sorted and you can eliminate half the search space each step.

---

### Pattern 2 — Same Direction (Write Pointer)

```java
// MENTAL MODEL: a fast reader scans everything; a slow writer trails behind and only copies the keepers.
// WHEN: filter/compact an array in place, no extra buffer
int i = 0;                           // i = write position
for (int j = 0; j < n; j++) {       // j = read position
    if (keepCondition(nums[j]))
        nums[i++] = nums[j];
}
return i;
```

`i` marks where the next valid element goes. `j` scans every element. Only write when the element passes the keep condition.

The generalised duplicate-skip pattern for "at most k duplicates":

```java
int i = 0;
for (int j = 0; j < n; j++)
    if (i < k || nums[j] != nums[i - k])  // compare write head to k slots back
        nums[i++] = nums[j];
return i;
```

- k = 1 → #26 (no duplicates)
- k = 2 → #80 (at most 2)

---

### Pattern 3 — Dutch Flag (3 Pointers)

```java
// MENTAL MODEL: one scan partitions into three buckets (low / mid / high) using two boundary pointers.
// WHEN: 3-way partition — sort 0/1/2, segregate by a pivot category
int i = 0, k = 0, j = n - 1;
while (k <= j) {
    if (nums[k] == LO) {
        swap(nums, i++, k++);  // confirmed small
    } else if (nums[k] == MID) {
        k++;                   // confirmed mid, skip
    } else {
        swap(nums, k, j--);    // large — don't advance k
    }
}
```

Three regions: `[0, i)` = confirmed small, `[i, k)` = confirmed mid, `(j, n)` = confirmed large. `k` is the frontier.  
Do **not** increment `k` after swapping with `j` — the swapped element is unknown.

---

### Pattern Comparison

| Pattern | Pointers move | Sort needed | Use when |
|---|---|---|---|
| Opposite | `i` right, `j` left, converge | Yes (usually) | Sum/target problems on sorted array |
| Same direction | `j` scans, `i` writes | No | Filter / compact array in-place |
| Dutch Flag | `k` scans, `i` low boundary, `j` high boundary | No | 3-way partition (< / = / >) |

### Duplicate-skip Cheat Sheet (for Opposite pointers after a hit)

```java
// After recording a result at (i, j):
i++; j--;
while (i < j && nums[i] == nums[i - 1]) i++;  // skip duplicate i
while (i < j && nums[j] == nums[j + 1]) j--;  // skip duplicate j
```

Always check `i < j` inside the skip loop to avoid crossing.

---
## Sliding Window  &nbsp;`sliding_window.md`

Three variants — pick by what the problem asks for.  
`i` = left boundary (inclusive), `j` = right boundary (loop variable, inclusive).  
Window = `[i, j]`, size = `j - i + 1`.

---

### The Three Templates

```java
// FIXED window of size k — shrink exactly once when full
// MENTAL MODEL: a constant-width window slides one step at a time; add the new cell, drop the old one.
// WHEN: "subarray/substring of size k"
int i = 0;
for (int j = 0; j < n; j++) {
    // 1. add nums[j] to state
    if (j - i + 1 == k) {
        // 2. record (window is exactly size k)
        // 3. remove nums[i] from state
        i++;
    }
}

// MAX variable window — find LONGEST valid window
// MENTAL MODEL: grow greedily; shrink only enough to restore validity, then the window is the best ending here.
// WHEN: "longest" + "at most k ..."
int i = 0, result = 0;
for (int j = 0; j < n; j++) {
    // 1. add nums[j] to state
    while (/* window exceeds constraint */) {  // shrink WHILE window exceeds constraint
        // remove nums[i] from state
        i++;
    }
    result = Math.max(result, j - i + 1);   // record after window is valid
}

// MIN variable window — find SHORTEST valid window
// MENTAL MODEL: grow until valid, then shrink aggressively while still valid to find the tightest fit.
// WHEN: "shortest/minimum" + "sum >= target" / "contains all of t"
int i = 0, result = Integer.MAX_VALUE;
for (int j = 0; j < n; j++) {
    // 1. add nums[j] to state
    while (/* window VALID */) {                // record then shrink WHILE window still valid
        result = Math.min(result, j - i + 1);  // record while valid
        // remove nums[i] from state
        i++;                                    // then try to shrink
    }
}
```

---

### Quick Reference Table

| # | Name | Description | Intuition | Time | Space | Key Implementation |
|---|---|---|---|---|---|---|
| 643 | Maximum Average Subarray I | Find the contiguous subarray of length k with the maximum average value. | Max average of fixed length = max sum; slide a width-k window and track the best running sum. | O(n) | O(1) | Standard |
| 567 | Permutation in String | Return true if any permutation of s1 appears as a substring of s2. | A permutation is just a fixed-length window whose letter counts match s1, so slide and check the counts. | O(n) | O(1) | Standard |
| 219 | Contains Duplicate II | Return true if any two equal values are at most k indices apart. | Keep only the last k values in a set; a failed insert means a duplicate within k indices. | O(n) | O(k) | Standard |
| 239 | Sliding Window Maximum | Return the maximum of every contiguous subarray of size k. | A smaller value with a larger one still in the window can never be the max again, so discard it. | O(n) | O(k) | Standard |
| 1004 | Max Consecutive Ones III | Flip at most k zeros. Return the length of the longest subarray of 1s. | "Flip at most k zeros" = longest window containing at most k zeros; grow, and shrink only when zeros exceed k. | O(n) | O(1) | Standard |
| 3 | Longest Substring Without Repeating Characters | Find the length of the longest substring with all unique characters. | A repeat appears the moment you add it, so shrink from the left until that one character is unique again. | O(n) | O(1) | Standard |
| 424 | Longest Repeating Character Replacement | Replace at most k characters. Find the longest substring with one repeated char. | A window is valid if the non-dominant chars (size − maxFreq) fit within k replacements; otherwise shrink. | O(n) | O(1) | Standard |
| 209 | Minimum Size Subarray Sum | Find the minimum length subarray with sum ≥ target. | Once the window reaches target, every extra left-trim that stays ≥ target gives a shorter candidate. | O(n) | O(1) | Standard |
| 76 | Minimum Window Substring | Find the shortest substring of s that contains all characters of t. | Expand until all of t is covered, then shrink as far as you can while still covering it to find the tightest window. | O(n) | O(1) | Standard |
| 438 | Find All Anagrams in a String | Given strings `s` and `p`, return a list of all start indices of `p`'s anagrams in `s`. (An anagram uses same characters with same frequencies.) | An anagram is a fixed-length window whose letter counts equal p's, so slide width-`p.length()` and compare counts. | O(n) | O(1) | Standard |
| 159 | Longest Substring with At Most 2 Distinct Characters | Return the length of the longest substring with at most 2 distinct characters. | Grow the window freely; whenever a third distinct character appears, drop from the left until only 2 remain. | O(n) | O(1) | shrink when >2 distinct |
| 340 | Longest Substring with At Most K Distinct Characters | Return the length of the longest substring with at most `k` distinct characters. | Same as #159 but the distinct cap is `k`; shrink whenever the map holds more than k distinct characters. | O(n) | O(k) | Parameterized generalization of #159 — replace the hard-coded `2` with `k`. |
| 1343 | Number of Sub-arrays of Size K and Average Greater than or Equal to Threshold | Return the number of contiguous subarrays of size `k` whose average is greater than or equal to `threshold`. | "Average ≥ threshold" over fixed width k is just "sum ≥ k·threshold"; slide a width-k window and count the hits. | O(n) | O(1) | fixed-size sliding window. To avoid floating-point division, compare `windowSum >= k * threshold`. |
| 30 | Substring with Concatenation of All Words | Given `s` and an array `words` (all of equal length), return all start indices of substrings in `s` that are a concatenation of every word in `words` exactly once, in any order. | Every candidate substring has fixed length `words.length * wordLen`. Slide a word-aligned window: start at each offset `0..wordLen-1` and move in steps of `wordLen`, maintaining a frequency map of words seen. | O(n * wordLen) | O(words.length * wordLen) | word-aligned window, step = wordLen |
| 187 | Repeated DNA Sequences | Return all 10-letter substrings that occur more than once in a DNA string `s` (characters `A`, `C`, `G`, `T`). | Fixed window of size 10; record each substring in a set and report it the first time a duplicate insert fails. | O(n) | O(n) | fixed window size 10 |
| 395 | Longest Substring with At Least K Repeating Characters | Return the length of the longest substring of `s` such that every character in it appears at least `k` times. | "At least k" is not monotone for a single window, so fix the number of distinct characters allowed. For each target `unique` from 1 to 26, run a max-window that holds exactly `unique` distinct chars, and record when all of them meet the count `k`. | O(26 * n) | O(1) | fix distinct count to restore monotonicity |
| 487 | Max Consecutive Ones II | Given a binary array `nums`, return the maximum number of consecutive 1s if you may flip at most one 0. | Identical to #1004 with `k = 1`: longest window containing at most one zero. Grow, and shrink only when a second zero enters. | O(n) | O(1) | at most one zero (k = 1) |
| 689 | Maximum Sum of 3 Non-Overlapping Subarrays | Find three non-overlapping subarrays of length `k` with maximum total sum and return their starting indices (lexicographically smallest on ties). | Precompute every window sum of size k, then for each middle window pick the best left window to its left and the best right window to its right. | O(n) | O(n) | middle window scan with k-gaps |
| 713 | Subarray Product Less Than K | Return the number of contiguous subarrays whose product of all elements is strictly less than `k`. | Max-variable window: grow the window while the product stays below k; every valid window ending at `j` contributes `j - i + 1` new subarrays. | O(n) | O(1) | count subarrays ending at j |
| 727 | Minimum Window Subsequence | Return the minimum-length substring (window) of `s1` such that `s2` is a subsequence of it. On ties, return the leftmost. | Walk forward matching `s2` as a subsequence; once fully matched at index `j`, walk backward to tighten the start, giving the smallest window ending at `j`. Restart the forward scan just past that start. | O(n * m) | O(1) | subsequence match, not contiguous |
| 1044 | Longest Duplicate Substring | Return any longest substring that appears at least twice in `s` (overlaps allowed); return `""` if none. | Binary search the answer length: if a duplicate of length `L` exists, a duplicate of any shorter length also exists. Check each candidate length with a rolling hash over a fixed-size window. | O(n log n) average | O(n) | binary search the window size |
| 1838 | Frequency of the Most Frequent Element | Given `nums` and `k` operations (each increments one element by 1), return the maximum possible frequency of any single value. | Sort the array; the cheapest target to raise a window of elements to is its maximum (the rightmost in a sorted window). A window `[i, j]` is achievable if raising all elements to `nums[j]` costs at most `k`. | O(n log n) | O(1) | sort so the window max is the cheapest target |

---

### Frequency Map Trick (used by 567 and 76)

Both use a `need[]` array and a `required` counter to avoid scanning the map each step.

```java
// Expanding j — add s.charAt(j):
if (need[s.charAt(j)]-- > 0) required--;   // was needed → satisfied one more

// Shrinking i — remove s.charAt(i):
if (need[s.charAt(i)]++ >= 0) required++;  // was 0 (used up) → now short one
i++;
```

`need[c]` is positive when still needed, zero or negative when excess.  
`required` reaches 0 exactly when all characters of t are covered.

---

### Choosing the Template

| Question asks for | Template | i moves |
|---|---|---|
| Fixed-size window operation | Fixed | when `j-i+1 == k` |
| Longest / maximum window | Max variable | while invalid (`while`) |
| Shortest / minimum window | Min variable | while valid (`while`) |

| Window content | State to maintain |
|---|---|
| Sum of values | `int sum` |
| Unique characters / no duplicates | `int[] freq` (128 or 26) or `Set` |
| Character frequency match | `int[] need` + `int required` counter |
| Running maximum | `Deque<Integer>` monotone decreasing indices |

---
## Prefix Sum + HashMap  &nbsp;`prefix_sum_hashmap.md`

Core idea: `subarray sum [l, r] = prefix[r+1] - prefix[l]`.  
To find a subarray with a target property, rephrase as: "has a prefix with value X been seen before?"  
Store that X in a HashMap for O(1) lookup.

---

### Core Template

```java
// MENTAL MODEL: a subarray is the difference of two prefixes; remember prefixes seen so far and look up the complement.
// WHEN: "subarray sum equals/divisible by k", "longest subarray with sum X" — anything reducible to prefix[r]-prefix[l]
Map<Long, Integer> map = new HashMap<>();
map.put(0L, ???);    // seed: empty prefix (sum=0) seen before index 0
long sum = 0;
// result = 0 (count) or Integer.MAX_VALUE (length sentinel) depending on problem

for (int i = 0; i < nums.length; i++) {
    sum += nums[i];
    long lookup = transform(sum);          // what to look up (sum-k, sum%k, etc.)
    // use map.get(lookup) → update result
    map.put(storeKey(sum), storeValue(i)); // what to store (sum or sum%k → count or index)
}
```

**What changes per problem:**

| Variable | Count problems (560, 974) | Length problems (325, 523) |
|---|---|---|
| Map value | `count` (how many times seen) | `first index` (earliest occurrence) |
| Seed value | `map.put(0L, 1)` | `map.put(0L, -1)` |
| On lookup hit | `count += map.get(lookup)` | `maxLen = max(i - map.get(lookup))` |
| Overwrite map? | Yes (merge count) | No (keep first index only) |

---

### Quick Reference Table

Read the two map-value modes first: **count** problems store `prefix sum → how many times seen` and answer "how many"; **length/index** problems store `prefix sum → earliest index seen` and answer "how long / where". The two modes also seed differently:

- Seed `(0, 1)` = the empty prefix has been **seen once** before we start — needed for *counting* (a prefix that itself equals the target counts as one valid subarray).
- Seed `(0, -1)` = the empty prefix lives at a **virtual index -1** — needed for *length* (length from start = `i - (-1) = i + 1`).

| # | Name | Description | Intuition | Time | Space | Key Implementation |
|---|---|---|---|---|---|---|
| 560 | Subarray Sum Equals K | Count the number of subarrays whose sum equals k. | A subarray summing to k ends here for every earlier prefix equal to `sum - k`; count those prefixes. | O(n) | O(n) | Standard |
| 325 | Maximum Size Subarray Sum Equals k | Find the length of the longest subarray summing to k. | Same complement as #560, but store the earliest index so `i - p` gives the longest subarray summing to k. | O(n) | O(n) | Standard |
| 974 | Subarray Sums Divisible by K | Count subarrays whose sum is divisible by k. | Two prefixes with the same remainder bracket a subarray divisible by k; count how many share each remainder. | O(n) | O(min(n, k)) | Standard |
| 523 | Continuous Subarray Sum | Return true if any subarray of length ≥ 2 has sum divisible by k. | Same-remainder pair means a divisible subarray; store the earliest index so the gap `i - p >= 2` proves length ≥ 2. | O(n) | O(min(n, k)) | Standard |
| 437 | Path Sum III | Count the number of paths in a binary tree that sum to targetSum. Paths can start and end at any node but must go downward. | Apply the #560 prefix-count idea along each root-to-node path; undo the prefix on the way back up so branches stay independent. | O(n) | O(h) (recursion + path-prefix map, h = tree height) | Standard |
| 1 | Two Sum | Given an array and a `target`, return the indices of the two numbers that add up to `target`. | Same "have I seen the complement before?" idea as prefix-sum, but the key is the raw value, so one pass finds the pair. | O(n) | O(n) | look up complement, not prefix sum |

---

### When to Use `long` vs `int`

- Use `long` for the prefix sum when values can be large (e.g., `nums[i]` up to `10^4` × `n` up to `2×10^4` → sum up to `2×10^8`, safe as int, but `10^5 × 10^5 = 10^10` overflows).
- Use `int` for the remainder key (modulo result is always in `[0, k-1]`).

#### Why `0L` (not `0`) in the seed

When the map is `Map<Long, Integer>`, the seed **key** must be a `long` literal:

```java
Map<Long, Integer> map = new HashMap<>();
map.put(0L, 1);     // ✓ long literal → boxes to Long (matches key type)
map.put(0, 1);      // ✗ compile error: int boxes to Integer, not Long
```

- The `L` suffix makes it a `long` literal so it autoboxes to `Long`, matching the key type (the keys are `long` because `sum` is `long` for the overflow guard above).
- **Subtle trap:** even numerically equal boxes of different types never compare equal — `Long.valueOf(0).equals(Integer.valueOf(0))` is `false`. Keeping every key `long`/`Long` avoids silent lookup misses.
- If `int` sums can't overflow, use `Map<Integer, Integer>` with plain `map.put(0, 1)` instead — simpler, no `L` needed.

---
## Binary Search  &nbsp;`binary_search.md`

Binary search appears in two forms: searching an **array index**, or searching an **answer value**.

---

### Master Quick Reference

| # | Name | Description | Intuition | Time | Space | Key Implementation |
|---|---|---|---|---|---|---|
| 704 | Binary Search | Given a sorted array and a target, return its index. Return -1 if not found. | Both bounds converge to a single index `i`. With `lowerBound`, `i` is the first slot `>= target`, so check `nums[i]`. With `upperBound`, `i` is one past the last `<= target`, so check `nums[i-1]`. Same loop, mirror edge. | O(log n) | O(1) | Standard |
| 34 | Find First and Last Position of Element in Sorted Array | Return `[first, last]` index of target. Return `{-1,-1}` if absent. | Find the boundary where "< target" flips to "≥ target" (first position), and the next boundary just past target. | O(log n) | O(1) | Standard |
| 35 | Search Insert Position | Return the index where target is or would be inserted to keep the array sorted. | The insert position is the first index whose value is ≥ target — exactly `lowerBound`. | O(log n) | O(1) | Standard |
| 33 | Search in Rotated Sorted Array | Array was sorted then rotated at an unknown pivot. Find target index, or -1. | First locate the rotation point with a boundary search, then the array splits into one sorted segment that must contain target — run a plain `lowerBound` there. | O(log n) | O(1) | Standard |
| 162 | Find Peak Element | Return any index where `arr[k] > arr[k-1]` and `arr[k] > arr[k+1]`. Edges are -∞. | Always walk uphill — an upward slope guarantees a peak to the right, so the slope direction is the "condition". | O(log n) | O(1) | Standard |
| 875 | Koko Eating Bananas | Minimum eating speed so Koko finishes all piles in h hours (one pile per hour, at most `speed` bananas eaten). | Feasibility is monotonic in speed (faster always works), so binary search the speed axis for the smallest that finishes in time. | O(n log(max(piles))) | O(1) | Standard |
| 1011 | Capacity to Ship Packages Within D Days | Minimum ship capacity to deliver all packages (in order) within d days. | Bigger capacity is always feasible, so binary search capacity for the smallest that ships within the day budget. | O(n log(sum(weights))) | O(1) | Standard |
| 410 | Split Array Largest Sum | Split array into m non-empty subarrays to minimize the largest subarray sum. | A larger allowed max-sum needs fewer parts, so binary search that cap for the smallest splittable into ≤ m parts. | O(n log(sum(nums))) | O(1) | Standard |
| 1283 | Find the Smallest Divisor Given a Threshold | Smallest positive divisor such that `sum of ceil(nums[i] / divisor) <= threshold`. | A bigger divisor shrinks the sum, so the condition flips false→true; binary search for the smallest divisor that fits the threshold. | O(n log(max(nums))) | O(1) | Standard |
| 1231 | Divide Chocolate ← MAXIMIZE (the one that differs) | Cut chocolate into k+1 pieces; keep the minimum-sweetness piece. Maximize that minimum. | A larger target-minimum yields fewer pieces, so feasibility flips true→false. MAXIMIZE = search the FIRST INFEASIBLE minimum and step back one: `condition(k) = !canDivide(k)` (pieces `< k+1`), false…false TRUE…true. Half-open `[lo, hi+1)`, return `i - 1` — no ceiling mid needed. | O(n log(sum(s))) | O(1) | Standard |
| 4 | Median of Two Sorted Arrays | Find the median of two sorted arrays of sizes m and n in O(log(m+n)) time. | Pick a split of the smaller array; the rest of the split is forced. Shrink the partition until the left half's max ≤ the right half's min, then the median falls out of the boundary values. | O(log(min(m, n))) | O(1) | search smaller array |
| 69 | Sqrt(x) | Compute the integer square root of a non-negative integer x without using sqrt(). | Feasibility `k*k <= x` is true…true then false as k grows. MAXIMIZE = find the FIRST INFEASIBLE k with `condition(k) = k*k > x` (false…false TRUE…true), over `[1, x+1)`, and return `i - 1` — the largest k still feasible. No ceiling mid needed. | O(log x) | O(1) | Standard |
| 74 | Search a 2D Matrix | Search for a target in an m×n matrix where each row is sorted and each row's first element > previous row's last. | The layout means the whole matrix reads as a single sorted sequence; map a flat index to `(row, col)` and run a standard `[i, j)` lowerBound, then verify the landed value. | O(log(m*n)) | O(1) | flatten index to 2D |
| 81 | Search in Rotated Sorted Array II | Search in a sorted, rotated array that may contain duplicates. | Duplicates can make both ends equal to the midpoint so neither half looks sorted; in that ambiguous case shrink both bounds by one and retry. | O(log n) average, O(n) worst | O(1) | ambiguous duplicates |
| 153 | Find Minimum in Rotated Sorted Array | Find the minimum element in a sorted, rotated array with no duplicates. | The minimum is the single point where the order breaks; if `arr[k] > arr[j]` the break is to the right, otherwise the min is at k or left. | O(log n) | O(1) | Standard |
| 240 | Search a 2D Matrix II | Search for a target in an m×n matrix where rows and columns are both sorted. | From the top-right, moving left strictly decreases and moving down strictly increases, so each comparison eliminates a full row or column. | O(m + n) | O(1) | start top-right corner |
| 278 | First Bad Version | Find the first bad version using a provided isBadVersion(n) API. Minimize API calls. | Versions are good...good then bad...bad once corrupted; this is the classic first-true boundary search. | O(log n) | O(1) | Standard |
| 374 | Guess Number Higher or Lower | Guess the number between 1 and n using a provided guess() API. Minimize calls. | `guess(k)` returns `-1` when the pick is lower than `k`, `1` when higher, `0` on a hit. So `guess(k) <= 0` is false…false TRUE…true as `k` grows, and the first true `k` is the answer. | O(log n) | O(1) | Standard |
| 475 | Heaters | Given house and heater positions, find the minimum heater radius so every house is covered by some heater. | Each house needs the closest heater; the required radius is the largest of those closest distances. Find each house's nearest heater by binary search. | O((m + n) log m) | O(1) | also check left neighbor |
| 540 | Single Element in a Sorted Array | Find the single non-duplicate element in a sorted array where all others appear twice. O(log n). | Before the unique element each pair starts at an even index; after it, the parity shifts. Force the midpoint even and check whether its partner matches to pick a half. | O(log n) | O(1) | force k even |
| 658 | Find K Closest Elements | Find k integers in a sorted array closest to x, ordered by closeness then value. | The answer is a contiguous window of size k; search for its start by comparing the distances of the two window edges to x and sliding toward the closer side. | O(log(n - k) + k) | O(k) | search window start [i, j] |
| 719 | Find K-th Smallest Pair Distance | Find the k-th smallest absolute distance among all pairs in the array. | The count of pairs with distance ≤ d is monotonic in d, so binary search the distance axis; count pairs ≤ d with a sliding window over the sorted array. | O(n log n + n log(maxDist)) | O(1) | search distance value [i, j] |
| 852 | Peak Index in a Mountain Array | Find the peak index in a mountain array (element greater than both neighbors). | An upward slope means the peak is strictly to the right; a downward slope means the peak is here or to the left. | O(log n) | O(1) | Standard |
| 1060 | Missing Element in Sorted Array | Find the kth missing number in a sorted array. | Missing count at each index increases monotonically, so binary search for the first index whose missing count is ≥ k, then offset from the previous element. | O(log n) | O(1) | kth missing beyond array end |
| 1428 | Leftmost Column with at Least a One | Find the leftmost column with at least one '1' in a binary matrix (rows sorted, accessed via BinaryMatrix API). | Each row is sorted 0...0 1...1; starting top-right, move left on a 1 (column might be even further left) and down on a 0, tracking the leftmost 1 seen. | O(rows + cols) | O(1) | start top-right corner |
| 1482 | Minimum Number of Days to Make m Bouquets | Find the minimum number of days to make m bouquets of k adjacent flowers. | Waiting more days only adds bloomed flowers, so feasibility is monotonic; binary search the day axis and greedily count adjacent runs of bloomed flowers. | O(n log(max(bloomDay))) | O(1) | impossible if not enough flowers |
| 1539 | Kth Missing Positive Number | Find the kth missing positive integer. | At each index the number of missing positives so far is `arr[k] - (k+1)`; binary search the first index whose missing count is ≥ k, then offset. | O(log n) | O(1) | i missing-free slots + k |
| 1818 | Minimum Absolute Sum Difference | Find the minimum absolute sum difference after one substitution. | Total cost is the sum of absolute differences; one swap can only help where the closest available nums1 value beats the current difference. Find that closest value by binary search and track the best gain. | O(n log n) | O(n) | also check left neighbor |
| 1891 | Cutting Ribbons | Find the maximum ribbon length such that m ribbons of that length can be cut. | Longer pieces produce fewer ribbons, so feasibility flips true→false as length grows. Search the first INFEASIBLE length (`condition(k) = countRibbons(k) < k`, false…false TRUE…true) and step back one; that is the largest feasible length. If no length is feasible the loop lands on `lo`, giving `i - 1 = 0`. | O(n log(max(ribbons))) | O(1) | [1, max+1) over lengths |

\* #162 uses `j = n-1` (not `n`) — loop reads `arr[k+1]`, out of bounds if `j = n`.

---

### The Only Template — `[i, j)`, find first `k` with `condition(k)`

**There is one binary search.** Define a monotone `condition(k)` (`false…false TRUE…true`); the loop returns the **first `k` where `condition(k)` is true**. Then look at `i`: if `i == n` no index qualified, otherwise `i` is the boundary — check the value to decide.

```java
int i = 0, j = nums.length;       // [i, j)
// find first k that meets condition(k)
while (i < j) {
    int k = i + (j - i) / 2;
    if (!condition(k)) {          // condition false → answer is strictly to the right
        i = k + 1;
    } else {                      // condition true  → k might be the answer
        j = k;
    }
}
// i in [0, nums.length]; if i == nums.length, no k met condition(k)
```

**Pick `condition(k)`:**

| Want | `condition(k)` | Answer after loop |
|---|---|---|
| `lowerBound` — first `>= target` | `nums[k] >= target` | `i` |
| `upperBound` — first `> target` | `nums[k] > target` | `i` |
| exact search (#704) | `nums[k] >= target` | `i < n && nums[i] == target ? i : -1` |
| insert position (#35) | `nums[k] >= target` | `i` |
| first / last occurrence (#34) | `>=` then `>` | `lowerBound`, `upperBound - 1` |
| count of target | — | `upperBound - lowerBound` |
| minimize feasible X | `feasible(k)` over value range | `i` |
| maximize feasible X | `!feasible(k)` (first infeasible) | `i - 1` |

**The rule:** the answer is always `i`. Guard `i == nums.length` (nothing met the condition) before reading `nums[i]`, then confirm the value.

---

### How to Choose

| Signal | `condition(k)` |
|---|---|
| Sorted array, find exact value | `arr[k] >= target`, then check `arr[i] == target` |
| Insert position / first occurrence | `arr[k] >= target` → return `i` (`= lowerBound`) |
| Last occurrence / count | `arr[k] > target` (`= upperBound`); last = `upperBound - 1`, count = `upper - lower` |
| Rotated / peak slope search | `condition(k)` compares `arr[k]` to a neighbor or endpoint |
| "minimum X such that feasible(X)" | `condition(k) = feasible(k)` over value range → return `i` |
| "maximum X such that feasible(X)" | `condition(k) = !feasible(k)` over `[lo, hi+1)` → return `i - 1` |

**The one rule:** define `condition(k)` so it is monotone `false…false TRUE…true`, then the answer is the first `k` that flips it true (`j = k` on true, `i = k + 1` on false). For MAXIMIZE, make the condition "first infeasible" and subtract 1 — same loop, no ceiling mid.

---

### Detail Table

| # | Name | Description | Interval | On `arr[k]==target` | Shrink left | Shrink right | Return |
|---|---|---|---|---|---|---|---|
| 704 | Binary Search | Find index of target; -1 if absent | Half-open | — | `i = k+1` | `j = k` | `lower, then arr[i]==target ? i : -1` |
| 34 | First & Last Position | First and last index of target | Half-open | — | `i = k+1` | `j = k` | `{lower, upper-1}` |
| 35 | Search Insert Position | Index where target is or would be inserted | Half-open | — | `i = k+1` | `j = k` | `i` |
| 33 | Search in Rotated Array | Find target after unknown-pivot rotation | Half-open | — | `i = k+1` | `j = k` | find pivot, then lowerBound; `nums[i]==target ? i : -1` |
| 162 | Find Peak Element | Any local peak index | Half-open* | — | `i = k+1` | `j = k` | `i` |

---

Search on the **answer value** itself, not an array index. All use half-open `[i, j)` with `while (i < j)`.

### Detail Table

| # | Name | Description | Variant | i init | j init | Mid | Condition true | Condition false | Helper checks |
|---|---|---|---|---|---|---|---|---|---|
| 875 | Koko Eating Bananas | Min speed to finish all piles in h hours | MINIMIZE | `1` | `max(piles)` | floor | `j = k` | `i = k+1` | `hours <= h` |
| 1011 | Ship Within D Days | Min capacity to ship all packages in d days | MINIMIZE | `max(w)` | `sum(w)` | floor | `j = k` | `i = k+1` | `days <= d` |
| 410 | Split Array Largest Sum | Min largest sum splitting array into m parts | MINIMIZE | `max(nums)` | `sum(nums)` | floor | `j = k` | `i = k+1` | `parts <= m` |
| 1283 | Smallest Divisor | Smallest divisor so ceil-div-sum ≤ threshold | MINIMIZE | `1` | `max(nums)` | floor | `j = k` | `i = k+1` | `divSum <= threshold` |
| 1231 | Divide Chocolate | Max min-sweetness cutting into k+1 pieces | MAXIMIZE | `min(s)` | `sum(s)/(k+1)+1` | floor | `j = k` | `i = k+1` | `pieces < k+1` (first infeasible), return `i-1` |

875 / 1011 / 410 / 1283 → identical structure, differ only in search bounds and condition helper.  
1231 → MAXIMIZE: same floor-mid `[i, j)` loop, but `condition(k) = !feasible(k)` (first infeasible) and return `i - 1`.

---
## Sorting  &nbsp;`sorting.md`

All recursive sorting uses **half-open intervals `[start, end)`** throughout.  
Inside merge and partition: `i`, `j`, `k` as scan/write pointers (consistent with binary search convention).

---

### Quick Reference Table

| # | Name | Description | Intuition | Time | Space | Key Implementation |
|---|---|---|---|---|---|---|
| 912 | Sort an Array | Sort an integer array. No built-in sort allowed. | Divide and conquer — either split-then-merge (merge sort) or partition-then-recurse (quick sort); both reach O(n log n). | O(n log n) | O(n) merge / O(log n) quick | Standard |
| 215 | Kth Largest Element in an Array | Return the k-th largest element without sorting the full array. | Quick select partitions around a pivot and only recurses into the side containing the target rank, so it averages O(n) instead of fully sorting. | O(n) avg | O(log n) | Standard |
| 973 | K Closest Points to Origin | Return the k closest points to origin (0,0). Any order. | Same quick select, but partition on squared distance — once the first k slots are filled with the closest points, their internal order doesn't matter. | O(n) avg | O(log n) | Standard |
| 148 | Sort List | Sort a linked list in O(n log n) time, O(log n) space. | Merge sort fits linked lists — there's no random access for quick sort, but splitting at the middle and merging two sorted lists needs only pointer rewiring. | O(n log n) | O(log n) | Standard |
| 179 | Largest Number | Given a list of non-negative integers, arrange them to form the largest number. | Order two numbers by which concatenation is bigger (`b+a` vs `a+b`) — this pairwise rule sorts the whole list into the largest possible string. | O(n log n) | O(n) | Standard |
| 315 | Count of Smaller Numbers After Self | For each element, count how many elements to its right are smaller. | During a merge, whenever a left-half element is placed, every right-half element already emitted is both smaller and to its right — so the merge counts the smaller-after-self pairs for free. | O(n log n) | O(n) | Standard |
| 56 | Merge Intervals | Merge all overlapping intervals. Return array of non-overlapping intervals. | After sorting by start, overlaps can only be with the most recent interval, so one scan either extends its end or appends a new one. | O(n log n) | O(n) | Standard |
| 88 | Merge Sorted Array | Given two sorted arrays `nums1` (with capacity for m+n) and `nums2`, merge `nums2` into `nums1` in-place. |  | O(m+n) | O(1) | Fill from the END backwards using three pointers `i` (end of nums1 valid data), `j` (end of nums2), `k` (end of merged result). This avoids the need to shift elements. |
| 327 | Count of Range Sum | Given an integer array, count the number of range sums `sum(i,j)` that lie within `[lower, upper]` (inclusive). |  | O(n log n) | O(n) | Build prefix sum array. Then use modified merge sort — during the merge phase, for each element in the left half, use two sliding pointers `j` and `k` into the right half to count valid prefix sums (those where `arr[k] - arr[i]` falls in range). This gives O(n log n) vs O(n²) brute force. |
| 164 | Maximum Gap | Given an unsorted array, return the maximum difference between successive elements in its sorted form. Must run in linear time. |  | O(n) | O(n) | bucket sort by pigeonhole principle. With n elements, the max gap is at least `ceil((max-min)/(n-1))`. Place elements into buckets of that size; the max gap spans between one bucket's max and the next non-empty bucket's min. |

---

### Template 1 — Merge Sort

```java
// MENTAL MODEL: split in half until trivially sorted, then merge two sorted halves into one.
// WHEN: need stable sort, sort a linked list, or count cross-pairs (inversions) during the merge.
// Entry point
public void mergeSort(int[] nums) {
    mergeSort(nums, 0, nums.length, new int[nums.length]);
}

// [start, end) half-open
private void mergeSort(int[] nums, int start, int end, int[] temp) {
    if (end - start <= 1) return;        // base case: end - start <= 1 → 0 or 1 elements, already sorted
    int mid = start + (end - start) / 2;
    mergeSort(nums, start, mid, temp);   // sort [start, mid)
    mergeSort(nums, mid,   end, temp);   // sort [mid, end)
    merge(nums, start, mid, end, temp);
}

// i scans left [start,mid), j scans right [mid,end), k writes to temp
private void merge(int[] nums, int start, int mid, int end, int[] temp) {
    int i = start, j = mid, k = start;
    while (i < mid || j < end) {
        if (j >= end || (i < mid && nums[i] <= nums[j])) {
            temp[k++] = nums[i++];
        } else {
            temp[k++] = nums[j++];
        }
    }
    for (i = start; i < end; i++) nums[i] = temp[i];
}
```

---

### Template 2 — Quick Sort (3-way Dutch Flag Partition)

```java
// MENTAL MODEL: pick a pivot, partition into <pivot | ==pivot | >pivot, recurse on the two ends only.
// WHEN: in-place sort with O(log n) stack; the ==pivot middle is already in final position.
// Entry point — no extra array needed (in-place)
public void quickSort(int[] nums) {
    quickSort(nums, 0, nums.length);
}

// [start, end) half-open
private void quickSort(int[] nums, int start, int end) {
    if (end - start <= 1) return;
    int pivot = nums[start + (end - start) / 2];
    int i = start, k = start, j = end - 1;
    // Invariant: [start,i) < pivot  |  [i,k) == pivot  |  [k,j] unknown  |  (j,end) > pivot
    while (k <= j) {
        if (nums[k] < pivot) {
            swap(nums, k++, i++);
        } else if (nums[k] == pivot) {
            k++;
        } else {
            swap(nums, k, j--);
        }
    }
    // After: [start,i) < pivot, [i,k) == pivot, [k,end) > pivot
    quickSort(nums, start, i);   // recurse on < region
    quickSort(nums, k, end);     // recurse on > region
}

private void swap(int[] nums, int i, int j) {
    int t = nums[i]; nums[i] = nums[j]; nums[j] = t;
}
```

---

### Template 3 — Quick Select (partial sort — k-th element)

Extends quick sort: after partition, only recurse into the side that contains `target` index.

```java
// MENTAL MODEL: same partition as quick sort, but recurse into only the one side holding target → O(n) avg.
// WHEN: "k-th largest/smallest", "k closest/most frequent" — you need a position, not a full sort.
// Returns value at 0-indexed position target after sorting
private int quickSelect(int[] nums, int start, int end, int target) {
    int pivot = nums[start + (end - start) / 2];
    int i = start, k = start, j = end - 1;
    while (k <= j) {
        if (nums[k] < pivot) {
            swap(nums, k++, i++);
        } else if (nums[k] == pivot) {
            k++;
        } else {
            swap(nums, k, j--);
        }
    }
    // [start,i) < pivot, [i,k) == pivot, [k,end) > pivot
    if (target < i) {
        return quickSelect(nums, start, i, target);
    } else if (target < k) {
        return pivot;                          // target lands in == region
    } else {
        return quickSelect(nums, k, end, target);
    }
}
```

---

### Template 4 — Counting Sort

O(n + range). Use when values are bounded integers.

```java
// MENTAL MODEL: tally how many times each value occurs, then emit values in order — no comparisons.
// WHEN: integers in a small bounded range; beats O(n log n) when range = O(n).
public void countingSort(int[] arr) {
    if (arr.length == 0) return;
    int min = Arrays.stream(arr).min().getAsInt();
    int max = Arrays.stream(arr).max().getAsInt();
    int[] buckets = new int[max - min + 1];
    for (int x : arr) buckets[x - min]++;
    int i = 0;
    for (int v = 0; v < buckets.length; v++)
        while (buckets[v]-- > 0) arr[i++] = v + min;
}
```

---

### Algorithm Chooser

| Signal | Algorithm |
|---|---|
| "sort array", stable, O(n) space OK | Merge Sort |
| "sort array", in-place, O(log n) space | Quick Sort |
| "k-th largest/smallest" | Quick Select — O(n) avg |
| "k closest / k most frequent" | Quick Select with custom comparator |
| "sort linked list" | Merge Sort (quick sort needs random access) |
| "count inversions / smaller after self" | Merge Sort — count during merge step |
| "arrange to maximize/compare" | Custom Sort comparator |
| "merge overlapping intervals" | Sort by start + linear scan |
| integers in bounded range | Counting Sort — O(n + range) |

### Half-open Interval Cheat Sheet

```
mergeSort(nums, start, end)   →  sorts [start, end)
  mid = start + (end-start)/2
  left:   [start, mid)
  right:  [mid, end)
  base:   end - start <= 1

quickSort(nums, start, end)   →  sorts [start, end)
  after partition: [start,i) < pivot, [i,k) == pivot, [k,end) > pivot
  recurse: (start, i)  and  (k, end)
```

---
## Linked List  &nbsp;`linked_list.md`

Four patterns cover almost every linked list problem.  
Consistent naming throughout: `sentinel`, `previous`, `current`, `next`, `slow`, `fast`.

---

### Quick Reference Table

| # | Name | Description | Intuition | Time | Space | Key Implementation |
|---|---|---|---|---|---|---|
| 203 | Remove Linked List Elements | Remove all nodes whose value equals `val`. |  | O(n) | O(1) | Standard |
| 83 | Remove Duplicates from Sorted List | Keep exactly one copy of each value. List is sorted. |  |  |  | Standard |
| 82 | Remove Duplicates from Sorted List II | Remove ALL nodes that have duplicate values — only distinct-valued nodes remain. |  | O(n) | O(1) | Standard |
| 19 | Remove Nth Node From End of List | Remove the nth node from the end. Return the head. |  |  |  | Standard |
| 206 | Reverse Linked List | Reverse the entire linked list. Return the new head. | flip each node's arrow to point at the node you just came from; `previous` is the reversed list built so far. |  |  | Standard |
| 92 | Reverse Linked List II | Reverse only the nodes from position `left` to `right` (1-indexed). |  |  |  | Standard |
| 25 | Reverse Nodes in k-Group | Reverse every consecutive group of k nodes. Leave remaining nodes (< k) as-is. |  | O(n) | O(1) | Standard |
| 876 | Middle of Linked List | Return the middle node. For even length, return the second middle. |  | O(n) | O(1) | Standard |
| 141 | Linked List Cycle | Return true if the list contains a cycle. |  | O(n) | O(1) | Standard |
| 142 | Linked List Cycle II | Return the node where the cycle begins. Return null if no cycle. | the distance from head to the cycle entry equals the distance from the meeting point to the entry, so two 1-step walkers from those spots collide exactly at the entry. | O(n) | O(1) | Standard |
| 21 | Merge Two Sorted Lists | Merge two sorted linked lists into one sorted list. | like a zipper — always splice on whichever current head is smaller, then advance that list. | O(n) | O(1) | Standard |
| 23 | Merge K Sorted Lists | Merge k sorted linked lists into one sorted list. |  | O(n log k) | O(k) | Standard |
| 143 | Reorder List | Reorder list as L0 → Ln → L1 → Ln-1 → L2 → ... |  |  |  | Standard |
| 328 | Odd Even Linked List | Group all odd-indexed nodes first, then even-indexed nodes. Preserve relative order within each group. (Indexing is 1-based.) |  |  |  | Standard |
| 2 | Add Two Numbers | Two non-empty linked lists represent non-negative integers stored in reverse order. Add and return the sum as a linked list in reverse order. |  | O(max(m, n)) | O(max(m, n)) | loop until carry clears |
| 88 | Merge Sorted Array | Merge `nums2` into `nums1` in-place. `nums1` has enough space at the end. Both arrays are sorted. |  | O(m + n) | O(1) | three pointers from END |
| 234 | Palindrome Linked List | Check if a singly linked list is a palindrome in O(n) time and O(1) space. |  | O(n) | O(1) | in-place reverse |
| 160 | Intersection of Two Linked Lists | Find the node at which two singly linked lists intersect. Return null if they do not intersect. |  | O(m + n) | O(1) | redirect to other list on null |
| 24 | Swap Nodes in Pairs | Swap every two adjacent nodes in a linked list and return the modified head. | A sentinel removes head special-casing. For each pair, `previous` is the node before the pair; re-wire the three pointers so the second node leads, then advance `previous` two nodes forward. | O(n) | O(1) | Standard |
| 61 | Rotate List | Rotate a linked list to the right by `k` places. | Rotating right by `k` is equivalent to making the list circular, then breaking it `k % length` nodes before the old tail. Compute the length, close the ring, then walk to the new tail. | O(n) | O(1) | only the remainder matters |
| 86 | Partition List | Partition a linked list so all nodes with value `< x` come before nodes with value `>= x`. Preserve the relative order within each group. | Build two separate chains with two sentinels — one for the "less" group and one for the "greater-or-equal" group — then stitch them together. Preserving original order falls out naturally because nodes are appended in traversal order. | O(n) | O(1) | Standard |
| 109 | Convert Sorted List to Binary Search Tree | Convert a sorted linked list to a height-balanced BST. | A sorted list is an in-order traversal of a BST. Repeatedly pick the middle node as the subtree root so each side gets a balanced number of nodes; recurse on the left half (before middle) and right half (after middle). | O(n log n) | O(log n) | stop at exclusive tail |
| 138 | Copy List with Random Pointer | Deep-copy a linked list where each node has a `random` pointer to any node or null. | Interleave each clone directly after its original so a clone's `random` is reachable as `original.random.next` — no hash map needed. Three passes: weave clones in, wire random pointers, then unweave. | O(n) | O(1) | Standard |
| 148 | Sort List | Sort a linked list. Aim for O(n log n) time and O(1) extra space (top-down recursion uses O(log n) stack). | Merge sort fits linked lists perfectly — splitting is a pointer cut and merging reuses the #21 zipper. Find the middle, sort each half, merge. | O(n log n) | O(log n) | Standard |
| 237 | Delete Node in a Linked List | Delete a node from a singly linked list given only a reference to that node (not the head). The node is guaranteed not to be the tail. | Without access to the previous node you cannot unlink the given node directly, but you can copy the next node's value into it and then delete the next node instead. | O(1) | O(1) | copy successor's value |
| 369 | Plus One Linked List | A non-negative integer is stored as a linked list of digits in big-endian order (most significant first). Add one to it and return the resulting list. | Reverse the list so addition flows least-significant-first like normal carry arithmetic, add one with carry propagation, then reverse back. A possible new leading digit is handled by extending the tail after reversal. | O(n) | O(1) | seed carry with the +1 |
| 430 | Flatten a Multilevel Doubly Linked List | Flatten a multilevel doubly linked list where nodes may have a `child` list. Produce a single-level list using the `next` pointers; all `child` pointers must be null. | A child list should be spliced in immediately after its parent, before the parent's original `next`. A stack lets you remember each deferred `next` while you dive into a child branch — effectively an iterative DFS. | O(n) | O(n) | clear child after splicing |
| 445 | Add Two Numbers II | Two numbers are stored as linked lists in big-endian order (most significant digit first). Add them and return the sum as a linked list, also in big-endian order. | Addition needs least-significant digits first, but reversing the inputs is discouraged here. Push all digits onto two stacks; popping yields least-significant-first. Build the result by prepending nodes so the final list is big-endian. | O(m + n) | O(m + n) | prepend to keep big-endian order |
| 708 | Insert into a Sorted Circular Linked List | Insert a value into a sorted circular linked list and return a reference to any node in the list. The given pointer may reference any node, or be null for an empty list. | Walk one full loop looking for the correct gap between a node and its successor. Three cases cover it: a normal in-between slot, the wrap-around boundary (max→min) where the value is an extreme, and a uniform-value list where any spot works. | O(n) | O(1) | wrap-around boundary |
| 725 | Split Linked List in Parts | Split a linked list into `k` consecutive parts as equal in size as possible. Earlier parts have sizes greater than or equal to later parts; some trailing parts may be empty. | With length `n`, each part gets `n / k` nodes, and the first `n % k` parts get one extra. Walk through cutting off each part at its computed size. | O(n) | O(k) | first `remainder` parts get +1 |
| 1171 | Remove Zero Sum Consecutive Nodes from Linked List | Repeatedly remove consecutive sequences of nodes that sum to zero until no such sequence remains. Return the resulting list. | Use prefix sums. If two nodes share the same running prefix sum, every node strictly between them sums to zero and can be dropped. A hash map from prefix sum to node lets you splice out those runs in one pass. | O(n) | O(n) | keep the latest node per sum |
| 1265 | Print Immutable Linked List in Reverse | Print all values of an immutable linked list in reverse, using only the exposed `getNext()` and `printValue()` API, without modifying the list. | Recursion naturally reverses order — recurse to the end first, then print on the way back up the call stack. | O(n) | O(n) | recurse first, print on unwind |

---

### When to Use — Signal → Pattern

| Signal in the prompt | Pattern |
|---|---|
| "remove / delete / skip" nodes by value or duplicate | Delete / Filter (sentinel + `previous`) |
| "reverse" the list, a sub-range, or in k-groups | Reversal |
| "middle node", "cycle", "nth node from the end" | Fast / Slow |
| "merge two sorted lists" (or k lists) | Merge (sentinel + heap for k) |
| chained steps ("reorder", "palindrome", "sort") | Composite (combine the above) |

---

### All Four Templates

```java
// 1. DELETE / FILTER  — sentinel guards head removal; previous tracks last kept node
// MENTAL MODEL: previous always points at the last node you decided to keep, so re-wiring it skips anything unwanted.
// WHEN: "remove / delete / skip nodes by value or duplicate"
ListNode sentinel = new ListNode(0);
sentinel.next = head;
ListNode previous = sentinel, current = head;
while (current != null) {
    if (shouldDelete(current)) {
        previous.next = current.next;   // skip node
    } else {
        previous = current;             // keep node, advance previous
    }
    current = current.next;
}
return sentinel.next;

// 2. REVERSAL — re-wire one node at a time
// MENTAL MODEL: flip each arrow to point backward; previous is the growing reversed list trailing behind current.
// WHEN: "reverse the list (whole, partial, or in k-groups)"
ListNode previous = null, current = head;
while (current != null) {
    ListNode next = current.next;   // save before overwrite
    current.next = previous;        // reverse pointer
    previous = current;             // advance
    current = next;
}
return previous;  // new head

// 3. FAST / SLOW — two pointers at different speeds
// MENTAL MODEL: fast covers twice the distance, so when it hits the end slow is exactly halfway; in a loop they must collide.
// WHEN: "middle node", "detect/locate cycle", "nth from end"
ListNode slow = head, fast = head;
while (fast != null && fast.next != null) {
    slow = slow.next;
    fast = fast.next.next;
}
// slow is at middle  (or cycle detection: slow == fast → cycle found)

// 4. MERGE — sentinel collects nodes from two lists in order
// MENTAL MODEL: repeatedly splice the smaller head onto a growing result tail, like a zipper.
// WHEN: "merge two (or k) sorted lists"
ListNode sentinel = new ListNode(0);
ListNode current = sentinel;
while (a != null && b != null) {
    if (a.val <= b.val) {
        current.next = a;
        a = a.next;
    } else {
        current.next = b;
        b = b.next;
    }
    current = current.next;
}
current.next = (a != null) ? a : b;
return sentinel.next;
```

---

`previous` stays on the last **kept** node. When deleting, re-wire `previous.next` to skip `current`. When keeping, advance `previous` to `current`. Always advance `current`.

`fast` moves 2× per step. When `fast` reaches the end, `slow` is at the middle.  
When `slow == fast` after the start, a cycle is detected.

`sentinel` collects the merged result. `current` is the write pointer.

Problems that chain multiple patterns together.

### Pattern Summary

| Pattern | Sentinel | Naming | When to use |
|---|---|---|---|
| Delete / Filter | Yes | `previous`, `current` | Remove or skip nodes by condition |
| Reversal | No (Yes for partial) | `previous`, `current`, `next` | Re-wire pointer direction |
| Fast / Slow | No | `slow`, `fast` | Middle, cycle, nth from end |
| Merge | Yes | `current` | Combine two or more lists |
| Composite | Both | Mix of above | Reorder, sort, rearrange |

### Sentinel Cheat Sheet

**SENTINEL:** dummy node before head so head removal needs no special-casing; use it whenever the head itself might be removed/replaced.

```java
// Always use sentinel when the head itself might be removed or replaced:
ListNode sentinel = new ListNode(0);
sentinel.next = head;
// ... operations ...
return sentinel.next;   // head may have changed; sentinel.next is always correct
```

---

## String  &nbsp;`string.md`

Core idioms first, then problems grouped by pattern.  
For sliding window string problems (#3, #76, #567, #424), see `sliding_window.md`.

---

### Quick Reference Table

| # | Name | Description | Intuition | Time | Space | Key Implementation |
|---|---|---|---|---|---|---|
| 242 | Valid Anagram | Return true if `t` is an anagram of `s` (same characters, same counts). | Anagrams have identical letter counts, so add up `s` and subtract `t` in one 26-slot array — all zeros means they match. | O(n) | O(1) | Standard |
| 383 | Ransom Note | Can `ransomNote` be constructed from the letters in `magazine` (each letter used at most once)? | Stock the letter counts from the magazine, then draw down for each note letter — if any count goes negative the magazine is short. | O(n) | O(1) | Standard |
| 387 | First Unique Character in a String | Return the index of the first non-repeating character. Return -1 if none exists. | One pass to count every letter, a second pass to return the first whose count is exactly 1. | O(n) | O(1) | Standard |
| 49 | Group Anagrams | Group strings that are anagrams of each other. | Anagrams share identical letter frequencies, so the frequency vector encoded as a string is a unique group key — O(k) to build vs O(k log k) to sort the characters. | O(nk) | O(n) | Standard |
| 451 | Sort Characters By Frequency | Sort characters in descending order of frequency. Ties can go in any order. | Frequencies are bounded by string length, so bucket chars by their count and read buckets high-to-low — no O(n log n) comparison sort needed. |  |  | Standard |
| 5 | Longest Palindromic Substring | Return the longest palindromic substring. | Every palindrome has a center; try all 2n-1 centers (each char and each gap) and grow outward while characters mirror. | O(n²) | O(1) | Standard |
| 647 | Palindromic Substrings | Count all palindromic substrings. | Same center-expansion, but each successful step outward is itself one more palindrome, so accumulate a count rather than a max. | O(n²) | O(1) | Standard |
| 8 | String to Integer (atoi) | Parse a string to an integer, handling leading spaces, optional sign, overflow, and non-digit stop. | Process the string in strict phases — spaces, then sign, then digits accumulated as `num*10 + digit` — clamping to int bounds the moment overflow would occur. | O(n) | O(1) | Standard |
| 14 | Longest Common Prefix | Find the longest common prefix string among an array of strings. | Start with the first string as the candidate prefix and trim its tail until every other string starts with it. | O(n·k) | O(1) | Standard |
| 443 | String Compression | Compress the char array in-place. Each group `aaa` becomes `a3`. Single chars stay as-is. Return new length. | Two pointers — read scans each run while write lays down the compressed `char + count` behind it; write never overtakes read, so it's safe in place. | O(n) | O(1) | Standard |
| 1047 | Remove All Adjacent Duplicates in String | Repeatedly remove adjacent equal characters until no more exist. | A stack mirrors the partially-cleaned string — if the next char equals the top it's an adjacent pair, so pop instead of pushing. | O(n) | O(n) | Standard |
| 6 | ZigZag Conversion | Convert a string into a zigzag pattern across `numRows` rows and read it row by row. | Walk the string once, appending each char to its current row's builder while bouncing the row index down then up. | O(n) | O(n) | Standard |
| 12 | Integer to Roman | Convert an integer to its Roman numeral representation (values 1–3999). | Greedily subtract the largest possible value (including the 4/9 subtractive pairs) and append its symbol. | O(1) | O(1) | Standard |
| 13 | Roman to Integer | Convert a Roman numeral string to an integer. | Add each symbol's value, but subtract instead when a smaller value precedes a larger one (subtractive notation). | O(n) | O(1) | Standard |
| 28 | Implement strStr() | Find the first occurrence of `needle` in `haystack`. Return -1 if not found. | Slide a window of needle's length across haystack and compare; the first full match wins. | O(n·m) | O(1) | Standard |
| 38 | Count and Say | Generate the nth term of the "count and say" sequence: read digits of the previous term aloud. | Starting from "1", repeatedly scan runs of equal digits and emit count followed by the digit. | O(n·m) | O(m) | Standard |
| 43 | Multiply Strings | Multiply two non-negative integers given as strings. Return the product as a string. | Schoolbook multiplication: digit i of num1 times digit j of num2 lands in result positions i+j and i+j+1. | O(n·m) | O(n+m) | Standard |
| 58 | Length of Last Word | Return the length of the last word in a string (word = max sequence of non-space chars). | Scan from the right: skip trailing spaces, then count letters until the next space. | O(n) | O(1) | Standard |
| 65 | Valid Number | Validate whether a string is a valid decimal number (integers, fractions, exponents). | A single left-to-right scan tracking whether we have seen a digit, a dot, and an exponent enforces all the ordering rules. | O(n) | O(1) | Standard |
| 68 | Text Justification | Format words into lines of `maxWidth`, fully justified (equal spaces, last line left-aligned). | Greedily pack as many words as fit per line, then distribute leftover spaces evenly between gaps (extras to the left); the last line is left-justified. | O(n·maxWidth) | O(n) | Standard |
| 125 | Valid Palindrome | Check if a string is a palindrome, ignoring non-alphanumeric characters and case. | Two pointers move inward, skipping non-alphanumeric chars and comparing lowercased letters. | O(n) | O(1) | Standard |
| 151 | Reverse Words in a String | Reverse the order of words in a string (split on spaces, handle multiple spaces). | Scan from the right, extract each word, and append them in reverse order with single spaces. | O(n) | O(n) | Standard |
| 161 | One Edit Distance | Determine if two strings are one edit distance apart (insert, delete, or replace one char). | Scan to the first mismatch; equal lengths force a replace, otherwise skip one char in the longer string and require the rest to match. | O(n) | O(n) | Standard |
| 163 | Missing Ranges | Given a sorted array, return missing ranges between `lower` and `upper` bounds. | Walk a running "next expected" value; whenever a number exceeds it, the gap before it is a missing range. | O(n) | O(1) | Standard |
| 165 | Compare Version Numbers | Compare two version number strings (dot-separated integers). Return -1, 0, or 1. | Parse both revisions position by position, treating missing components as 0, and compare numerically. | O(n) | O(n) | Standard |
| 166 | Fraction to Recurring Decimal | Convert a fraction numerator/denominator to a decimal string, noting repeating parts in parentheses. | Do long division; remember the position of each remainder so a repeat reveals the cycle to wrap in parentheses. | O(den) | O(den) | Standard |
| 179 | Largest Number | Arrange numbers so their concatenation forms the largest possible number. | Sort by a custom comparator that prefers the order producing a larger concatenation (a+b vs b+a). | O(n log n · k) | O(n) | Standard |
| 186 | Reverse Words in a String II | Reverse words in a character array in-place (words separated by spaces). | Reverse the whole array, then reverse each word back so the order flips but each word reads forward. | O(n) | O(1) | Standard |
| 205 | Isomorphic Strings | Check if two strings follow the same character-substitution pattern (isomorphic). | Maintain a bijective mapping both ways; any conflicting mapping breaks isomorphism. | O(n) | O(1) | Standard |
| 214 | Shortest Palindrome | Find the shortest palindrome by adding characters in front of a string. | Find the longest palindromic prefix via KMP failure on `s + '#' + reverse(s)`; reverse the leftover suffix and prepend it. | O(n) | O(n) | Standard |
| 228 | Summary Ranges | Given a sorted unique integer array, summarize consecutive runs as ranges. | Track the start of each consecutive run; when the run breaks, emit either a single number or a "start->end" range. | O(n) | O(1) | Standard |
| 246 | Strobogrammatic Number | Check if a number reads the same when rotated 180 degrees. | Two pointers move inward; each pair must be a valid strobogrammatic mapping (0-0, 1-1, 6-9, 8-8, 9-6). | O(n) | O(1) | Standard |
| 249 | Group Shifted Strings | Group strings that follow the same shift sequence (each char shifted by the same amount). | Encode each string by the gaps between consecutive chars (mod 26) so all members of a shift group share the same key. | O(n·k) | O(n·k) | Standard |
| 266 | Palindrome Permutation | Check if a string can be rearranged into a palindrome (at most one odd-count char). | A palindrome allows at most one character with an odd count; track parity with a set. | O(n) | O(1) | Standard |
| 271 | Encode and Decode Strings | Encode a list of strings to a single string and decode it back. | Length-prefix each string ("len#str") so the decoder always knows exactly how many chars to read, regardless of content. | O(n) | O(n) | Standard |
| 273 | Integer to English Words | Convert a non-negative integer to its English words representation. | Process the number in groups of three digits, naming each group and appending the right scale word (Thousand, Million, Billion). | O(1) | O(1) | Standard |
| 290 | Word Pattern | Check if a string `s` follows a given pattern (bijective character-to-word mapping). | Maintain a two-way mapping between pattern chars and words; any conflict breaks the bijection. | O(n) | O(n) | Standard |
| 299 | Bulls and Cows | Count bulls (right digit, right place) and cows (right digit, wrong place) in a number guessing game. | Count exact-position matches as bulls; for the rest, use a digit-count array where positive entries (secret surplus) and negative entries (guess surplus) reveal cows. | O(n) | O(1) | Standard |
| 344 | Reverse String | Reverse a character array in-place. | Two pointers swap from both ends moving inward. | O(n) | O(1) | Standard |
| 345 | Reverse Vowels of a String | Reverse only the vowels of a string. | Two pointers advance until each lands on a vowel, then swap those vowels. | O(n) | O(n) | Standard |
| 388 | Longest Absolute File Path | Find the length of the longest absolute file path in a file system string. | Tab depth gives the nesting level; keep a stack of path lengths per level and, on hitting a file (has a dot), compute the full path length. | O(n) | O(n) | Standard |
| 392 | Is Subsequence | Check if string `s` is a subsequence of string `t`. | Walk `t` with one pointer; advance the `s` pointer each time chars match. If `s` is exhausted, it is a subsequence. | O(n) | O(1) | Standard |
| 408 | Valid Word Abbreviation | Check if an abbreviation matches a word (digits represent skipped characters). | Walk both with pointers; on a digit, parse the skip count (no leading zero) and jump the word pointer; otherwise chars must match. | O(n) | O(1) | Standard |
| 409 | Longest Palindrome | Find the length of the longest palindrome that can be built from the given letters. | Use every pair of each letter; if any letter has a leftover single, one of them can sit in the center. | O(n) | O(1) | Standard |
| 415 | Add Strings | Add two non-negative integers given as strings. Return the sum as a string. | Add digit by digit from the right with a carry, exactly like grade-school addition. | O(max(n,m)) | O(max(n,m)) | Standard |
| 422 | Valid Word Square | Given a sequence of words, check whether they form a valid word square (kth row equals kth column). | For each cell (i,j), the char must equal the char at (j,i); guard against ragged rows by bounds-checking. | O(n·m) | O(1) | Standard |
| 423 | Reconstruct Original Digits from English | Given a scrambled string of digit-word letters, decode the original digits in order. | Some letters are unique to one digit (z→zero, w→two, u→four, x→six, g→eight); count those first, then peel off the remaining digits using letters that become unique after subtraction. | O(n) | O(1) | Standard |
| 434 | Number of Segments in a String | Count the number of segments (maximal runs of non-space chars) in a string. | A new segment starts at each non-space char whose predecessor is a space (or string start). | O(n) | O(1) | Standard |
| 459 | Repeated Substring Pattern | Check if a string can be built by repeating one of its substrings multiple times. | If `s` is a repeated pattern, it appears inside `(s+s)` with the first and last char removed. | O(n) | O(n) | Standard |
| 468 | Validate IP Address | Validate whether a string is a valid IPv4 or IPv6 address. | Dispatch on the separator: dots mean IPv4 (four 0–255 octets, no leading zeros), colons mean IPv6 (eight 1–4 hex groups). | O(n) | O(n) | Standard |
| 500 | Keyboard Row | Find all words that can be typed on a single row of a QWERTY keyboard. | Map each letter to its row index, then keep words whose letters all share one row. | O(n·k) | O(n) | Standard |
| 520 | Detect Capital | Check if a word is capitalized correctly (all caps, all lower, or first letter only). | Count uppercase letters: valid only if all are uppercase, none are, or exactly the first one is. | O(n) | O(1) | Standard |
| 524 | Longest Word in Dictionary through Deleting | Find the longest word in a dictionary that is a subsequence of string `s` (smallest lexicographically on ties). | Check each candidate with the subsequence two-pointer, keeping the best by length then lexicographic order. | O(n·k) | O(1) | Standard |
| 541 | Reverse String II | Reverse the first `k` characters of every `2k`-character block in a string. | Step through the array in `2k` jumps, reversing the first `k` chars of each block (or all that remain). | O(n) | O(n) | Standard |
| 551 | Student Attendance Record I | Check if a record is award-eligible (fewer than 2 absences total, no 3 consecutive lates). | Count total absences and track the current run of lates; fail on the second absence or third consecutive late. | O(n) | O(1) | Standard |
| 556 | Next Greater Element III | Find the next greater number by rearranging the digits of `n`. Return -1 if none or on overflow. | Standard next-permutation on digits: find the rightmost ascending pair, swap with the next larger digit to its right, reverse the suffix. | O(d) | O(d) | Standard |
| 557 | Reverse Words in a String III | Reverse individual words in a string while preserving word order. | Split on spaces, reverse each word, and rejoin with single spaces. | O(n) | O(n) | Standard |
| 592 | Fraction Addition and Subtraction | Add or subtract a sequence of fractions, returning the result in lowest terms. | Parse each signed fraction, accumulate over a common denominator, then reduce by the GCD. | O(n) | O(1) | Standard |
| 616 | Add Bold Tag in String | Wrap every substring of `s` that matches a word in the dictionary with `<b>...</b>`, merging overlaps. | Mark every covered index in a boolean array, then emit bold tags around maximal marked runs. | O(n·m) | O(n) | Standard |
| 657 | Robot Return to Origin | Check if a robot following an instruction string (UDLR) returns to the origin. | Track net horizontal and vertical displacement; the robot returns only if both are zero. | O(n) | O(1) | Standard |
| 670 | Maximum Swap | Swap two digits at most once to get the maximum possible value. | Record the last index of each digit; scanning left to right, swap the first digit with the largest later digit that exceeds it. | O(d) | O(1) | Standard |
| 680 | Valid Palindrome II | Check if a string is a palindrome after deleting at most one character. | Two pointers inward; at the first mismatch, try skipping either the left or right char and check the remainder. | O(n) | O(1) | Standard |
| 681 | Next Closest Time | Find the next closest valid time using only the digits present in a given time string. | From the current minute, advance one minute at a time and return the first time whose digits are all in the allowed set. | O(1) | O(1) | Standard |
| 686 | Repeated String Match | Find the minimum number of times string `a` must repeat so `b` is a substring. Return -1 if impossible. | Repeat `a` until its length covers `b`, then check one extra copy to handle offset overlap. | O(n·m) | O(n) | Standard |
| 709 | To Lower Case | Convert a string to lowercase. | Uppercase ASCII letters differ from lowercase by 32, so shift any A–Z char. | O(n) | O(n) | Standard |
| 726 | Number of Atoms | Parse a chemical formula string and return atom counts in sorted order. | Recursive-descent style parse with a stack of count maps for parentheses; multiply a group's counts by the number following its closing paren. | O(n) | O(n) | Standard |
| 748 | Shortest Completing Word | Find the shortest word in a list that contains all letters of a license plate (case-insensitive, with multiplicity). | Build the plate's letter-count vector, then keep the shortest word whose own counts cover it. | O(n·k) | O(1) | Standard |
| 788 | Rotated Digits | Count numbers in `[1, n]` that become a different valid number when each digit is rotated 180 degrees. | A number is "good" if all digits are valid rotations and at least one digit (2,5,6,9) actually changes. | O(n·d) | O(1) | Standard |
| 791 | Custom Sort String | Sort string `s` so its characters appear in the order given by string `order`. | Count chars in `s`, emit them in `order`'s sequence, then append any chars not mentioned in `order`. | O(n) | O(n) | Standard |
| 794 | Valid Tic-Tac-Toe State | Decide whether the given tic-tac-toe board is reachable from valid play. | Count X and O; X count must equal O or be one more, and if a player has won the move counts must be consistent (both can't win). | O(1) | O(1) | Standard |
| 796 | Rotate String | Check if string `t` is a rotation of string `s`. | Every rotation of `s` is a substring of `s+s`, so check containment after a length match. | O(n²) | O(n) | Standard |
| 809 | Expressive Words | Determine how many query words match a stretched version of `s` (groups stretched to length ≥ 3). | Compare run lengths group by group: the stretched group must be ≥ 3, or equal to the original run length. | O(n·k) | O(1) | Standard |
| 824 | Goat Latin | Convert words to Goat Latin: append "ma" (plus per-word index of 'a's); move leading consonants to the end for non-vowel words. | For each word, decide vowel vs consonant start, transform, then append "ma" and i+1 trailing 'a's. | O(n) | O(n) | Standard |
| 833 | Find And Replace in String | Apply non-overlapping indexed replacements: at each index, if `sources[k]` matches, replace it with `targets[k]`. | Map each start index to its replacement; rebuild the string, jumping over matched sources and copying unmatched chars verbatim. | O(n) | O(n) | Standard |
| 859 | Buddy Strings | Check if two strings are "buddy strings": swapping exactly one pair of chars makes them equal. | Equal length is required; if the strings are identical, you need a duplicate char to swap; otherwise exactly two positions must differ and be mirror images. | O(n) | O(1) | Standard |
| 953 | Verifying an Alien Dictionary | Check if words are sorted in a given alien language's alphabetical order. | Map each letter to its rank, then verify each adjacent pair is in non-decreasing order under that ranking. | O(n·k) | O(1) | Standard |
| 1055 | Shortest Way to Form String | Find the minimum number of subsequences of `source` whose concatenation equals `target`. Return -1 if impossible. | Greedily consume as much of `target` as possible from each pass over `source`; if a pass makes no progress, a needed char is missing. | O(n·m) | O(1) | Standard |
| 1108 | Defanging an IP Address | Defang an IP address by replacing each '.' with '[.]'. | Append each char, expanding dots into the bracketed form. | O(n) | O(n) | Standard |
| 1221 | Split a String in Balanced Strings | Find the maximum number of balanced strings ('R' count == 'L' count) to split into. | Track a running balance; every time it returns to zero a balanced piece has closed. | O(n) | O(1) | Standard |
| 1328 | Break a Palindrome | Break a palindrome by changing one character to get the lexicographically smallest non-palindrome. | Change the first non-'a' in the first half to 'a'; if all are 'a', change the last char to 'b'. Single-char strings can't be broken. | O(n) | O(n) | Standard |
| 1392 | Longest Happy Prefix | Find the longest happy prefix (a non-empty prefix that is also a suffix). | The KMP failure value at the last index is exactly the length of the longest proper prefix that is also a suffix. | O(n) | O(n) | Standard |
| 1446 | Consecutive Characters | Find the maximum number of consecutive same characters in a string (the "power" of the string). | Track the current run length, resetting on a change, and keep the maximum seen. | O(n) | O(1) | Standard |
| 1554 | Strings Differ by One Character | Check if any two strings in a list differ by exactly one character (same length, same position). | For each position, hash each word with that position wildcarded; a collision among same-length words means they differ in only that spot. | O(n·m²) | O(n·m) | Standard |
| 1556 | Thousand Separator | Format an integer with a dot as the thousands separator. | Build the result from the right, inserting a separator after every three digits. | O(d) | O(d) | Standard |
| 1736 | Latest Time by Replacing Hidden Digits | Find the latest valid time by replacing each '?' with an appropriate digit. | Greedily choose the largest valid digit at each '?' position, respecting hour (≤ 23) and minute (≤ 59) constraints. | O(1) | O(1) | Standard |
| 1816 | Truncate Sentence | Truncate a sentence to its first `k` words. | Copy chars until the (k)th space is reached. | O(n) | O(n) | Standard |
| 1844 | Replace All Digits with Characters | Replace each digit at an odd index with the letter shifted from the preceding char by that digit. | Even indices are letters; for each odd index, shift the previous letter forward by the digit's value. | O(n) | O(n) | Standard |

---

### Core Idioms

```java
// MENTAL MODEL: a lowercase string is a length-26 frequency vector; most string problems are vector ops on it.
// WHEN: "anagram", "char count", "group by letters", "first unique", "sort by frequency".
// 1. CHAR COUNT — lowercase letters
int[] count = new int[26];
// WHY ch - 'a': ASCII 'a'=97, so 'a'→0, 'b'→1, ..., 'z'→25 — a clean 0–25 bucket index into count[].
for (char ch : s.toCharArray()) count[ch - 'a']++;     // ← ch - 'a' maps a→0, b→1, ..., z→25

// 2. CHAR COUNT — digits 0–9
int[] count = new int[10];
for (char ch : s.toCharArray()) count[ch - '0']++;     // ← ch - '0' maps '0'→0, '9'→9

// 3. CHAR TO INTEGER — build number digit by digit
int num = 0;
for (int i = 0; i < s.length(); i++)
    num = num * 10 + (s.charAt(i) - '0');              // ← shift left × 10, add new digit

// 4. ANAGRAM HASH KEY — frequency-based (bucket sort style) O(k) vs sort O(k log k)
// WHY it works: anagrams share identical letter frequencies, so encoding the frequency vector
//   ITSELF gives a unique key for the whole group — O(k) to build vs O(k log k) to sort the chars.
String hashKey(String s) {
    int[] count = new int[26];
    for (char ch : s.toCharArray()) count[ch - 'a']++;
    StringBuilder builder = new StringBuilder();
    for (int i = 0; i < 26; i++) {
        builder.append((char)('a' + i));                    // ← letter as label
        builder.append(count[i]);                           // ← its count
    }
    return builder.toString();                              // e.g., "a2b0c1...z0"
}
// Alternative: sort the characters (simpler, slightly slower)
char[] chars = s.toCharArray();
Arrays.sort(chars);
String key = new String(chars);                        // anagrams → same sorted key

// 5. BUCKET SORT — sort by frequency without comparison sort
int[] count = new int[128];                            // ASCII
for (char ch : s.toCharArray()) count[ch]++;
List<Character>[] buckets = new List[s.length() + 1]; // index = frequency
for (int i = 0; i < 128; i++) {
    if (count[i] > 0) {
        int freq = count[i];
        if (buckets[freq] == null) buckets[freq] = new ArrayList<>();
        buckets[freq].add((char) i);
    }
}
StringBuilder builder = new StringBuilder();
for (int freq = buckets.length - 1; freq > 0; freq--) {    // ← descending frequency
    if (buckets[freq] == null) continue;
    for (char ch : buckets[freq])
        for (int i = 0; i < freq; i++) builder.append(ch);
}

// 6. EXPAND FROM CENTER — palindrome check in O(1) space
int expand(String s, int i, int j) {          // i == j: odd length; i+1 == j: even length
    while (i >= 0 && j < s.length() && s.charAt(i) == s.charAt(j)) { i--; j++; }
    return j - i - 1;                         // ← length of palindrome found
}
```

---

### Template

```java
// Call for each center: odd-length palindromes (i == i) and even-length (i, i+1)
for (int i = 0; i < s.length(); i++) {
    // odd:  single center at i
    // even: center between i and i+1
    processExpansion(s, i, i);     // odd
    processExpansion(s, i, i + 1); // even
}

// Shared expand helper — returns length of palindrome
int expand(String s, int i, int j) {
    while (i >= 0 && j < s.length() && s.charAt(i) == s.charAt(j)) { i--; j++; }
    return j - i - 1;
}
```

---

### String Idioms Cheat Sheet

```java
// Char ↔ index
'a' + i             // int → char (i=0→'a', i=25→'z')
ch - 'a'            // char → index (a→0, z→25)
ch - '0'            // char → digit (0→0, 9→9)
Character.isDigit(ch)
Character.isLetter(ch)
Character.toLowerCase(ch)

// String operations
s.charAt(i)                          // char at index
s.toCharArray()                      // → char[]
new String(charArray)                // char[] → String
String.valueOf(charArray)            // char[] → String
s.substring(i, j)                    // [i, j)
s.contains(sub)                      // boolean
s.startsWith(prefix)                 // boolean
s.split("\\s+")                      // split on whitespace

// Building strings
StringBuilder builder = new StringBuilder();
builder.append(ch);        builder.append(str);
builder.deleteCharAt(i);
builder.reverse();
builder.toString();
String.join(", ", list)              // join with delimiter

// computeIfAbsent — key pattern for grouping
map.computeIfAbsent(key, k -> new ArrayList<>()).add(value);
```

### Pattern Chooser

| Signal | Pattern |
|---|---|
| Are two strings anagrams? | Count array: fill from s, drain from t |
| Group strings by anagram | Frequency hash key (`hashKey`) or `Arrays.sort` key |
| Sort/rank by character frequency | Bucket sort: count[], then buckets[freq] |
| Longest/count palindromic substrings | Expand from center (i,i) odd + (i,i+1) even |
| Parse a number from string | `num = num * 10 + (ch - '0')` |
| Remove adjacent duplicate pairs | Stack: push, pop on match |
| Sliding window over characters | See `sliding_window.md` |

---
## Stack / Queue / Heap  &nbsp;`stack_queue.md`

Four data structures — each with a canonical template and representative problems.

---

### Quick Reference Table

| # | Name | Description | Intuition | Time | Space | Key Implementation |
|---|---|---|---|---|---|---|
| 20 | Valid Parentheses | Given a string of brackets `()[]{}`, return true if all brackets are properly closed and ordered. | the most recent unmatched open bracket is the only one a closing bracket can legally match — that is exactly LIFO. | O(n) | O(n) | Standard |
| 155 | Min Stack | Design a stack that supports push, pop, top, and `getMin()` in O(1). |  | O(1) per operation | O(n) | Standard |
| 394 | Decode String | Decode a string like `"3[a2[bc]]"` → `"abcbcabcbc"`. |  | O(n) (n = length of decoded output) | O(n) | Standard |
| 739 | Daily Temperatures | For each day, how many days until a warmer temperature? Return 0 if none. | a colder day just waits on the stack until the first warmer day arrives and resolves it. | O(n) | O(n) | Standard |
| 496 | Next Greater Element I | For each element in `nums1` (a subset of `nums2`), find the first greater element to its right in `nums2`. Return -1 if none. |  | O(m + n) | O(n) | Standard |
| 84 | Largest Rectangle in Histogram | Find the largest rectangle that can be formed within the histogram bars. | a bar can only stretch sideways until it hits a shorter bar; the stack remembers each bar's left limit so the right limit (current shorter bar) closes the rectangle. | O(n) | O(n) | Standard |
| 42 | Trapping Rain Water | How much water can be trapped between the bars after rain? | water sits in a dip between a left wall and a right wall, and its depth is set by whichever wall is shorter. | O(n) | O(n) | Standard |
| 239 | Sliding Window Maximum | Return the maximum in each sliding window of size k. | any element smaller than a newer element can never be the window max again, so discard it; the front always holds the current best. | O(n) | O(k) | Standard |
| 1046 | Last Stone Weight | Smash the two heaviest stones repeatedly. Return the last remaining weight (or 0). |  | O(n log n) | O(n) | Standard |
| 347 | Top K Frequent Elements | Return the k most frequent elements. |  | O(n log k) | O(n) | Standard |
| 295 | Find Median from Data Stream | Add integers to a stream and find the median at any time in O(log n) add and O(1) find. | keep the smaller half and larger half balanced; the median always lives right at the boundary, on the tops of the two heaps. | O(log n) addNum, O(1) findMedian | O(n) | Standard |
| 502 | IPO | Before each project you must have enough capital. Start with capital `w`. Pick at most `k` projects to maximize final capital. |  | O(n log n) | O(n) | Standard |
| 767 | Reorganize String | Rearrange characters so no two adjacent characters are the same. Return `""` if impossible. |  | O(n log k) (k = distinct chars ≤ 26) | O(k) | Standard |
| 503 | Next Greater Element II | Given a circular integer array, return the next greater number for every element. The next greater number of an element is the first greater number found by traversing the array circularly. |  | O(n) | O(n) | Monotone decreasing stack. Iterate through the array TWICE (indices 0 to 2n-1, using `i % n`). Only push index `i` onto the stack during the first pass (`i < n`) to avoid duplicates. |
| 85 | Maximal Rectangle | Given a binary matrix filled with 0s and 1s, find the largest rectangle containing only 1s and return its area. |  | O(m·n) | O(n) | For each row, compute cumulative histogram heights (1s stack vertically). Then apply the Largest Rectangle in Histogram algorithm (#84) on each row's histogram. |
| 224 | Basic Calculator | Evaluate a string expression containing `+`, `-`, `(`, `)`, digits, and spaces. |  | O(n) | O(n) | When encountering `(`, push current (result, sign) onto stack and reset. When encountering `)`, combine current result with the saved result and sign from the stack. |
| 227 | Basic Calculator II | Evaluate a string expression with `+`, `-`, `*`, `/` and integers (no parentheses). |  | O(n) | O(n) | Process operator BEFORE the current number. Push positive/negative numbers for `+`/`-`. For `*`/`/`, immediately multiply/divide the top of the stack. Sum the stack at the end. |
| 378 | Kth Smallest Element in a Sorted Matrix | Given an n×n matrix where each row and column is sorted in ascending order, return the kth smallest element. |  | O(n log(max-min)) | O(1) | Binary search on the VALUE range [matrix[0][0], matrix[n-1][n-1]]. For a given `mid`, count elements ≤ mid by scanning from the bottom-left corner: if `matrix[row][col] <= mid`, all `row+1` elements in this column (0..row) are ≤ mid. |
| 373 | Find K Pairs with Smallest Sums | Given two sorted arrays `nums1` and `nums2`, return the `k` pairs `(u, v)` (one from each) with the smallest sums. |  | O(k log k) | O(k) | Seed min-heap with `(nums1[i], nums2[0])` for i = 0..min(k, n1.length)-1. On each pop, if `j+1 < nums2.length`, push `(nums1[i], nums2[j+1])`. This expands row-by-row in the implicit pair matrix. |
| 621 | Task Scheduler | Given a list of tasks (characters) and a cooldown `n`, return the minimum number of intervals to finish all tasks. Between two same tasks there must be at least `n` intervals. |  | O(k) | O(1) | Greedy formula. Find the most frequent task (maxFreq). It creates `maxFreq - 1` "frames" of `n + 1` slots, plus `maxCount` (count of tasks with maxFreq) slots. The answer is `max(tasks.length, (maxFreq - 1) * (n + 1) + maxCount)`. |
| 358 | Rearrange String k Distance Apart | Rearrange a string so that the same characters are at least `k` distance apart. Return "" if impossible. |  | O(n log k) | O(k) | greedy with a max-heap by frequency plus a cooldown queue of size k that holds recently used characters until they're eligible again. |
| 480 | Sliding Window Median | Return the median of every window of size k as it slides across the array. |  | O(n·k) with heap remove (O(n log k) with indexed sets) | O(k) | two heaps (maxHeap = lower half, minHeap = upper half) with lazy deletion — defer removing elements that left the window, tracking balance with counts. |
| 692 | Top K Frequent Words | Return the k most frequent words. Sort by frequency descending; ties broken by lexicographic order. |  | O(n log k) | O(n) | min-heap of size k ordered so the "smallest" (lowest freq, or same freq with lexicographically larger word) sits on top for eviction. |
| 772 | Basic Calculator III | Evaluate an arithmetic expression with `+`, `-`, `*`, `/`, and parentheses. |  | O(n) | O(n) | combines #224 (parentheses via recursion) and #227 (operator precedence: apply `*`/`/` immediately, defer `+`/`-`). |
| 32 | Longest Valid Parentheses | Find the length of the longest valid (well-formed) parentheses substring. | push indices onto a stack; the bottom of the stack is always the index just before the current valid run, so the gap to it gives the run length. | O(n) | O(n) | Standard |
| 71 | Simplify Path | Simplify an absolute Unix file path (handle `.`, `..`, multiple slashes). | split on `/` and treat directories as a stack — `..` pops the last directory, `.` and empty tokens are ignored. | O(n) | O(n) | Standard |
| 150 | Evaluate Reverse Polish Notation | Evaluate a Reverse Polish Notation expression with `+`, `-`, `*`, `/`. | push operands; on an operator pop the two most recent operands, apply, and push the result back — exactly LIFO. | O(n) | O(n) | Standard |
| 215 | Kth Largest Element in an Array | Find the kth largest element in an unsorted array (not necessarily distinct). | a min-heap of size k keeps the k largest seen so far; its top is the kth largest. | O(n log k) | O(k) | Standard |
| 218 | The Skyline Problem | Given building rectangles, return the skyline as a list of key points. | sweep left to right over building edges; a max-heap of active heights tracks the tallest standing building, and a key point is emitted whenever that maximum changes. | O(n^2) (heap remove) | O(n) | Standard |
| 225 | Implement Stack using Queues | Implement a LIFO stack using only queue operations. | after each push, rotate the queue so the newest element sits at the front — then `poll`/`peek` behave like stack `pop`/`top`. | O(n) push, O(1) others | O(n) | Standard |
| 232 | Implement Queue using Stacks | Implement a queue using two stacks. | one stack receives pushes, the other serves pops; moving elements over reverses their order, restoring FIFO. Amortized O(1) per element. | O(1) amortized | O(n) | two stacks emulate FIFO |
| 316 | Remove Duplicate Letters | Remove duplicate letters so each appears once, result is lexicographically smallest. | monotone increasing stack of letters — pop a larger letter when a smaller one arrives, but only if the popped letter appears again later (so we can re-add it). | O(n) | O(1) (26 letters) | Standard |
| 402 | Remove K Digits | Remove k digits from a number string to get the smallest possible number. | monotone increasing stack of digits — whenever a smaller digit arrives, pop larger preceding digits (each pop is one removal) so high places hold the smallest digits. | O(n) | O(n) | Standard |
| 456 | 132 Pattern | Check if a 1-3-2 pattern exists in an integer array. |  | O(n) | O(n) | scan right to left with a monotone decreasing stack; pop to track the largest value that is still smaller than some element to its right (the "2"). If a later element is below that "2", a 132 pattern exists. |
| 506 | Relative Ranks | Assign ranks ("Gold Medal", "Silver Medal", "Bronze Medal", then 4, 5, ...) to athletes by score. | a max-heap of (score, index) pops athletes in descending score order, so each pop assigns the next rank back to its original position. | O(n log n) | O(n) | Standard |
| 636 | Exclusive Time of Functions | Given a log of function start/end times, compute exclusive time per function. | a call stack mirrors execution; when a new call starts, the currently running function pauses (accumulate its slice), and when a call ends, the resumed parent restarts its clock. | O(L) (L = number of logs) | O(n) | Standard |
| 678 | Valid Parenthesis String | Check if a string with `(`, `)`, `*` (wildcard) can be a valid parenthesis string. |  | O(n) | O(1) | track a range `[low, high]` of possible open-paren counts; `*` widens the range (could be `(`, `)`, or empty). Valid iff the range can return to 0 and never goes negative. |
| 703 | Kth Largest Element in a Stream | Design a class to find the kth largest element in a stream. | a min-heap capped at size k always holds the k largest seen; its top is the running kth largest. | O(log k) per add | O(k) | Standard |
| 716 | Max Stack | Design a stack with push, pop, top, getMax, and popMax operations. |  | O(n) popMax, O(1) others | O(n) | mirror an auxiliary `maxStack` (like #155). `popMax` pops down to the max into a temp buffer, removes it, then pushes the buffer back — re-establishing both stacks. |
| 735 | Asteroid Collision | Simulate asteroids moving in a row: right-moving collide with left-moving. | a stack holds surviving asteroids; a left-moving asteroid only collides with a right-moving one on top, resolving collisions repeatedly until it survives, explodes, or the stack clears. | O(n) | O(n) | Standard |
| 759 | Employee Free Time | Find the free time intervals common to all employees given their schedules. | flatten all intervals, sort by start, then sweep tracking the furthest end seen so far; any gap between that end and the next start is common free time. | O(n log n) | O(n) | Standard |
| 844 | Backspace String Compare | Check if two strings are equal after processing `#` as backspace. | build each string with a stack where `#` pops the last character, then compare the resulting stacks. | O(n) | O(n) | Standard |
| 856 | Score of Parentheses | Calculate the score of a valid parentheses string (empty=0, AB=A+B, (A)=2A or 1 if empty). |  | O(n) | O(n) | stack holds the accumulated score at each depth; push 0 on `(`, and on `)` collapse the inner score (`max(2*inner, 1)`) into the parent frame. |
| 862 | Shortest Subarray with Sum at Least K | Find the length of the shortest subarray with sum at least k (k can be negative). |  | O(n) | O(n) | monotone increasing deque over prefix sums — pop from the front when a window qualifies, and from the back when a newer prefix is smaller (dominating older larger ones). |
| 907 | Sum of Subarray Minimums | Find the sum of subarray minimums for all subarrays. |  | O(n) | O(n) | monotone increasing stack — for each element as the minimum, count subarrays via distance to the previous strictly-smaller and next smaller-or-equal element, then weight by the value. |
| 921 | Minimum Add to Make Parentheses Valid | Find the minimum additions to make a parentheses string valid. | track open parentheses as a counter (stack of size); each unmatched `)` needs an added `(`, and leftover `(` each need a `)`. | O(n) | O(1) | Standard |
| 946 | Validate Stack Sequences | Check if a sequence can be produced by a series of push-pop operations on a stack. | simulate — push each value, then greedily pop whenever the stack top matches the next expected popped value. If everything pops, the sequence is valid. | O(n) | O(n) | Standard |
| 973 | K Closest Points to Origin | Find the k points closest to the origin. | a max-heap of size k keyed on squared distance keeps the k closest seen; evict the farthest whenever the heap overflows. | O(n log k) | O(k) | Standard |
| 1086 | High Five | For each student, compute the average of their top five scores. | keep a min-heap of size 5 per student so only their five highest scores remain, then average those. | O(n log 5) | O(n) | Standard |
| 1190 | Reverse Substrings Between Each Pair of Parentheses | Reverse the substrings between each pair of parentheses (innermost first). |  | O(n^2) | O(n) | stack of builders — push current builder on `(`; on `)` reverse the inner builder and append it to the parent frame. |
| 1209 | Remove All Adjacent Duplicates in String II | Remove all adjacent duplicates of length k in a string repeatedly. |  | O(n) | O(n) | stack of (char, count) pairs — increment the top's count on a repeat, and pop the frame once its count reaches k. |
| 1249 | Minimum Remove to Make Valid Parentheses | Remove the minimum number of parentheses to make the string valid. |  | O(n) | O(n) | stack stores indices of unmatched `(`; a `)` with no match is marked for removal, and any `(` left on the stack at the end is also removed. |
| 1337 | The K Weakest Rows in a Matrix | Find the k weakest rows in a matrix (fewest soldiers, ties broken by row index). |  | O(m·n + m log k) | O(k) | max-heap of size k keyed on (soldier count, row index) so the strongest qualifying row sits on top for eviction; the remaining k are the weakest. |
| 1541 | Minimum Insertions to Balance a Parentheses String | Find the minimum insertions to make a string balanced (every `(` needs two `)`). |  | O(n) | O(1) | counter-style stack tracking open `(`; each `(` demands two `)`. Handle `)` carefully since they come in pairs, inserting a `)` when only one is available. |
| 1614 | Maximum Nesting Depth of the Parentheses | Find the maximum nesting depth of parentheses in a string. | the stack depth equals the current nesting level; track a running counter for `(`/`)` and record its peak. | O(n) | O(1) | Standard |
| 1792 | Maximum Average Pass Ratio | Maximize the average pass ratio by adding extra students optimally. |  | O((n + extra) log n) | O(n) | max-heap keyed on the marginal gain from adding one student to a class; greedily assign each extra student where it helps most, then push the updated gain back. |
| 1944 | Number of Visible People in a Queue | Count the number of people each person can see in a queue (taller blocks view). |  | O(n) | O(n) | monotone decreasing stack scanned right to left; pop shorter people (each is visible) until a taller one blocks the view — that taller person is visible too. |
| 1985 | Find the Kth Largest Integer in the Array | Find the kth largest integer in an array of number strings. |  | O(n log k) | O(k) | min-heap of size k comparing the numeric strings by length first, then lexicographically (so big-integer values compare correctly without overflow). |

---

### All Templates

```java
// 1. STACK (LIFO) — use ArrayDeque, not Stack class
Deque<Integer> stack = new ArrayDeque<>();
stack.push(x);     // add to top
stack.pop();       // remove from top
stack.peek();      // view top, no remove

// 2A. MONOTONE DECREASING STACK — next GREATER element
// MENTAL MODEL: keep only candidates still waiting for a bigger neighbor; current resolves them all.
// WHEN: "next/previous greater element", "warmer/taller to the right"
// Invariant: stack values decrease from bottom to top
// Pop when current is GREATER than top → top found its next greater
Deque<Integer> stack = new ArrayDeque<>();  // stores indices
for (int i = 0; i < n; i++) {
    while (!stack.isEmpty() && nums[stack.peek()] < nums[i])
        result[stack.pop()] = nums[i];     // nums[i] is next greater for popped index
    stack.push(i);
}
// Remaining in stack: no next greater element exists

// 2B. MONOTONE INCREASING STACK — next SMALLER element / span width
// MENTAL MODEL: each popped bar's reach extends until something shorter blocks it on both sides.
// WHEN: "largest rectangle", "trapped water", "span/width bounded by smaller elements"
// Invariant: stack values increase from bottom to top
// Pop when current is SMALLER than top → use popped index to compute width/span
Deque<Integer> stack = new ArrayDeque<>();  // stores indices
for (int i = 0; i < n; i++) {
    while (!stack.isEmpty() && nums[stack.peek()] > nums[i]) {
        int height = nums[stack.pop()];
        int width  = stack.isEmpty() ? i : i - stack.peek() - 1;  // span between boundaries
        // process height * width
    }
    stack.push(i);
}

// 3. MONOTONE DEQUE — sliding window max/min
// MENTAL MODEL: the front is the current window's answer; anything a newer-and-bigger value beats is dead weight.
// WHEN: "max/min of every window of size k"
// Deque stores INDICES; values at those indices are decreasing front-to-back (for max)
Deque<Integer> queue = new ArrayDeque<>();
for (int i = 0; i < n; i++) {
    while (!queue.isEmpty() && nums[queue.peekLast()] <= nums[i])
        queue.pollLast();               // remove smaller elements — they can never be window max
    queue.offerLast(i);
    if (queue.peekFirst() < i - k + 1) queue.pollFirst();  // evict out-of-window elements
    if (i >= k - 1) result[i - k + 1] = nums[queue.peekFirst()];
}

// 4. PRIORITY QUEUE
PriorityQueue<Integer> minPQ = new PriorityQueue<>();                      // min-heap (default)
PriorityQueue<Integer> maxPQ = new PriorityQueue<>(Collections.reverseOrder()); // max-heap
PriorityQueue<int[]>    pq   = new PriorityQueue<>((a, b) -> a[1] - b[1]); // custom: sort by index 1
pq.offer(x);   // add
pq.poll();     // remove and return min/max
pq.peek();     // view min/max without removing

// 5. TWO HEAPS — maintain median in O(log n)
// MENTAL MODEL: split the data at the median; the median is always sitting on the two heaps' tops.
// WHEN: "running median", "median of a data stream"
// maxHeap = lower half (smaller numbers), minHeap = upper half (larger numbers)
// Invariant: maxHeap.size() == minHeap.size() or maxHeap.size() == minHeap.size() + 1
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
void addNum(int num) {
    maxHeap.offer(num);
    minHeap.offer(maxHeap.poll());              // push one to minHeap (possibly num itself)
    if (maxHeap.size() < minHeap.size())
        maxHeap.offer(minHeap.poll());          // rebalance: maxHeap always ≥ minHeap in size
}
double findMedian() {
    return maxHeap.size() > minHeap.size()
        ? maxHeap.peek()
        : (maxHeap.peek() + minHeap.peek()) / 2.0;
}
```

---

### Decreasing vs Increasing

```
DECREASING stack (pop when current > top):     finds NEXT GREATER element for each popped index
INCREASING stack (pop when current < top):     finds NEXT SMALLER element — used for span width

Both store INDICES (not values) so you can compute distances and widths.
```

---

### Structure Chooser

| Goal | Structure | Why |
|---|---|---|
| Next greater/smaller element | Monotone stack | O(n) total — each element pushed/popped once |
| Sliding window max/min | Monotone deque | Front = window extreme; stale indices evicted |
| Global min/max, k-th element | PriorityQueue | O(log n) per op |
| Running median | Two heaps | Split at median; each heap half is O(log n) |
| O(1) stack minimum | Aux min-stack | Mirror min value at every level |
| Nested structure (brackets, k-repeats) | Two stacks | One for counts, one for strings |

### Deque API Cheat Sheet

**One class, three roles.** `ArrayDeque` adds/removes at *both* ends, so stack, queue, and deque are just usage patterns of the same structure — the only difference is **which end you remove from**. Always declare it `Deque<Integer> queue = new ArrayDeque<>();` (never the legacy `Stack` class, which is synchronized and `Vector`-backed; and `ArrayDeque` beats `LinkedList` as a queue). Name the variable for the *role* it plays (`stack` / `queue`).

```
        addFirst / push                          addLast / offer
              ↓                                       ↓
            [ FRONT ............................. BACK ]
              ↑                                       ↑
        pollFirst / pop                          pollLast

STACK (LIFO): add + remove at FRONT  → newest out first
QUEUE (FIFO): add at BACK, remove at FRONT → oldest out first
```

| Intent | Stack (LIFO) | Queue (FIFO) |
|---|---|---|
| Add | `push(x)` → `addFirst` | `offer(x)` → `addLast` |
| Remove | `pop()` → `removeFirst` | `poll()` → `removeFirst` |
| Peek | `peek()` → `peekFirst` | `peek()` → `peekFirst` |

Both **remove from the front** — the discipline comes from *where you add*: stack adds to the front (so newest is popped = LIFO), queue adds to the back (so oldest is polled = FIFO).

```java
Deque<Integer> queue = new ArrayDeque<>();

// As STACK (LIFO):    push()/pop()/peek()  → operate on FRONT
queue.push(x);    // = offerFirst
queue.pop();      // = pollFirst
queue.peek();     // = peekFirst

// As QUEUE (FIFO):   offer()/poll()/peek() → back-in, front-out
queue.offerLast(x);
queue.pollFirst();
queue.peekFirst();

// As DEQUE:          explicit first/last (e.g. monotone sliding-window)
queue.offerFirst(x);  queue.pollFirst();  queue.peekFirst();
queue.offerLast(x);   queue.pollLast();   queue.peekLast();
```

---
## BFS (Tree)  &nbsp;`bfs.md`

Core structure: `Queue<TreeNode> queue = new ArrayDeque<>()`.  
The only decision: do you need to know **which level** a node is on?

---

### The Two Templates

```java
// 1. LEVEL-AWARE PROCESSING — snapshot size to make per-level decisions
// MENTAL MODEL: the queue holds exactly one full level; freeze its size, then drain just that many.
// WHEN: "level by level", "per row", "rightmost/leftmost in level", "min depth"
Queue<TreeNode> queue = new ArrayDeque<>();
queue.offer(root);
int level = 0;
while (!queue.isEmpty()) {
    int size = queue.size();       // ← snapshot: all nodes currently in queue = this level
    level++;
    for (int i = 0; i < size; i++) {
        TreeNode node = queue.poll();
        // process node (know: level, i==0 → first, i==size-1 → last)
        if (node.left  != null) queue.offer(node.left);
        if (node.right != null) queue.offer(node.right);
    }
}

// 2. WITHOUT LEVEL TRACKING — simple node-by-node
// MENTAL MODEL: just visit every node in BFS order; you don't care which level it's on.
Queue<TreeNode> queue = new ArrayDeque<>();
queue.offer(root);
while (!queue.isEmpty()) {
    TreeNode node = queue.poll();
    // process node
    if (node.left  != null) queue.offer(node.left);
    if (node.right != null) queue.offer(node.right);
}
```

Almost all tree BFS problems use **Template 1** — you nearly always need `size` to know when a level ends.

### When to Use — Signal → Pattern

| Problem signal phrase | Pattern / group |
|---|---|
| "level order", "values per level", "each row" | Group 1 — collect entire level |
| "average / max / sum of each level" | Group 2 — aggregate per level |
| "right side view" (last in level), "bottom-left" (first in level) | Group 2 — record boundary node (`i==size-1` / `i==0`) |
| "minimum depth", "first level that satisfies X" | Group 3 — early return on condition |
| "connect next pointers at the same level" | Group 4 — wire nodes within a level |
| "same depth, different parent" (cousins), per-node metadata | Group 5 — track per-node metadata |
| "maximum width of a level" (counting null gaps) | Group 6 — position indexing |
| no level info needed, just visit every node | Template 2 — node-by-node |

### The One Rule — Snapshot Level Size First

```
Always snapshot the level size BEFORE the inner for loop:
    int size = queue.size();
    for (int i = 0; i < size; i++) { ... }

Without the snapshot, newly added children mix with the current level
and i == size-1 / i == 0 checks become meaningless.
```

---

### Quick Reference Table

| # | Name | Description | Intuition | Time | Space | Key Implementation |
|---|---|---|---|---|---|---|
| 102 | Binary Tree Level Order Traversal | Return all node values level by level, left to right. |  | O(n) | O(n) | Standard |
| 107 | Binary Tree Level Order Traversal II | Same as #102 but return levels from bottom to top. |  | O(n) | O(n) | Standard |
| 103 | Binary Tree Zigzag Level Order Traversal | Level 1 left-to-right, level 2 right-to-left, alternating. |  | O(n) | O(n) | Standard |
| 637 | Average of Levels in Binary Tree | Return the average value of nodes at each level. |  | O(n) | O(n) | Standard |
| 199 | Binary Tree Right Side View | Return the value of the rightmost node at each level. |  | O(n) | O(n) | Standard |
| 513 | Find Bottom Left Tree Value | Return the leftmost value in the last level (deepest row). |  | O(n) | O(n) | Standard |
| 515 | Find Largest Value in Each Tree Row | Return the maximum value found at each level. |  | O(n) | O(n) | Standard |
| 1161 | Maximum Level Sum of a Binary Tree | Return the smallest level number (1-indexed) whose node sum is maximum. |  | O(n) | O(n) | Standard |
| 111 | Minimum Depth of Binary Tree | Minimum number of nodes from root to the nearest leaf. | BFS reaches nodes in depth order, so the first leaf it dequeues is necessarily the shallowest. | O(n) | O(n) | Standard |
| 116 | Populating Next Right Pointers in Each Node | Connect each node's `next` to the node immediately to its right at the same level. Tree is a perfect binary tree. | BFS already visits a level left to right, so just chain each node to the one polled before it. | O(n) | O(n) | Standard |
| 117 | Populating Next Right Pointers in Each Node II | Same as #116 but the tree can be any binary tree (not necessarily perfect). |  | O(n) | O(n) | Standard |
| 993 | Cousins in Binary Tree | Two nodes `x` and `y` are cousins if they are at the same depth but have different parents. Return true if `x` and `y` are cousins. | cousins must surface in the *same* BFS level; if only one shows up per level, their depths differ. | O(n) | O(n) | Standard |
| 662 | Maximum Width of Binary Tree | Return the maximum width of any level of a binary tree. Width is defined as the length between the leftmost and rightmost non-null nodes, including all the null nodes in between. |  | O(n) | O(n) | BFS with position tracking. Assign each node a position: root=1, left child of node at pos `p` gets `2*p`, right child gets `2*p+1`. Width of level = `lastPos - firstPos + 1`. Normalize by subtracting `firstPos` of each level to prevent overflow. |

---

### Pattern Summary

| What changes per level | Key variable | Example problems |
|---|---|---|
| Collect all values | `List<Integer> level` | 102, 107, 103 |
| Compute aggregate | `int sum` / `int max` | 637, 515, 1161 |
| Record boundary node | check `i == 0` or `i == size-1` | 199, 513 |
| Return on first match | `return depth` | 111 |
| Wire nodes together | `Node previous` | 116, 117 |
| Track parent metadata | `TreeNode xParent, yParent` | 993 |

### The One Rule (recap)

Snapshot the level size **before** the inner `for` loop — see "The One Rule" at the top of this file for the full explanation.

---
## DFS / Backtracking  &nbsp;`dfs.md`

DFS appears in five forms. The pattern determines naming, return type, and where the answer is built.

---

### When to Use — Signal → Pattern

| Problem signal phrase | Pattern / template |
|---|---|
| "height / depth / sum OF the subtree", combine results upward | #1 Process children first, combine at node (post-order) |
| "root-to-leaf path", "number built along the path" | #2 Process node first, pass state down (pre-order) |
| "longest/best path that may bend through a node" (spans both arms) | #3 Tree global answer |
| "count islands / largest region / flood fill" on a grid | #4 Grid DFS |
| "can finish all", "detect cycle", "valid course order" (directed) | #5 Graph DFS 3-color |
| "all subsets / permutations / combinations", "find every way" | #6 Backtracking |
| "valid BST", "kth smallest", "closest value", "successor" | BST templates (pass bounds / inorder / binary search) |

---

### Quick Reference Table

| # | Name | Description | Intuition | Time | Space | Key Implementation |
|---|---|---|---|---|---|---|
| 104 | Maximum Depth of Binary Tree | Maximum number of nodes along the longest root-to-leaf path. | my depth is just one more than my deeper child's depth. | O(n) | O(h) | Standard |
| 543 | Diameter of Binary Tree | Length of the longest path between any two nodes (path does not need to pass through root). | the longest path bends at some node using both arms, but only one arm can extend to its parent. | O(n) | O(h) | Standard |
| 124 | Binary Tree Maximum Path Sum | Maximum sum of any path between any two nodes. Values can be negative. | a negative arm is worse than taking nothing, so clamp it to 0 before adding. | O(n) | O(h) | Standard |
| 110 | Balanced Binary Tree | Is every node's left and right subtree within 1 height of each other? | fold "is it balanced" into the height return — a poisoned -1 bubbles up and stops the work. | O(n) | O(h) | Standard |
| 226 | Invert Binary Tree | Mirror a binary tree — swap left and right subtrees at every node. | invert both children, then swap the pointers at this node. | O(n) | O(h) | Standard |
| 112 | Path Sum | Does any root-to-leaf path sum to `targetSum`? | subtract each node from the target on the way down; a leaf with remaining 0 is a hit. | O(n) | O(h) | Standard |
| 113 | Path Sum II | Return all root-to-leaf paths that sum to `targetSum`. | the same `path` list is reused for every branch, so undo your add as you unwind. | O(n) | O(n) for output paths | Standard |
| 257 | Binary Tree Paths | Return all root-to-leaf paths as strings (`"1->2->5"`). | append to a shared StringBuilder, then truncate back to your entry length to undo. | O(n) | O(n) for output paths | Standard |
| 129 | Sum Root to Leaf Numbers | Each root-to-leaf path represents a number (e.g., 1→2→3 = 123). Return the total sum. | build the number digit by digit on the way down (`current*10 + val`); add it up at each leaf. | O(n) | O(h) | Standard |
| 200 | Number of Islands | Count the number of islands (connected groups of `'1'`) in a binary grid. | each unvisited land cell starts a new island; flood-fill sinks the whole island so it's counted once. | O(m·n) | O(m·n) | Standard |
| 695 | Max Area of Island | Return the area of the largest island. | an island's area is 1 (this cell) plus the areas its four neighbors flood back. | O(m·n) | O(m·n) | Standard |
| 207 | Course Schedule | Can you finish all courses given prerequisites? Return false if there is a cycle. | re-entering a node still on the current DFS stack means you looped back to a prerequisite → cycle. | O(V+E) | O(V+E) | Standard |
| 210 | Course Schedule II | Return a valid order to take all courses. Return `[]` if a cycle exists. | a node finishes only after all it depends on do, so post-order reversed is a valid prerequisite order. | O(V+E) | O(V+E) | Standard |
| 46 | Permutations | All permutations of distinct integers. | order matters, so every position considers all unused elements (no `start` index). | O(n·n!) | O(n) | Standard |
| 78 | Subsets | All subsets (power set) of distinct integers. | every prefix on the way down is itself a valid subset, so record at every node. | O(n·2ⁿ) | O(n) | Standard |
| 39 | Combination Sum | All combinations summing to target. Same element may be used unlimited times. No duplicate combos. | passing `i` (not `i+1`) lets you pick the same element again; `start` still forbids going backward, so no reordered dups. | O(n · 2ⁿ) | O(target/min) | Standard |
| 40 | Combination Sum II | Each element used at most once. Input may have duplicates. No duplicate combos in output. | after sorting, equal values sit together; skipping a repeat at the *same level* prevents producing the same combo twice. | O(n · 2ⁿ) | O(target/min) | Standard |
| 79 | Word Search | Given a board of characters, return true if the word exists as a connected path (no cell reused). | the grid itself is the state — temporarily blank a cell so the same path can't reuse it, then restore on the way back. | O(m·n·4^L) where L = word length | O(L) | Standard |
| 131 | Palindrome Partitioning | Partition string `s` such that every substring is a palindrome. Return all such partitions. | try every prefix as the first cut; only recurse on the rest when that prefix is a palindrome. | O(n · 2ⁿ) | O(n) | Standard |
| 98 | Validate Binary Search Tree | Determine if a binary tree is a valid BST. Each node's value must be strictly greater than all values in its left subtree and strictly less than all values in its right subtree. |  | O(n) | O(h) | Pass min/max bounds down — each call tightens the valid range. Use `long` to handle `Integer.MIN_VALUE` and `Integer.MAX_VALUE` edge cases. |
| 230 | Kth Smallest Element in a BST | Find the kth smallest element in a BST (1-indexed). |  | O(k) average, O(n) worst | O(h) | BST inorder traversal visits nodes in ascending order. Count nodes visited; when count reaches k, record the answer and stop early. |
| 270 | Closest Binary Search Tree Value | Given a BST and a `target` (double), return the value in the BST closest to target. |  | O(h) | O(1) | Use BST structure to navigate in O(h). At each node, compare distance to closest seen so far, then binary-search left or right. |
| 285 | Inorder Successor in BST | Given a node `p` in a BST, return its inorder successor (the smallest node with value greater than `p.val`). Return null if no such node exists. |  | O(h) | O(1) | Navigate the BST. When `root.val > p.val`, this root is a candidate — save it and go left (to find a smaller valid candidate). When `root.val <= p.val`, go right (must find something larger). |
| 687 | Longest Univalue Path | Return the length of the longest path in a binary tree where every node along the path has the same value. The path does not need to pass through the root. |  | O(n) | O(h) | Post-order DFS. At each node, extend the left or right path only if the child's value matches. The path through the current node = leftPath + rightPath. Return the max single-direction extension upward. |
| 37 | Sudoku Solver | Fill a partially filled 9×9 Sudoku so every row, column, and 3×3 box contains digits 1-9. |  | O(9^m) m=empty cells | O(1) | backtracking that tries digits 1-9 in each empty cell, validating against row, column, and box constraints before recursing. |
| 47 | Permutations II | Return all unique permutations of an array that may contain duplicates. |  | O(n·n!) | O(n) | sort first; use a `used[]` array; skip a value if the previous equal value at the same tree level has not been used (prevents duplicate permutations). |
| 51 | N-Queens | Place n queens on an n×n board so no two attack each other; return all distinct solutions. |  | O(n!) | O(n) | backtrack row by row; track occupied columns and both diagonals. Cells on the same `\` diagonal share `r-c`; cells on the same `/` diagonal share `r+c`. |
| 60 | Permutation Sequence | Return the kth permutation (1-indexed) of the sequence 1..n. |  | O(n²) | O(n) | no backtracking — use the factorial number system. Each position's digit is determined directly by `(k-1) / (remaining-1)!`. |
| 90 | Subsets II | Return all possible unique subsets of an array that may contain duplicates. |  | O(n·2ⁿ) | O(n) | sort first; within a recursion level, skip a value equal to its predecessor to avoid duplicate subsets. |
| 216 | Combination Sum III | Find all combinations of k numbers from 1-9 (each used at most once) that sum to n. |  | O(C(9,k)) | O(k) | standard combination backtracking with start index `i+1` (no reuse), but with two stopping constraints — count and remaining sum. |
| 549 | Binary Tree Longest Consecutive Sequence II | Find the length of the longest consecutive path in a binary tree. The path can be increasing or decreasing and may go through a node (child-parent-child). |  | O(n) | O(h) | post-order DFS returns a pair `{increasing, decreasing}` for each node. A path through the node combines an increasing run from one child with a decreasing run from the other. |
| 17 | Letter Combinations of a Phone Number | Given a string of digits 2-9, return all letter combinations the phone keypad could represent. | backtrack one digit at a time, appending each candidate letter and undoing it. | O(4ⁿ·n) | O(n) | Standard |
| 22 | Generate Parentheses | Generate all combinations of n pairs of well-formed parentheses. | add `(` while opens remain; add `)` only while closes outstanding; backtrack each choice. | O(4ⁿ/√n) | O(n) | Standard |
| 36 | Valid Sudoku | Determine if a filled-in 9×9 Sudoku board is valid (no repeats in any row, column, or 3×3 box). | encode each digit's row/column/box membership into a HashSet of unique keys; a collision means invalid. | O(1) (fixed 81 cells) | O(1) | Standard |
| 77 | Combinations | Return all combinations of k numbers chosen from 1 to n. | standard backtracking with start index advancing to i+1; record when path reaches size k. | O(k·C(n,k)) | O(k) | Standard |
| 93 | Restore IP Addresses | Return all valid IP addresses formable by inserting dots into a digit string. | backtrack choosing 1-3 digit segments; each segment must be 0-255 and have no leading zero. | O(1) (bounded branching) | O(1) | Standard |
| 94 | Binary Tree Inorder Traversal | Return the inorder traversal (left → root → right) of a binary tree. | recurse left, visit node, recurse right. | O(n) | O(h) | Standard |
| 95 | Unique Binary Search Trees II | Generate all structurally unique BSTs storing values 1..n. | pick each value as root; recursively build all left subtrees from the smaller range and all right subtrees from the larger range, then combine. | O(n·Catalan(n)) | O(n·Catalan(n)) | Standard |
| 99 | Recover Binary Search Tree | Two nodes of a BST were swapped by mistake; recover the tree without changing its structure. | an inorder traversal of a valid BST is ascending; the swapped pair shows up as one or two descents. Track them and swap their values. | O(n) | O(h) | Standard |
| 100 | Same Tree | Check if two binary trees are structurally identical with the same node values. | both null is equal; one null or differing values is not; otherwise recurse on both children. | O(n) | O(h) | Standard |
| 101 | Symmetric Tree | Check if a binary tree is a mirror image of itself. | compare the outer pairs and inner pairs of two mirrored subtrees. | O(n) | O(h) | Standard |
| 102 | Binary Tree Level Order Traversal | Return node values level by level, left to right. | BFS with a queue; drain one level's worth of nodes per outer iteration. | O(n) | O(n) | Standard |
| 103 | Binary Tree Zigzag Level Order Traversal | Return node values level by level, alternating left-to-right and right-to-left. | standard BFS, but reverse the level list on alternate levels. | O(n) | O(n) | Standard |
| 105 | Construct Binary Tree from Preorder and Inorder Traversal | Reconstruct a binary tree from its preorder and inorder traversals. | the first preorder element is the root; its position in inorder splits left/right subtree sizes. | O(n) | O(n) | Standard |
| 106 | Construct Binary Tree from Inorder and Postorder Traversal | Reconstruct a binary tree from its inorder and postorder traversals. | the last postorder element is the root; build right subtree before left since postorder is consumed back to front. | O(n) | O(n) | Standard |
| 107 | Binary Tree Level Order Traversal II | Return node values level by level, from bottom to top. | standard BFS, then reverse the list of levels. | O(n) | O(n) | Standard |
| 108 | Convert Sorted Array to Binary Search Tree | Convert a sorted array to a height-balanced BST. | pick the middle element as the root so left and right halves are balanced; recurse on each half. | O(n) | O(log n) | Standard |
| 111 | Minimum Depth of Binary Tree | Find the shortest path length from root to any leaf. | like max depth, but a node with one missing child must take the existing child's depth (a non-leaf cannot end a root-to-leaf path). | O(n) | O(h) | skip the null side |
| 114 | Flatten Binary Tree to Linked List | Flatten a binary tree into a right-pointer linked list following preorder, in place. | reverse-preorder traversal (right, left, node) lets you prepend each node to a running tail. | O(n) | O(h) | Standard |
| 116 | Populating Next Right Pointers in Each Node | Connect each node's `next` pointer to its right neighbor in a perfect binary tree, using O(1) extra space. | use already-established `next` links of the current level to thread the next level. | O(n) | O(1) | Standard |
| 117 | Populating Next Right Pointers in Each Node II | Same as #116 but for an arbitrary binary tree. | walk each level via `next` links, building the next level's chain through a dummy head since children may be missing. | O(n) | O(1) | Standard |
| 144 | Binary Tree Preorder Traversal | Return the preorder traversal (root → left → right) of a binary tree. | visit node, recurse left, recurse right. | O(n) | O(h) | Standard |
| 145 | Binary Tree Postorder Traversal | Return the postorder traversal (left → right → root) of a binary tree. | recurse left, recurse right, visit node. | O(n) | O(h) | Standard |
| 199 | Binary Tree Right Side View | Return the values visible from the right side, one per level. | BFS each level; the last node dequeued in a level is the rightmost visible one. | O(n) | O(n) | Standard |
| 222 | Count Complete Tree Nodes | Count nodes in a complete binary tree faster than O(n). | if leftmost and rightmost depths match, the subtree is perfect (2^h − 1 nodes); otherwise recurse on both children. | O(log²n) | O(log n) | perfect subtree shortcut |
| 235 | Lowest Common Ancestor of a Binary Search Tree | Find the LCA of two nodes in a BST. | if both values are less than the node, go left; if both greater, go right; otherwise the node is the split point = LCA. | O(h) | O(1) | Standard |
| 236 | Lowest Common Ancestor of a Binary Tree | Find the LCA of two nodes in a general binary tree. | post-order: if p or q matches the node, return it; the node where both arms return non-null is the LCA. | O(n) | O(h) | Standard |
| 241 | Different Ways to Add Parentheses | Compute all results obtainable by parenthesizing an expression differently. | at each operator, split into left and right subexpressions, recursively evaluate both, and combine every pair. | O(Catalan(n)) | O(Catalan(n)) | Standard |
| 250 | Count Univalue Subtrees | Count subtrees in which all nodes share the same value. | post-order; a subtree is univalue if both children are univalue and their values match the node's value. | O(n) | O(h) | Standard |
| 255 | Verify Preorder Sequence in Binary Search Tree | Verify whether an array is a valid BST preorder traversal. | use a stack to simulate the path; popping when a value exceeds the top sets a lower bound. Any later value below that bound is invalid. | O(n) | O(n) | Standard |
| 267 | Palindrome Permutation II | Return all palindrome permutations of a string. | a palindrome needs at most one odd-count character; build half the palindrome by permuting half the characters, then mirror it. | O((n/2)!) | O(n) | Standard |
| 272 | Closest Binary Search Tree Value II | Find the k values in a BST closest to a target. | inorder gives sorted values; keep a sliding window of size k, evicting the farther end while a closer candidate exists. | O(n) | O(n) | values only get farther, stop early |
| 282 | Expression Add Operators | Insert +, -, * between digits of a string to reach a target value; return all expressions. | backtrack each operand prefix; track running value and the last multiplied term so * can fold correctly. | O(4ⁿ) | O(n) | Standard |
| 291 | Word Pattern II | Check if a string follows a pattern where each pattern char maps to a non-empty, non-overlapping substring. | backtrack assigning substrings to pattern characters, enforcing a bijection via two maps. | O(exponential) | O(n) | Standard |
| 293 | Flip Game | Given a string of '+' and '-', return all states after flipping one "++" to "--". | scan for each "++" occurrence and produce the flipped string. | O(n²) | O(n) | Standard |
| 294 | Flip Game II | Determine if the first player can guarantee a win in Flip Game. | the current player wins if any "++" flip leaves the opponent in a losing position; memoize states. | O(exponential, memoized) | O(states) | Standard |
| 297 | Serialize and Deserialize Binary Tree | Serialize a binary tree to a string and deserialize it back. | preorder with explicit "#" null markers uniquely encodes structure; rebuild by consuming tokens in the same order. | O(n) | O(n) | Standard |
| 298 | Binary Tree Longest Consecutive Sequence | Find the longest consecutive increasing-by-1 path going from parent to child. | pass the current run length down; extend it when the child is exactly parent + 1, otherwise reset to 1. | O(n) | O(h) | Standard |
| 301 | Remove Invalid Parentheses | Remove the minimum number of parentheses to make a string valid; return all distinct results. | BFS by removal count; the first level whose strings include valid ones is the minimum-removal answer. | O(2ⁿ) | O(2ⁿ) | Standard |
| 306 | Additive Number | Check if a string forms an additive sequence (each number is the sum of the two preceding). | backtrack the first two numbers; the rest of the string is forced, so just verify it matches the running sums. | O(n³) | O(n) | Standard |
| 314 | Binary Tree Vertical Order Traversal | Return node values ordered by column, then by row. | BFS tracking each node's column; collect values per column, then read columns left to right. | O(n) | O(n) | Standard |
| 320 | Generalized Abbreviation | Return all abbreviations of a word (replace any non-adjacent groups of letters with their counts). | for each character, choose to either abbreviate it (extend a count) or keep it literally; backtrack. | O(2ⁿ·n) | O(n) | Standard |
| 339 | Nested List Weight Sum | Sum each integer in a nested list weighted by its depth. | DFS carrying the current depth; integers add `value·depth`, lists recurse one level deeper. | O(n) | O(d) | Standard |
| 364 | Nested List Weight Sum II | Sum each integer weighted by its inverse depth (deepest integers have weight 1). | weight = (maxDepth − depth + 1). Accumulate sum of values at each level and a running unweighted total per BFS level so deeper values get counted more often. | O(n) | O(n) | shallow values re-counted each level |
| 386 | Lexicographical Numbers | Return integers 1..n in lexicographical order. | DFS a 10-ary prefix tree: start at each digit, append 0-9 as long as the number stays ≤ n. | O(n) | O(log n) | Standard |
| 404 | Sum of Left Leaves | Sum the values of all left leaves in a binary tree. | pass down whether a node is a left child; add its value when it is both a left child and a leaf. | O(n) | O(h) | Standard |
| 426 | Convert Binary Search Tree to Sorted Doubly Linked List | Convert a BST into a sorted circular doubly linked list in place. | inorder traversal yields sorted order; link each node to the previous one, then close the ring between head and tail. | O(n) | O(h) | Standard |
| 429 | N-ary Tree Level Order Traversal | Return the level order traversal of an N-ary tree. | BFS, enqueuing all children of each node per level. | O(n) | O(n) | Standard |
| 437 | Path Sum III | Count downward paths (any node to any descendant) summing to a target. | prefix-sum the running root-to-node sum; the number of paths ending here equals how many earlier prefixes equal `current − target`. | O(n) | O(n) | prefix-sum count |
| 440 | K-th Smallest in Lexicographical Order | Find the kth smallest integer in 1..n by lexicographical order. | count how many numbers share a prefix; skip whole subtrees of the 10-ary prefix tree when k exceeds their size, otherwise descend. | O(log²n) | O(1) | Standard |
| 449 | Serialize and Deserialize BST | Serialize and deserialize a BST compactly. | preorder alone reconstructs a BST using value bounds, so no null markers are needed. | O(n) | O(n) | Standard |
| 450 | Delete Node in a BST | Delete a key from a BST and return the new root. | find the node; if it has two children, replace its value with the inorder successor (smallest in right subtree) and delete that successor. | O(h) | O(h) | Standard |
| 473 | Matchsticks to Square | Determine if matchsticks can form a square (4 equal sides) using all sticks. | backtrack placing each stick into one of 4 side buckets; prune when total isn't divisible by 4 or a stick exceeds the side length. | O(4ⁿ) | O(n) | skip equal buckets |
| 488 | Zuma Game | Find the minimum balls from hand to insert to clear the board (or -1). | DFS each board state, trying every hand ball at every insertion point, removing groups of 3+; memoize visited states. | O(exponential) | O(states) | Standard |
| 489 | Robot Room Cleaner | Clean an entire room with a robot that has only relative move/turn/clean APIs and no map. | DFS with backtracking using relative coordinates; clean, try all four directions, and reverse-move to return after each branch. | O(cells) | O(cells) | Standard |
| 491 | Increasing Subsequences | Return all increasing subsequences of length ≥ 2 (input may have duplicates). | backtrack choosing elements ≥ the last picked; within one recursion level use a set to skip duplicate starts. Cannot sort (would destroy original order). | O(2ⁿ·n) | O(n) | skip dup at same level |
| 501 | Find Mode in Binary Search Tree | Find the mode(s) (most frequent values) in a BST that may have duplicates. | inorder gives sorted values, so equal values are adjacent; track current run count and update the mode list when counts tie or exceed the max. | O(n) | O(h) | Standard |
| 508 | Most Frequent Subtree Sum | Find the subtree sum(s) that occur most frequently. | post-order compute each subtree's sum, tally frequencies in a map, then collect the keys with the max frequency. | O(n) | O(n) | Standard |
| 510 | Inorder Successor in BST II | Find the inorder successor of a node given only a parent pointer (no root). | if a right subtree exists, the successor is its leftmost node; otherwise climb up until you come from a left child. | O(h) | O(1) | Standard |
| 513 | Find Bottom Left Tree Value | Find the leftmost value in the last (deepest) row of a binary tree. | BFS scanning right-to-left so the final node dequeued is the bottom-left value. | O(n) | O(n) | Standard |
| 515 | Find Largest Value in Each Tree Row | Return the maximum value in each row of a binary tree. | BFS level by level, tracking the max per level. | O(n) | O(n) | Standard |
| 526 | Beautiful Arrangement | Count permutations of 1..n where each number divides or is divisible by its position. | backtrack placing numbers position by position, only choosing a number when it satisfies the divisibility rule. | O(k) where k = valid arrangements | O(n) | Standard |
| 536 | Construct Binary Tree from String | Build a binary tree from a string like `4(2(3)(1))(6(5))`. | parse the leading number as the node, then the first parenthesized group as the left subtree and the second as the right subtree. | O(n) | O(h) | Standard |
| 538 | Convert BST to Greater Tree | Replace each node's value with the sum of all values greater than or equal to it. | reverse inorder (right → node → left) visits values in descending order; carry a running sum and add it into each node. | O(n) | O(h) | Standard |
| 545 | Boundary of Binary Tree | Return the boundary: root, left boundary top-down, leaves left-to-right, right boundary bottom-up, no duplicates. | collect three parts separately — left boundary (excluding leaves), all leaves, and right boundary reversed (excluding leaves). | O(n) | O(h) | Standard |
| 559 | Maximum Depth of N-ary Tree | Find the maximum depth of an N-ary tree. | depth is 1 plus the max depth among all children. | O(n) | O(h) | Standard |
| 563 | Binary Tree Tilt | Sum the tilt of every node, where tilt = \|left subtree sum − right subtree sum\|. | post-order return each subtree sum; accumulate the absolute difference into a global total. | O(n) | O(h) | Standard |
| 572 | Subtree of Another Tree | Check whether `subRoot` is a subtree of `root`. | at every node of `root`, test for structural equality with `subRoot`. | O(m·n) | O(h) | Standard |
| 589 | N-ary Tree Preorder Traversal | Return the preorder traversal of an N-ary tree. | visit the node, then recurse into each child in order. | O(n) | O(h) | Standard |
| 590 | N-ary Tree Postorder Traversal | Return the postorder traversal of an N-ary tree. | recurse into all children first, then visit the node. | O(n) | O(h) | Standard |
| 606 | Construct String from Binary Tree | Build a preorder string with parentheses, e.g. `1(2(4))(3)`. | append the value, then each non-null child wrapped in parentheses; keep empty `()` for a left child only when a right child exists. | O(n) | O(h) | Standard |
| 617 | Merge Two Binary Trees | Merge two binary trees by summing overlapping node values. | if either node is null, return the other; otherwise sum values and recurse on both child pairs. | O(n) | O(h) | Standard |
| 637 | Average of Levels in Binary Tree | Return the average value of nodes on each level. | BFS each level, summing values and dividing by the level size. | O(n) | O(n) | Standard |
| 652 | Find Duplicate Subtrees | Return one root per group of structurally identical, duplicated subtrees. | serialize each subtree post-order into a canonical string; the second time a serialization appears, record its root. | O(n²) | O(n²) | Standard |
| 653 | Two Sum IV - Input is a BST | Find whether two nodes in a BST sum to a target. | traverse, storing seen values in a set; for each node check if `target − val` was seen. | O(n) | O(n) | Standard |
| 654 | Maximum Binary Tree | Build a tree where the root is the array max, left subtree from the left subarray, right subtree from the right subarray. | find the max in the range as root, recurse on the two halves. | O(n²) | O(n) | Standard |
| 662 | Maximum Width of Binary Tree | Return the maximum width of any level, where width counts the gap between the leftmost and rightmost non-null nodes. | assign heap-style indices (left = 2i, right = 2i+1); per level the width is last index − first index + 1. | O(n) | O(n) | Standard |
| 671 | Second Minimum Node In a Binary Tree | In a tree where each node's value is the min of its children, find the second smallest value overall. | the root is the global minimum; DFS for the smallest value strictly greater than the root. | O(n) | O(h) | Standard |
| 679 | 24 Game | Determine if four numbers can be combined with +, −, ×, ÷ to make 24. | backtrack: pick any two numbers, apply each operator, replace them with the result, and recurse until one number remains. | O(1) (bounded) | O(1) | Standard |
| 698 | Partition to K Equal Sum Subsets | Determine if an array can be split into k subsets of equal sum. | target = total/k; backtrack filling one bucket at a time, sorting descending to fail fast, skipping when total isn't divisible. | O(k·2ⁿ) | O(n) | Standard |
| 700 | Search in a Binary Search Tree | Find the subtree rooted at the node with a given value in a BST. | binary-search the tree: go left if target is smaller, right if larger. | O(h) | O(1) | Standard |
| 701 | Insert into a Binary Search Tree | Insert a value into a BST and return the root. | descend like a search until reaching a null child, then attach a new node there. | O(h) | O(h) | Standard |
| 742 | Closest Leaf in a Binary Tree | Find the value of the leaf nearest to the node with a given value. | convert the tree to an undirected graph, then BFS from the target node until the first leaf is reached. | O(n) | O(n) | Standard |
| 776 | Split BST | Split a BST into two trees: one with values ≤ V and one with values > V. | recurse; at each node decide which result tree it belongs to based on V, then reattach the recursively-split child. | O(h) | O(h) | Standard |
| 784 | Letter Case Permutation | Return all strings formable by toggling the case of letters in a string. | backtrack character by character; digits have one choice, letters branch into lower and upper case. | O(2ⁿ·n) | O(n) | Standard |
| 814 | Binary Tree Pruning | Remove every subtree that contains no node with value 1. | post-order prune children first; drop a node if both children become null and its own value is 0. | O(n) | O(h) | Standard |
| 842 | Split Array into Fibonacci Sequence | Split a digit string into a Fibonacci-like sequence (each term = sum of previous two), with terms fitting in a 32-bit int. | backtrack the first two numbers; the rest is forced. Prune leading zeros and overflow. | O(n²) | O(n) | Standard |
| 863 | All Nodes Distance K in Binary Tree | Find all node values exactly distance k from a target node. | build parent links so the tree becomes an undirected graph, then BFS k levels from the target. | O(n) | O(n) | Standard |
| 865 | Smallest Subtree with all the Deepest Nodes | Find the smallest subtree containing all of the tree's deepest leaves. | post-order return (depth, lca). If left and right depths tie, the current node is the LCA; otherwise carry up the deeper side. | O(n) | O(h) | tie → this node is LCA |
| 889 | Construct Binary Tree from Preorder and Postorder Traversal | Reconstruct a binary tree from preorder and postorder traversals (any valid tree). | preorder[start] is the root; preorder[start+1] is the left subtree root, whose position in postorder gives the left subtree size. | O(n) | O(h) | Standard |
| 897 | Increasing Order Search Tree | Rearrange a BST into a right-skewed tree following inorder order. | inorder traversal; relink each node as the right child of the previous, clearing left pointers. | O(n) | O(h) | Standard |
| 919 | Complete Binary Tree Inserter | Design a structure that supports O(1) insertion into a complete binary tree. | keep a BFS queue of nodes that still have a free child slot; insert into the front node and enqueue the new node. | O(1) insert | O(n) | Standard |
| 932 | Beautiful Array | Construct an array of 1..n where no three indices i<j<k satisfy 2·a[j] = a[i] + a[k]. | divide and conquer: a beautiful array of odds followed by evens stays beautiful, since odd + even is never twice an integer. | O(n log n) | O(n) | Standard |
| 938 | Range Sum of BST | Sum all node values within the inclusive range [low, high]. | prune branches outside the range using BST ordering. | O(n) | O(h) | Standard |
| 951 | Flip Equivalent Binary Trees | Check if two trees are flip-equivalent (can be made identical by swapping some children). | match children either directly or swapped at each node. | O(n) | O(h) | Standard |
| 958 | Check Completeness of a Binary Tree | Determine if a binary tree is complete. | BFS including null children; once a null is seen, no real node may follow. | O(n) | O(n) | real node after a gap |
| 987 | Vertical Order Traversal of a Binary Tree | Group node values by column, then by row, then by value within the same position. | DFS recording (col, row, val); sort by column, then row, then value. | O(n log n) | O(n) | Standard |
| 988 | Smallest String Starting From Leaf | Return the lexicographically smallest root-to-leaf string, where each node maps to a letter 'a'..'z' and the string is read leaf to root. | build the path down, reverse it at each leaf, and track the minimum. | O(n·h) | O(h) | Standard |
| 993 | Cousins in Binary Tree | Check if two values are cousins (same depth, different parents). | BFS recording each value's depth and parent; cousins share depth but differ in parent. | O(n) | O(n) | Standard |
| 998 | Maximum Binary Tree II | Insert a value into a maximum tree built by appending the value to the original array's end. | since the value was appended last, it lies on the rightmost spine; insert where it first exceeds the current node. | O(h) | O(h) | Standard |
| 1008 | Construct Binary Search Tree from Preorder Traversal | Build a BST from its preorder traversal. | the first value is the root; values less than it form the left subtree, the rest form the right. Use an upper bound to decide where to stop. | O(n) | O(h) | Standard |
| 1026 | Maximum Difference Between Node and Ancestor | Find the maximum \|a − d\| over all ancestor a and descendant d pairs. | pass the min and max seen on the path down; at each node update the answer with the largest gap against those extremes. | O(n) | O(h) | Standard |
| 1038 | Binary Search Tree to Greater Sum Tree | Replace each node's value with the sum of all values greater than or equal to it. | reverse inorder (right → node → left) processes descending order; carry a running sum. | O(n) | O(h) | Standard |
| 1087 | Brace Expansion | Expand a string with brace options like `{a,b}c{d,e}` into all sorted concatenations. | parse each position into a sorted list of choices, then backtrack the Cartesian product. | O(product of group sizes) | O(n) | Standard |
| 1104 | Path In Zigzag Labelled Binary Tree | Return the root-to-node path of labels in a zigzag-labeled infinite binary tree. | the normal parent of label is label/2, but rows alternate direction, so mirror the parent within its row range. | O(log n) | O(log n) | mirror then halve |
| 1110 | Delete Nodes And Return Forest | Delete the given values and return the roots of the resulting forest. | post-order; if a node is deleted, its surviving children become new roots. A node is a root if its parent was deleted (or it's the original root) and it itself survives. | O(n) | O(h) | Standard |
| 1123 | Lowest Common Ancestor of Deepest Leaves | Find the LCA of all the deepest leaves. | post-order return (depth, lca); when both arms reach equal depth, the node is the LCA, else carry up the deeper arm. | O(n) | O(h) | Standard |
| 1161 | Maximum Level Sum of a Binary Tree | Return the 1-indexed level with the largest sum of node values. | BFS level by level, tracking the level whose sum is maximum. | O(n) | O(n) | Standard |
| 1214 | Two Sum BSTs | Given two BSTs and a target, decide if a value from each sums to the target. | store all values of the first BST in a set, then traverse the second checking for the complement. | O(m + n) | O(m) | Standard |
| 1305 | All Elements in Two Binary Search Trees | Return all elements from two BSTs in sorted order. | inorder each tree into a sorted list, then merge the two lists like merge sort. | O(m + n) | O(m + n) | Standard |
| 1361 | Validate Binary Tree Nodes | Given child arrays, verify the nodes form exactly one valid binary tree. | exactly one node has no parent (the root); every other node has exactly one parent, there are no cycles, and all nodes are reachable from the root. | O(n) | O(n) | Standard |
| 1382 | Balance a Binary Search Tree | Rebuild a BST so it becomes height-balanced. | inorder gives a sorted array; build a balanced BST by recursively choosing the middle element as root. | O(n) | O(n) | Standard |
| 1522 | Diameter of N-Ary Tree | Find the diameter (longest path between any two nodes) of an N-ary tree. | like binary-tree diameter, but track the two deepest child heights to form the longest path through each node. | O(n) | O(h) | Standard |
| 1644 | Lowest Common Ancestor of a Binary Tree II | Find the LCA of two nodes that may not both exist in the tree; return null if either is missing. | standard LCA but count how many of p, q were actually found, so a node returned without seeing both isn't accepted. | O(n) | O(h) | Standard |
| 1650 | Lowest Common Ancestor of a Binary Tree III | Find the LCA of two nodes given parent pointers, without root access. | like finding the intersection of two linked lists — walk both pointers up, switching to the other node when one reaches the top; they meet at the LCA. | O(h) | O(1) | Standard |

---

### All Templates

```java
// 1. PROCESS CHILDREN FIRST, COMBINE AT NODE (post-order)
// MENTAL MODEL: each node trusts its children to return a finished answer, then merges them.
// WHEN: "what is the height/sum/property OF the subtree rooted here"
private int dfs(TreeNode node) {
    if (node == null) return BASE;          // 0 for depth, true for balanced
    int left  = dfs(node.left);
    int right = dfs(node.right);
    // combine left, right, node.val → answer propagates up
    return ...;
}

// 2. PROCESS NODE FIRST, PASS STATE DOWN (pre-order)
// MENTAL MODEL: carry what you've seen so far down the path; the leaf has the full picture.
// WHEN: "root-to-leaf path", "running sum/number built along the way"
private void dfs(TreeNode node, int accumulated) {
    if (node == null) return;
    accumulated += node.val;                // update state on way down
    if (isLeaf(node)) { /* record */ return; }
    dfs(node.left,  accumulated);
    dfs(node.right, accumulated);
    // backtrack: no undo needed for primitive; undo List.add if using collection
}

// 3. TREE — GLOBAL ANSWER (return up the best single arm; update global across both arms)
// MENTAL MODEL: the answer may bend through a node using both arms, but only one arm can extend upward.
// WHEN: use when the best path spans across a node, not just up one arm.
int answer = Integer.MIN_VALUE;
private int dfs(TreeNode node) {
    if (node == null) return 0;
    int left  = Math.max(0, dfs(node.left));   // clamp negative
    int right = Math.max(0, dfs(node.right));
    answer = Math.max(answer, left + right + node.val);   // cross-node path
    return Math.max(left, right) + node.val;              // single arm up
}

// 4. GRID DFS — mark visited by mutating grid; 4-directional flood fill
// MENTAL MODEL: stand on a cell, flood into all 4 neighbors, sinking each as you visit it.
// WHEN: "connected region / island / flood fill" on a grid
private void dfs(int[][] grid, int r, int c) {
    if (r < 0 || r >= grid.length || c < 0 || c >= grid[0].length) return;
    if (grid[r][c] != TARGET) return;
    grid[r][c] = VISITED;
    dfs(grid, r+1, c); dfs(grid, r-1, c);
    dfs(grid, r, c+1); dfs(grid, r, c-1);
}

// 5. GRAPH DFS — 3-color visited: 0=unseen 1=in-stack 2=done
// MENTAL MODEL: if you re-enter a node still on the current stack, you've looped back → cycle.
// WHEN: "can finish all", "detect cycle", "valid ordering" on a directed graph
int[] state;
private boolean dfs(int node) {
    if (state[node] == 1) return true;    // back edge → cycle
    if (state[node] == 2) return false;   // already safe
    state[node] = 1;
    for (int neighbor : graph.get(node))
        if (dfs(neighbor)) return true;
    state[node] = 2;
    return false;
}

// 6. BACKTRACKING — choose / recurse / undo
// MENTAL MODEL: build a candidate one element at a time; undo each choice to explore the next branch.
// WHEN: "all subsets / permutations / combinations", "find all ways"
private void backtrack(int start, List<Integer> current) {
    if (baseCase) { result.add(new ArrayList<>(current)); return; }
    for (int i = start; i < n; i++) {
        if (skipCondition(i)) continue;    // prune duplicates
        current.add(nums[i]);              // choose
        backtrack(next, current);          // next = i (reuse) or i+1 (no reuse)
        current.remove(current.size()-1);  // undo
    }
}
```

---

### PROCESS CHILDREN FIRST, COMBINE AT NODE (post-order)

Recurse into children first, then combine results at the current node. Answer propagates upward.

### PROCESS NODE FIRST, PASS STATE DOWN (pre-order)

State is built on the way **down** and consumed at leaves. Use backtracking when state is a mutable collection.

### Grid DFS (4-directional flood fill)

Mark visited by overwriting the cell value. Return the accumulated property (count, area) or void.

### Graph DFS — 3-Color Cycle Detection

Three states: `0` = unvisited, `1` = in current DFS stack (visiting), `2` = fully processed (safe).  
A back edge (reaching a node with state `1`) means a cycle.

**Template:** choose → recurse → undo.  
`start` controls which elements are eligible at each level. `current` is the in-progress candidate.

```java
// MENTAL MODEL: grow one candidate by picking an element, recurse, then undo to try the next branch.
private void backtrack(int start, List<Integer> current) {
    if (baseCase) { result.add(new ArrayList<>(current)); return; }
    for (int i = start; i < n; i++) {
        if (skipCondition) continue;
        current.add(nums[i]);               // choose
        backtrack(nextStart, current);      // nextStart = i (reuse) or i+1 (no reuse)
        current.remove(current.size() - 1); // undo
    }
}
```

### Backtracking Decision Table

| # | All orderings? | Reuse element? | Has duplicates? | Start index | Skip condition |
|---|---|---|---|---|---|
| 46 Permutations | Yes — `used[]` | No | No | Loop 0..n, `used[i]` | `used[i]` |
| 78 Subsets | No | No | No | `start` → `i+1` | None |
| 39 Combination Sum | No | Yes | No | `start` → `i` | `candidates[i] > remaining` |
| 40 Combination Sum II | No | No | Yes | `start` → `i+1` | `i > start && nums[i] == nums[i-1]` |
| 131 Palindrome Part. | No | No | No | `start` → `end` | `!isPalindrome(sub)` |

---

### Tree DFS Summary

```
Pattern             When to use                         Answer location
Return up           Combine children at node            return value bubbles up
Pass down           Accumulate state toward leaves      check at leaf
Global variable     Path spans across a node (not up)   int/long field, updated inside dfs
```

---

BST key property: `left subtree values < node.val < right subtree values`. This allows O(h) search/insert/delete by binary-searching the tree.

### BST Template: Pass Bounds Down

```java
// Validate BST by passing min/max constraints down the tree
boolean validate(TreeNode node, long min, long max) {
    if (node == null) return true;
    if (node.val <= min || node.val >= max) return false;   // ← bounds check
    return validate(node.left, min, node.val)               // left: tighten max
        && validate(node.right, node.val, max);             // right: tighten min
}

// Call with: validate(root, Long.MIN_VALUE, Long.MAX_VALUE)
// Use Long to handle Integer.MIN_VALUE / Integer.MAX_VALUE edge cases
```

### BST Template: Inorder Traversal = Sorted Order

```java
// BST inorder (left → node → right) visits nodes in ascending order
void inorder(TreeNode node) {
    if (node == null) return;
    inorder(node.left);
    // process node (kth smallest: increment counter, return when k)
    inorder(node.right);
}
```

### BST Template: Binary Search on Tree

```java
// Navigate BST like binary search: go left or right based on comparison
TreeNode search(TreeNode root, int target) {
    while (root != null) {
        if (root.val == target) {
            return root;
        } else if (root.val < target) {
            root = root.right;
        } else {
            root = root.left;
        }
    }
    return null;
}
```

---
## Graph  &nbsp;`graph.md`

`Queue<Integer> queue = new ArrayDeque<>()` throughout.  
Six algorithms — each with a canonical template and representative problems.

---

### Complexity Legend

```
BFS / DFS         O(V + E)            visit each vertex and edge once
Topo sort (Kahn)  O(V + E)            each node enqueued once, each edge relaxed once
Union-Find        ~O(n·α(n)) ≈ O(n)   α = inverse Ackermann, effectively constant
Dijkstra          O((V + E) log V)    non-negative weights ONLY
Bellman-Ford      O(V · E)            allows negative weights; run k+1 rounds for a k-hop limit
Prim's MST        O(E log V)          PQ of candidate edges
```

### Quick Reference Table

| # | Name | Description | Intuition | Time | Space | Key Implementation |
|---|---|---|---|---|---|---|
| 994 | Rotting Oranges | Grid of `0` (empty), `1` (fresh), `2` (rotten). Each minute rotten oranges infect adjacent fresh ones. Return minutes until no fresh remain, or -1. |  | O(V+E) | O(V) | Standard |
| 542 | 01 Matrix | For each cell, return the distance to the nearest `0`. |  | O(m·n) | O(m·n) | Standard |
| 127 | Word Ladder | Minimum number of transformations from `beginWord` to `endWord`, changing one letter at a time. Each intermediate word must be in `wordList`. |  | O(N·L·26) where N = words, L = word length | O(N·L) | Standard |
| 130 | Surrounded Regions | Flip all `'O'` regions not connected to the border to `'X'`. |  | O(m·n) | O(m·n) | Standard |
| 417 | Pacific Atlantic Water Flow | Return all cells from which water can flow to both the Pacific (top/left border) and Atlantic (bottom/right border). |  | O(m·n) | O(m·n) | Standard |
| 207 | Course Schedule | Can you finish all courses given prerequisites? Detect if there is a directed cycle. |  | O(V+E) | O(V+E) | Standard |
| 210 | Course Schedule II | Return a valid order to take all courses. Return `[]` if impossible. |  | O(V+E) | O(V+E) | Standard |
| 310 | Minimum Height Trees | Find all roots that minimize tree height. At most 2 answers — they are the center node(s) of the longest path. | the best root sits at the center of the longest path; peeling leaves layer by layer converges there. | O(V+E) | O(V+E) | Standard |
| 547 | Number of Provinces | Count the number of connected components (provinces) in an undirected graph given as an adjacency matrix. | start with `n` separate sets; every successful merge drops the count by one. | O(n²·α(n)) | O(n) | Standard |
| 684 | Redundant Connection | Find the edge that creates a cycle in an undirected graph that would otherwise be a tree. | if both endpoints are already in the same set, this edge closes a cycle — it's the redundant one. | O(n·α(n)) | O(n) | Standard |
| 1319 | Number of Operations to Make Network Connected | Minimum cable moves to connect all `n` computers. Return -1 if impossible. | each redundant cable can be moved to bridge one gap, so `components - 1` moves suffice if you have enough spare cables. | O(E·α(n)) | O(n) | Standard |
| 743 | Network Delay Time | Time for a signal from `k` to reach all `n` nodes. Return -1 if unreachable. | every node is reached by its shortest delay; the network is "done" when the slowest of those arrives. | O((V+E)logV) | O(V+E) | Standard |
| 787 | Cheapest Flights Within K Stops | Cheapest price from `src` to `dst` using at most `k` stops (k+1 edges). | each round lets paths grow by one more edge, so `k+1` rounds caps the path at `k` stops. | O(k·E) | O(V) | Standard |
| 1514 | Path with Maximum Probability | Find the path from `start` to `end` with maximum success probability (product of edge probabilities). | probabilities in [0,1] only shrink when multiplied, so the "closest" (highest-probability) node settles first — Dijkstra still applies. | O((V+E)logV) | O(V+E) | Standard |
| 785 | Is Graph Bipartite? | Can graph nodes be split into two groups where every edge connects nodes in different groups? | paint each neighbor the opposite color; a clash means an odd-length cycle, which can't be 2-colored. | O(V+E) | O(V) | Standard |
| 1584 | Min Cost to Connect All Points | Connect all points (on a 2D plane) with minimum total Manhattan distance. Return that total cost. | grow one tree, always swallowing the cheapest edge that reaches a node not yet in it. | O(n²logn) | O(n²) | Standard |
| 1631 | Path With Minimum Effort | Find a path from top-left `[0,0]` to bottom-right `[m-1,n-1]` that minimizes the maximum absolute difference between adjacent cells. |  | O(m·n·log(m·n)) | O(m·n) | Modified Dijkstra. Instead of summing edge weights, the "cost" of a path is the maximum edge cost. Priority queue ordered by effort; `effort[r][c]` = minimum over all paths of their max-abs-diff. |
| 269 | Alien Dictionary | Given a sorted list of alien words, determine the order of characters in the alien alphabet. Return the order as a string, or empty string if invalid. |  | O(C) where C = total characters across all words | O(1) (at most 26 nodes) | Build a directed graph of character ordering. Compare each adjacent pair of words to find the first differing character → that gives an edge. Then topological sort. Return empty if there's a cycle or if shorter word is a prefix of longer word in wrong order. |
| 261 | Graph Valid Tree | Given `n` nodes labeled 0..n-1 and a list of undirected edges, determine if they form a valid tree (connected, no cycles). |  | O(n·α(n)) ≈ O(n) | O(n) | A valid tree has exactly `n-1` edges. Use Union Find to detect cycles. If any edge connects two nodes already in the same component → cycle → not a tree. |
| 323 | Number of Connected Components in an Undirected Graph | Given `n` nodes and a list of undirected edges, return the number of connected components. |  | O(n·α(n)) ≈ O(n) | O(n) | decrement on merge |
| 286 | Walls and Gates | Each cell is a gate (0), wall (-1), or empty (INF = 2147483647). Fill each empty room with distance to its nearest gate. |  | O(m·n) | O(m·n) | multi-source BFS — seed the queue with every gate at distance 0, then expand outward simultaneously. |
| 721 | Accounts Merge | Each account has a name and a list of emails. Merge accounts that share any email. Return merged accounts with emails sorted. |  | O(n·α) with sorting O(n log n) | O(n) | Union Find over emails. Assign each unique email an integer id, union all emails within the same account, then group emails by their root. |
| 827 | Making A Large Island | In a binary grid you may change at most one 0 to 1. Return the size of the largest island possible. |  | O(m·n) | O(m·n) | two passes. First DFS-color each island with a unique id (starting at 2) and record its size. Then for every 0, sum the sizes of distinct neighboring islands + 1. |
| 909 | Snakes and Ladders | On an n×n board numbered in boustrophedon (zigzag) order, find the minimum dice moves (1-6) from square 1 to square n². Ladders/snakes teleport you. |  | O(n²) | O(n²) | BFS over square numbers. Convert a square number to (row, col) accounting for the zigzag layout. |
| 1091 | Shortest Path in Binary Matrix | In an n×n binary grid, find the length of the shortest clear path (cells of 0) from top-left to bottom-right, moving in 8 directions. |  | O(m·n) | O(m·n) | standard BFS but with 8-directional movement (includes diagonals). |
| 126 | Word Ladder II | Find all shortest transformation sequences from `beginWord` to `endWord`, changing one letter at a time, each intermediate word in `wordList`. | BFS level-by-level builds a parent (predecessor) map of which words lead to which; once `endWord` is reached, DFS backtracks through parents to reconstruct every shortest path. | O(N·L·26) BFS + paths | O(N·L) | Standard |
| 133 | Clone Graph | Deep-copy an undirected graph where each node has a value and a list of neighbors. | Use a map from original node to its clone to avoid re-cloning and to wire neighbors correctly; BFS the graph, creating clones on first sight. | O(V+E) | O(V) | Standard |
| 277 | Find the Celebrity | Among `n` people, find the celebrity: known by everyone, knows nobody. `knows(a, b)` is the API. | A single linear scan narrows to one candidate (if `candidate` knows `i`, the candidate can't be the celebrity, so `i` becomes the new candidate); a second pass verifies. | O(n) | O(1) | Standard |
| 296 | Best Meeting Point | Given a grid where `1` marks a home, find the minimum total Manhattan distance to a single meeting point. | Manhattan distance separates into independent x and y components; the optimal coordinate on each axis is the median of the occupied coordinates. | O(m·n) | O(m·n) | Standard |
| 305 | Number of Islands II | Land cells are added one at a time to a water grid; after each addition return the current number of islands. |  | O(k·α(m·n)) | O(m·n) | Online Union-Find — when a cell becomes land, union it with any already-land 4-neighbors; track component count. |
| 317 | Shortest Distance from All Buildings | Find the empty land cell `0` minimizing total walking distance to every building `1` (`2` = obstacle). | BFS from each building, accumulating distances into every reachable empty cell and counting how many buildings reach it; the answer is the minimum total among cells reachable by all buildings. | O(B·m·n) where B = buildings | O(m·n) | Standard |
| 399 | Evaluate Division | Given equations `a/b = value`, answer queries `c/d`. Return -1.0 if undeterminable. | Treat variables as nodes and ratios as weighted directed edges; the answer to a query is the product of edge weights along any path from numerator to denominator. | O(Q·(V+E)) | O(V+E) | Standard |
| 407 | Trapping Rain Water II | Given a 2D height map, compute how much water it can trap after raining. |  | O(m·n·log(m·n)) | O(m·n) | Dijkstra-style BFS from the border inward using a min-heap of boundary heights; water level at a cell is the highest of the minimum boundary it must pass — pop the lowest wall first. |
| 463 | Island Perimeter | Given a grid with exactly one island, return its perimeter. | Each land cell contributes 4 sides, minus 2 for every shared edge with an adjacent land cell (counted once per pair). | O(m·n) | O(1) | Standard |
| 529 | Minesweeper | Reveal a cell on a Minesweeper board. `'M'` mine, `'E'` unrevealed empty, `'B'` revealed blank, digit = adjacent mine count. |  | O(m·n) | O(m·n) | BFS/DFS flood fill with 8 directions; if the clicked cell is a mine, mark `'X'`; otherwise count adjacent mines, and only recurse when count is 0. |
| 694 | Number of Distinct Islands | Count islands that are distinct by shape (translations are the same, rotations are not). |  | O(m·n) | O(m·n) | DFS recording the path signature (the direction taken at each step plus a backtrack marker); two islands with identical signatures have the same shape. |
| 733 | Flood Fill | Starting at `(sr, sc)`, change all connected same-color pixels to `color`. |  | O(m·n) | O(m·n) | Standard |
| 752 | Open the Lock | A 4-wheel lock starts at `"0000"`; each move turns one wheel ±1. Find minimum moves to reach `target`, avoiding `deadends`. |  | O(10^4 · 8) | O(10^4) | BFS over the 4-digit state space; each state has 8 neighbors (each wheel up or down). Treat deadends as visited. |
| 778 | Swim in Rising Water | At time `t` you can stand on any cell with elevation ≤ `t`. Find the least time to swim from `(0,0)` to `(n-1,n-1)`. |  | O(n²·log(n)) | O(n²) | Modified Dijkstra — minimize the maximum elevation along the path (not the sum). Min-heap ordered by current max elevation. |
| 797 | All Paths From Source to Target | In a DAG given as adjacency list `graph`, return all paths from node `0` to node `n-1`. | Since it is a DAG with no cycles, plain DFS backtracking enumerates every path; no visited set is needed. | O(2^V · V) | O(V) | Standard |
| 802 | Find Eventual Safe States | A node is safe if every path from it eventually reaches a terminal node (no outgoing edges). Return all safe nodes sorted. |  | O(V+E) | O(V+E) | Topological sort on the reversed graph (Kahn's) — start from terminal nodes (out-degree 0); a node becomes safe once all its outgoing edges lead to safe nodes. |
| 815 | Bus Routes | `routes[i]` is the stops served by bus `i`. Find the minimum number of buses to travel from `source` to `target`. |  | O(sum of route lengths) | O(sum of route lengths) | BFS where the "nodes" are buses (routes); build stop→routes index, then BFS route-to-route through shared stops, counting buses taken. |
| 847 | Shortest Path Visiting All Nodes | Find the length of the shortest path in an undirected graph that visits every node (may revisit nodes/edges). |  | O(2^n · n²) | O(2^n · n) | BFS over states `(node, visitedMask)` where `mask` is a bitmask of visited nodes; the goal is any state with all bits set. Start BFS from every node simultaneously. |
| 851 | Loud and Rich | `richer[i] = [a, b]` means `a` is richer than `b`; `quiet[i]` is the quietness of person `i`. For each person find the quietest person among everyone at least as rich (themselves included). |  | O(V+E) | O(V+E) | Topological sort (Kahn's) on the richer→poorer graph; propagate the quietest-known answer from richer people down to poorer ones in topo order. |
| 886 | Possible Bipartition | Given `dislikes` pairs, split `n` people into two groups so disliking people are never in the same group. |  | O(V+E) | O(V+E) | Standard |
| 913 | Cat and Mouse | A mouse (start node 1) and cat (start node 2) move on a graph; mouse wins by reaching node 0, cat wins by catching the mouse, else draw. Return 0/1/2 with optimal play. |  | O(V³) | O(V²) | Game-theory BFS over states `(mouse, cat, turn)`; start from known terminal states and propagate results backward (retrograde analysis) by counting undecided moves. |
| 934 | Shortest Bridge | A grid has exactly two islands of `1`s. Find the minimum number of `0`s to flip to connect them. |  | O(n²) | O(n²) | DFS to mark the first island (seeding a BFS queue with its cells), then multi-source BFS expanding outward until reaching the second island; BFS levels = bridge length. |
| 1034 | Coloring A Border | Color the border cells of the connected component containing `(row, col)` with `color`. A border cell touches the grid edge or a cell of a different original color. |  | O(m·n) | O(m·n) | BFS over same-color connected cells; mark a cell as a border when it has fewer than 4 same-component neighbors, recolor borders after traversal. |
| 1102 | Path With Maximum Minimum Value | Find a path from top-left to bottom-right maximizing the minimum cell value along the path (4-directional). |  | O(m·n·log(m·n)) | O(m·n) | Modified Dijkstra with a max-heap — the path "score" is the minimum cell value seen; greedily expand the highest-scoring frontier first. |
| 1136 | Parallel Courses | Courses 1..n with prerequisite `relations`; in each semester take all courses whose prerequisites are done. Return minimum semesters, or -1 if impossible. |  | O(V+E) | O(V+E) | Topological sort (Kahn's) processed level-by-level — each BFS level is one semester; if not all courses are processed, a cycle exists. |
| 1162 | As Far from Land as Possible | In a grid of `0` (water) and `1` (land), find the water cell whose distance to the nearest land is maximized; return that distance, or -1. |  | O(n²) | O(n²) | Multi-source BFS seeded with all land cells; the last BFS level expanded gives the maximum distance. |
| 1197 | Minimum Knight Moves | On an infinite chessboard, find the minimum knight moves from `(0,0)` to `(x, y)`. |  | O(max(x,y)²) | O(max(x,y)²) | BFS over knight moves (8 jump offsets); exploit symmetry by working in the first quadrant to bound the visited set. |
| 1202 | Smallest String With Swaps | Given index `pairs` that may be swapped any number of times, return the lexicographically smallest string achievable. |  | O(n·log(n) + E·α(n)) | O(n) | Union-Find groups swappable indices into connected components; within each component, sort the characters and place them back in ascending index order. |
| 1245 | Tree Diameter | Given the edges of an undirected tree, return its diameter (the number of edges on the longest path between any two nodes). |  | O(V+E) | O(V+E) | Two BFS passes — BFS from any node finds the farthest node `u`; a second BFS from `u` gives the diameter as the maximum distance. |
| 1293 | Shortest Path in a Grid with Obstacles Elimination | Find the shortest path from `(0,0)` to `(m-1,n-1)` in a grid where you may eliminate at most `k` obstacles (`1`s). |  | O(m·n·k) | O(m·n) | BFS over states `(row, col, remainingK)`; the visited set tracks the best remaining eliminations per cell so a cell can be revisited with more budget. |
| 1559 | Detect Cycles in 2D Grid | Return true if the grid contains a cycle of length ≥ 4 made of the same character. |  | O(m·n·α(m·n)) | O(m·n) | Union-Find over grid cells — for each cell union it with its up and left same-character neighbors; if a union finds them already connected, a cycle exists. |
| 1743 | Restore the Array From Adjacent Pairs | Given all adjacent pairs of an array (in any order), reconstruct the original array. |  | O(n) | O(n) | Build an adjacency graph; the two endpoints have a single neighbor. Start from an endpoint and walk the path, avoiding the previous node. |

---

### Graph Representation

```java
// Adjacency list (most common)
List<List<Integer>> graph = new ArrayList<>();
for (int i = 0; i < n; i++) graph.add(new ArrayList<>());
for (int[] edge : edges) {
    graph.get(edge[0]).add(edge[1]);
    graph.get(edge[1]).add(edge[0]);   // omit for directed
}

// Weighted adjacency list: int[] = {neighbor, weight}
List<List<int[]>> graph = new ArrayList<>();
for (int i = 0; i < n; i++) graph.add(new ArrayList<>());
for (int[] edge : edges)
    graph.get(edge[0]).add(new int[]{edge[1], edge[2]});

// Grid 4-directional neighbors
int[] dr = {1, -1, 0,  0};
int[] dc = {0,  0, 1, -1};
```

---

### All Six Templates

```java
// 1. BFS — shortest path / level order
// MENTAL MODEL: explore in rings of equal distance, so the first time you reach a node is the shortest.
// WHEN: "fewest steps", "shortest path" on an unweighted graph
Queue<Integer> queue = new ArrayDeque<>();
boolean[] visited = new boolean[n];
queue.offer(start);
visited[start] = true;
while (!queue.isEmpty()) {
    int node = queue.poll();
    for (int neighbor : graph.get(node)) {
        if (!visited[neighbor]) {
            visited[neighbor] = true;
            queue.offer(neighbor);
        }
    }
}

// 2. TOPOLOGICAL SORT — Kahn's BFS
// MENTAL MODEL: peel off nodes with no remaining prerequisites; if any get stuck, a cycle exists.
// WHEN: "valid order", "dependencies/prerequisites", "detect cycle" on a directed graph
int[] inDegree = new int[n];
for (int[] edge : edges) inDegree[edge[1]]++;
Queue<Integer> queue = new ArrayDeque<>();
for (int i = 0; i < n; i++) if (inDegree[i] == 0) queue.offer(i);
List<Integer> order = new ArrayList<>();
while (!queue.isEmpty()) {
    int node = queue.poll();
    order.add(node);
    for (int neighbor : graph.get(node))
        if (--inDegree[neighbor] == 0) queue.offer(neighbor);
}
// order.size() == n → no cycle

// 3. UNION FIND
// MENTAL MODEL: each set points to one representative; merge sets by linking roots, query by finding roots.
// WHEN: "connected components", "is it already connected", "merge groups dynamically"
int[] parent, rank;
void init(int n) {
    parent = new int[n]; rank = new int[n];
    for (int i = 0; i < n; i++) parent[i] = i;
}
int find(int x) {
    if (parent[x] != x) parent[x] = find(parent[x]);  // path compression
    return parent[x];
}
boolean union(int x, int y) {
    int px = find(x), py = find(y);
    if (px == py) return false;
    if (rank[px] < rank[py]) { int t = px; px = py; py = t; }
    parent[py] = px;
    if (rank[px] == rank[py]) rank[px]++;
    return true;
}

// 4. DIJKSTRA — shortest path (non-negative weights)
// MENTAL MODEL: greedily settle the closest unfinished node; non-negative weights guarantee it's final.
// WHEN: "shortest/cheapest path" with non-negative weights
int[] dist = new int[n];
Arrays.fill(dist, Integer.MAX_VALUE);
dist[src] = 0;
PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);  // min-heap on cost
pq.offer(new int[]{src, 0});
while (!pq.isEmpty()) {
    int[] current = pq.poll();
    int node = current[0], d = current[1];
    if (d > dist[node]) continue;   // stale entry
    for (int[] nb : graph.get(node)) {
        int next = nb[0], w = nb[1];
        if (dist[node] + w < dist[next]) {
            dist[next] = dist[node] + w;
            pq.offer(new int[]{next, dist[next]});
        }
    }
}

// 5. BIPARTITE CHECK — BFS 2-coloring
// MENTAL MODEL: paint neighbors the opposite color; a neighbor that's already your color means an odd cycle.
// WHEN: "split into two groups", "2-colorable", "no edge within a group"
int[] color = new int[n];
Arrays.fill(color, -1);
Queue<Integer> queue = new ArrayDeque<>();
for (int start = 0; start < n; start++) {
    if (color[start] != -1) continue;
    color[start] = 0;
    queue.offer(start);
    while (!queue.isEmpty()) {
        int node = queue.poll();
        for (int neighbor : graph.get(node)) {
            if (color[neighbor] == -1) { color[neighbor] = 1 - color[node]; queue.offer(neighbor); }
            else if (color[neighbor] == color[node]) return false;  // conflict
        }
    }
}
return true;

// 6. PRIM'S MST — greedy, always add cheapest edge to growing tree
// MENTAL MODEL: grow one tree outward, each step absorbing the cheapest edge that reaches a new node.
// WHEN: "connect all nodes at minimum total cost"
boolean[] inMST = new boolean[n];
int[] minEdge = new int[n];
Arrays.fill(minEdge, Integer.MAX_VALUE);
minEdge[0] = 0;
PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
pq.offer(new int[]{0, 0});
int total = 0;
while (!pq.isEmpty()) {
    int[] current = pq.poll();
    int node = current[0], cost = current[1];
    if (inMST[node]) continue;
    inMST[node] = true;
    total += cost;
    for (int[] nb : graph.get(node))
        if (!inMST[nb[0]] && nb[1] < minEdge[nb[0]]) {
            minEdge[nb[0]] = nb[1];
            pq.offer(new int[]{nb[0], nb[1]});
        }
}
```

---

### Single-Source vs Multi-Source

```
Single-source:  one starting node, find distances to all others
Multi-source:   seed queue with ALL starting nodes at once → BFS fans out from all simultaneously
                → avoids nested loops, handles "nearest X" questions in O(n)
```

---

**Core idea:** repeatedly remove nodes with `inDegree == 0` (no prerequisites). If all nodes removed → no cycle. Post-order in DFS = reverse of `order` here.

**Template (always the same three methods):**

```java
int[] parent, rank;

void init(int n) {
    parent = new int[n];
    rank   = new int[n];
    for (int i = 0; i < n; i++) parent[i] = i;
}
int find(int x) {
    if (parent[x] != x) parent[x] = find(parent[x]);  // path compression
    return parent[x];
}
boolean union(int x, int y) {               // returns false if already connected
    int px = find(x), py = find(y);
    if (px == py) return false;
    if (rank[px] < rank[py]) { int t = px; px = py; py = t; }
    parent[py] = px;
    if (rank[px] == rank[py]) rank[px]++;
    return true;
}
```

---

### Dijkstra vs Bellman-Ford

```
                    Dijkstra                    Bellman-Ford
Weights:            Non-negative only           Any (handles negative)
Constraint:         —                           k-hop limit (run k+1 rounds)
Time:               O((V+E) log V)              O(k·E)
When to use:        Standard shortest path      k-stop limit or negative weights
Key trick:          stale check: d > dist[node] copy array each round (temp[])
```

---

### Algorithm Chooser

| Signal in problem | Algorithm |
|---|---|
| Shortest path, unweighted / unit weight | BFS |
| Shortest path, non-negative weights | Dijkstra |
| Shortest path, k-hop limit | Bellman-Ford (k+1 rounds) |
| Shortest path, negative weights | Bellman-Ford (n-1 rounds) |
| Connected components, cycle detection | Union Find |
| Directed cycle / valid ordering | Topological Sort (Kahn's) |
| 2-colorable graph | Bipartite BFS coloring |
| Connect all nodes minimum cost | Prim's / Kruskal's MST |
| "nearest X for all cells" | Multi-source BFS |

### Stale Entry Pattern (Dijkstra)

```java
int[] current = pq.poll();
int node = current[0], d = current[1];
if (d > dist[node]) continue;   // ← this node was already relaxed to a better distance
```

Without this check, stale entries in the heap cause re-processing and wrong results.  
It replaces a `visited[]` array — simpler and correct because a better distance always wins.

---
## Greedy  &nbsp;`greedy.md`

Two interval templates plus non-interval greedy patterns.

---

### Quick Reference Table

| # | Name | Description | Intuition | Time | Space | Key Implementation |
|---|---|---|---|---|---|---|
| 435 | Non-overlapping Intervals | Remove the minimum number of intervals to make the rest non-overlapping. | Always keep the interval that finishes earliest — it leaves the most room for the rest, so greedily picking by end maximizes how many you keep. | O(n log n) | O(1) | Standard |
| 452 | Minimum Number of Arrows to Burst Balloons | Balloons span `[start, end]`. An arrow shot at `x` pops all balloons with `start ≤ x ≤ end`. Minimum arrows to pop all balloons. | Shoot the arrow at the earliest end point to pop every balloon overlapping it; only start a new arrow when a balloon begins past the current arrow. | O(n log n) | O(1) | Standard |
| 646 | Maximum Length of Pair Chain | Given pairs `[a, b]`, form a chain where `b < c` for each consecutive pair `[a,b]` → `[c,d]`. Maximum chain length. | Picking the pair that ends earliest each time leaves the most slack for later links, maximizing the chain. | O(n log n) | O(1) | Standard |
| 56 | Merge Intervals | Merge all overlapping intervals. Return the minimum set of non-overlapping intervals. | sort to make overlaps adjacent, then sweep once — each interval only ever compares against the most recently kept one. | O(n log n) | O(n) | Standard |
| 57 | Insert Interval | Insert a new interval into a sorted list of non-overlapping intervals; merge if necessary. The input is already sorted — no sort needed. | Walk the sorted list in three phases — copy everything that ends before the new interval, absorb everything that overlaps it, then copy the rest. | O(n) | O(n) | Standard |
| 253 | Meeting Rooms II | Minimum number of meeting rooms required to host all meetings. | USE WHEN counting simultaneous/overlapping resources — "minimum rooms", "max concurrent". The heap size at any moment is exactly how many meetings are running at once. | O(n log n) | O(n) | Standard |
| 55 | Jump Game | Each element is the max jump from that position. Can you reach the last index? | Sweep left to right tracking the farthest index reachable; if you ever stand past that frontier you're stuck. | O(n) | O(1) | Standard |
| 45 | Jump Game II | Minimum jumps to reach the last index. | Treat each jump as a BFS layer — extend through the whole current reach before incrementing the jump count. | O(n) | O(1) | Standard |
| 763 | Partition Labels | Partition string into as many parts as possible so each letter appears in at most one part. Return the size of each part. | A partition can't close until you pass the last occurrence of every letter seen inside it, so extend `end` to that frontier and cut when you reach it. | O(n) | O(1) | Standard |
| 406 | Queue Reconstruction by Height | People given as `[h, k]` (height h, k taller/equal people in front). Reconstruct the queue. | Place tallest first so that inserting a person at index `k` is always correct — only taller/equal people are already placed, and shorter insertions later don't disturb their counts. | O(n²) | O(n) | Standard |
| 252 | Meeting Rooms | Given an array of meeting intervals, determine if a person could attend all meetings (no two meetings overlap). | After sorting by start, any overlap must be between adjacent intervals, so one linear scan comparing neighbors is enough. | O(n log n) | O(1) | start < previous end = overlap |
| 134 | Gas Station | There are n gas stations on a circular route. `gas[i]` is the gas at station i; `cost[i]` is the gas needed to travel from i to i+1. Return the starting station index if you can complete the circuit, or -1 if not. | If the tank ever drops below 0, no station between the old start and here can work, so jump the start past the failure point; a valid start exists iff total gas ≥ total cost. | O(n) | O(1) | reset start when tank goes negative |
| 135 | Candy | Assign minimum candies to children in a line: each child gets at least 1 candy, and a child with a higher rating than an adjacent neighbor gets more candies than that neighbor. | Two passes capture the two directions of the constraint — a left-to-right pass enforces "higher than left neighbor gets more", a right-to-left pass enforces "higher than right neighbor gets more". Taking the max of both satisfies both. | O(n) | O(n) | higher than left neighbor |
| 274 | H-Index | Given an array of citation counts, find the largest `h` such that at least `h` papers each have at least `h` citations. | After sorting ascending, if a paper at index `i` has `citations[i]` citations, then there are `n - i` papers with at least that many. The h-index is found where `citations[i] >= n - i` first holds. | O(n log n) | O(1) | n-i papers have >= citations[i] |
| 455 | Assign Cookies | Each child `i` has a greed factor `g[i]` (minimum cookie size needed); each cookie `j` has size `s[j]`. Each cookie satisfies at most one child. Maximize the number of content children. | Sort both arrays; give the smallest sufficient cookie to the least greedy child. This never wastes a large cookie on a child a small one could satisfy. | O(n log n) | O(1) | Standard |
| 575 | Distribute Candies | Distribute `n` candies (the holder eats exactly `n/2`) to maximize the number of distinct candy types eaten. | You can eat at most `n/2` candies, and at best one of each distinct type. So the answer is the smaller of the number of distinct types and `n/2`. | O(n) | O(n) | capped by half the total |
| 605 | Can Place Flowers | Given a flowerbed (array of 0s and 1s where 1 is a planted flower), determine if `n` new flowers can be planted without any two flowers being adjacent. | Greedily plant a flower at the first empty plot whose neighbors are also empty — planting as early as possible never blocks a future placement that a later choice would allow. | O(n) | O(1) | plot and both neighbors empty |
| 630 | Course Schedule III | Each course has `(duration, lastDay)`. Starting at day 0 and taking courses one at a time, find the maximum number of courses that can be taken so each finishes by its `lastDay`. | Sort by deadline so deadlines are considered in order. Greedily take each course; if total time exceeds the current deadline, drop the previously taken course with the largest duration (a max-heap) — swapping out the longest course frees the most time while keeping the count. | O(n log n) | O(n) | over deadline → drop longest |
| 881 | Boats to Save People | Each boat carries at most 2 people with total weight at most `limit`. Given people's weights, find the minimum number of boats to rescue everyone. | Pair the heaviest remaining person with the lightest remaining one if they fit together; otherwise the heaviest goes alone. Sorting plus two pointers makes this pairing optimal. | O(n log n) | O(1) | Standard |
| 986 | Interval List Intersections | Given two lists of pairwise-disjoint, sorted intervals, return the intersection of the two lists. | Two pointers walk both sorted lists together. The overlap of the two current intervals is `[max(starts), min(ends)]`, which is valid only when `max(starts) <= min(ends)`. Advance whichever interval ends first. | O(m + n) | O(m + n) | valid overlap |
| 1005 | Maximize Sum Of Array After K Negations | Given an array and `k`, perform exactly `k` operations, each negating one element (the same index may be chosen repeatedly), to maximize the array sum. | Flipping the most negative number first yields the biggest gain. After all negatives are flipped (or k runs out), any leftover flips should land on the smallest-magnitude element, since flipping it twice is a no-op. | O(n log n) | O(1) | leftover odd flips hit smallest |
| 1094 | Car Pooling | Given trips `[numPassengers, from, to]` and a car capacity, determine whether all trips can be completed without exceeding capacity at any point. | A difference array (sweep line) over locations records passengers boarding at `from` and leaving at `to`. Running the prefix sum gives the occupancy at each point; if it ever exceeds capacity, fail. | O(n + maxLocation) | O(maxLocation) | over capacity → fail |
| 1272 | Remove Interval | Given a sorted list of disjoint intervals and an interval `toBeRemoved`, return the set of intervals after removing every point that lies inside `toBeRemoved`. | Each interval is either fully outside the removal range (keep as is) or partially overlaps it (keep the non-overlapping left and/or right slivers). Walk once and emit the surviving pieces. | O(n) | O(n) | keep left sliver |
| 1326 | Minimum Number of Taps to Open to Water a Garden | A garden spans `[0, n]`. Tap `i` at position `i` waters `[i - ranges[i], i + ranges[i]]`. Find the minimum number of taps to water the whole garden, or -1 if impossible. | This is a jump-game in disguise: for each starting point record the farthest reach of any tap covering it, then greedily extend coverage layer by layer like minimum jumps. | O(n) | O(n) | gap in coverage → impossible |
| 1353 | Maximum Number of Events That Can Be Attended | Each event `[start, end]` can be attended on any single day in `[start, end]`. Attend at most one event per day. Find the maximum number of events you can attend. | Process days in increasing order; among all events available on the current day, attend the one that ends soonest (a min-heap by end day) — saving longer-lived events for later days. | O(n log n) | O(n) | attend earliest-ending event |
| 1488 | Avoid Flood in The City | `rains[i] > 0` means lake `rains[i]` fills with rain on day `i`; `rains[i] == 0` is a dry day on which you may dry exactly one lake. A full lake that rains again floods. Return an array where dry days hold the lake to dry (any valid choice) and rain days hold -1, or an empty array if flooding is unavoidable. | When a lake that is already full rains again, you must have used a dry day between its two rains. Greedily assign the earliest available dry day that falls after the lake was last filled — a TreeSet of dry-day indices gives that earliest day. | O(n log n) | O(n) | no dry day available → flood |

---

### Two Interval Templates

```
MERGE DIRECTION RULE (for merge-style problems like #56, where both keys work):
    Sort by START  →  traverse FORWARD  (i = 0 → n-1), extend the END of last kept
    Sort by END    →  traverse BACKWARD (i = n-1 → 0), extend the START of last kept
    These two are exact mirror images. See #56 for both written out side by side.
    (NOTE: this mirror only applies to merging. Template 1 below sorts by end but
     still sweeps FORWARD — there the goal is counting, not merging.)

TEMPLATE 1 — Sort by END time, sweep forward, track end of last kept interval
             Use when: maximizing count of non-overlapping intervals
             Greedy insight: earliest-finishing interval leaves most room for future ones

TEMPLATE 2 — Sort by START time, sweep forward, merge when overlapping
             Use when: merging/counting overlapping intervals
             Greedy insight: processing in start order → each interval only needs to
             compare with the last merged result
```

```java
// MENTAL MODEL: sort to expose a local greedy choice, then sweep once making the locally-best pick.
// WHEN: intervals + "max non-overlapping / min arrows / merge / min rooms", or jump/partition sweeps.
// TEMPLATE 1: Sort by end, compare start
Arrays.sort(intervals, (a, b) -> a[1] - b[1]);      // sort by END time
int lastEnd = Integer.MIN_VALUE;
for (int[] interval : intervals) {
    if (interval[0] >= lastEnd) {                    // start >= lastEnd → no overlap → keep
        lastEnd = interval[1];
        // count++ or add to result
    } else {
        // overlap → skip (or count as removed)
    }
}

// TEMPLATE 2: Sort by start, compare end
Arrays.sort(intervals, (a, b) -> a[0] - b[0]);      // sort by START time
List<int[]> result = new ArrayList<>();
for (int[] interval : intervals) {
    if (result.isEmpty() || result.get(result.size()-1)[1] < interval[0]) {
        result.add(interval);                        // no overlap → new interval
    } else {
        result.get(result.size()-1)[1] =             // overlap → extend end
            Math.max(result.get(result.size()-1)[1], interval[1]);
    }
}

// TEMPLATE 3: Sort by start + min-heap of end times (multi-resource)
// USE WHEN counting simultaneous/overlapping resources — "minimum rooms", "max concurrent".
Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
PriorityQueue<Integer> pq = new PriorityQueue<>();   // min-heap of active end times
for (int[] interval : intervals) {
    if (!pq.isEmpty() && pq.peek() <= interval[0])
        pq.poll();                                   // reuse: earliest-ending resource is free
    pq.offer(interval[1]);                           // occupy a resource until interval[1]
}
// pq.size() = resources needed
```

---

### Sort-by-End vs Sort-by-Start+Heap

```
                    Sort by End             Sort by Start + Heap
Goal:               count non-overlapping   count simultaneous active
Tracks:             lastEnd (scalar)        all active end times (heap)
Question answered:  max intervals I can keep  min rooms (resources) needed
Examples:           #435, #452, #646        #253 Meeting Rooms
```

---

### Greedy Pattern Identifier

| Signal | Template |
|---|---|
| "minimum removal to make non-overlapping" | Sort by end, keep non-overlapping (Template 1) |
| "minimum resources (arrows, groups)" | Sort by end, count groups (Template 1) |
| "merge overlapping intervals" | Sort by start, extend or add (Template 2) |
| "minimum rooms/machines" | Sort by start + min-heap (Template 3) |
| "can you reach the end?" | Track max reachable index |
| "minimum steps to reach the end?" | BFS layers via `currentEnd` |
| "partition string by last occurrence" | Track `last[]` array + extend `end` |
| "reconstruct order by two constraints" | Sort by one constraint, insert by the other |
| "can you complete the circuit / circular route?" | Track cumulative tank; reset start when tank < 0 |
| "can person attend all meetings (no overlap)?" | Sort by start, compare adjacent intervals |

---
## Dynamic Programming  &nbsp;`dynamic_programming.md`

Six template families. Every problem maps to one loop skeleton and one dp-state definition.

---

### Quick Reference Table

| # | Name | Description | Intuition | Time | Space | Key Implementation |
|---|---|---|---|---|---|---|
| 70 | Climbing Stairs | Each step you can climb 1 or 2 steps. How many distinct ways to reach step n? | the last move was a 1-step or a 2-step, so ways to reach n = ways to n-1 + ways to n-2. | O(n) | O(n) | Standard |
| 198 | House Robber | Rob houses on a line — can't rob two adjacent. Maximize total. | at each house, either skip it (keep `dp[i-1]`) or rob it (`dp[i-2] + value`, since i-1 is now off-limits). | O(n) | O(n) | Standard |
| 213 | House Robber II | Houses arranged in a circle — first and last are adjacent. Can't rob both. | breaking the circle means either the first house is excluded or the last is — solve both lines and keep the better. | O(n) | O(1) | Standard |
| 300 | Longest Increasing Subsequence | Length of the longest strictly increasing subsequence. | the best subsequence ending at i extends the longest earlier one whose last value is still smaller. | O(n²) | O(n) | Standard |
| 139 | Word Break | Can `s` be segmented into a sequence of dictionary words? | a prefix is breakable if some earlier breakable cut leaves a dictionary word as the final piece. | O(n²·L) where L = substring length | O(n) | Standard |
| 416 | Partition Equal Subset Sum | Can the array be partitioned into two subsets with equal sum? |  | O(n) | O(sum) | Standard |
| 494 | Target Sum | Assign `+` or `-` to each number to reach `target`. How many ways? |  | O(n) | O(sum) | Standard |
| 474 | Ones and Zeroes | Given strings of '0'/'1', find the largest subset using at most `m` zeros and `n` ones. |  | O(l) | O(mn) | Standard |
| 322 | Coin Change | Minimum number of coins to make `amount`. Coins can be reused. |  | O(amount) | O(amount) | Standard |
| 518 | Coin Change II | Number of distinct combinations (order doesn't matter) to make `amount`. |  | O(amount) | O(amount) | Standard |
| 377 | Combination Sum IV | Number of ordered sequences (order matters) that sum to `target`. |  | O(target) | O(target) | Standard |
| 1143 | Longest Common Subsequence | Length of the longest subsequence present in both strings. | if the last chars match, they're part of the LCS (+1 on the diagonal); otherwise drop one char from whichever string and keep the better. | O(m·n) | O(m·n) | Standard |
| 72 | Edit Distance | Minimum operations (insert, delete, replace) to convert `word1` to `word2`. | matched chars cost nothing (diagonal); otherwise take the cheapest of replace/delete/insert and add 1. | O(m·n) | O(m·n) | Standard |
| 115 | Distinct Subsequences | Number of ways `s` contains `t` as a subsequence. | you can always skip the current char of s; if it matches the current char of t, you may also use it to advance t. | O(m·n) | O(m·n) | Standard |
| 647 | Palindromic Substrings | Count all palindromic substrings of `s`. | `s[i..j]` is a palindrome when its two ends match AND the inside `s[i+1..j-1]` already is. | O(n²) | O(n²) | Standard |
| 516 | Longest Palindromic Subsequence | Length of the longest subsequence of `s` that is a palindrome. | matching ends add 2 to the inner range's best; otherwise drop one end and keep the larger. | O(n²) | O(n²) | Standard |
| 312 | Burst Balloons | Burst all balloons to maximize coins. Coins from bursting balloon `k` between open boundaries `i` and `j` = `balloons[i] * balloons[k] * balloons[j]`. |  | O(n³) | O(n²) | Standard |
| 62 | Unique Paths | Number of paths from top-left to bottom-right, moving only right or down. | you reach a cell only from above or from the left, so its path count is the sum of those two. | O(m·n) | O(m·n) | Standard |
| 64 | Minimum Path Sum | Minimum sum path from top-left to bottom-right, moving only right or down. | the cheapest way into a cell is its own value plus the cheaper of the cell above or to its left. | O(m·n) | O(m·n) | Standard |
| 221 | Maximal Square | Find the largest all-1 square in a binary matrix. Return its area. |  | O(m·n) | O(m·n) | Standard |
| 329 | Longest Increasing Path in a Matrix | Find the longest strictly increasing path. Can move in all 4 directions. | strictly increasing values forbid revisiting, so each cell's longest path is 1 + the best of its larger neighbors — cache it. | O(m·n) | O(m·n) | Standard |
| 121 | Best Time to Buy and Sell Stock (at most 1 transaction) |  | `hold` is the best profit if you currently own a share bought at the lowest price seen; sell whenever today's price beats that. | O(n) | O(1) | Standard |
| 122 | Best Time to Buy and Sell Stock II (unlimited transactions) |  | with unlimited trades, buying can fund itself from accumulated `cash`, so capture every upward move. | O(n) | O(1) | Standard |
| 123 | Best Time to Buy and Sell Stock III (at most 2 transactions) |  | the second buy can only spend profit left after the first sell, so chain the states in trade order. | O(n) | O(1) | Standard |
| 309 | Best Time to Buy and Sell Stock with Cooldown | After selling, must wait 1 day before buying again. | the cooldown forces buying to draw from cash that's at least one day old, so carry yesterday's cash forward. | O(n) | O(1) | Standard |
| 714 | Best Time to Buy and Sell Stock with Transaction Fee | Pay a fee per transaction (on sell). Unlimited transactions. | the fee just shrinks every sale, so a trade is only worth making when the gain clears the fee. | O(n) | O(1) | Standard |
| 746 | Min Cost Climbing Stairs | Each step has a cost. You can start from index 0 or 1, and from each step you can climb 1 or 2 steps. Return the minimum cost to reach the top (past the last index). |  | O(n) | O(n) | Standard |
| 91 | Decode Ways | A string of digits can be decoded: '1'-'9' → single letter, "10"-"26" → two-digit letter. Count total decoding ways. |  | O(n) | O(n) | Two sources at each position. If the current digit is non-zero, it can be decoded alone (`dp[i] += dp[i-1]`). If the previous two digits form a valid two-letter code (10-26), add `dp[i-2]`. |
| 279 | Perfect Squares | Return the minimum number of perfect squares (1, 4, 9, 16, ...) that sum to `n`. |  | O(n√n) | O(n) | iterate all squares ≤ i |
| 96 | Unique Binary Search Trees | Return the number of structurally unique BSTs that store values 1 to n. |  | O(n²) | O(n) | Catalan number recurrence. `dp[i]` = number of unique BSTs with i nodes. When root = j, left subtree has j-1 nodes, right subtree has i-j nodes: `dp[i] += dp[j-1] * dp[i-j]`. |
| 63 | Unique Paths II | A robot moves from top-left to bottom-right in an m×n grid with obstacles. Count unique paths. Cells with `obstacleGrid[i][j] == 1` are blocked. |  | O(m·n) | O(m·n) | Same as #62 (Unique Paths) but skip cells with obstacles: `dp[i][j] = 0` if blocked, else `dp[i-1][j] + dp[i][j-1]`. |
| 583 | Delete Operation for Two Strings | Return the minimum number of deletions to make `word1` and `word2` equal. |  | O(m·n) | O(m·n) | Reduce to LCS. Minimum deletions = `len(word1) + len(word2) - 2 * LCS(word1, word2)`. Compute LCS using standard 2D DP. |
| 368 | Largest Divisible Subset | Find the largest subset of distinct positive integers such that for every pair (a, b), either `a % b == 0` or `b % a == 0`. |  | O(n²) | O(n) | Sort first, then apply LIS-style DP. `dp[i]` = size of largest divisible subset ending at `nums[i]`. If `nums[i] % nums[j] == 0`, then `dp[i] = max(dp[i], dp[j] + 1)`. Track parent indices to reconstruct the subset. |
| 931 | Minimum Falling Path Sum | Given an n×n matrix, return the minimum sum of a falling path. A falling path starts at any element in the first row and chooses the element directly below or diagonally adjacent in each row. |  | O(n²) | O(n²) | Grid DP with three sources from the row above. `dp[i][j] = matrix[i][j] + min(dp[i-1][j-1], dp[i-1][j], dp[i-1][j+1])`. |
| 10 | Regular Expression Matching | Implement regex matching with `.` (any single char) and `*` (zero or more of the preceding element). Match must cover the entire input string. |  | O(m·n) | O(m·n) | 2D DP. `dp[i][j]` = whether `s[0..i)` matches `p[0..j)`. The `*` has two cases: zero occurrences (`dp[i][j-2]`) or one-more occurrence when the preceding pattern char matches `s[i-1]`. |
| 87 | Scramble String | Given s1 and s2, return true if s2 is a scrambled string of s1 (formed by recursively partitioning into two non-empty substrings and optionally swapping them). |  | O(n⁴) | O(n³) | memoized recursion over (i1, i2, len). At each length, try every split point both swapped and non-swapped. |
| 1049 | Last Stone Weight II | Repeatedly smash the two heaviest stones (result is their difference). Return the smallest possible weight of the remaining stone. |  | O(n·sum) | O(sum) | equivalent to splitting stones into two groups to minimize the difference of their sums. 0/1 knapsack to find the max subset sum ≤ total/2. |
| 1312 | Minimum Insertion Steps to Make a String Palindrome | Return the minimum number of insertions needed to make a string a palindrome. |  | O(n²) | O(n²) | answer = n − longest palindromic subsequence (LPS). LPS = LCS of the string and its reverse; or solve directly via interval DP. |
| 44 | Wildcard Matching | Match string `s` against pattern `p` with `?` (any single char) and `*` (any sequence including empty). | `*` either consumes one more char of `s` (`dp[i-1][j]`) or matches empty (`dp[i][j-1]`); everything else is a 1-to-1 char/`?` match. | O(m·n) | O(m·n) | '*' matches empty prefix |
| 53 | Maximum Subarray | Find the contiguous subarray with the largest sum. | the best sum ending at `i` either extends the previous best or restarts at `nums[i]` (Kadane). | O(n) | O(1) | Kadane restart vs extend |
| 97 | Interleaving String | Return whether `s3` is formed by interleaving `s1` and `s2` while preserving each one's order. | the last char of `s3[0..i+j)` comes from either `s1` or `s2`; reuse the answer for the smaller prefix. | O(m·n) | O(m·n) | take from s1 |
| 120 | Triangle | Find the minimum path sum from top to bottom, moving to adjacent indices on the row below. | working bottom-up, each cell's best is its value plus the cheaper of the two children directly below. | O(n²) | O(n) | bottom-up over rows |
| 132 | Palindrome Partitioning II | Return the minimum number of cuts so that every substring of the partition is a palindrome. | if `s[j..i]` is a palindrome, a cut after `j-1` lets `cuts[i] = cuts[j-1] + 1`; precompute palindromes with interval DP. | O(n²) | O(n²) | interval DP precompute palindromes |
| 140 | Word Break II | Return all sentences obtained by segmenting `s` into space-separated dictionary words. | memoize on each suffix the list of valid segmentations, prepending each matching word to the segmentations of the remainder. | O(n²·2ⁿ) worst case | O(2ⁿ) | memoized DFS returns sentences |
| 152 | Maximum Product Subarray | Find the contiguous subarray with the largest product. | a negative number flips max and min, so track both; the running max product ending at `i` may come from the prior max or min. | O(n) | O(1) | negative swaps max/min |
| 174 | Dungeon Game | Find the minimum starting health so the knight survives from top-left to bottom-right (each cell adds/subtracts health, must stay ≥ 1). | health needed depends on the future, so fill from the bottom-right: needed entering a cell = max(1, min child need − cell value). | O(m·n) | O(m·n) | fill from bottom-right |
| 188 | Best Time to Buy and Sell Stock IV | Maximize profit with at most `k` transactions. | for each allowed transaction count `t`, track best buy and sell; this is #123 generalized to `k` chained state pairs. | O(n·k) | O(k) | k chained state pairs |
| 264 | Ugly Number II | Find the nth ugly number (positive integers whose only prime factors are 2, 3, 5). | every ugly number is a previous ugly number times 2, 3, or 5; merge the three multiples with pointers. | O(n) | O(n) | merge multiples via pointers |
| 313 | Super Ugly Number | Find the nth super ugly number whose prime factors all come from a given `primes` list. | generalize #264 to arbitrary primes — keep one pointer per prime and pick the minimum next candidate. | O(n·k) | O(n+k) | one pointer per prime |
| 337 | House Robber III | Houses form a binary tree; you cannot rob two directly-linked houses. Maximize the total. | each node returns two values — best if it is robbed (skip children) vs not robbed (children free to choose). | O(n) | O(h) | tree DP returns {notRob, rob} |
| 343 | Integer Break | Break `n` into the sum of at least two positive integers maximizing their product. | for each split `j`, the rest can stay as `i-j` or be broken further (`dp[i-j]`); take the best. | O(n²) | O(n) | split point, break further or not |
| 375 | Guess Number Higher or Lower II | Find the minimum amount of money to guarantee a win when guessing a number in `[1, n]`, paying the guessed value on each wrong guess. | for range `[i,j]`, guessing `k` costs `k` plus the worst of the two resulting subranges; minimize over `k`. | O(n³) | O(n²) | interval DP over range length |
| 376 | Wiggle Subsequence | Find the length of the longest subsequence whose consecutive differences strictly alternate between positive and negative. | track the best subsequence ending with an up-move and with a down-move; each rise extends `down`, each fall extends `up`. | O(n) | O(1) | rise extends down-ending seq |
| 413 | Arithmetic Slices | Count the number of arithmetic subarrays (length ≥ 3, constant difference). | if `nums[i]` continues the arithmetic run ending at `i-1`, it adds `dp[i-1]+1` new slices ending at `i`. | O(n) | O(1) | extend arithmetic run |
| 446 | Arithmetic Slices II - Subsequence | Count the arithmetic subsequences (length ≥ 3) of the array. | for each pair `(j, i)` with difference `d`, weak slices ending at `i` extend those ending at `j`; promote weak to valid when length reaches 3. | O(n²) | O(n²) | per-index map keyed by difference |
| 486 | Predict the Winner | Two players alternately take a number from either end; decide whether player 1 can win (score ≥ player 2). | on range `[i,j]` the current player maximizes value − opponent's best on the remaining range. | O(n²) | O(n²) | interval DP, score difference |
| 509 | Fibonacci Number | Return the nth Fibonacci number. | each term is the sum of the previous two — the canonical linear 1D recurrence. | O(n) | O(1) | Standard |
| 552 | Student Attendance Record II | Count length-`n` attendance records that are rewardable (at most one 'A', no three consecutive 'L'), modulo 1e9+7. | state = (number of 'A's so far 0/1, trailing 'L' run 0/1/2); each day append P, A, or L respecting limits. | O(n) | O(1) | state = (A count, trailing L run) |
| 576 | Out of Boundary Paths | Count paths that move a ball off the grid in exactly `maxMove` steps from a start cell, modulo 1e9+7. | moving off the boundary counts as one path; otherwise spread current-step counts to 4 neighbors for the next step. | O(maxMove·m·n) | O(m·n) | spread to 4 neighbors |
| 600 | Non-negative Integers without Consecutive Ones | Count integers in `[0, n]` whose binary representation has no two adjacent 1 bits. | scan bits high-to-low; precompute Fibonacci-style counts of valid suffixes, adding them when a free bit is `1`, and stop early if two consecutive 1s appear in `n`. | O(1) (32 bits) | O(1) | fib[i] = valid i-bit strings |
| 629 | K Inverse Pairs Array | Count permutations of `1..n` with exactly `k` inverse pairs, modulo 1e9+7. | inserting `n` into a permutation of `1..n-1` adds `0..n-1` inversions; this gives a sliding-window sum over the previous row. | O(n·k) | O(n·k) | prefix sums of previous row |
| 638 | Shopping Offers | Buy exactly `needs[i]` of each item at minimum cost, given unit prices and special bundle offers (each usable multiple times). | treat the remaining needs vector as the state; either buy everything at unit price, or apply an affordable offer and recurse. | O(offers·∏needsᵢ) | O(∏needsᵢ) | DFS+memo over needs vector |
| 639 | Decode Ways II | Count decodings of a digit string where `*` is a wildcard for digits 1-9, modulo 1e9+7. | extend #91 — each position can decode one char (count 1-9 options) or two chars (count valid 10-26 combinations); `*` multiplies the options. | O(n) | O(n) | single char, count options |
| 650 | 2 Keys Keyboard | Starting with one 'A', using only Copy-All and Paste, return the minimum operations to obtain `n` 'A's. | the answer is the sum of `n`'s prime factors — building `i` from a divisor `j` costs `i/j` operations. | O(n√n) | O(n) | build i from divisor j |
| 673 | Number of Longest Increasing Subsequence | Count the number of longest strictly increasing subsequences. | alongside LIS length, track how many ways achieve it; a longer extension resets the count, an equal-length extension accumulates it. | O(n²) | O(n) | longer extension resets count |
| 674 | Longest Continuous Increasing Subsequence | Find the length of the longest continuous (contiguous) strictly increasing subarray. | extend the current run while values rise, otherwise restart; a simpler linear scan of #300. | O(n) | O(1) | contiguous run, reset on drop |
| 688 | Knight Probability in Chessboard | Return the probability that a knight remains on an `n×n` board after exactly `k` moves from a start cell, each move chosen uniformly among 8. | spread the probability at each cell to its 8 knight-move targets per step; off-board moves lose probability. | O(k·n²) | O(n²) | 8 knight moves, each prob 1/8 |
| 718 | Maximum Length of Repeated Subarray | Find the length of the longest subarray common to two arrays (contiguous). | unlike LCS, the match must be contiguous, so a mismatch resets the running length to 0. | O(m·n) | O(m·n) | contiguous, no carry on mismatch |
| 740 | Delete and Earn | Deleting `nums[i]` earns its value but removes all copies of `nums[i]-1` and `nums[i]+1`; maximize earnings. | bucket points by value, then it becomes House Robber over the value line — you cannot take adjacent values. | O(n + max) | O(max) | bucket points by value |
| 873 | Length of Longest Fibonacci Subsequence | Given a strictly increasing array, find the length of the longest Fibonacci-like subsequence (each term = sum of the previous two). | a fib-like subseq is determined by its last two elements `(j, i)`; look up whether the required predecessor `arr[i]-arr[j]` exists earlier. | O(n²) | O(n²) | predecessor before arr[j] |
| 887 | Super Egg Drop | With `k` eggs and `n` floors, return the minimum number of moves to determine the critical floor in the worst case. | invert the problem — `dp[m][k]` = highest floor count solvable with `m` moves and `k` eggs; a move either breaks (test below) or survives (test above), plus the current floor. | O(k·log n) | O(n·k) | dp[m][k] = floors solvable in m moves |
| 918 | Maximum Sum Circular Subarray | Find the maximum subarray sum where the array is circular (subarray may wrap around). | the answer is either a normal max subarray (Kadane) or the total minus the minimum subarray (wrap); guard the all-negative case. | O(n) | O(1) | track min subarray for wrap |
| 935 | Knight Dialer | Count distinct phone numbers of length `n` dialable by knight moves on a phone keypad, modulo 1e9+7. | from each digit a knight can reach a fixed set of digits; spread counts across the adjacency map each step. | O(n) | O(1) | knight adjacency per digit |
| 983 | Minimum Cost For Tickets | Given travel days and the cost of 1-day, 7-day, and 30-day passes, return the minimum cost to cover all travel days. | on a travel day choose the cheapest pass covering it by looking back 1, 7, or 30 days; non-travel days inherit the prior cost. | O(lastDay) | O(lastDay) | non-travel day inherits cost |
| 1027 | Longest Arithmetic Subsequence | Find the length of the longest arithmetic subsequence (constant difference). | for each pair `(j, i)`, the arithmetic subseq ending at `i` with difference `d` extends the one ending at `j`. | O(n²) | O(n²) | per-index map keyed by difference |
| 1048 | Longest String Chain | Find the longest chain of words where each word is a predecessor of the next (insert exactly one char). | sort by length; for each word, try removing each character to find a shorter predecessor and extend its best chain. | O(n·L²) | O(n) | process shortest first |
| 1137 | N-th Tribonacci Number | Return the nth Tribonacci number (each term is the sum of the previous three). | the linear 1D recurrence with three rolling variables instead of two. | O(n) | O(1) | sum of previous three |
| 1216 | Valid Palindrome III | Return whether `s` becomes a palindrome after removing at most `k` characters. | the minimum removals to make `s` a palindrome equals `n − LPS(s)`; check whether that is `≤ k`. | O(n²) | O(n²) | interval DP for LPS |
| 1218 | Longest Arithmetic Subsequence of Given Difference | Find the longest arithmetic subsequence with a fixed difference `difference`. | with a known difference, the predecessor of `num` must be `num - difference`; one hashmap pass suffices. | O(n) | O(n) | fixed difference, value-keyed map |
| 1269 | Number of Ways to Stay in the Same Place After Some Steps | Count the ways to return to index 0 after `steps` moves (stay, left, or right) without leaving an array of size `arrLen`, modulo 1e9+7. | position can never exceed `steps/2`, so cap the reachable range; each step a position spreads to stay/left/right. | O(steps·min(arrLen, steps)) | O(min(arrLen, steps)) | cap reachable positions |
| 1395 | Count Number of Teams | Count triplets `(i, j, k)` with `i < j < k` whose ratings are strictly increasing or strictly decreasing. | fix the middle soldier `j`; the answer is its number of smaller-before × larger-after, plus the mirror case. | O(n²) | O(1) | fix middle soldier |
| 1567 | Maximum Length of Subarray With Positive Product | Find the length of the longest subarray whose product is positive. | track the lengths of positive-product and negative-product runs ending at `i`; a negative number swaps them, a zero resets both. | O(n) | O(1) | zero resets both runs |
| 1696 | Jump Game VI | From index 0, each move jumps 1 to `k` indices forward; maximize the sum of values landed on, reaching the last index. | `dp[i]` = best score reaching `i` = `nums[i] +` max `dp[j]` in the window `[i-k, i-1]`; a monotonic queue keeps that window max in O(1). | O(n) | O(n) | monotonic queue of indices |
| 1884 | Egg Drop With 2 Eggs and N Floors | With exactly 2 eggs and `n` floors, return the minimum number of moves to determine the critical floor in the worst case. | `dp[i]` = min worst-case moves for `i` floors; dropping at floor `j` costs `1 + max(dp[j-1] from break, dp[i-j] from survive)`. | O(n²) | O(n) | first drop at floor j |

---

### All Six Templates

```java
// 1. LINEAR 1D — each cell depends on a fixed number of previous cells
// MENTAL MODEL: the answer at i is a fixed recipe over the last one or two answers.
// WHEN: "ways/cost to reach step i", "can't pick adjacent"
int[] dp = new int[n + 1];
dp[0] = base;
for (int i = 1; i <= n; i++)
    dp[i] = f(dp[i-1], dp[i-2], ...);

// 2A. LOOK-BACK 1D — dp[i] depends on all j < i
// MENTAL MODEL: to finish position i, scan every earlier position j and extend the best valid one.
// WHEN: "longest increasing/chain ending here", "can the prefix be segmented"
int[] dp = new int[n];
for (int i = 0; i < n; i++) {
    for (int j = 0; j < i; j++) {
        dp[i] = f(dp[i], dp[j]);        // e.g., LIS, word break
    }
}

// ──────────────────────────────────────────────────────────────
// MENTAL MODEL: both are the same 2D recurrence collapsed to 1D.
//   dp[i][j] = ways to make sum j using the first i items.
//   After dropping the i dimension, dp[j-nums[i]] is read from:
//     • the PREVIOUS row (item i not yet used)  → 0/1, no reuse
//     • the CURRENT  row (item i already used)   → unbounded, reuse
//   Loop direction decides which one you read.
// Mnemonic: DESCENDING = Distinct (each once), ASCENDING = Again (reusable).
// Seed/operator picks the flavor:
//   count       → dp[0]=1, dp[j] += dp[j-w]
//   max-value   → dp[0]=0, dp[j] = Math.max(dp[j], dp[j-w] + v)
// ──────────────────────────────────────────────────────────────

// 2B. KNAPSACK 0/1 — each item at most once
int[] dp = new int[target + 1];
dp[0] = 1;                                       // 1 way to make 0: take nothing
for (int i = 0; i < nums.length; i++)
    for (int j = target; j >= nums[i]; j--)      // ↓ DESCENDING
        dp[j] += dp[j - nums[i]];
        //         ^^^^^^^^^^^^^ j-nums[i] < j, not yet touched THIS pass
        //                       → still "previous row" → item i unused → no reuse

// 2C. KNAPSACK UNBOUNDED — each item reusable
int[] dp = new int[target + 1];
dp[0] = 1;
for (int i = 0; i < nums.length; i++)
    for (int j = nums[i]; j <= target; j++)      // ↑ ASCENDING
        dp[j] += dp[j - nums[i]];
        //         ^^^^^^^^^^^^^ j-nums[i] < j, ALREADY updated THIS pass
        //                       → "current row" → item i can reappear → reuse

// 3. 2D SEQUENCE — two strings/arrays; i indexes one, j indexes the other
// MENTAL MODEL: compare the last char of each prefix — match consumes both, mismatch drops one side.
// WHEN: "compare two strings/arrays" (LCS, edit distance, subsequence count)
int[][] dp = new int[m + 1][n + 1];
for (int i = 1; i <= m; i++) {
    for (int j = 1; j <= n; j++) {
        if (match(i, j)) {
            dp[i][j] = dp[i-1][j-1] + val;
        } else {
            dp[i][j] = combine(dp[i-1][j], dp[i][j-1]);
        }
    }
}

// 4. INTERVAL DP — i goes RIGHT to LEFT; j goes i+1 to end
//    "shorter comes first": when computing dp[i][j], dp[i+1][*] is already done
// MENTAL MODEL: build answers for short ranges first, then combine them into longer ranges.
// WHEN: "palindrome substring/subseq", "merge/burst in a range", split-point problems
int[][] dp = new int[n][n];
for (int i = 0; i < n; i++) dp[i][i] = base;   // length-1 intervals
for (int i = n - 1; i >= 0; i--) {              // ← right-to-left
    for (int j = i + 1; j < n; j++) {
        dp[i][j] = f(dp[i+1][j-1], dp[i+1][j], dp[i][j-1]);
    }
}

// 5. GRID DP — 4-directional neighbors
// MENTAL MODEL: each cell's answer accumulates from the cells you could have arrived from.
// WHEN: "paths / min-cost in a grid moving right+down", "largest square"
int[] dr = {1,-1,0,0}, dc = {0,0,1,-1};   // DOWN UP RIGHT LEFT
// Standard grid (dag, only right/down):
int[][] dp = new int[rows][cols];
for (int i = 0; i < rows; i++)
    for (int j = 0; j < cols; j++)
        dp[i][j] = grid[i][j] + combine(dp[i-1][j], dp[i][j-1]);

// 6. STATE MACHINE — named states updated simultaneously each step
// MENTAL MODEL: track the best value in each named situation; each day every state updates from yesterday's states.
// WHEN: "buy/sell/hold", "limited transactions", "cooldown/fee"
int cash = 0, hold = -prices[0];
for (int i = 1; i < prices.length; i++) {
    cash = Math.max(cash, hold + prices[i]);
    hold = Math.max(hold, ??? - prices[i]);   // ??? depends on problem
}
```

#### Knapsack Decision Tree

```
Want count or min/max?
├── Count (dp[j] += dp[j - num])
│   ├── 0/1 (each item once):    j descending → #416, #494
│   └── Unbounded (reuse):       j ascending  → #518
│       └── Ordered (permuts):   target outer, nums inner → #377
└── Min/Max (dp[j] = min/max(...))
    ├── 0/1 minimize:            j descending → #474 (maximize)
    └── Unbounded minimize:      j ascending  → #322
```

---

### Canonical Templates

```java
// ── 0/1 KNAPSACK ── each item at most once
int[] dp = new int[target + 1];
dp[0] = 1;
for (int i = 0; i < nums.length; i++) {
    for (int j = target; j >= nums[i]; j--)   // DESCENDING: sees OLD dp (before item i)
        dp[j] += dp[j - nums[i]];
}

// ── UNBOUNDED KNAPSACK ── each item reusable
int[] dp = new int[target + 1];
dp[0] = 1;
for (int i = 0; i < nums.length; i++) {
    for (int j = nums[i]; j <= target; j++)    // ASCENDING: sees NEW dp (after item i already used)
        dp[j] += dp[j - nums[i]];
}

// ── PERMUTATION COUNT ── order matters (Combination Sum IV)
int[] dp = new int[target + 1];
dp[0] = 1;
for (int j = 1; j <= target; j++) {           // OUTER: target
    for (int num : nums) {                     // INNER: try all nums (not fixing order)
        if (j >= num) dp[j] += dp[j - num];
    }
}
```

**Why descending for 0/1:**  
`dp[j - nums[i]]` is read **before** `dp[j]` is updated (j > j-nums[i]). So it always sees the dp state from before item `i` was considered — no item is used twice.

**Why ascending for unbounded:**  
`dp[j - nums[i]]` was already updated in this same pass (j - nums[i] < j, processed earlier). This allows item `i` to be picked multiple times.

**2D anchor:** both loops are `dp[i][j] = dp[i-1][j] + dp[i-?][j-w]` collapsed to 1D — descending keeps `dp[j-w]` on the *previous* row (item i unused), ascending pulls it from the *current* row (item i reused).

**Mnemonic:** DESCENDING = **D**istinct (each item once), ASCENDING = **A**gain (reusable).

**Flavor = seed + operator (same skeleton):**
- count → `dp[0]=1`, `dp[j] += dp[j-w]`
- feasibility → `dp[0]=true`, `dp[j] = dp[j] || dp[j-w]`
- max-value → `dp[0]=0`, `dp[j] = Math.max(dp[j], dp[j-w] + v)`

---

### Canonical Template

```java
// i indexes string/array 1 (1-indexed), j indexes string/array 2
int[][] dp = new int[m + 1][n + 1];
// Init dp[0][*] and dp[*][0] based on problem
for (int i = 1; i <= m; i++) {
    for (int j = 1; j <= n; j++) {
        if (s1.charAt(i-1) == s2.charAt(j-1)) {
            dp[i][j] = dp[i-1][j-1] + 1;          // characters match
        } else {
            dp[i][j] = combine(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]);
        }
    }
}
```

---

### Canonical Template

**Rule:** `i` goes right-to-left (ensures shorter/inner intervals are computed first). `j` goes left-to-right from `i+1`. When computing `dp[i][j]`, all `dp[i'][j']` with `i' > i` or `j' < j` are already done.

```java
int[][] dp = new int[n][n];
for (int i = 0; i < n; i++) dp[i][i] = base_case;   // single elements
for (int i = n - 1; i >= 0; i--) {                   // right-to-left
    for (int j = i + 1; j < n; j++) {                // left-to-right from i+1
        // dp[i][j] can safely use dp[i+1][j], dp[i][j-1], dp[i+1][j-1]
        dp[i][j] = ...;
    }
}
```

**Alternative (length-based):** Equivalent, sometimes clearer for k-partition problems:

```java
for (int len = 2; len <= n; len++) {           // outer: length of interval
    for (int i = 0; i + len - 1 < n; i++) {   // inner: left endpoint
        int j = i + len - 1;
        dp[i][j] = ...;
    }
}
```

**Alternative (forward `i`, inner `j` descending):** `i` is the right endpoint going left-to-right; `j` is the left endpoint sweeping back from `i-1`. Inner intervals (larger `j`, smaller `i`) are already filled.

```java
int[][] dp = new int[n][n];
for (int i = 0; i < n; i++) dp[i][i] = base_case;   // single elements
for (int i = 0; i < n; i++) {                        // i = right endpoint, left-to-right
    for (int j = i - 1; j >= 0; j--) {               // j = left endpoint, from i-1 down to 0
        // dp[i][j] can safely use dp[i-1][j], dp[i][j+1], dp[i-1][j+1]
        dp[i][j] = ...;
    }
}
```

**Alternative (triangular fill, column base case):** used when `dp[i][j]` depends only on the previous row/column (e.g. counting problems). Fill row by row with `j` from `0` to `i`.

```java
int[][] dp = new int[n][n];
for (int i = 0; i < n; i++) dp[i][0] = 1;   // base: dp[i][0] = 1; dp[0][j] = 0 for j > 0
for (int i = 1; i < n; i++) {
    for (int j = 1; j <= i; j++) {           // j from 1 to i
        // dp[i][j] can safely use dp[i-1][j], dp[i][j-1], dp[i-1][j-1]
        dp[i][j] = ...;
    }
}
```

---

### Canonical Template

```java
int[] dr = {1,-1,0,0}, dc = {0,0,1,-1};   // DOWN UP RIGHT LEFT

// Standard grid (only move right/down — DAG, no cycle):
int[][] dp = new int[rows][cols];
// initialize first row and first column
for (int i = 0; i < rows; i++)
    for (int j = 0; j < cols; j++)
        dp[i][j] = grid[i][j] + f(dp[i-1][j], dp[i][j-1]);

// All-direction grid (memoized DFS for increasing/decreasing paths):
int[][] memo = new int[rows][cols];
for (int i = 0; i < rows; i++)
    for (int j = 0; j < cols; j++)
        dfs(grid, i, j, memo, dr, dc);
```

---

### Canonical States

```
cash      = max profit when NOT holding (free to buy or idle)
hold      = max profit when HOLDING stock (bought it at some cost)
cooldown  = max profit right after selling (can't buy today)
```

### All Five Transitions

```
                    buy                 sell                re-buy condition
#121 (1 tx):        hold = max(hold, -price)                no re-buy (ignore cash)
#122 (unlimited):   hold = max(hold, cash - price)          re-buy with full cash
#123 (2 tx):        chain: buy2 uses sell1 cash             4 states chained
#309 (cooldown):    hold = max(hold, cooldown - price)      must wait 1 day
#714 (fee):         hold = max(hold, cash - price)          pay fee on sell
```

---

### Stock Problems — Differences at a Glance

```
Problem     hold update                   cash update                 Extra state
#121        max(hold, -price)            max(cash, hold+price)       none
#122        max(hold, cash-price)        max(cash, hold+price)       none
#123        4 variables, chained          —                           sell1 feeds buy2
#309        max(hold, cooldown-price)    max(cash, hold+price)       cooldown = prevCash
#714        max(hold, cash-price)        max(cash, hold+price-fee)   none
```

---

### Template Chooser

| Signal in problem | Template |
|---|---|
| `dp[i]` depends on `dp[i-1]`, `dp[i-2]` | Linear 1D — fixed lookback |
| `dp[i]` depends on all `dp[j]` where `j < i` | Look-back 1D — O(n²) inner loop |
| Each item used at most once, sum target | Knapsack 0/1 — j descending |
| Items reusable, sum target, order irrelevant | Knapsack Unbounded — j ascending |
| Items reusable, order matters (permutations) | Permutation count — target outer |
| Two strings/arrays, compare characters | 2D Sequence DP |
| Palindrome, substring merge, balloon burst | Interval DP — i right-to-left |
| Grid, only right/down movement | Grid DP — cumulative from edges |
| Grid, all 4 directions, monotone constraint | DFS + memo (no cycle in DAG) |
| Buy/sell/hold decision changes day to day | State Machine — named states |

---
## Trie  &nbsp;`trie.md`

---

### Quick Reference Table

| # | Name | Description | Intuition | Time | Space | Key Implementation |
|---|---|---|---|---|---|---|
| 208 | Implement Trie | Implement `insert(word)`, `search(word)`, and `startsWith(prefix)`. | each word is a path of letters down the tree; shared prefixes share the same path, so searching is just walking that path. | O(k) per operation, k = word length | O(n·k) total | Standard |
| 211 | Design Add and Search Words Data Structure | Same as Trie but `search` supports `.` which matches any single letter. |  | O(k) insert, O(26^k) search worst case (all `.`) | O(n·k) | when character is `.`, recursively try every non-null child. |
| 212 | Word Search II | Given a board and a list of words, find all words that exist in the board (connected adjacent cells, no reuse). |  | O(M·N·4·3^(L-1)) where L = max word length | O(total chars in words) | build a Trie from the word list; during grid DFS, follow the Trie path to prune branches that can't form any word. This avoids re-scanning the grid for each word independently. |
| 648 | Replace Words | Replace every word in a sentence with its shortest root from a dictionary. If multiple roots are prefixes, use the shortest. |  | O(n·k) build + O(sentence) search | O(dict·k) | insert dictionary into Trie. For each word in sentence, traverse the Trie and return immediately when `isEnd` is hit — that's the shortest matching root. |
| 1268 | Search Suggestions System | For each prefix of `searchWord` (length 1, 2, ..., n), return up to 3 products from `products` that share that prefix, in lexicographic order. |  | O(n·k·log n) build + O(k) search | O(n·k) | sort products first, then insert into Trie. At each node on the insertion path, cache the word (up to 3) — since products are sorted, the first 3 cached are always lexicographically smallest. Lookup is then O(1) per prefix. |
| 745 | Prefix and Suffix Search | Design a class `WordFilter` with `f(pref, suff)` that returns the index of the word with the given prefix and suffix. If multiple words match, return the largest index. |  | O(W·L²) build, O(p+s) query | O(W·L²) where W=words.length, L=max word length | precompute all prefix-suffix pairs |
| 336 | Palindrome Pairs | Given a list of unique words, find all pairs of distinct indices `(i, j)` such that `words[i] + words[j]` is a palindrome. | insert every word **reversed** into a Trie, tagging each end node with its index. For a query word, walk the Trie char by char; whenever the remainder of the word is itself a palindrome and we sit on a complete reversed word, those two concatenate into a palindrome. | O(n·k²) where n = words count, k = max word length | O(n·k) | words whose remaining suffix is a palindrome |
| 676 | Implement Magic Dictionary | Build a dictionary from a list of words. Implement `search(word)` that returns true if you can change **exactly one** character of `word` to make it match a dictionary word. | standard Trie insert; on search, DFS the Trie tracking how many characters have been changed so far. Allow exactly one mismatch. | O(k) insert, O(26^k) search worst case | O(n·k) | exactly one change required |
| 720 | Longest Word in Dictionary | Given a list of words, return the longest word that can be built one character at a time by other words in the list. If multiple, return the lexicographically smallest. | a word is buildable only if **every** prefix of it is also a complete word in the list. Insert all words, then DFS the Trie only through `isEnd` nodes — any reachable end node represents a fully buildable word. | O(n·k) build + O(n·k) DFS | O(n·k) | longest, ties broken lexicographically |
| 1233 | Remove Sub-Folders from the Filesystem | Given a list of folder paths, remove all sub-folders so only top-level folders remain. `"/a/b"` is a sub-folder of `"/a"`. | split each path into its `/`-separated components and build a Trie keyed by component (map-based, since components are arbitrary strings). Mark the node ending a folder. A folder is a sub-folder iff some ancestor node on its path is already an `isEnd` folder. | O(n·k) where n = folders, k = avg components | O(n·k) | map keyed by path component |

---

### When to Use Trie (vs HashMap/Array)

| Signal | Use |
|---|---|
| Prefix queries / `startsWith` / autocomplete | **Trie** — shares prefixes, prefix lookup is O(k) |
| Wildcard match (`.` matches any char) | **Trie** — DFS branches over children |
| Prune a search space by shared prefixes (e.g. Word Search II) | **Trie** — dead branches cut early |
| Exact-key lookup only (no prefix logic) | **HashMap** — O(k) hash is simpler and faster, no node overhead |

---

### Canonical Template

```java
// MENTAL MODEL: every node is a shared prefix; walking down spells a word, so common prefixes are stored once.
// WHEN: "prefix / startsWith / autocomplete", "wildcard match", "prune a search by shared prefixes"

// ── TRIE NODE ──
// Array vs Map TrieNode mental model:
//   array  = O(1) per char, fixed 26 letters, wastes space when sparse
//   HashMap = variable alphabet, smaller for sparse, hashing overhead
class TrieNode {
    TrieNode[] children = new TrieNode[26];   // array-based: O(1) access, O(26) per node
    boolean isEnd = false;
}
// Alternative: Map-based (for non-lowercase or variable alphabets)
class TrieNode {
    Map<Character, TrieNode> children = new HashMap<>();
    boolean isEnd = false;
}

// ── INSERT ──
void insert(TrieNode root, String word) {
    TrieNode node = root;
    for (char c : word.toCharArray()) {
        int idx = c - 'a';
        if (node.children[idx] == null) node.children[idx] = new TrieNode();
        node = node.children[idx];
    }
    node.isEnd = true;
}

// ── SEARCH (exact match) ──
boolean search(TrieNode root, String word) {
    TrieNode node = root;
    for (char c : word.toCharArray()) {
        int idx = c - 'a';
        if (node.children[idx] == null) return false;
        node = node.children[idx];
    }
    return node.isEnd;    // must end at a marked word boundary
}

// ── STARTS WITH (prefix match) ──
boolean startsWith(TrieNode root, String prefix) {
    TrieNode node = root;
    for (char c : prefix.toCharArray()) {
        int idx = c - 'a';
        if (node.children[idx] == null) return false;
        node = node.children[idx];
    }
    return true;          // ← difference from search: don't check node.isEnd
}
```

---

### Variations

```java
// VARIATION 1: DFS for wildcard '.' (Add and Search Words)
// When char is '.', try all 26 children recursively instead of following one path.
boolean dfs(TrieNode node, String word, int i) {
    if (i == word.length()) return node.isEnd;
    char c = word.charAt(i);
    if (c == '.') {
        for (TrieNode child : node.children)            // ← VARIATION: try all children
            if (child != null && dfs(child, word, i+1)) return true;
        return false;
    }
    int idx = c - 'a';
    if (node.children[idx] == null) return false;
    return dfs(node.children[idx], word, i + 1);
}

// VARIATION 2: early-exit on isEnd (Replace Words — find shortest root)
String findRoot(TrieNode root, String word) {
    TrieNode node = root;
    for (int i = 0; i < word.length(); i++) {
        int idx = word.charAt(i) - 'a';
        if (node.children[idx] == null) return word;    // no root found → return original
        node = node.children[idx];
        if (node.isEnd) return word.substring(0, i+1);  // ← VARIATION: return at first root hit
    }
    return word;
}

// VARIATION 3: store words at each node (Search Suggestions — top-3 per prefix)
// During insert, each node on the path caches the word (up to 3).
// Products must be inserted in sorted order → first 3 are lexicographically smallest.
void insert(TrieNode root, String word) {
    TrieNode node = root;
    for (char c : word.toCharArray()) {
        int idx = c - 'a';
        if (node.children[idx] == null) node.children[idx] = new TrieNode();
        node = node.children[idx];
        if (node.words.size() < 3) node.words.add(word);  // ← VARIATION: cache at every node
    }
    node.isEnd = true;
}

// VARIATION 4: Trie + grid DFS pruning (Word Search II)
// Build Trie from word list. DFS the grid; at each cell, check if current path
// follows a Trie path. Prune entire branch if no Trie node exists.
void dfs(char[][] board, int i, int j, TrieNode node, StringBuilder path, Set<String> result) {
    if (i < 0 || i >= board.length || j < 0 || j >= board[0].length) return;
    char c = board[i][j];
    if (c == '#' || node.children[c - 'a'] == null) return;  // ← VARIATION: Trie prune
    node = node.children[c - 'a'];
    path.append(c);
    if (node.isEnd) result.add(path.toString());
    board[i][j] = '#';
    dfs(board, i+1, j, node, path, result);
    dfs(board, i-1, j, node, path, result);
    dfs(board, i, j+1, node, path, result);
    dfs(board, i, j-1, node, path, result);
    board[i][j] = c;
    path.deleteCharAt(path.length() - 1);
}
```

---

### search vs startsWith — One Line Difference

```
search:      return node.isEnd;   // must land on a word boundary
startsWith:  return true;         // any node reached = valid prefix
```

---

### Trie vs HashMap vs Sorting — When to Use Trie

| Operation | HashMap | Sorting | Trie |
|---|---|---|---|
| Exact key lookup | O(k) ✓ | O(log n · k) | O(k) |
| Prefix check | O(k) per key | O(log n) | O(k) ✓ |
| All words with prefix | O(n · k) | O(log n + result) | O(k + result) ✓ |
| Wildcard match | Not supported | Not supported | O(26^k) with DFS ✓ |
| Space | O(n · k) | O(n · k) | O(n · k) alphabet-dependent |

**Use Trie when:** prefix queries, wildcard search, or pruning a search space by shared prefixes (Word Search II).

### Insert → Search — Structural Parallel

```
Both traverse the same path. Insert creates nodes; search reads them.
The only decision point after traversal:

  search:      return node.isEnd         ← complete word?
  startsWith:  return true               ← any prefix is fine
  findRoot:    return early if isEnd     ← want the shallowest word boundary
  cache words: node.words.add(word)      ← accumulate at every node during insert
```

---
## Bit Manipulation  &nbsp;`bit_manipulation.md`

---

### Quick Reference Table

| # | Name | Description | Intuition | Time | Space | Key Implementation |
|---|---|---|---|---|---|---|
| 136 | Single Number | Array where every element appears twice except one. Find it. | XOR is its own inverse, so every duplicated pair cancels to 0 and only the lone element is left standing. | O(n) | O(1) | Standard |
| 268 | Missing Number | Array of n distinct numbers from [0, n] with one missing. Find it. | XOR-ing every index against every value pairs each present number with its index — the missing number's index has no partner to cancel. | O(n) | O(1) | XOR each index `i` with `nums[i]`. Indices 0..n XOR'd with the n elements — the missing index has no pair. |
| 137 | Single Number II | Every element appears three times except one. Find it. | XOR cancels pairs (mod 2); here we need a counter mod 3, so two state bits (`ones`, `twos`) cycle each bit through 1→2→0 and the survivor sits in `ones`. | O(n) | O(1) | Two-state XOR machine. `ones` tracks bits seen 1 mod 3 times, `twos` tracks bits seen 2 mod 3 times. When a bit reaches 3, it clears from both. |
| 260 | Single Number III | Two elements appear exactly once; all others appear twice. Find both. | XOR of all leaves `a ^ b`; any set bit in it is a bit where a and b differ, so it splits the array into two groups each holding one unique. | O(n) | O(1) | XOR all → get `a ^ b`. Use lowest set bit of `a ^ b` to partition nums into two groups (one containing `a`, one containing `b`). XOR each group independently. |
| 191 | Number of 1 Bits | Return the number of set bits in an unsigned integer. | Each `n & (n-1)` erases exactly one set bit, so the loop runs once per set bit — no need to scan all 32 positions. | O(k) k = number of set bits | O(1) | Standard |
| 338 | Counting Bits | Return an array `result` where `result[i]` = number of 1 bits in `i`, for i in [0, n]. | `i` has the same set bits as `i >> 1` plus possibly its own last bit, so reuse the already-computed smaller answer instead of recounting. | O(n) | O(n) | DP relation — `i >> 1` is `i` with last bit removed (already computed), plus the last bit `i & 1`. |
| 190 | Reverse Bits | Reverse the 32 bits of an unsigned integer. | Peel the lowest bit off `n` and stack it onto `result` from the bottom — after 32 shifts the bit order is fully mirrored. | O(32) = O(1) | O(1) | Fixed 32 iterations — each time take the LSB of `n`, append it to `result`, then shift both. |
| 201 | Bitwise AND of Numbers Range | Return the AND of all numbers in `[left, right]`. | AND only keeps bits that are 1 in every number; the low bits flip somewhere in the range, so only the common high-bit prefix of `left` and `right` survives. | O(log n) | O(1) | right-shift both until equal to find shared prefix; shift back. |
| 371 | Sum of Two Integers | Return `a + b` without using `+` or `-`. | Addition splits into a carry-free sum (XOR) and the carries (AND shifted left); feed the carry back until nothing carries over. | O(32) = O(1) | O(1) | XOR computes bit sum without carry; AND shifted left computes carry. Repeat until no carry. |
| 318 | Maximum Product of Word Lengths | Given a list of words, find the maximum product `len(a) * len(b)` where `a` and `b` share no common letters. | Compress each word's letter set into a 26-bit integer so "share a letter?" becomes a single AND, replacing slow character-by-character comparison. | O(n² + n·k) k = avg word length | O(n) | encode each word as a 26-bit integer where bit `i` = 1 if letter `'a' + i` appears. Two words share a letter iff their bitmasks have any common bit (`mask[i] & mask[j] != 0`). |
| 231 | Power of Two | Given an integer `n`, return true if it is a power of two. | A power of two is a single 1 bit, and `n & (n-1)` clears that one bit to 0 — anything else leaves bits behind. | O(1) | O(1) | single-bit property of powers of 2 |
| 342 | Power of Four | Given an integer `n`, return true if it is a power of four. | Powers of four are powers of two (one set bit) whose bit sits at an even position; masking against the odd-position mask `0xAAAAAAAA` must give 0. | O(1) | O(1) | Power of four must be power of two (one set bit) AND that bit must be at an even bit position (0, 2, 4, 6, ...). Mask `0xAAAAAAAA` has bits set at ALL odd positions; if `n & 0xAAAAAAAA == 0`, the set bit is at an even position. |
| 287 | Find the Duplicate Number | Given an array of `n+1` integers where each is in `[1, n]`, find the duplicate. No extra space, no modifying the array. | Following `i → nums[i]` turns the array into a linked list; a duplicate value means two indices point to the same node, forming a cycle whose entry is the duplicate. | O(n) | O(1) | Floyd's Cycle Detection. Treat the array as a linked list where `nums[i]` is the next node. Since there's a duplicate, two indices point to the same value → creates a cycle. Find cycle entry = duplicate. |
| 405 | Convert a Number to Hexadecimal | Given an integer `num`, return its hexadecimal representation as a lowercase string. For negative numbers use two's complement. | Hex is base 16, so each group of 4 bits maps to one hex digit; mask the lowest 4 bits with `num & 15` and shift right 4 at a time, using an unsigned shift so the two's-complement sign bit fills with zeros. | O(8) = O(1) | O(1) | Standard |
| 461 | Hamming Distance | Given two integers `x` and `y`, return the Hamming distance — the number of bit positions where they differ. | XOR sets exactly the bits where `x` and `y` differ, so the answer is just the number of set bits in `x ^ y`. | O(k) k = differing bits | O(1) | Standard |
| 476 | Number Complement | Given a positive integer `num`, return its complement: flip every bit up to and including the most significant set bit. | Build a mask of all 1s spanning the bit width of `num` (from the MSB down to bit 0), then XOR — flipping exactly the meaningful bits while leaving the leading zeros untouched. | O(log num) | O(1) | Standard |
| 957 | Prison Cells After N Days | 8 prison cells (`cells[i]` is 0 or 1) update each day: a cell becomes 1 if both neighbors are equal, else 0. The two end cells always become 0 (they lack two neighbors). Return the state after `n` days. | With only 8 cells the state space is finite, so the configuration must cycle; detect the cycle length and reduce `n` modulo it to avoid simulating huge day counts. | O(min(n, cycle) · 8) | O(states) | Standard |

---

### Canonical Template

```java
// MENTAL MODEL: bits are a set/counter — XOR cancels duplicates, AND/OR/shift edit individual bits.
// WHEN: "appears once/odd among pairs", "count set bits", "no shared letters", "power of 2/4".
// ── XOR CANCEL ── pairs cancel; lone element survives
int result = 0;
for (int num : nums) result ^= num;

// ── BIT OPERATIONS ──
boolean isSet  = ((n >> i) & 1) == 1;     // check if bit i is set
int set        = n | (1 << i);             // set bit i
int clear      = n & ~(1 << i);            // clear bit i
int toggle     = n ^ (1 << i);             // toggle bit i
int lowest     = n & (-n);                 // isolate lowest set bit
boolean isPow2 = n > 0 && (n & (n-1)) == 0;

// ── COUNT SET BITS ── Brian Kernighan: each iteration removes one set bit
// WHY n & (n-1) clears the lowest set bit:
//   n     = ...1000   (lowest set bit at this position)
//   n-1   = ...0111   (borrow flips that bit to 0 and all lower bits to 1)
//   n&(n-1)=...0000   (AND keeps higher bits, wipes the lowest set bit + below)
int count = 0;
while (n != 0) { count++; n &= (n - 1); }  // n & (n-1) clears lowest set bit

// ── BITMASK AS SET ── 26-bit integer represents presence of 26 letters
int mask = 0;
for (char c : word.toCharArray()) mask |= (1 << (c - 'a'));
// check no overlap between two words:
if ((mask[i] & mask[j]) == 0) { /* no shared letter */ }
```

---

### Variations

```java
// VARIATION 1: mod-3 state machine (Single Number II)
// MENTAL MODEL: extend XOR from mod-2 (cancel pairs) to mod-3 (cancel triples);
//               ones/twos track bits seen 1 or 2 times mod 3.
// Instead of XOR canceling pairs (mod 2), cancel triples (mod 3)
// ones = bits seen exactly 1 mod 3 times; twos = bits seen exactly 2 mod 3 times
int ones = 0, twos = 0;
for (int num : nums) {
    ones = (ones ^ num) & ~twos;    // ← add to ones if not already in twos
    twos = (twos ^ num) & ~ones;    // ← add to twos if not already in ones
}
// After all: ones holds the element appearing once (0 mod 3 remainder = survive)

// VARIATION 2: split XOR into two groups (Single Number III)
// Two unique elements a, b. XOR of all = a ^ b.
// Use lowest set bit of (a^b) to split nums into two groups → each group has one unique.
int xor  = 0;
for (int num : nums) xor ^= num;      // xor = a ^ b
int diff = xor & (-xor);              // ← lowest set bit that differs between a and b
int a = 0;
for (int num : nums)
    if ((num & diff) != 0) a ^= num;  // ← XOR one group → one unique element
int b = xor ^ a;                       // ← the other unique element

// VARIATION 3: DP relation (Counting Bits)
// dp[i] = dp[i/2] + last bit of i
// i >> 1 = i without last bit (same or fewer ones); last bit = i & 1
int[] dp = new int[n + 1];
for (int i = 1; i <= n; i++)
    dp[i] = dp[i >> 1] + (i & 1);    // ← right-shift halves the problem

// VARIATION 4: common prefix (Bitwise AND of Range)
// AND of any range [left, right]: bits that differ between left and right get cleared.
// Right-shift both until equal → find shared high-bit prefix → shift back.
int shift = 0;
while (left != right) { left >>= 1; right >>= 1; shift++; }
return left << shift;                  // ← shift back to original magnitude

// VARIATION 5: carry loop (Sum of Two Integers)
// XOR gives bit sum without carry; AND shifted left gives carry.
// Repeat until no carry remains.
int add(int a, int b) {
    while (b != 0) {
        int carry = a & b;            // ← carry bits
        a = a ^ b;                    // ← partial sum (no carry)
        b = carry << 1;               // ← carry propagated one position left
    }
    return a;
}
```

---

### Bit Trick Cheat Sheet

```java
n & (n-1)          // clear lowest set bit  → count bits, check power of 2
n & (-n)           // isolate lowest set bit → split into groups
n ^ n = 0          // same value cancels    → XOR pairs
n ^ 0 = n          // identity              → XOR with index
(n >> i) & 1       // check bit i
n | (1 << i)       // set bit i
n & ~(1 << i)      // clear bit i
n ^ (1 << i)       // toggle bit i
i >> 1             // divide by 2 (fast)
i & 1              // last bit (0 = even, 1 = odd)

// --- Divisibility by powers of two ---
(n & 1) == 0           // divisible by 2  (even)   ← LSB is the 2^0 place
(n & 1) == 1           // NOT divisible by 2 (odd)
(n & ((1 << k) - 1))   // remainder of n / 2^k ; == 0 means divisible by 2^k
(n & 3) == 0           // divisible by 4   (k = 2)
(n & 7) == 0           // divisible by 8   (k = 3)
// Note: n & 1 is safe for NEGATIVE numbers (two's complement) where
//       n % 2 returns -1 for odd negatives. Prefer & 1 for parity.
```

### Pattern Chooser

| Signal | Technique | Time |
|---|---|---|
| "appears odd/once, rest appear even/twice" | XOR all | O(n) |
| "appears once, rest appear 3 times" | mod-3 state machine (`ones`, `twos`) | O(n) |
| "two unique elements" | XOR → split by `xor & (-xor)` | O(n) |
| Count set bits | Brian Kernighan `n &= (n-1)` | O(k) k = set bits |
| Count bits for all 0..n | DP: `dp[i] = dp[i>>1] + (i&1)` | O(n) |
| AND of a range | Right-shift to find common prefix | O(log n) |
| Add without `+` | XOR + carry loop | O(1) (32 iters) |
| "no shared characters between two strings" | 26-bit bitmask, check AND == 0 | O(n²) pairwise |
| "is n a power of two?" | `n > 0 && (n & (n-1)) == 0` | O(1) |
| "is n a power of four?" | Power of 2 AND set bit at even position: `(n & 0xAAAAAAAA) == 0` | O(1) |
| "find duplicate, no extra space, no modification" | Floyd's cycle detection on array-as-linked-list | O(n) |

---
## Design  &nbsp;`design.md`

---

### Quick Reference Table

| # | Name | Description | Intuition | Time | Space | Key Implementation |
|---|---|---|---|---|---|---|
| 146 | LRU Cache | Design a data structure that follows the LRU (Least Recently Used) eviction policy. `get(key)` returns the value or -1. `put(key, value)` inserts/updates; evicts LRU when over capacity. Both operations must be O(1). | the HashMap answers "where is this key" instantly while the linked list keeps everything ordered by recency, so the victim to evict is always the node next to the tail. | O(1) get/put | O(capacity) | Standard |
| 460 | LFU Cache | Design a data structure for a Least Frequently Used cache. Both `get` and `put` must be O(1). On eviction, remove the least frequently used key; among ties in frequency, remove the least recently used. | bucket keys by how often they're used; the eviction victim is always the oldest key in the lowest-frequency bucket, which `minFreq` points straight at. | O(1) all operations | O(capacity) | frequency tracking on every access |
| 380 | Insert Delete GetRandom O(1) | Design a set where `insert`, `remove`, and `getRandom` all run in O(1) average time. `getRandom` returns any element with equal probability. | an array gives O(1) random indexing but O(n) middle-deletion; swapping the victim with the last element turns deletion into an O(1) pop while staying dense. | O(1) all ops | O(n) | swap target with last element |
| 170 | Two Sum III - Data structure design | Design a data structure with `add(number)` to store a number and `find(value)` returning true if any pair of stored numbers sums to `value`. | the complement check from classic Two Sum, but persisted across calls; the frequency map lets a single number satisfy a pair only when it appears at least twice. | O(1) add, O(n) find | O(n) | Standard |
| 173 | Binary Search Tree Iterator | Implement an iterator over a BST: `next()` returns the next smallest element and `hasNext()` reports whether one exists. Use O(h) memory. | an in-order traversal paused mid-flight — the stack stores exactly the unvisited ancestors, so memory stays proportional to tree height. | O(1) amortized next/hasNext | O(h) | Standard |
| 244 | Shortest Word Distance II | Initialize with a word list. `shortest(word1, word2)` returns the minimum index distance between the two words, supporting repeated queries efficiently. | because both index lists are sorted, the closest pair is found by always advancing the pointer at the smaller index — the same merge step as in sorted-list intersection. | O(n) init, O(a+b) per query | O(n) | Standard |
| 245 | Shortest Word Distance III | Given a word list and two words (which may be equal), return the shortest index distance. When `word1 == word2`, find the closest pair of distinct occurrences of that word. | one scan suffices for a single query; the equal-word case is just "closest pair of repeated occurrences," handled by remembering the previous match. | O(n) | O(1) | equal words use previous i |
| 251 | Flatten 2D Vector | Design an iterator over a 2D vector with `next()` and `hasNext()` that yields all elements in row-major order. | keep a `(row, col)` cursor and lazily skip empty rows; the skip logic concentrated in one helper keeps both methods correct. | O(1) amortized per call | O(1) | Standard |
| 281 | Zigzag Iterator | Given two lists, design an iterator that returns elements alternating between them; when one is exhausted, continue with the other. | a round-robin queue of iterators rotates through the lists; finished iterators simply fall out of the queue. | O(1) per call | O(k) | Standard |
| 341 | Flatten Nested List Iterator | Implement an iterator that flattens a nested list of integers, given the `NestedInteger` interface (`isInteger()`, `getInteger()`, `getList()`). | a stack performs the depth-first unwrap lazily — flattening happens only as far as the next requested integer. | O(1) amortized next, O(n) total | O(n) | Standard |
| 346 | Moving Average from Data Stream | Given a window size, design `next(val)` that returns the moving average of the last `size` values in the stream. | the running sum avoids re-summing the window; the queue only tracks which value leaves next. | O(1) per call | O(size) | Standard |
| 348 | Design Tic-Tac-Toe | Design an `n x n` Tic-Tac-Toe game. `move(row, col, player)` returns the winning player (1 or 2) if that move wins, else 0. Detect a winner in O(1) per move. | signing the contributions lets a single counter detect either player — only checking the four lines that the current move touches keeps it O(1). | O(1) per move | O(n) | Standard |
| 381 | Insert Delete GetRandom O(1) - Duplicates allowed | Like #380 but duplicates are allowed. `insert` returns true if the value was not already present, `remove` removes one occurrence, and `getRandom` picks proportionally to multiplicity. | the swap-with-last trick from #380 extends to duplicates by storing a set of indices per value instead of a single index. ← VARIATION: value → set of indices. | O(1) average all ops | O(n) | swap target with last |
| 519 | Random Flip Matrix | Design a structure over an `m x n` grid of zeros. `flip()` randomly picks a remaining 0-cell, sets it to 1, and returns its `[row, col]`. `reset()` restores all zeros. | virtual swap-to-end on a 1D index space gives uniform O(1) flips without materializing the full grid — the map only records cells that were moved. | O(1) flip, O(1) reset | O(flips between resets) | Standard |
| 622 | Design Circular Queue | Design a fixed-capacity circular queue with `enQueue`, `deQueue`, `Front`, `Rear`, `isEmpty`, `isFull`. | tracking `head` and `count` (rather than head/tail pointers) avoids the empty-vs-full ambiguity entirely. | O(1) all ops | O(k) | Standard |
| 641 | Design Circular Deque | Design a double-ended circular queue with `insertFront`, `insertLast`, `deleteFront`, `deleteLast`, `getFront`, `getRear`, `isEmpty`, `isFull`. | the #622 head/count model extends to both ends — inserting at the front just rotates `head` backward. | O(1) all ops | O(k) | rotate head backward |
| 705 | Design HashSet | Design a HashSet without built-in hash libraries, supporting `add`, `remove`, and `contains`. | separate chaining is the textbook collision strategy; a fixed prime-ish bucket count keeps chains short for typical inputs. | O(1) average per op | O(n) | Standard |
| 706 | Design HashMap | Design a HashMap without built-in hash libraries, supporting `put`, `get`, and `remove`. | identical structure to #705 but each node carries a value, so collisions are resolved by scanning a short chain of entries. | O(1) average per op | O(n) | update existing value |
| 707 | Design Linked List | Design a linked list supporting `get`, `addAtHead`, `addAtTail`, `addAtIndex`, and `deleteAtIndex`. | sentinels remove all null-edge cases for head/tail insertion, so every operation is the same splice on interior nodes. | O(index) get/add/delete | O(n) | Standard |
| 729 | My Calendar I | Implement `book(start, end)` for a half-open interval `[start, end)`; return true and add the booking if it does not overlap any existing one, else false. | the sorted map narrows the conflict check to at most two neighbors, giving O(log n) per booking. | O(log n) per book | O(n) | Standard |
| 731 | My Calendar II | Implement `book(start, end)`; return true unless adding it would cause a triple booking (three events overlapping at the same instant). | the difference array turns "max concurrent events" into a prefix-sum scan, and rolling back keeps the structure clean on rejection. | O(n) per book | O(n) | triple booking detected, roll back |
| 732 | My Calendar III | Implement `book(start, end)` returning the maximum `k` such that some instant is covered by `k` events (the largest k-booking so far). | the same difference-array sweep as #731, but here we report the peak concurrency rather than reject it. | O(n) per book | O(n) | track peak overlap |
| 933 | Number of Recent Calls | Implement `ping(t)` (calls arrive with strictly increasing `t`) returning how many pings occurred in the inclusive window `[t - 3000, t]`. | because times arrive sorted, expired pings are always at the front — a sliding window over a queue. | O(1) amortized per ping | O(window size) | Standard |
| 1570 | Dot Product of Two Sparse Vectors | Design a `SparseVector` initialized from an array; `dotProduct(other)` returns the dot product, taking advantage of sparsity. | since most entries are zero, storing and iterating only nonzeros makes the cost proportional to the number of nonzero terms, not the vector length. | O(n) init, O(min nonzeros) per dot product | O(nonzeros) | iterate fewer entries |

---

### Canonical Template — HashMap + Doubly Linked List (LRU)

```java
// MENTAL MODEL: HashMap gives O(1) lookup; the doubly linked list orders by recency so the LRU is always one hop from tail.
// WHEN: "O(1) get/put with eviction by recency or frequency"

// CacheNode for doubly linked list (named CacheNode to distinguish from ListNode contexts)
class CacheNode {
    int key, value;
    CacheNode previous, next;
    CacheNode(int key, int value) { this.key = key; this.value = value; }
}

// ── SENTINEL NODES ── head (MRU side) ↔ ... ↔ tail (LRU side)
CacheNode head = new CacheNode(0, 0), tail = new CacheNode(0, 0);
// Initialize: head <-> tail
head.next = tail; tail.previous = head;

// ── REMOVE NODE ──
void remove(CacheNode node) {
    node.previous.next = node.next;
    node.next.previous = node.previous;
}

// ── INSERT AFTER HEAD (= mark as MRU) ──
void insertAfterHead(CacheNode node) {
    node.next = head.next;
    node.previous = head;
    head.next.previous = node;
    head.next = node;
}

// ── LRU EVICTION ── tail.previous is LRU
CacheNode lru = tail.previous;
remove(lru);
map.remove(lru.key);
```

---

### Variations

```java
// VARIATION 1: LFU — adds a frequency dimension
// Need: key→value, key→freq, freq→orderedSet<key>, and minFreq
// When a key is accessed: freq++, move from freqToKeys[oldFreq] to freqToKeys[newFreq]
// On eviction: remove first element from freqToKeys[minFreq]
// LinkedHashSet preserves insertion order → oldest at front for same frequency

// VARIATION 2: Insert Delete GetRandom — use array for O(1) random
// ArrayList stores values; HashMap stores val→index in array
// On remove: swap target with last element, update map, remove last
// On getRandom: return list.get(random.nextInt(list.size()))
```

---

### LRU vs LFU vs RandomizedSet — Pattern Chooser

| Signal | Design |
|---|---|
| "evict least **recently** used" | LRU: HashMap + doubly linked list, move to head on access |
| "evict least **frequently** used" | LFU: 3 HashMaps + LinkedHashSet + `minFreq` tracking |
| "O(1) insert/delete/random" | RandomizedSet: HashMap + ArrayList, swap-with-last on delete |

### Key Invariants

```
LRU:  head.next = MRU,  tail.previous = LRU
LFU:  minFreq always points to the smallest existing frequency bucket
      LinkedHashSet preserves insertion order → iterator().next() = LRU within bucket
RandomizedSet: list[map[val]] == val at all times (after swap, update the map for the swapped key)
```

---
## Math  &nbsp;`math.md`

---

### Quick Reference Table

| # | Name | Description | Intuition | Time | Space | Key Implementation |
|---|---|---|---|---|---|---|
| 7 | Reverse Integer | Given a signed 32-bit integer `x`, return `x` with its digits reversed. Return 0 if the result overflows. | Peel the last digit with `%10` and push it onto a growing `result` with `*10`. The only hazard is overflow, so check capacity *before* the push. | O(log n) | O(1) | Overflow guard — before `result = result*10 + digit`, verify `result` is not past `Integer.MAX_VALUE/10` (or below `MIN_VALUE/10`). |
| 9 | Palindrome Number | Return true if integer `x` reads the same forwards and backwards. Negatives are never palindromes. | No need to reverse the whole number — build up the reversed second half until it meets or passes the shrinking first half. At the meeting point the two halves should match. | O(log n) | O(1) | Half reverse — loop while `x > reversed`; the middle digit (odd-length case) is dropped via `reversed / 10`. |
| 50 | Pow(x, n) | Implement `pow(x, n)`, computing `x` raised to the integer power `n`. | Squaring the base doubles the exponent reach, so each bit of `n` decides whether the current power of `x` joins the product — O(log n) multiplications instead of O(n). | O(log n) | O(1) | Handle negative exponent by inverting `x` and negating `N` (use `long` so `-Integer.MIN_VALUE` doesn't overflow); multiply into `result` only when the current exponent bit is set. |
| 372 | Super Pow | Compute `a^b mod 1337` where `b` is given as an array of digits (so `b` may be astronomically large). | Exponents add when powers multiply, and reading `b` digit by digit means `a^b = (a^(b/10))^10 * a^(b%10)`. Fold left across the digits, applying the modulus at every step to keep numbers small. | O(log n) | O(1) | Digit-by-digit modular exponentiation — at each new digit `d`, raise the running result to the 10th power and multiply by `a^d`, all mod 1337. |
| 168 | Excel Sheet Column Title | Given a column number, return its Excel-style title (1→"A", 27→"AA", 28→"AB"). | It's base-26, but Excel has no zero digit — columns start at A=1, so the system is 1-indexed (a "bijective base 26"). Decrement before each digit to shift into the standard 0..25 range. | O(log n) | O(1) | 1-indexed — do `columnNumber--` before extracting each digit so that `% 26` yields 0..25 mapping cleanly onto 'A'..'Z'. |
| 171 | Excel Sheet Column Number | Given an Excel column title (e.g. "AB"), return its column number (28). | Horner's rule for base-26, but each letter contributes `c-'A'+1` (A=1, not 0) because the system is 1-indexed. | O(L) L = title length | O(1) | 1-indexed letters — `(c - 'A' + 1)` so 'A' maps to 1 rather than 0. |
| 67 | Add Binary | Given two binary strings `a` and `b`, return their sum as a binary string. | Grade-school addition from the rightmost digit, tracking a carry — identical to adding two linked-list numbers (#2), but the base is 2 and the operands are strings. | O(n) n = max length | O(n) | Char arithmetic per column — `(a.charAt(i)-'0') + (b.charAt(j)-'0') + carry`; emit `sum % 2` and carry `sum / 2`. |
| 204 | Count Primes | Count the number of prime numbers strictly less than `n`. | Instead of testing each number for primality, cross out every multiple of each prime once. When you reach an unmarked `i`, it's prime; its multiples below `i*i` were already crossed out by smaller primes, so start marking at `i*i`. | O(n log log n) | O(n) | Start marking at `i*i` — multiples `k*i` with `k < i` were already handled by the smaller factor `k`. |
| 1201 | Ugly Number III | Find the nth positive integer that is divisible by at least one of `a`, `b`, or `c`. | The count of valid numbers ≤ `x` is monotonic in `x`, so binary-search the smallest `x` whose count reaches `n`. Counting "≤ mid divisible by a, b, or c" is a classic inclusion-exclusion over the three sets, subtracting pairwise LCM overlaps and adding back the triple LCM. | O(log min(range)) | O(1) | Inclusion-exclusion — `count = mid/a + mid/b + mid/c - mid/ab - mid/bc - mid/ac + mid/abc` using LCMs to avoid double counting. |
| 29 | Divide Two Integers | Divide two integers `dividend` and `divisor` without using multiplication, division, or mod, truncating toward zero. Clamp the result to the 32-bit signed range. | Repeated subtraction is too slow, so subtract the largest doubling of the divisor that still fits — this is long division in binary. Work in negatives so `Integer.MIN_VALUE` cannot overflow. | O(log n * log n) | O(1) | Exponential search of the divisor — double `divisor` and the matching quotient bit until it would exceed the remaining dividend. |
| 59 | Spiral Matrix II | Given `n`, generate an `n x n` matrix filled with the numbers `1` to `n*n` in spiral order. | Walk the four borders inward, shrinking the boundary after completing each side, filling a running counter. | O(n^2) | O(1) extra | Layer boundaries — maintain `top/bottom/left/right` and fill right, down, left, up in turn. |
| 66 | Plus One | Given a large integer represented as an array of digits (most significant first), increment it by one and return the resulting digit array. | Add one from the rightmost digit; a digit below 9 absorbs the carry and we're done, otherwise it becomes 0 and the carry propagates. If every digit was 9 we need one extra leading digit. | O(n) | O(1) extra (O(n) only for all-nines) | Early return — the moment a digit is incremented without rolling over, return; only an all-9 array needs a longer result. |
| 118 | Pascal's Triangle | Given `numRows`, generate the first `numRows` rows of Pascal's triangle. | Each interior entry is the sum of the two entries above it; the edges are always 1. | O(numRows^2) | O(numRows^2) | Row-by-row build — `row[j] = previous[j-1] + previous[j]`. |
| 119 | Pascal's Triangle II | Given a row index `rowIndex`, return that row of Pascal's triangle using only O(rowIndex) extra space. | Update a single row in place; iterating right-to-left lets each entry read its left neighbor before that neighbor is overwritten. | O(rowIndex^2) | O(rowIndex) | In-place reverse update — `row[j] += row[j-1]` scanning from the right. |
| 149 | Max Points on a Line | Given an array of points on a plane, return the maximum number of points lying on the same straight line. | Fix one point as the anchor; every other point defines a slope from it, and collinear points share that slope. Count the most common slope per anchor, using a reduced integer fraction as the key to avoid floating-point error. | O(n^2) | O(n) | Slope histogram per anchor — key on `(dy/g, dx/g)` reduced by gcd, with sign normalization. |
| 172 | Factorial Trailing Zeroes | Given an integer `n`, return the number of trailing zeroes in `n!`. | A trailing zero comes from a factor of 10 = 2*5, and factors of 2 are far more plentiful than factors of 5, so just count the factors of 5. Multiples of 25 contribute an extra 5, of 125 another, and so on. | O(log n) | O(1) | Count factors of 5 — sum `n/5 + n/25 + n/125 + ...` via `n /= 5`. |
| 202 | Happy Number | A happy number reaches 1 by repeatedly replacing it with the sum of the squares of its digits; return whether `n` is happy. | The sequence either hits 1 or enters a cycle, so this is cycle detection — use Floyd's slow/fast pointers over the "sum of digit squares" transformation. | O(log n) per step | O(1) | Floyd cycle detection on a number transform — `slow = f(slow)`, `fast = f(f(fast))`. |
| 223 | Rectangle Area | Given the coordinates of two axis-aligned rectangles, return the total area they cover (counting the overlap once). | Total area is the sum of both areas minus the overlap; the overlap is itself a rectangle whose width and height are the intersections of the projections onto each axis (zero if they don't intersect). | O(1) | O(1) | Inclusion-exclusion of areas — overlap width = `min(rights) - max(lefts)` clamped at 0. |
| 233 | Number of Digit One | Given an integer `n`, count the total number of digit `1` appearing in all non-negative integers from 0 to `n`. | Count contributions of the digit 1 at each place value separately. For a given place, the count depends on the higher digits, the current digit, and the lower digits, which split cleanly into full cycles plus a partial cycle. | O(log n) | O(1) | Per-place digit counting — for each power-of-ten place, `count += high*place + adjust(cur, low, place)`. |
| 243 | Shortest Word Distance | Given an array of words and two distinct words, return the shortest distance (in indices) between any occurrence of the two words. | A single pass tracking the most recent index of each target word suffices; whenever both have been seen, the gap between the two latest positions is a candidate minimum. | O(n) | O(1) | Two latest-index trackers — update `result` whenever both indices are valid. |
| 258 | Add Digits | Repeatedly add all the digits of a non-negative integer until the result has a single digit; return it (the digital root). | The digital root has a closed form derived from numbers being congruent to their digit sum modulo 9: the answer is `0` for 0, otherwise `1 + (n-1) % 9`. | O(1) | O(1) | Digital root formula — no loop, just `1 + (num - 1) % 9`. |
| 263 | Ugly Number | An ugly number has no prime factors other than 2, 3, or 5; return whether `n` is ugly. | Divide out all factors of 2, 3, and 5; what remains is 1 exactly when no other prime factor exists. Non-positive numbers are never ugly. | O(log n) | O(1) | Factor stripping — repeatedly divide by each of 2, 3, 5 and check the remainder is 1. |
| 292 | Nim Game | You and an opponent alternate removing 1 to 3 stones; whoever takes the last stone wins. Given `n` stones and you move first, return whether you can win. | If `n` is a multiple of 4 you always lose, because whatever you take (1-3) the opponent can complete a group of four, keeping `n` a multiple of 4 on your turn until 0. | O(1) | O(1) | Multiple-of-four loss — win exactly when `n % 4 != 0`. |
| 319 | Bulb Switcher | There are `n` bulbs initially off; in round `i` you toggle every `i`-th bulb. Return how many bulbs are on after `n` rounds. | Bulb `k` is toggled once per divisor of `k`, ending on only if it has an odd number of divisors — which happens exactly for perfect squares. The count of perfect squares up to `n` is `floor(sqrt(n))`. | O(1) | O(1) | Perfect-square count — answer is `(int) sqrt(n)`. |
| 326 | Power of Three | Given an integer `n`, return whether it is a power of three. | Within the 32-bit range the largest power of three is `3^19 = 1162261467`; any power of three must divide it exactly, so a single divisibility test works. | O(1) | O(1) | Max-power divisibility — `n > 0 && 1162261467 % n == 0`. |
| 357 | Count Numbers with Unique Digits | Given `n`, count all numbers `x` with `0 <= x < 10^n` that have no repeated digits. | Count by length: the first digit has 9 choices (1-9), the next 9 (any but the first), then 8, 7, ..., multiplying as digits are added. Sum these counts across lengths 1 to n, plus the single number 0. | O(n) | O(1) | Permutation counting per length — `9 * 9 * 8 * ... ` accumulated. |
| 365 | Water and Jug Problem | Given two jugs of capacities `x` and `y` and a target `target`, determine if you can measure exactly `target` liters using fill/empty/pour operations. | Any amount measurable is a non-negative integer combination of `x` and `y`, which by Bezout's identity is exactly the multiples of `gcd(x, y)`. So the target must be reachable in total capacity and divisible by the gcd. | O(log(min(x,y))) | O(1) | Bezout / gcd test — `target % gcd(x, y) == 0` with `target <= x + y`. |
| 367 | Valid Perfect Square | Given a positive integer `num`, return whether it is a perfect square, without using any built-in sqrt function. | The square root lies in `[1, num]` and squaring is monotonic, so binary search the candidate root and compare its square (in `long` to avoid overflow) against `num`. | O(log n) | O(1) | Binary search on the root — midpoint `k = i + (j-i)/2`, compare `k*k` to `num`. |
| 397 | Integer Replacement | Given a positive integer `n`, each step you may replace it with `n/2` if even, or `n+1`/`n-1` if odd; return the minimum steps to reach 1. | Halving is always best when possible. For odd `n`, choosing `+1` vs `-1` should expose more trailing zeros to halve next; `n == 3` is the special case where `-1` is better. | O(log n) | O(1) | Greedy on the last two bits — for odd `n != 3`, add 1 when `(n & 2) != 0` else subtract 1. |
| 398 | Random Pick Index | Given an array `nums`, implement `pick(target)` returning a uniformly random index where `nums[index] == target`. | Reservoir sampling lets us pick uniformly in one pass without storing all matching indices: the `k`-th matching element replaces the current pick with probability `1/k`. | O(n) per pick | O(1) | Reservoir sampling of size 1 — keep the index with probability `1/count` as matches stream by. |
| 400 | Nth Digit | Given `n`, return the `n`-th digit in the infinite sequence of concatenated positive integers `123456789101112...`. | Numbers group by digit-length: there are `9*10^(d-1)` numbers with `d` digits, contributing `d * 9 * 10^(d-1)` digits. Subtract whole groups to find the length, locate the exact number, then index into it. | O(log n) | O(1) | Length-bucket walk — subtract `count * digitLength` until `n` falls inside the current bucket. |
| 412 | Fizz Buzz | Return a list of strings for `1..n` where multiples of 3 become "Fizz", multiples of 5 become "Buzz", multiples of both become "FizzBuzz", and others the number itself. | Build each entry by concatenating "Fizz" and/or "Buzz" based on divisibility; if neither applies, use the number's string. | O(n) | O(1) extra | Concatenate divisibility tags — append "Fizz" on `%3`, "Buzz" on `%5`. |
| 441 | Arranging Coins | You have `n` coins to form a staircase where the `k`-th row has exactly `k` coins; return the number of complete rows. | After `k` complete rows you've used `k(k+1)/2` coins, so the answer is the largest `k` with `k(k+1)/2 <= n`. Binary search this `k` (or solve the quadratic). | O(log n) | O(1) | Binary search on rows — compare triangular number `k(k+1)/2` against `n` using `long`. |
| 453 | Minimum Moves to Equal Array Elements | In one move you increment `n-1` elements of the array by 1; return the minimum moves to make all elements equal. | Incrementing all but one is equivalent (for the purpose of equalizing) to decrementing a single element by 1. So the answer is the total amount each element exceeds the minimum: `sum - n * min`. | O(n) | O(1) | Relative-decrement reframing — total moves = `sum(nums) - n * min(nums)`. |
| 458 | Poor Pigs | With `buckets` buckets one of which is poisoned, `minutesToDie` for poison to act, and `minutesToTest` total time, return the minimum pigs needed to find the poisoned bucket. | Each pig can be tested `t = minutesToTest / minutesToDie` times, so it has `t + 1` distinguishable states (died after round 1..t, or survived). With `p` pigs we cover `(t+1)^p` buckets, so we need the smallest `p` with `(t+1)^p >= buckets`. | O(log buckets) | O(1) | Base-(tests+1) counting — `p = ceil(log_{t+1}(buckets))`. |
| 470 | Implement Rand10() Using Rand7() | Given `rand7()` uniform in [1,7], implement `rand10()` uniform in [1,10]. | Two calls form a uniform value in [1,49]; reject anything above 40 and map the remaining 40 outcomes evenly onto [1,10]. Rejection keeps the distribution exactly uniform. | O(1) expected | O(1) | Rejection sampling on a 7x7 grid — accept index `< 40`, return `index % 10 + 1`. |
| 492 | Construct the Rectangle | Given a target `area`, return the dimensions `[L, W]` with `L >= W`, `L * W == area`, and `L - W` minimized. | The most square-like factor pair minimizes the difference, so start `W` at `floor(sqrt(area))` and walk down until it divides `area`. | O(sqrt(area)) | O(1) | Search down from sqrt — first divisor `W <= sqrt(area)` gives the closest pair. |
| 495 | Teemo Attacking | Given sorted attack `timeSeries` and a poison `duration`, return the total time the target is poisoned (overlaps counted once). | Each attack would add `duration`, but if the next attack comes before the current poison ends, only the gap between attacks counts. Sum the capped gaps and add a full duration for the last attack. | O(n) | O(1) | Capped gaps — add `min(gap, duration)` between consecutive attacks. |
| 528 | Random Pick with Weight | Given an array `w` of weights, implement `pickIndex()` returning index `i` with probability proportional to `w[i]`. | Build prefix sums so the cumulative weights partition `[1, total]` into intervals; draw a random target in that range and binary-search the first prefix sum reaching it. | O(log n) per pick, O(n) build | O(n) | Prefix-sum + binary search — find leftmost prefix `>= target`. |
| 593 | Valid Square | Given four points, return whether they form a valid square (positive area). | Among the six pairwise squared distances of a square there are exactly two distinct values: four equal sides and two equal (larger) diagonals, with the diagonal twice the side. Use squared distances to stay in integers. | O(1) | O(1) | Two-distinct-distance check — collect six squared distances; require exactly two values, the smaller nonzero, the larger double it. |
| 598 | Range Addition II | Given an `m x n` matrix of zeros and operations each incrementing the top-left `a x b` submatrix, return how many cells hold the maximum value. | Every operation always covers cell (0,0), so the maximum value sits in the intersection of all operation rectangles — its area is the product of the smallest row bound and smallest column bound. | O(ops) | O(1) | Intersection area of all ops — `min(all a) * min(all b)`. |
| 633 | Sum of Square Numbers | Given a non-negative integer `c`, decide whether there exist non-negative integers `a, b` with `a*a + b*b == c`. | Squeeze two pointers from `0` and `floor(sqrt(c))`: if the squared sum is too small move the low pointer up, too large move the high pointer down. | O(sqrt(c)) | O(1) | Two pointers on squares — `a` from 0 up, `b` from sqrt(c) down. |
| 656 | Coin Path | Given `coins` (cost per index, `-1` blocked) and a max jump `maxJump`, find the lexicographically smallest cheapest path of indices from index 0 to the last. | Work backwards with DP: the best cost from index `i` is its cost plus the cheapest reachable next index within `maxJump`. Filling from the right and preferring the smaller next index yields the lexicographically smallest path on ties. | O(n * maxJump) | O(n) | Backward DP with path reconstruction — `cost[i] = coins[i] + min over j in (i, i+maxJump]`, tie-break to smaller `j`. |
| 781 | Rabbits in Forest | Each surveyed rabbit reports how many other rabbits share its color; given the `answers`, return the minimum number of rabbits in the forest. | Rabbits answering `k` form groups of size `k+1`. For each answer value, every full group of `k+1` such replies fills one color group; partial groups still require a whole `k+1` block. | O(n) | O(n) | Group-rounding by answer — for count `c` of answer `k`, add `ceil(c/(k+1)) * (k+1)`. |
| 789 | Escape The Ghosts | Starting at the origin with a `target`, and given `ghosts` positions, you all move simultaneously in Manhattan steps; return whether you can reach the target before any ghost catches you. | You win iff you reach the target strictly before every ghost. Since all move optimally with Manhattan distance, compare your distance from origin to each ghost's distance to the target; if no ghost is at least as close, you escape. | O(g) | O(1) | Manhattan-distance race — you win when your distance to target < every ghost's distance to target. |
| 792 | Number of Matching Subsequences | Given a string `s` and an array of `words`, return how many words are subsequences of `s`. | Rather than scan `s` per word, bucket words by their next-needed character. Sweep `s` once; each character releases its waiting words, advancing them to their next character bucket, and any word that runs out of characters is a match. | O(\|s\| + total word length) | O(total word length) | Waiting lists per next-char — advance words bucketed by the character they currently need as `s` streams. |
| 829 | Consecutive Numbers Sum | Given `n`, return the number of ways to write it as a sum of consecutive positive integers. | A run of `k` consecutive integers starting at `a` sums to `k*a + k(k-1)/2`, so `n - k(k-1)/2` must be positive and divisible by `k`. Try each `k` while the triangular offset stays below `n`. | O(sqrt(n)) | O(1) | Count valid run-lengths — for each `k`, valid iff `(n - k(k-1)/2) % k == 0` and positive. |
| 836 | Rectangle Overlap | Given two axis-aligned rectangles `rec1` and `rec2` as `[x1,y1,x2,y2]`, return whether they overlap in positive area. | Two rectangles overlap iff their projections on both axes overlap; equivalently, neither is entirely to one side of the other on either axis. | O(1) | O(1) | Separating-axis on both projections — overlap iff `x` ranges and `y` ranges each intersect. |
| 858 | Mirror Reflection | A square room with mirrored walls has receptors at corners 0,1,2; a laser leaves the southwest corner and first travels to the east wall at height `q` (room side `p`). Return which receptor it first meets. | Unfold the reflections so the beam travels straight; it hits a corner after going up a multiple of `p` that is also a multiple of `q`, i.e. `lcm(p,q)`. The parities of how many room-widths and room-heights that represents determine the receptor. | O(log(min(p,q))) | O(1) | Parity of `lcm/p` and `lcm/q` — reduce `p,q` by gcd, then the receptor follows from which is odd/even. |
| 869 | Reordered Power of 2 | Given an integer `n`, return whether some permutation of its digits (no leading zero) equals a power of 2. | Two numbers are digit-permutations iff they have the same multiset of digits. So compute a digit-count signature of `n` and compare it against the signatures of all powers of 2 within the 32-bit range. | O(log^2 n) | O(1) | Digit-count signature match — compare sorted-digit fingerprint against each power of 2. |
| 939 | Minimum Area Rectangle | Given points in the plane, find the minimum area of an axis-aligned rectangle formed by four of them, or 0 if none exists. | A rectangle is fixed by its diagonal corners; for each pair of points with different x and y, the other two corners are determined, so check whether both exist in a point set. | O(n^2) | O(n) | Diagonal-pair lookup — for each pair, test if the complementary corners are present in a hash set. |
| 963 | Minimum Area Rectangle II | Given points in the plane, find the minimum area of any rectangle (any orientation) formed by four of them, or 0. | A rectangle's diagonals share the same midpoint and the same length. Group point pairs by `(midpoint, diagonal length)`; any two pairs in a group are the two diagonals of a rectangle, whose sides come from the corner vectors. | O(n^2) groups, worst O(n^2) per group | O(n^2) | Group diagonals by midpoint+length — within a group, combine pairs and compute area via vectors. |
| 1041 | Robot Bounded In Circle | A robot starts at the origin facing north and repeats `instructions` ('G' forward, 'L'/'R' turn) forever; return whether it stays within some bounded circle. | After one pass, the robot is bounded iff it returns to the origin, or it no longer faces north — a non-north heading guarantees the net displacement rotates and cancels over at most four cycles. | O(n) | O(1) | One-cycle check — bounded iff back at origin OR final direction != initial north. |
| 1160 | Find Words That Can Be Formed by Characters | Given `words` and a string `chars`, return the total length of words that can be formed using letters of `chars` (each letter used at most as often as it appears). | Count available letters once; a word is formable iff its own letter counts never exceed the available counts. Sum lengths of formable words. | O(total characters) | O(1) | Frequency containment — compare per-word letter counts against the `chars` budget. |
| 1304 | Find N Unique Integers Sum up to Zero | Given `n`, return any array of `n` unique integers that sum to zero. | Pair each positive `i` with its negation `-i`; that cancels to zero, and add a lone 0 if `n` is odd. | O(n) | O(1) extra | Symmetric pairs — emit `i` and `-i`, plus a central 0 for odd `n`. |
| 1344 | Angle Between Hands of a Clock | Given an `hour` and `minutes`, return the smaller angle (in degrees) between the hour and minute hands. | The minute hand moves 6 degrees per minute; the hour hand moves 30 degrees per hour plus 0.5 degree per minute. The answer is the absolute difference, folded to at most 180. | O(1) | O(1) | Per-hand angular position — minute = `6*m`, hour = `30*(h%12) + 0.5*m`, take `min(diff, 360-diff)`. |
| 1583 | Count Unhappy Friends | Given `n` friends, their `preferences`, and a `pairs` assignment, count friends who are unhappy — paired with someone they prefer less than another friend who also prefers them over their own partner. | Precompute each friend's preference rank for every other friend. A friend `x` (paired with `y`) is unhappy if some `u` ranks higher than `y` for `x`, and `u` ranks `x` higher than `u`'s own partner. Compare ranks pairwise. | O(n^2) | O(n^2) | Rank-matrix mutual-preference scan — `x` unhappy if exists `u` with `rank[x][u] < rank[x][y]` and `rank[u][x] < rank[u][partner[u]]`. |
| 1588 | Sum of All Odd Length Subarrays | Given an array `arr`, return the sum of all elements over all odd-length contiguous subarrays. | Instead of enumerating subarrays, count how many odd-length subarrays include each index. With `i+1` choices for the left boundary and `n-i` for the right, the number of odd-length ones is computed in closed form, weighting each element. | O(n) | O(1) | Per-element contribution — element `i` appears in `ceil(((i+1)*(n-i))/2)` odd-length subarrays. |
| 1646 | Get Maximum in Generated Array | Build array `nums` where `nums[0]=0`, `nums[1]=1`, `nums[2i]=nums[i]`, `nums[2i+1]=nums[i]+nums[i+1]`; return its maximum for size `n`. | Generate the array directly from the recurrence, tracking the running maximum. Handle the tiny base cases for `n < 2`. | O(n) | O(n) | Direct recurrence fill — even index copies, odd index sums the two halves. |
| 1823 | Find the Winner of the Circular Game | `n` friends in a circle eliminate every `k`-th friend repeatedly; return the 1-indexed winner (Josephus problem). | The Josephus recurrence builds the survivor's position from a circle of size 1 upward: the winner in a circle of `i` is `(winner_{i-1} + k) % i`. Convert the final 0-indexed answer to 1-indexed. | O(n) | O(1) | Josephus recurrence — `winner = (winner + k) % i` for `i = 2..n`. |
| 1969 | Minimum Non-Zero Product of the Array Elements | For the array of all integers `1..2^p - 1`, you may swap bits between elements any number of times; return the minimum non-zero product modulo `1e9+7`. | Pair the largest value `2^p - 1` (kept whole) with the rest: each other pair can be made `(2^p - 2)` and `1`, so the product is `(2^p - 1) * (2^p - 2)^(2^(p-1) - 1)` — compute with modular fast power, but the base of the exponent must use the true (non-reduced) count. | O(p) | O(1) | Pairing + modular fast power — `(max) * pow(max-1, half-1) mod M`. |

---

### Canonical Templates

```java
// MENTAL MODEL: number = sequence of digits in some base; iterate by repeatedly
//               peeling the last digit (% base) and shifting (/ base).
// WHEN: "reverse digits", "x^n", "base conversion", "count primes", "nth divisible-by".

// ── DIGIT EXTRACTION LOOP ── peel digits right-to-left
while (n != 0) {
    int digit = n % 10;   // last digit
    n /= 10;              // drop last digit
    // ... use digit ...
}

// ── FAST POWER (exponentiation by squaring) ──
// WHY: x^n needs only O(log n) multiplications by squaring the base
//      and consuming one exponent bit per step.
//   x^13 = x^8 * x^4 * x^1   (13 = 1101 in binary)
double fastPow(double x, long n) {
    double result = 1;
    while (n > 0) {
        if ((n & 1) == 1) result *= x;   // bit set → include this power of x
        x *= x;                          // square the base for the next bit
        n >>= 1;                         // consume one exponent bit
    }
    return result;
}

// ── BASE CONVERSION ── generic base b, 0-indexed
// number → digits: peel with % b, shift with / b, collect, then reverse
StringBuilder builder = new StringBuilder();
while (num > 0) {
    builder.append(num % b);
    num /= b;
}
builder.reverse();
// digits → number: Horner's rule
int value = 0;
for (int digit : digits) value = value * b + digit;

// ── SIEVE OF ERATOSTHENES ── mark composites up to n
// WHY start at i*i: any multiple k*i with k < i was already marked by k.
boolean[] composite = new boolean[n];
for (int i = 2; i * i < n; i++) {
    if (composite[i]) continue;
    for (int j = i * i; j < n; j += i)   // start at i*i, step by i
        composite[j] = true;
}
```

---

### Math Cheat Sheet

```java
n % 10               // last decimal digit
n /= 10              // drop last digit
result * 10 + digit  // push a digit (build number left-to-right)
(n & 1) == 1         // odd
(n & 1) == 0         // even
n >>= 1              // halve (consume one bit)
x *= x               // square base in fast power
c - '0'              // char → digit value
c - 'A' + 1          // Excel letter → 1-indexed value
(char)('A' + d)      // 0..25 → 'A'..'Z'
i * i                // sieve marking start point
x / gcd(x,y) * y     // LCM without overflow (divide first)
```

### Pattern Chooser

| Signal | Technique | Time |
|---|---|---|
| "reverse the digits of a number" | Digit pop (`%10`) / push (`*10`) loop | O(log n) |
| "is the number a palindrome?" | Reverse only half, compare halves | O(log n) |
| "compute x^n / a^b efficiently" | Exponentiation by squaring (binary exp) | O(log n) |
| "x^huge mod m" / exponent given as array | Digit-by-digit modular fast power | O(log n) |
| "add two big numbers as strings" | Right-to-left add with carry | O(n) |
| "convert column number ↔ Excel title" | Base-26 conversion, **1-indexed** | O(log n) / O(L) |
| "convert between number and base-b string" | Horner (parse) / peel-and-reverse (build) | O(L) |
| "count primes below n" | Sieve of Eratosthenes, mark from `i*i` | O(n log log n) |
| "nth number divisible by a/b/c" | Binary search on answer + inclusion-exclusion (LCM) | O(log range) |
| "check if n is power of 2/4" | Bit trick `n & (n-1) == 0` (see bit_manipulation) | O(1) |

---


---

# Complete Problem Index — by Template Category

All **737 problems** from `LeetCode_Complete_Reference.tex`, assigned to their template category. **★** marks problems with a worked template/solution already in this file's category sections above; unmarked problems are catalogued here for coverage. Source category shown when it differs (e.g. Trees & Backtracking → DFS; Heap → Stack/Queue).

## Two Pointers  (93 problems, 93 templated)

| # | ★ | Name | Complexity | Description |
|---|---|---|---|---|
| 1 | ★ | Two Sum | O(n) / O(1) | Given an integer array and a target sum, return the indices of two numbers that add up to target. Exactly one solution exists; cannot use the same element twice. |
| 11 | ★ | Container With Most Water | O(n) / O(1) | Given n vertical lines at positions 1..n with heights, find two lines that together with the x-axis form a container holding the most water. |
| 15 | ★ | 3Sum | O(n^2) / O(n) | Find all unique triplets [a,b,c] in an integer array such that a+b+c=0. No duplicate triplets. |
| 16 | ★ | 3Sum Closest |  | Find three integers closest to a given target sum. Return the sum of those three integers. |
| 18 | ★ | 4Sum | O(n³) / O(n) | Find all unique quadruplets in an array that sum to a given target. No duplicates. |
| 26 | ★ | Remove Duplicates from Sorted Array | O(n) / O(1) | Remove duplicates from a sorted array in-place. Return the count of unique elements. |
| 27 | ★ | Remove Element | O(n) / O(1) | Remove all occurrences of a value from an array in-place. Return the new length. |
| 31 | ★ | Next Permutation |  | Rearrange an array of integers to its lexicographically next greater permutation. If none, rearrange to lowest order. |
| 41 | ★ | First issing Positive |  | Find the smallest missing positive integer in an unsorted array. Must run in O(n) time and O(1) space. |
| 42 | ★ | Trapping Rain Water | O(n) / O(1) | Given an elevation map (array of bar heights), compute how much water it can trap after raining. |
| 48 | ★ | Rotate Image |  | Rotate an n×n matrix 90 degrees clockwise in-place. |
| 54 | ★ | Spiral Matrix |  | Return all elements of an m×n matrix in spiral order. |
| 73 | ★ | Set Matrix Zeroes |  | Given an m×n matrix, set entire row and column to 0 if any element is 0. Do it in-place. |
| 75 | ★ | Sort Colors | O(n) / O(1) | Sort an array of 0s, 1s, and 2s in-place without using sort (Dutch National Flag problem). |
| 80 | ★ | Remove Duplicates from Sorted Array II | O(n) / O(1) | Remove duplicates from a sorted array so each element appears at most twice in-place. |
| 88 | ★ | Merge Sorted Array | O(m+n) / O(1) | Merge two sorted integer arrays nums1 and nums2 into nums1 in-place (nums1 has extra space). |
| 128 | ★ | Longest Consecutive Sequence |  | Find the length of the longest consecutive sequence of integers in an unsorted array. O(n) required. |
| 164 | ★ | Maximum Gap | O(n) / O(n) | Find the maximum gap between successive elements in a sorted form of an array. O(n) required. |
| 167 | ★ | Two Sum II - Input Array Is Sorted |  | Given a sorted array, find two numbers that add to a target (1-indexed). Exactly one solution. |
| 169 | ★ | Majority Element |  | Find the majority element that appears more than n/2 times. |
| 189 | ★ | Rotate Array |  | Rotate an array to the right by k positions in-place. |
| 217 | ★ | Contains Duplicate |  | Check if any value appears at least twice in an integer array. |
| 219 | ★ | Contains Duplicate II | O(n) / O(k) | Check if there are two distinct indices i and j such that nums[i]==nums[j] and i-j. |
| 220 | ★ | Contains Duplicate III |  | Check if there are two indices i and j such that nums[i]-nums[j] and i-j. |
| 229 | ★ | Majority Element II |  | Find all elements appearing more than n/3 times in an array. |
| 238 | ★ | Product of Array Except Self |  | Return an array where output[i] is the product of all elements except nums[i]. No division. |
| 259 | ★ | 3Sum Smaller |  | Count triplets with sum smaller than a target (sorted array). |
| 280 | ★ | Wiggle Sort |  | Rearrange an array in-place so it alternates peaks and valleys. |
| 283 | ★ | Move Zeroes | O(n) / O(1) | Move all zeroes in an array to the end while maintaining relative order of non-zero elements. |
| 289 | ★ | Game of Life |  | Simulate Conway's Game of Life: update all cells simultaneously based on neighbor counts. |
| 303 | ★ | Range Sum Query - Immutable |  | Answer multiple range sum queries on a static array efficiently. |
| 304 | ★ | Range Sum Query 2D - Immutable |  | Answer multiple 2D region sum queries on a static matrix efficiently. |
| 307 | ★ | Range Sum Query - Mutable |  | Support range sum queries and point updates on an array. |
| 311 | ★ | Sparse Matrix Multiplication |  | Multiply two sparse matrices efficiently (skip zero elements). |
| 315 | ★ | Count of Smaller Numbers After Self | O(n log n) / O(n) | For each element, count elements to its right that are smaller. |
| 325 | ★ | Maximum Size Subarray Sum Equals k | O(n) / O(n) | Find the maximum length subarray with sum equal to k. |
| 327 | ★ | Count of Range Sum | O(n log n) / O(n) | Count range sums that lie in [lower, upper]. |
| 334 | ★ | Increasing Triplet Subsequence |  | Return true if there exists `i < j < k` with `nums[i] < nums[j] < nums[k]`. |
| 349 | ★ | Intersection of Two Arrays |  | Find the intersection of two integer arrays (unique elements only). |
| 350 | ★ | Intersection of Two Arrays II |  | Find the intersection of two integer arrays including duplicates. |
| 370 | ★ | Range Addition |  | Apply range updates `[start, end] += inc` then return the final array. |
| 384 | ★ | Shuffle an Array |  | Shuffle an integer array so each permutation is equally likely. |
| 414 | ★ | Third Maximum Number |  | Find the third maximum distinct integer. Return the maximum if no third. |
| 419 | ★ | Battleships in a Board |  | Count battleships in a board ('X's forming horizontal or vertical lines). |
| 442 | ★ | Find All Duplicates in an Array |  | Values in [1,n], each appears once or twice. Return the ones appearing twice. O(n) time, O(1) extra space. |
| 448 | ★ | Find All Numbers Disappeared in an Array |  | Find all integers in range [1,n] that are missing from an array of size n. |
| 454 | ★ | 4Sum II |  | Count quadruplets (i,j,k,l) such that A[i]+B[j]+C[k]+D[l]==0. |
| 457 | ★ | Circular Array Loop |  | Detect a cycle of length > 1 with consistent direction in a circular array of jumps. |
| 485 | ★ | Max Consecutive Ones |  | Find the maximum number of consecutive 1s in a binary array. |
| 493 | ★ | Reverse Pairs |  | Count pairs (i,j) with `i < j` and `nums[i] > 2 * nums[j]`. |
| 498 | ★ | Diagonal Traverse |  | Traverse an m×n matrix diagonally, alternating direction. |
| 517 | ★ | Super Washing Machines |  | Minimize the max number of moves to equalize dresses across machines (one dress to a neighbor per move). |
| 523 | ★ | Continuous Subarray Sum | O(n) / O(n) | Check if a subarray exists with sum divisible by k. |
| 525 | ★ | Contiguous Array |  | Find the maximum length subarray with equal number of 0s and 1s. |
| 532 | ★ | K-diff Pairs in an Array |  | Count unique k-diff pairs (i,j) in an array where nums[i]-nums[j]==k. |
| 560 | ★ | Subarray Sum Equals K | O(n) / O(n) | Count subarrays that sum to exactly k. |
| 566 | ★ | Reshape the Matrix |  | Reshape an m×n matrix to r×c without changing element order. |
| 581 | ★ | Shortest Unsorted Continuous Subarray |  | Find the shortest subarray that, if sorted, makes the whole array sorted. |
| 594 | ★ | Longest Harmonious Subsequence |  | Find the longest subsequence where max and min differ by exactly 1. |
| 599 | ★ | Minimum Index Sum of Two Lists |  | Find the common strings between two lists with the minimum index sum. |
| 611 | ★ | Valid Triangle Number |  | Count the number of valid triangles from a sorted array of lengths. |
| 661 | ★ | Image Smoother |  | Replace each cell with the floor of the average of itself and its up-to-8 neighbors. |
| 723 | ★ | Candy Crush |  | Simulate Candy Crush: repeatedly remove groups of 3 same-color candies and drop. |
| 724 | ★ | Find Pivot Index |  | Find a pivot index where left sum equals right sum. |
| 766 | ★ | Toeplitz Matrix |  | Check if a matrix is Toeplitz (all diagonals have the same value). |
| 769 | ★ | Max Chunks To Make Sorted |  | Array is a permutation of [0,n-1]. Max number of chunks that can be sorted independently to sort the whole. |
| 795 | ★ | Number of Subarrays with Bounded Maximum |  | Count subarrays with a maximum value in range [L, R]. |
| 807 | ★ | Max Increase to Keep City Skyline |  | Maximize the total increase in building heights while preserving the city's skyline from all 4 directions. |
| 825 | ★ | Friends Of Appropriate Ages |  | Count pairs of people where one person's age allows them to friend the other. |
| 838 | ★ | Push Dominoes |  | Given a string of dominoes ('L', 'R', '.'), simulate their fall. |
| 845 | ★ | Longest Mountain in Array |  | Find the length of the longest mountain subarray (increases then decreases). |
| 896 | ★ | Monotonic Array |  | Check if an array is monotonically increasing or decreasing. |
| 912 | ★ | Sort an Array | O(n log n) / O(n) | Sort an integer array. Implement an O(n log n) sort. |
| 974 | ★ | Subarray Sums Divisible by K | O(n) / O(k) | Count subarrays whose sum is divisible by k. |
| 977 | ★ | Squares of a Sorted Array |  | Return the squares of a sorted array in sorted order. |
| 1013 | ★ | Partition Array Into Three Parts With Equal Sum |  | Can the array be split into three contiguous parts with equal sums? |
| 1074 | ★ | Number of Submatrices That Sum to Target |  | Count submatrices summing to target. |
| 1109 | ★ | Corporate Flight Bookings |  | Given bookings `[first, last, seats]`, return total seats booked per flight. |
| 1213 | ★ | Intersection of Three Sorted Arrays |  | Find the intersection of three sorted arrays. |
| 1275 | ★ | Find Winner on a Tic Tac Toe Game |  | Determine the winner of a Tic-Tac-Toe game given a sequence of moves. |
| 1351 | ★ | Count Negative Numbers in a Sorted Matrix |  | Count the number of negative numbers in a sorted matrix. |
| 1424 | ★ | Diagonal Traverse II |  | Traverse a matrix diagonally from bottom-left to top-right. |
| 1460 | ★ | Make Two Arrays Equal by Reversing Sub-arrays |  | Check if two arrays become equal after reversing any sub-array of one. |
| 1480 | ★ | Running Sum of 1d Array |  | Return the running sum of an array. |
| 1498 | ★ | Number of Subsequences That Satisfy the Given Sum Condition |  | Count the number of subsequences where min+max target. |
| 1748 | ★ | Sum of Unique Elements |  | Find the sum of all unique elements in an array. |
| 1762 | ★ | Buildings With an Ocean View |  | Find all buildings with an ocean view (nothing taller to their right). |
| 1868 | ★ | Product of Two Run-Length Encoded Arrays |  | Multiply two run-length encoded arrays. |
| 1877 | ★ | Minimize Maximum Pair Sum in Array |  | Minimize the maximum pair sum after optimally pairing elements. |
| 1893 | ★ | Check if All the Integers in a Range Are Covered |  | Check if all integers in [left, right] are covered by at least one given range. |
| 1894 | ★ | Find the Student that Will Replace the Chalk |  | Find the index of the student who will replace the chalk. |
| 1920 | ★ | Build Array from Permutation |  | Build an array where result[i] = nums[nums[i]]. |
| 1929 | ★ | Concatenation of Array |  | Return the concatenation of an array with itself. |

## Sliding Window  (21 problems, 21 templated)

| # | ★ | Name | Complexity | Description |
|---|---|---|---|---|
| 3 | ★ | Longest Substring Without Repeating Characters | O(n) / O(1) | Find the length of the longest substring without any repeating characters in a given string. |
| 30 | ★ | Substring with Concatenation of All Words |  | Find all starting indices in s where a concatenation of all words in an array appears as a substring. |
| 76 | ★ | Minimum Window Substring | O(n) / O(k) | Find the minimum window substring of s that contains all characters in t. |
| 159 | ★ | Longest Substring with At Most Two Distinct Characters | O(n) / O(1) | Find the length of the longest substring containing at most two distinct characters. |
| 187 | ★ | Repeated DNA Sequences |  | Find all 10-letter DNA sequences (substrings) that occur more than once. |
| 209 | ★ | Minimum Size Subarray Sum |  | Find the minimal length subarray whose sum target. Return 0 if none. |
| 239 | ★ | Sliding Window Maximum | O(n) / O(k) | Return the maximum value in each sliding window of size k across an array. |
| 340 | ★ | Longest Substring with At Most K Distinct Characters | O(n) / O(k) | Find the length of the longest substring containing at most k distinct characters. |
| 395 | ★ | Longest Substring with At Least K Repeating Characters |  | Find the longest substring where every character appears at least k times. |
| 424 | ★ | Longest Repeating Character Replacement | O(n) / O(1) | Find the length of the longest substring where you can replace at most k characters to make all same. |
| 438 | ★ | Find All Anagrams in a String | O(n) / O(1) | Find all anagram start indices of pattern p in string s. |
| 487 | ★ | Max Consecutive Ones II |  | Given a binary array `nums`, return the maximum number of consecutive 1s if you may flip at most one 0. |
| 567 | ★ | Permutation in String | O(n) / O(1) | Check if any permutation of pattern p exists as a substring of string s. |
| 643 | ★ | Maximum Average Subarray I |  | Find the maximum average of any subarray of length k. |
| 689 | ★ | Maximum Sum of 3 Non-Overlapping Subarrays |  | Find 3 non-overlapping subarrays of length k with maximum total sum. |
| 713 | ★ | Subarray Product Less Than K |  | Return the number of contiguous subarrays whose product of all elements is strictly less than `k`. |
| 727 | ★ | Minimum Window Subsequence |  | Find the minimum window in s that contains all characters of t in order (subsequence). |
| 1004 | ★ | Max Consecutive Ones III | O(n) / O(1) | Find the maximum consecutive 1s if you can flip at most k zeros. |
| 1044 | ★ | Longest Duplicate Substring |  | Find the longest duplicate substring using binary search and rolling hash. |
| 1343 | ★ | #1343 | O(n) / O(1) | Count subarrays of size k with average >= threshold. |
| 1838 | ★ | Frequency of the Most Frequent Element |  | Find the minimum operations to make an array element appear the most frequently in a window. |

## Binary Search  (30 problems, 30 templated)

| # | ★ | Name | Complexity | Description |
|---|---|---|---|---|
| 4 | ★ | Median of Two Sorted Arrays |  | Find the median of two sorted arrays of sizes m and n in O(log(m+n)) time. |
| 33 | ★ | Search in Rotated Sorted Array | O(log n) / O(1) | Search for a target in a sorted array that has been rotated at an unknown pivot. Return index or -1. |
| 34 | ★ | Find First and Last Position of Element in Sorted Array | O(log n) / O(1) | Find the starting and ending positions of a target value in a sorted array. Return [-1,-1] if not found. |
| 35 | ★ | Search Insert Position | O(log n) / O(1) | Find the index where a target would be inserted in a sorted array to keep it sorted. |
| 69 | ★ | Sqrt(x) |  | Compute the integer square root of a non-negative integer x without using sqrt(). |
| 74 | ★ | Search a 2D Matrix |  | Search for a target in an m×n matrix where each row is sorted and each row's first element > previous row's last. |
| 81 | ★ | Search in Rotated Sorted Array II |  | Search in a sorted, rotated array that may contain duplicates. |
| 153 | ★ | Find Minimum in Rotated Sorted Array |  | Find the minimum element in a sorted, rotated array with no duplicates. |
| 162 | ★ | Find Peak Element | O(log n) / O(1) | Find any peak element (element greater than its neighbors) in an array. O(log n) required. |
| 240 | ★ | Search a 2D Matrix II |  | Search for a target in an m×n matrix where rows and columns are both sorted. |
| 278 | ★ | First Bad Version |  | Find the first bad version using a provided isBadVersion(n) API. Minimize API calls. |
| 374 | ★ | Guess Number Higher or Lower |  | Guess the number between 1 and n using a provided guess() API. Minimize calls. |
| 378 | ★ | Kth Smallest Element in a Sorted Matrix | O(n log n) / O(n) | Find the kth smallest element in an n×n matrix where rows and columns are sorted. |
| 410 | ★ | Split Array Largest Sum | O(n log sum) / O(1) | Split an array into m subarrays to minimize the largest subarray sum. |
| 475 | ★ | Heaters |  | Given house and heater positions, find the minimum heater radius so every house is covered by some heater. |
| 540 | ★ | Single Element in a Sorted Array |  | Find the single non-duplicate element in a sorted array where all others appear twice. O(log n). |
| 658 | ★ | Find K Closest Elements |  | Find k integers in a sorted array closest to x, ordered by closeness then value. |
| 704 | ★ | Binary Search | O(log n) / O(1) | Classic binary search: find target in sorted array. |
| 719 | ★ | Find K-th Smallest Pair Distance |  | Find the k-th smallest absolute distance among all pairs in the array. |
| 852 | ★ | Peak Index in a Mountain Array |  | Find the peak index in a mountain array (element greater than both neighbors). |
| 875 | ★ | Koko Eating Bananas | O(n log max) / O(1) | Find the minimum eating speed k so Koko can eat all banana piles within h hours. |
| 1011 | ★ | Capacity To Ship Packages Within D Days | O(n log sum) / O(1) | Find the minimum capacity to ship all packages within D days. |
| 1060 | ★ | Missing Element in Sorted Array |  | Find the kth missing number in a sorted array. |
| 1231 | ★ | #1231 | O(n log max) / O(1) | Max min-piece when cutting chocolate into k pieces. |
| 1283 | ★ | #1283 | O(n log max) / O(1) | Smallest divisor so sum of ceil(nums[i]/divisor) <= threshold. |
| 1428 | ★ | Leftmost Column with at Least a One |  | Find the leftmost column with at least one '1' in a binary matrix. |
| 1482 | ★ | Minimum Number of Days to Make m Bouquets |  | Find the minimum number of days to make m bouquets of k adjacent flowers. |
| 1539 | ★ | Kth Missing Positive Number |  | Find the kth missing positive integer. |
| 1818 | ★ | Minimum Absolute Sum Difference |  | Find the minimum absolute sum difference after one substitution. |
| 1891 | ★ | Cutting Ribbons |  | Find the maximum ribbon length such that m ribbons of that length can be cut. |

## Linked List  (31 problems, 31 templated)

| # | ★ | Name | Complexity | Description |
|---|---|---|---|---|
| 2 | ★ | Add Two Numbers | O(n) / O(1) | Add two non-negative integers represented as reversed linked lists (ones digit first). Return the sum as a reversed linked list. |
| 19 | ★ | Remove Nth Node From End of List |  | Remove the nth node from the end of a linked list and return the head. |
| 21 | ★ | Merge Two Sorted Lists | O(n) / O(1) | Merge two sorted linked lists into one sorted linked list in-place. |
| 24 | ★ | Swap Nodes in Pairs |  | Swap every two adjacent nodes in a linked list and return the modified head. |
| 25 | ★ | Reverse Nodes in k-Group | O(n) / O(1) | Reverse nodes in a linked list k at a time. If remaining nodes < k, leave them as-is. |
| 61 | ★ | Rotate List |  | Rotate a linked list to the right by k places. |
| 82 | ★ | Remove Duplicates from Sorted List II | O(n) / O(1) | Remove all nodes with duplicate values from a sorted linked list; keep only distinct values. |
| 83 | ★ | Remove Duplicates from Sorted List |  | Remove duplicate nodes from a sorted linked list; keep one copy of each value. |
| 86 | ★ | Partition List |  | Partition a linked list so all nodes with value < x come before nodes with value x. |
| 92 | ★ | Reverse Linked List II |  | Reverse nodes m through n (1-indexed) of a linked list in one pass. |
| 109 | ★ | Convert Sorted List to Binary Search Tree |  | Convert a sorted linked list to a height-balanced BST. |
| 138 | ★ | Copy List with Random Pointer |  | Deep-copy a linked list where each node has a 'random' pointer to any node or null. |
| 141 | ★ | Linked List Cycle | O(n) / O(1) | Detect if a linked list has a cycle. |
| 142 | ★ | Linked List Cycle II | O(n) / O(1) | Find the node where a cycle begins in a linked list. |
| 143 | ★ | Reorder List |  | Reorder a linked list L01… to L01-1… in-place. |
| 148 | ★ | Sort List |  | Sort a linked list in O(n log n) time and O(1) extra space. |
| 160 | ★ | Intersection of Two Linked Lists | O(n) / O(1) | Find the node where two singly linked lists intersect. |
| 203 | ★ | Remove Linked List Elements | O(n) / O(1) | Remove all nodes with a given value from a linked list. |
| 206 | ★ | Reverse Linked List |  | Reverse a singly linked list. |
| 234 | ★ | Palindrome Linked List | O(n) / O(1) | Check if a linked list is a palindrome in O(n) time and O(1) space. |
| 237 | ★ | Delete Node in a Linked List |  | Delete a node from a singly linked list given only a reference to that node (not the head). |
| 287 | ★ | Find the Duplicate Number | O(n) / O(1) | Find the duplicate number in an array of n+1 integers in range [1,n]. O(1) space required. |
| 328 | ★ | Odd Even Linked List |  | Rearrange a linked list so all odd-indexed nodes come before even-indexed nodes. |
| 369 | ★ | Plus One Linked List |  | A non-negative integer is stored as a linked list of digits in big-endian order (most significant first). Add one to it and return the resulting list. |
| 430 | ★ | Flatten a Multilevel Doubly Linked List |  | Flatten a multilevel doubly linked list where nodes may have a child list. |
| 445 | ★ | Add Two Numbers II |  | Two numbers are stored as linked lists in big-endian order (most significant digit first). Add them and return the sum as a linked list, also in big-endian order. |
| 708 | ★ | Insert into a Sorted Circular Linked List |  | Insert a value into a sorted circular linked list. |
| 725 | ★ | Split Linked List in Parts |  | Split a linked list into k consecutive parts as equal in size as possible. |
| 876 | ★ | Middle of the Linked List | O(n) / O(1) | Find the middle node of a linked list (if two middles, return second). |
| 1171 | ★ | Remove Zero Sum Consecutive Nodes from Linked List |  | Remove consecutive nodes from a linked list whose values sum to zero. |
| 1265 | ★ | Print Immutable Linked List in Reverse |  | Print all values of an immutable linked list in reverse without modifying it. |

## String  (87 problems, 87 templated)

| # | ★ | Name | Complexity | Description |
|---|---|---|---|---|
| 6 | ★ | ZigZag Conversion |  | Convert a string into a zigzag pattern across numRows rows and read it row by row. |
| 7 | ★ | Reverse Integer | O(log n) / O(1) | Reverse the digits of a 32-bit signed integer. Return 0 if the reversed value overflows. |
| 8 | ★ | String to Integer (atoi) |  | Implement atoi: parse a string, skip whitespace, handle optional sign, read digits, clamp to 32-bit integer range. |
| 12 | ★ | Integer to Roman |  | Convert an integer to its Roman numeral representation (values 1--3999). |
| 13 | ★ | Roman to Integer |  | Convert a Roman numeral string to an integer. |
| 14 | ★ | Longest Common Prefix |  | Find the longest common prefix string among an array of strings. Return '' if none. |
| 28 | ★ | Implement strStr() |  | Find the first occurrence of needle in haystack. Return -1 if not found. |
| 38 | ★ | Count and Say |  | Generate the nth term of the 'count and say' sequence: read digits of previous term aloud. |
| 43 | ★ | Multiply Strings |  | Multiply two non-negative integers given as strings. Return product as a string. |
| 49 | ★ | Group Anagrams | O(nk) / O(n) | Group an array of strings so that anagrams are together. |
| 58 | ★ | Length of Last Word |  | Return the length of the last word in a string (word = max sequence of non-space chars). |
| 65 | ★ | Valid Number |  | Validate whether a string is a valid decimal number (integers, fractions, exponents). |
| 67 | ★ | Add Binary | O(n) / O(n) | Add two binary strings and return their binary sum as a string. |
| 68 | ★ | Text Justification |  | Format words into lines of maxWidth, fully justified (equal spaces, last line left-aligned). |
| 125 | ★ | Valid Palindrome |  | Check if a string is a palindrome, ignoring non-alphanumeric characters and case. |
| 151 | ★ | Reverse Words in a String |  | Reverse the order of words in a string (split on spaces, handle multiple spaces). |
| 161 | ★ | One Edit Distance |  | Determine if two strings are one edit distance apart (insert, delete, or replace one char). |
| 163 | ★ | Missing Ranges |  | Given a sorted array, return missing ranges between lower and upper bounds. |
| 165 | ★ | Compare Version Numbers |  | Compare two version number strings (dot-separated integers). Return -1, 0, or 1. |
| 166 | ★ | Fraction to Recurring Decimal |  | Convert a fraction numerator/denominator to a decimal string, noting repeating parts in parentheses. |
| 168 | ★ | Excel Sheet Column Title | O(log n) / O(1) | Convert an integer to its Excel column title (1, 26, 27, …). |
| 171 | ★ | Excel Sheet Column Number | O(L) / O(1) | Convert an Excel column title (A1, Z26, AA27) to its integer number. |
| 179 | ★ | Largest Number |  | Arrange numbers so their concatenation forms the largest possible number. |
| 186 | ★ | Reverse Words in a String II |  | Reverse words in a character array in-place (words separated by spaces). |
| 205 | ★ | Isomorphic Strings |  | Check if two strings follow the same character-substitution pattern (isomorphic). |
| 214 | ★ | Shortest Palindrome |  | Find the shortest palindrome by adding characters in front of a string. |
| 228 | ★ | Summary Ranges |  | Given a sorted unique integer array, summarize consecutive runs as ranges. |
| 242 | ★ | Valid Anagram | O(n) / O(1) | Determine if two strings are anagrams of each other. |
| 246 | ★ | Strobogrammatic Number |  | Check if a number reads the same when rotated 180 degrees. |
| 249 | ★ | Group Shifted Strings |  | Group strings that follow the same shift sequence (each char shifted by the same amount). |
| 266 | ★ | Palindrome Permutation |  | Check if a string can be rearranged into a palindrome (at most one odd-count char). |
| 271 | ★ | Encode and Decode Strings |  | Encode a list of strings to a single string and decode it back. |
| 273 | ★ | Integer to English Words |  | Convert a non-negative integer to its English words representation. |
| 290 | ★ | Word Pattern |  | Check if a string s follows a given pattern (bijective character mapping). |
| 299 | ★ | Bulls and Cows |  | Count bulls (right digit, right place) and cows (right digit, wrong place) in a number guessing game. |
| 344 | ★ | Reverse String |  | Reverse a character array in-place. |
| 345 | ★ | Reverse Vowels of a String |  | Reverse only the vowels of a string. |
| 383 | ★ | Ransom Note | O(n) / O(1) | Determine if a ransom note can be constructed from a magazine's letters. |
| 387 | ★ | First Unique Character in a String |  | Find the first non-repeating character in a string. Return its index or -1. |
| 388 | ★ | Longest Absolute File Path |  | Find the length of the longest absolute file path in a file system string. |
| 392 | ★ | Is Subsequence |  | Check if string s is a subsequence of string t. |
| 408 | ★ | Valid Word Abbreviation |  | Check if an abbreviation matches a word (digits represent skipped characters). |
| 409 | ★ | Longest Palindrome |  | Find the length of the longest palindrome that can be built from the given letters. |
| 415 | ★ | Add Strings |  | Add two non-negative integers given as strings. Return the sum as a string. |
| 422 | ★ | Valid Word Square |  | Given a sequence of words, check whether they form a valid word square (kth row equals kth column). |
| 423 | ★ | Reconstruct Original Digits from English |  | Given a scrambled string of digit-word letters, decode original digits in order. |
| 434 | ★ | Number of Segments in a String |  | Count the number of segments (maximal runs of non-space chars) in a string. |
| 443 | ★ | String Compression |  | Compress an array of chars in-place: 'aabcc' 'a2bc2'. Return new length. |
| 459 | ★ | Repeated Substring Pattern |  | Check if a string can be built by repeating one of its substrings multiple times. |
| 468 | ★ | Validate IP Address |  | Validate whether a string is a valid IPv4 or IPv6 address. |
| 500 | ★ | Keyboard Row |  | Find all words that can be typed on a single row of a QWERTY keyboard. |
| 520 | ★ | Detect Capital |  | Check if a word is capitalized correctly (all caps, all lower, or first letter only). |
| 524 | ★ | Longest Word in Dictionary through Deleting |  | Find the longest word in a dictionary that is a subsequence of string s. |
| 541 | ★ | Reverse String II |  | Reverse the first k characters of every 2k-character block in a string. |
| 551 | ★ | Student Attendance Record I |  | Check if a student's attendance record is eligible for an award (no late > 1, no absence 3 consecutive). |
| 556 | ★ | Next Greater Element III |  | Find the next greater element by rearranging the digits of n. Return -1 if not possible or overflow. |
| 557 | ★ | Reverse Words in a String III |  | Reverse individual words in a string while preserving word order. |
| 592 | ★ | Fraction Addition and Subtraction |  | Add or subtract fractions, returning the result in lowest terms. |
| 616 | ★ | Add Bold Tag in String |  | Wrap every substring of `s` that matches a word in the dictionary with `<b>...</b>`, merging overlaps. |
| 657 | ★ | Robot Return to Origin |  | Check if a robot following instruction string (UDLR) returns to origin. |
| 670 | ★ | Maximum Swap |  | Swap two digits in a number to get the maximum possible value. |
| 680 | ★ | Valid Palindrome II |  | Check if a string is a palindrome after deleting at most one character. |
| 681 | ★ | Next Closest Time |  | Find the next closest time using only the digits from a given time string. |
| 686 | ★ | Repeated String Match |  | Find the minimum number of times string a must repeat so b is a substring. |
| 709 | ★ | To Lower Case |  | Convert a string to lowercase. |
| 726 | ★ | Number of Atoms |  | Parse a chemical formula string and return atom counts in sorted order. |
| 748 | ★ | Shortest Completing Word |  | Find the shortest word in a list that contains all letters of a license plate (case-insensitive, with multiplicity). |
| 788 | ★ | Rotated Digits |  | Count numbers in `[1, n]` that become a different valid number when each digit is rotated 180 degrees. |
| 791 | ★ | Custom Sort String |  | Sort string s so its characters appear in the order given by string order. |
| 794 | ★ | Valid Tic-Tac-Toe State |  | Decide whether the given tic-tac-toe board is reachable from valid play. |
| 796 | ★ | Rotate String |  | Check if string t is a rotation of string s. |
| 809 | ★ | Expressive Words |  | Determine if a query word matches a stretched version of a word in a list. |
| 824 | ★ | Goat Latin |  | Convert words to Goat Latin: append 'ma', move leading consonants to end + 'ma'. |
| 833 | ★ | Find And Replace in String |  | Apply non-overlapping indexed replacements: at each index, if `sources[k]` matches, replace it with `targets[k]`. |
| 859 | ★ | Buddy Strings |  | Check if two strings are 'buddy strings': swapping exactly one pair makes them equal. |
| 953 | ★ | Verifying an Alien Dictionary |  | Check if words are sorted in a given alien language's alphabetical order. |
| 1055 | ★ | Shortest Way to Form String |  | Find the minimum number of subsequences of `source` whose concatenation equals `target`. Return -1 if impossible. |
| 1108 | ★ | Defanging an IP Address |  | Defang an IP address by replacing '.' with '[.]'. |
| 1221 | ★ | Split a String in Balanced Strings |  | Find the maximum number of balanced strings ('R' count == 'L' count) to split into. |
| 1328 | ★ | Break a Palindrome |  | Break a palindrome by changing one character to get the lexicographically smallest non-palindrome. |
| 1392 | ★ | Longest Happy Prefix |  | Find the longest happy prefix (prefix that is also a suffix). |
| 1446 | ★ | Consecutive Characters |  | Find the maximum number of consecutive same characters in a string. |
| 1554 | ★ | Strings Differ by One Character |  | Check if any two strings in a list differ by exactly one character. |
| 1556 | ★ | Thousand Separator |  | Format an integer with a dot as the thousands separator. |
| 1736 | ★ | Latest Time by Replacing Hidden Digits |  | Find the latest valid time by replacing '?' with appropriate digits. |
| 1816 | ★ | Truncate Sentence |  | Truncate a sentence to the first k words. |
| 1844 | ★ | Replace All Digits with Characters |  | Replace each digit at odd positions with the corresponding letter. |

## Stack / Queue / Heap  (55 problems, 55 templated)

| # | ★ | Name | Complexity | Description |
|---|---|---|---|---|
| 20 | ★ | Valid Parentheses | O(n) / O(n) | Determine if a string of brackets '()[]\\' is valid --- every open bracket is closed in the correct order. |
| 23 | ★ | Merge k Sorted Lists | O(n log k) / O(k) | Merge k sorted linked lists into one sorted linked list. |
| 32 | ★ | Longest Valid Parentheses |  | Find the length of the longest valid (well-formed) parentheses substring. |
| 71 | ★ | Simplify Path |  | Simplify an absolute Unix file path (handle '.', '..', multiple slashes). |
| 84 | ★ | Largest Rectangle in Histogram | O(n) / O(n) | Find the area of the largest rectangle that can be formed in a histogram. |
| 85 | ★ | Maximal Rectangle | O(mn) / O(n) | Find the largest rectangle containing only 1s in a binary matrix. |
| 150 | ★ | Evaluate Reverse Polish Notation |  | Evaluate a Reverse Polish Notation expression with +, -, *, /. |
| 155 | ★ | Min Stack |  | Design a stack that supports push, pop, top, and retrieving the minimum in O(1). |
| 215 | ★ | Kth Largest Element in an Array | O(n) avg / O(1) | Find the kth largest element in an unsorted array (not necessarily distinct). |
| 218 | ★ | The Skyline Problem |  | Given building rectangles, return the skyline as a list of key points. |
| 224 | ★ | Basic Calculator | O(n) / O(n) | Evaluate a string expression with '+', '-', and nested parentheses. |
| 225 | ★ | Implement Stack using Queues |  | Implement a LIFO stack using only queue operations. |
| 227 | ★ | Basic Calculator II | O(n) / O(n) | Evaluate a string expression with '+', '-', '*', '/' (no parentheses, integer division). |
| 232 | ★ | Implement Queue using Stacks |  | Implement a queue using two stacks. |
| 295 | ★ | Find Median from Data Stream | O(log n) / O(n) | Design a data structure to find the median of a stream of integers efficiently. |
| 316 | ★ | Remove Duplicate Letters |  | Remove duplicate letters so each appears once, result is lexicographically smallest. |
| 347 | ★ | Top K Frequent Elements | O(n) / O(n) | Find the k most frequent elements in an integer array. |
| 373 | ★ | Find K Pairs with Smallest Sums | O(k log k) / O(k) | Find the k pairs (u,v) with the smallest sums, one from each of two sorted arrays. |
| 394 | ★ | Decode String |  | Decode a string encoded as k[encoded_string] where brackets can be nested. |
| 402 | ★ | Remove K Digits |  | Remove k digits from a number string to get the smallest possible number. |
| 451 | ★ | Sort Characters By Frequency |  | Sort characters in a string by frequency of occurrence (descending). |
| 456 | ★ | 132 Pattern |  | Check if a 1-3-2 pattern exists in an integer array. |
| 480 | ★ | Sliding Window Median | O(n log k) / O(k) | Find the median in each sliding window of size k across an array. |
| 496 | ★ | Next Greater Element I | O(n) / O(n) | For each element in nums1, find the first greater element to its right in nums2. |
| 502 | ★ | IPO |  | Maximize profit by choosing at most k projects, each requiring capital and providing profit. |
| 503 | ★ | Next Greater Element II | O(n) / O(n) | Find the next greater element for each element in a circular array. |
| 506 | ★ | Relative Ranks |  | Assign ranks ("Gold Medal", "Silver Medal", "Bronze Medal", then 4, 5, ...) to athletes by score. |
| 636 | ★ | Exclusive Time of Functions |  | Given a log of function start/end times, compute exclusive time per function. |
| 678 | ★ | Valid Parenthesis String |  | Check if a string with '(', ')', '*' (wildcard) can be a valid parenthesis string. |
| 692 | ★ | Top K Frequent Words | O(n log k) / O(n) | Find the k most frequent words (sorted by frequency, then lex). |
| 703 | ★ | Kth Largest Element in a Stream |  | Design a class to find the kth largest element in a stream. |
| 716 | ★ | Max Stack |  | Design a stack with push, pop, top, getMax, and popMax operations. |
| 735 | ★ | Asteroid Collision |  | Simulate asteroids moving in a row: right-moving collide with left-moving. |
| 739 | ★ | Daily Temperatures | O(n) / O(n) | Given temperatures, find the number of days until a warmer temperature. |
| 759 | ★ | Employee Free Time |  | Find the free time intervals common to all employees given their schedules. |
| 767 | ★ | Reorganize String | O(n log n) / O(n) | Rearrange a string so no two adjacent characters are the same. |
| 772 | ★ | Basic Calculator III | O(n) / O(n) | Evaluate an arithmetic expression with `+`, `-`, `*`, `/`, and parentheses. |
| 844 | ★ | Backspace String Compare |  | Check if two strings are equal after processing '#' as backspace. |
| 856 | ★ | Score of Parentheses |  | Calculate the score of a valid parentheses string (empty=0, AB=A+B, (A)=2A or 1 if empty). |
| 862 | ★ | Shortest Subarray with Sum at Least K |  | Find the length of the shortest subarray with sum k (k can be negative). |
| 907 | ★ | Sum of Subarray Minimums |  | Find the sum of subarray minimums for all subarrays. |
| 921 | ★ | Minimum Add to Make Parentheses Valid |  | Find the minimum additions to make a parentheses string valid. |
| 946 | ★ | Validate Stack Sequences |  | Check if a sequence can be produced by a series of push-pop operations on a stack. |
| 973 | ★ | K Closest Points to Origin | O(n) avg / O(k) | Find the k points closest to the origin. |
| 1047 | ★ | Remove All Adjacent Duplicates In String |  | Remove all adjacent duplicate characters until no more adjacent duplicates exist. |
| 1086 | ★ | High Five |  | For each student, compute the average of their top five scores. |
| 1190 | ★ | Reverse Substrings Between Each Pair of Parentheses |  | Reverse the substrings between each pair of parentheses (innermost first). |
| 1209 | ★ | Remove All Adjacent Duplicates in String II |  | Remove all adjacent duplicates of length k in a string repeatedly. |
| 1249 | ★ | Minimum Remove to Make Valid Parentheses |  | Remove the minimum number of parentheses to make the string valid. |
| 1337 | ★ | The K Weakest Rows in a Matrix |  | Find the k weakest rows in a matrix (fewest soldiers, ties broken by row index). |
| 1541 | ★ | Minimum Insertions to Balance a Parentheses String |  | Find the minimum insertions to make a string balanced (every ')' needs two '('). |
| 1614 | ★ | Maximum Nesting Depth of the Parentheses |  | Find the maximum nesting depth of parentheses in a string. |
| 1792 | ★ | Maximum Average Pass Ratio |  | Maximize the average pass ratio by adding extra students optimally. |
| 1944 | ★ | Number of Visible People in a Queue |  | Count the number of people each person can see in a queue (taller blocks view). |
| 1985 | ★ | Find the Kth Largest Integer in the Array |  | Find the kth largest integer in an array of number strings. |

## DFS / Backtracking  (140 problems, 140 templated)

| # | ★ | Name | Complexity | Description |
|---|---|---|---|---|
| 17 | ★ | Letter Combinations of a Phone Number |  | Given a string of digits 2-9, return all possible letter combinations a phone keypad could represent. |
| 22 | ★ | Generate Parentheses |  | Generate all combinations of n pairs of well-formed parentheses. |
| 36 | ★ | Valid Sudoku |  | Determine if a 9×9 Sudoku board is valid (rows, columns, and 3×3 boxes each contain 1-9 with no repeats). |
| 37 | ★ | Sudoku Solver | O(9\^m) / O(1) | Solve a Sudoku puzzle by filling empty cells with digits 1-9 such that each row, column, and 3×3 box is valid. |
| 39 | ★ | Combination Sum | O(2^n) / O(n) | Find all unique combinations of candidates (may reuse) that sum to a target. |
| 40 | ★ | Combination Sum II | O(2^n) / O(n) | Find all unique combinations of candidates (each used once) that sum to a target. Candidates may have duplicates. |
| 46 | ★ | Permutations | O(n!) / O(n) | Return all possible permutations of a distinct-integer array. |
| 47 | ★ | Permutations II | O(n!) / O(n) | Return all unique permutations of an array that may contain duplicates. |
| 51 | ★ | N-Queens | O(n!) / O(n) | Place n queens on an n×n chessboard so no two attack each other. Return all distinct solutions. |
| 60 | ★ | Permutation Sequence | O(n) / O(n) | Find the kth permutation sequence of numbers 1 to n. |
| 77 | ★ | Combinations |  | Return all combinations of k numbers from 1 to n. |
| 78 | ★ | Subsets | O(2^n) / O(n) | Return all possible subsets (power set) of a distinct-integer array. |
| 79 | ★ | Word Search | O(mn4\^L) / O(L) | Search for a word in an m×n grid of characters by adjacent (up/down/left/right) traversal without reuse. |
| 90 | ★ | Subsets II | O(2^n) / O(n) | Return all unique subsets of an array that may contain duplicates. |
| 93 | ★ | Restore IP Addresses |  | Restore all possible valid IP address strings from a string of digits. |
| 94 | ★ | Binary Tree Inorder Traversal |  | Return the inorder traversal (left--root--right) of a binary tree. |
| 95 | ★ | Unique Binary Search Trees II |  | Generate all structurally unique BSTs with values 1..n. |
| 98 | ★ | Validate Binary Search Tree | O(n) / O(h) | Validate whether a binary tree is a valid Binary Search Tree. |
| 99 | ★ | Recover Binary Search Tree |  | Recover a BST where exactly two nodes have been swapped. |
| 100 | ★ | Same Tree |  | Check if two binary trees are structurally identical with the same node values. |
| 101 | ★ | Symmetric Tree |  | Check if a binary tree is symmetric (mirror image of itself). |
| 102 | ★ | Binary Tree Level Order Traversal | O(n) / O(n) | Return node values level by level (left to right) in a binary tree. |
| 103 | ★ | Binary Tree Zigzag Level Order Traversal | O(n) / O(n) | Return node values in zigzag level order (left-to-right for odd levels, right-to-left for even). |
| 104 | ★ | Maximum Depth of Binary Tree | O(n) / O(h) | Find the maximum depth (number of nodes along the longest root-to-leaf path) of a binary tree. |
| 105 | ★ | Construct Binary Tree from Preorder and Inorder Traversal |  | Reconstruct a binary tree from its preorder and inorder traversal arrays. |
| 106 | ★ | Construct Binary Tree from Inorder and Postorder Traversal |  | Reconstruct a binary tree from its inorder and postorder traversal arrays. |
| 107 | ★ | Binary Tree Level Order Traversal II |  | Return node values level by level from bottom to top. |
| 108 | ★ | Convert Sorted Array to Binary Search Tree |  | Convert a sorted integer array to a height-balanced BST. |
| 110 | ★ | Balanced Binary Tree | O(n) / O(h) | Determine if a binary tree is height-balanced (every node's subtrees differ in depth by at most 1). |
| 111 | ★ | Minimum Depth of Binary Tree | O(n) / O(h) | Find the minimum depth of a binary tree (shortest path from root to a leaf). |
| 112 | ★ | Path Sum |  | Check if a root-to-leaf path exists whose node values sum to a given target. |
| 113 | ★ | Path Sum II |  | Find all root-to-leaf paths whose values sum to a given target. |
| 114 | ★ | Flatten Binary Tree to Linked List |  | Flatten a binary tree into a linked list in-place (preorder, using right pointers). |
| 116 | ★ | Populating Next Right Pointers in Each Node |  | Populate each node's 'next' pointer to its right neighbor (perfect binary tree). Use O(1) extra space. |
| 117 | ★ | Populating Next Right Pointers in Each Node II |  | Same as 116 but for an arbitrary binary tree. |
| 124 | ★ | Binary Tree Maximum Path Sum | O(n) / O(h) | Find the maximum path sum in a binary tree (path can start/end at any node). |
| 129 | ★ | Sum Root to Leaf Numbers |  | Sum all root-to-leaf numbers where each path forms a number (root digit is most significant). |
| 144 | ★ | Binary Tree Preorder Traversal |  | Return the preorder traversal (root → left → right) of a binary tree. |
| 145 | ★ | Binary Tree Postorder Traversal |  | Return the postorder traversal (left → right → root) of a binary tree. |
| 199 | ★ | Binary Tree Right Side View | O(n) / O(n) | Return the values visible from the right side of a binary tree (one per level). |
| 216 | ★ | Combination Sum III | O(C(9,k)) / O(k) | Find all combinations of k distinct numbers from 1--9 that sum to n. |
| 222 | ★ | Count Complete Tree Nodes |  | Count nodes in a complete binary tree without visiting all nodes. Faster than O(n). |
| 226 | ★ | Invert Binary Tree |  | Invert (mirror) a binary tree. |
| 230 | ★ | Kth Smallest Element in a BST | O(n) / O(h) | Find the kth smallest element in a BST. |
| 235 | ★ | Lowest Common Ancestor of a Binary Search Tree |  | Find the lowest common ancestor of two nodes in a BST. |
| 236 | ★ | Lowest Common Ancestor of a Binary Tree |  | Find the lowest common ancestor of two nodes in a binary tree (not necessarily a BST). |
| 241 | ★ | Different Ways to Add Parentheses |  | Given an expression string, compute all possible results from different ways to parenthesize it. |
| 250 | ★ | Count Univalue Subtrees |  | Count subtrees in which all nodes share the same value. |
| 255 | ★ | Verify Preorder Sequence in Binary Search Tree |  | Verify whether an array of integers is the correct preorder traversal of a BST. |
| 257 | ★ | Binary Tree Paths |  | Return all root-to-leaf paths in a binary tree as strings ('1->2->5'). |
| 267 | ★ | Palindrome Permutation II |  | Return all palindrome permutations of a string. |
| 270 | ★ | Closest Binary Search Tree Value | O(h) / O(1) | Find the value in a BST closest to a given target. |
| 272 | ★ | Closest Binary Search Tree Value II |  | Find k values in a BST closest to target. |
| 282 | ★ | Expression Add Operators |  | Insert operators +, -, * between digits of a string num to reach a target value. Return all expressions. |
| 285 | ★ | Inorder Successor in BST | O(h) / O(1) | Find the inorder successor of a given node in a BST. |
| 291 | ★ | Word Pattern II |  | Check if a string s follows a given pattern where pattern chars map to non-overlapping substrings. |
| 293 | ★ | Flip Game |  | Given a string of '+' and '-', return all states after flipping one "++" to "--". |
| 294 | ★ | Flip Game II |  | Determine if the first player can guarantee a win in Flip Game. |
| 297 | ★ | Serialize and Deserialize Binary Tree |  | Serialize and deserialize a binary tree to/from a string. |
| 298 | ★ | Binary Tree Longest Consecutive Sequence |  | Find the longest consecutive sequence in a binary tree (parent to child, values increasing by 1). |
| 301 | ★ | Remove Invalid Parentheses |  | Remove the minimum number of parentheses to make the string valid. Return all results. |
| 306 | ★ | Additive Number |  | Check if a string forms an additive number (each number = sum of two preceding). |
| 314 | ★ | Binary Tree Vertical Order Traversal |  | Return the binary tree's node values ordered by column, then by row. |
| 320 | ★ | Generalized Abbreviation |  | Return all possible abbreviations of a word. |
| 339 | ★ | Nested List Weight Sum |  | Compute the weighted sum of a nested integer list where weight equals depth. |
| 364 | ★ | Nested List Weight Sum II |  | Sum each integer weighted by its inverse depth (deepest integers have weight 1). |
| 386 | ★ | Lexicographical Numbers |  | Return integers 1..n in lexicographical order. |
| 404 | ★ | Sum of Left Leaves |  | Find the sum of all left leaves in a binary tree. |
| 426 | ★ | Convert Binary Search Tree to Sorted Doubly Linked List |  | Convert a BST to a sorted circular doubly linked list in-place. |
| 429 | ★ | N-ary Tree Level Order Traversal |  | Return the level order traversal of an N-ary tree. |
| 437 | ★ | Path Sum III | O(n) / O(n) | Count paths in a binary tree that sum to a given value (path goes downward, any node to any node). |
| 440 | ★ | K-th Smallest in Lexicographical Order |  | Find the kth smallest integer in 1..n by lexicographical order. |
| 449 | ★ | Serialize and Deserialize BST |  | Serialize and deserialize a BST compactly. |
| 450 | ★ | Delete Node in a BST |  | Delete a given key from a BST and return the updated root. |
| 473 | ★ | Matchsticks to Square |  | Determine if n matchsticks can form exactly 4 equal-length sides of a square. |
| 488 | ★ | Zuma Game |  | Find the minimum number of marbles to insert in Zuma to clear the board. |
| 489 | ★ | Robot Room Cleaner |  | Design a robot cleaner: given room-cleaning robot with no map, clean the entire room. |
| 491 | ★ | Increasing Subsequences |  | Return all increasing subsequences of length ≥ 2 (input may have duplicates). |
| 501 | ★ | Find Mode in Binary Search Tree |  | Find the mode(s) in a BST (values that appear most frequently). |
| 508 | ★ | Most Frequent Subtree Sum |  | Find the subtree sum(s) that occur most frequently. |
| 510 | ★ | Inorder Successor in BST II |  | Find the inorder successor of a node given only a parent pointer (no root). |
| 513 | ★ | #513 | O(n) / O(n) | Find leftmost value in last row of binary tree. |
| 515 | ★ | Find Largest Value in Each Tree Row |  | Return the maximum value found at each level. |
| 526 | ★ | Beautiful Arrangement |  | Count 'beautiful arrangements': n numbers placed so each divides or is divisible by its position. |
| 536 | ★ | Construct Binary Tree from String |  | Construct a binary tree from its string representation '4(2(3)(1))(6(5))'. |
| 538 | ★ | Convert BST to Greater Tree |  | Convert each BST node's value to the sum of all values greater than or equal to it. |
| 543 | ★ | Diameter of Binary Tree | O(n) / O(h) | Find the diameter of a binary tree (longest path between any two nodes). |
| 545 | ★ | Boundary of Binary Tree |  | Return the boundary of a binary tree: left boundary + leaves + right boundary (no duplicates). |
| 549 | ★ | Binary Tree Longest Consecutive Sequence II | O(n) / O(h) | Find the longest consecutive sequence in a binary tree (can go up or down, must be consecutive). |
| 559 | ★ | Maximum Depth of N-ary Tree |  | Find the maximum depth of an N-ary tree. |
| 563 | ★ | Binary Tree Tilt |  | Find the total tilt of a binary tree (sum of leftSum - rightSum for all nodes). |
| 572 | ★ | Subtree of Another Tree |  | Check if tree t is a subtree of tree s. |
| 589 | ★ | N-ary Tree Preorder Traversal |  | Return the preorder traversal of an N-ary tree. |
| 590 | ★ | N-ary Tree Postorder Traversal |  | Return the postorder traversal of an N-ary tree. |
| 606 | ★ | Construct String from Binary Tree |  | Construct a string from a binary tree using preorder with parentheses. |
| 617 | ★ | Merge Two Binary Trees |  | Merge two binary trees by summing overlapping nodes. |
| 637 | ★ | Average of Levels in Binary Tree |  | Return the average value of each level of a binary tree. |
| 652 | ★ | Find Duplicate Subtrees |  | Find all duplicate subtrees in a binary tree; return root of each. |
| 653 | ★ | Two Sum IV - Input is a BST |  | Find two numbers in a BST that sum to a given target. |
| 654 | ★ | Maximum Binary Tree |  | Build the maximum binary tree: root is array max, left from left subarray, right from right. |
| 662 | ★ | Maximum Width of Binary Tree | O(n) / O(n) | Return the maximum width of any level of a binary tree. Width is defined as the length between the leftmost and rightmost non-null nodes, including all the null nodes in between. |
| 671 | ★ | Second Minimum Node In a Binary Tree |  | In a tree where each node's value is the min of its children, find the second smallest value overall. |
| 679 | ★ | 24 Game |  | Check if 4 numbers with any order and any of +,-,*,/ can produce 24. |
| 687 | ★ | #687 | O(n) / O(h) | Longest univalue path --- edges between nodes of equal value. |
| 698 | ★ | Partition to K Equal Sum Subsets |  | Determine if an array can be split into k subsets of equal sum. |
| 700 | ★ | Search in a Binary Search Tree |  | Search for a value in a BST. |
| 701 | ★ | Insert into a Binary Search Tree |  | Insert a value into a BST and return the updated root. |
| 742 | ★ | Closest Leaf in a Binary Tree |  | Find the node in a binary tree closest to the target that is a leaf. |
| 776 | ★ | Split BST |  | Split a BST into two trees: one with values V and one with values > V. |
| 784 | ★ | Letter Case Permutation |  | Return all strings formed by toggling the case of letters in a string. |
| 814 | ★ | Binary Tree Pruning |  | Prune a binary tree by removing subtrees containing no 1s. |
| 842 | ★ | Split Array into Fibonacci Sequence |  | Check if a string can be split into a Fibonacci-like sequence. |
| 863 | ★ | All Nodes Distance K in Binary Tree |  | Find all nodes at distance k from a target node in a binary tree. |
| 865 | ★ | Smallest Subtree with all the Deepest Nodes |  | Find the smallest subtree containing all the deepest leaves. |
| 889 | ★ | Construct Binary Tree from Preorder and Postorder Traversal |  | Reconstruct a binary tree from preorder and postorder traversals (any valid tree). |
| 897 | ★ | Increasing Order Search Tree |  | Transform a BST into an increasing-order search tree (right-skewed). |
| 919 | ★ | Complete Binary Tree Inserter |  | Design a complete binary tree inserter with O(1) insert. |
| 932 | ★ | Beautiful Array |  | Construct a beautiful array where no three elements form an arithmetic progression. |
| 938 | ★ | Range Sum of BST |  | Return the sum of all BST node values within the range [low, high]. |
| 951 | ★ | Flip Equivalent Binary Trees |  | Check if two binary trees are flip-equivalent (can make them identical by flipping children). |
| 958 | ★ | Check Completeness of a Binary Tree |  | Check if a binary tree is a complete binary tree. |
| 987 | ★ | Vertical Order Traversal of a Binary Tree |  | Return node values grouped by vertical position (column), then by row, then by value. |
| 988 | ★ | Smallest String Starting From Leaf |  | Find the lexicographically smallest string from root-to-leaf path. |
| 993 | ★ | Cousins in Binary Tree |  | Check if two nodes in a binary tree are cousins (same depth, different parents). |
| 998 | ★ | Maximum Binary Tree II |  | Insert a value into a maximum tree built by appending the value to the original array's end. |
| 1008 | ★ | Construct Binary Search Tree from Preorder Traversal |  | Construct a BST from its preorder traversal. |
| 1026 | ★ | Maximum Difference Between Node and Ancestor |  | Find the maximum difference between a node and its ancestor in a binary tree. |
| 1038 | ★ | Binary Search Tree to Greater Sum Tree |  | Convert each BST node to the sum of all nodes with a greater or equal value. |
| 1087 | ★ | Brace Expansion |  | Return all strings formed by expanding brace expressions (comma-separated choices). |
| 1104 | ★ | Path In Zigzag Labelled Binary Tree |  | Find the parent node in a zigzag-labeled infinite binary tree. |
| 1110 | ★ | Delete Nodes And Return Forest |  | Delete given nodes from a binary tree and return the roots of the remaining forest. |
| 1123 | ★ | Lowest Common Ancestor of Deepest Leaves |  | Find the LCA of the deepest leaves in a binary tree. |
| 1161 | ★ | Maximum Level Sum of a Binary Tree |  | Find the level of a binary tree with the maximum sum of node values. |
| 1214 | ★ | Two Sum BSTs |  | Given two BSTs and a target, decide if a value from each sums to the target. |
| 1305 | ★ | All Elements in Two Binary Search Trees |  | Return all elements from two BSTs in sorted order. |
| 1361 | ★ | Validate Binary Tree Nodes |  | Given child arrays, verify the nodes form exactly one valid binary tree. |
| 1382 | ★ | Balance a Binary Search Tree |  | Convert a BST to a balanced BST. |
| 1522 | ★ | Diameter of N-Ary Tree |  | Find the diameter of an N-ary tree. |
| 1644 | ★ | Lowest Common Ancestor of a Binary Tree II |  | Find the LCA of two nodes in a binary tree where nodes may not exist. |
| 1650 | ★ | Lowest Common Ancestor of a Binary Tree III |  | Find the LCA of two nodes given parent pointers (no root access). |

## Graph  (58 problems, 58 templated)

| # | ★ | Name | Complexity | Description |
|---|---|---|---|---|
| 126 | ★ | Word Ladder II |  | Find all shortest transformation sequences from beginWord to endWord, changing one letter at a time. |
| 127 | ★ | Word Ladder | O(V+E) / O(V) | Find the length of the shortest transformation sequence from beginWord to endWord (one letter at a time, each word must be in wordList). |
| 130 | ★ | Surrounded Regions | O(mn) / O(mn) | Capture all 'O' regions not connected to the border (surrounded by 'X'); flip them to 'X'. |
| 133 | ★ | Clone Graph |  | Deep-copy (clone) an undirected graph where each node has a value and a neighbors list. |
| 200 | ★ | Number of Islands | O(mn) / O(mn) | Count the number of islands (connected regions of '1's) in a 2D binary grid. |
| 207 | ★ | Course Schedule | O(V+E) / O(V+E) | Determine if all n courses can be finished given prerequisite pairs (detect cycle in directed graph). |
| 210 | ★ | Course Schedule II | O(V+E) / O(V+E) | Return a valid course order given prerequisites (topological sort). Return [] if impossible. |
| 261 | ★ | Graph Valid Tree | O((V+E)) / O(V) | Determine if n nodes and given edges form a valid undirected tree. |
| 269 | ★ | Alien Dictionary | O(V+E) / O(V+E) | Given a sorted list of alien words, determine the order of characters in the alien alphabet. Return the order as a string, or empty string if invalid. |
| 277 | ★ | Find the Celebrity |  | Find the celebrity in a group of n people: everyone knows them, they know nobody. |
| 286 | ★ | Walls and Gates | O(mn) / O(mn) | Walls and Gates: fill each empty room (INF) with its distance to the nearest gate (0). |
| 296 | ★ | Best Meeting Point |  | Find the point minimizing total Manhattan distance to a set of buildings on a grid. |
| 305 | ★ | Number of Islands II |  | Count islands after each cell is added (online algorithm). |
| 310 | ★ | Minimum Height Trees | O(V+E) / O(V+E) | Find all minimum height trees in an undirected tree graph. |
| 317 | ★ | Shortest Distance from All Buildings |  | Find the empty land cell minimizing total walking distance to all buildings. |
| 323 | ★ | Number of Connected Components in an Undirected Graph | O((V+E)) / O(V) | Count connected components in an undirected graph. |
| 329 | ★ | Longest Increasing Path in a Matrix |  | Find the length of the longest increasing path in a matrix (4-directional movement). |
| 399 | ★ | Evaluate Division |  | Given equations and ratios, evaluate new queries (transitive division). |
| 407 | ★ | Trapping Rain Water II |  | Given a 2D height map, compute how much water it can trap after raining. |
| 417 | ★ | Pacific Atlantic Water Flow | O(mn) / O(mn) | Find all cells from which water can flow to both Pacific and Atlantic oceans (4-directional). |
| 463 | ★ | Island Perimeter |  | Calculate the perimeter of islands in a grid. |
| 529 | ★ | Minesweeper |  | Simulate the first click in Minesweeper: reveal cells per the game rules. |
| 542 | ★ | 01 Matrix |  | For each cell in a binary matrix, find the distance to the nearest 0. |
| 547 | ★ | Number of Provinces |  | Count the number of provinces (connected components) among n cities given friendship pairs. |
| 684 | ★ | #684 | O(E) / O(V) | Remove one redundant edge to make graph a tree. |
| 694 | ★ | Number of Distinct Islands |  | Count the number of distinct islands in a binary grid (by shape, not position). |
| 695 | ★ | Max Area of Island | O(mn) / O(mn) | Find the maximum area of any island in a binary grid. |
| 721 | ★ | #721 | O(n^2) / O(n) | Merge email accounts sharing a common email address. |
| 733 | ★ | Flood Fill |  | Flood-fill a pixel in an image: change all connected same-color pixels. |
| 743 | ★ | Network Delay Time | O((V+E) log V) / O(V+E) | Find the minimum time for a signal to reach all nodes in a network (Dijkstra). |
| 752 | ★ | Open the Lock |  | Find the minimum number of turns to open a 4-digit lock from '0000', avoiding dead-ends. |
| 778 | ★ | Swim in Rising Water |  | Find the minimum time to swim from top-left to bottom-right of a grid (elevation = wait time). |
| 785 | ★ | Is Graph Bipartite? |  | Check if an undirected graph can be 2-colored (bipartite). |
| 797 | ★ | All Paths From Source to Target |  | Find all paths from node 0 to node n-1 in a DAG. |
| 802 | ★ | Find Eventual Safe States |  | Find all safe nodes (nodes from which all paths lead to terminal nodes) in a DAG. |
| 815 | ★ | Bus Routes |  | Find the minimum number of buses to take to travel from source to target stop. |
| 827 | ★ | Making A Large Island | O(mn) / O(mn) | Connect two islands to maximize island size; return the maximum. |
| 847 | ★ | Shortest Path Visiting All Nodes |  | Find the shortest path visiting all nodes in an undirected graph. |
| 851 | ★ | Loud and Rich |  | Find the quietest person among those richer than each person. |
| 886 | ★ | Possible Bipartition |  | Check if people can be split into two groups with no one in the same group disliking each other. |
| 909 | ★ | Snakes and Ladders | O(n^2) / O(n^2) | Find the minimum number of dice rolls to reach the last square (snakes and ladders). |
| 913 | ★ | Cat and Mouse |  | A mouse (start node 1) and cat (start node 2) move on a graph; mouse wins by reaching node 0, cat wins by catching the mouse, else draw. Return 0/1/2 with optimal play. |
| 934 | ★ | Shortest Bridge |  | Find the shortest bridge between two islands in a binary matrix. |
| 994 | ★ | Rotting Oranges | O(mn) / O(mn) | Find the minimum time to rot all fresh oranges (multi-source BFS). |
| 1034 | ★ | Coloring A Border |  | Color cells on the border of an island (connected component) with a given color. |
| 1091 | ★ | Shortest Path in Binary Matrix | O(mn) / O(mn) | Find the shortest path from top-left to bottom-right in a binary matrix (8-directional). |
| 1102 | ★ | Path With Maximum Minimum Value |  | Find the path from top-left to bottom-right maximizing the minimum value on the path. |
| 1136 | ★ | Parallel Courses |  | Find the minimum number of months to complete all courses given prerequisites and durations. |
| 1162 | ★ | As Far from Land as Possible |  | In a grid of `0` (water) and `1` (land), find the water cell whose distance to the nearest land is maximized; return that distance, or -1. |
| 1197 | ★ | Minimum Knight Moves |  | Find the minimum knight moves from origin to a target on an infinite board. |
| 1202 | ★ | Smallest String With Swaps |  | Swap characters at given index pairs to get the lexicographically smallest string. |
| 1245 | ★ | Tree Diameter |  | Find the diameter of an N-ary tree (longest path between any two nodes). |
| 1293 | ★ | Shortest Path in a Grid with Obstacles Elimination |  | Find the shortest path from start to end in a grid, eliminating at most k obstacles. |
| 1319 | ★ | Number of Operations to Make Network Connected |  | Find the minimum number of additional connections to make a network fully connected. |
| 1514 | ★ | #1514 | O(E log V) / O(V+E) | Max probability path between two nodes. |
| 1559 | ★ | Detect Cycles in 2D Grid |  | Detect if a 2D grid contains a cycle of the same character. |
| 1631 | ★ | Path With Minimum Effort | O(mn log mn) / O(mn) | Find the path from top-left to bottom-right minimizing the maximum absolute difference. |
| 1743 | ★ | Restore the Array From Adjacent Pairs |  | Restore the original array from a list of all adjacent pairs. |

## Greedy  (28 problems, 28 templated)

| # | ★ | Name | Complexity | Description |
|---|---|---|---|---|
| 45 | ★ | Jump Game II | O(n) / O(1) | Find the minimum number of jumps to reach the last index. Each element is max jump length. |
| 55 | ★ | Jump Game | O(n) / O(1) | Given array of jump lengths, determine if you can reach the last index from index 0. |
| 56 | ★ | Merge Intervals | O(n log n) / O(n) | Merge all overlapping intervals in a collection and return non-overlapping sorted intervals. |
| 57 | ★ | Insert Interval | O(n) / O(n) | Insert a new interval into a sorted non-overlapping list of intervals, merging if necessary. |
| 134 | ★ | Gas Station | O(n) / O(1) | Find the starting gas station index from which you can complete a circular route. Return -1 if impossible. |
| 135 | ★ | Candy |  | Assign minimum candies to children in a line: each child 1 candy; child with higher rating than neighbor gets more. |
| 252 | ★ | Meeting Rooms | O(n log n) / O(1) | Determine if a person can attend all meetings (no overlapping intervals). |
| 253 | ★ | Meeting Rooms II | O(n log n) / O(n) | Find the minimum number of conference rooms required to hold all meetings. |
| 274 | ★ | H-Index |  | Given citation counts, find the largest h such that h papers have citations each. |
| 358 | ★ | Rearrange String k Distance Apart | O(n log k) / O(k) | Rearrange a string so that the same characters are at least `k` distance apart. Return "" if impossible. |
| 406 | ★ | Queue Reconstruction by Height |  | Reconstruct a queue of people given (height, k) pairs where k = taller-or-equal people in front. |
| 435 | ★ | Non-overlapping Intervals | O(n log n) / O(1) | Find the minimum number of intervals to remove so the rest don't overlap. |
| 452 | ★ | Minimum Number of Arrows to Burst Balloons |  | Find the minimum number of arrows to burst all balloons (each arrow goes through all balloons at that x). |
| 455 | ★ | Assign Cookies |  | Assign cookies greedily: each child needs minimum size, each cookie satisfies one child. |
| 575 | ★ | Distribute Candies |  | Distribute n candies (n/2 to eat) maximizing the number of distinct types. |
| 605 | ★ | Can Place Flowers |  | Determine if n flowers can be planted in a flowerbed without adjacent flowers. |
| 621 | ★ | Task Scheduler | O(n) / O(1) | Find the minimum intervals needed to execute n tasks with cooldown k between same-type tasks. |
| 630 | ★ | Course Schedule III |  | Find the maximum courses you can take given (duration, deadline) pairs. |
| 646 | ★ | Maximum Length of Pair Chain |  | Find the longest chain of pairs [a,b] where b < next_a. |
| 763 | ★ | Partition Labels |  | Partition a string into as many parts as possible so each letter appears in at most one part. |
| 881 | ★ | Boats to Save People |  | Find the minimum number of boats to rescue people given weight limit 2 per boat. |
| 986 | ★ | Interval List Intersections |  | Find all intersections of two lists of intervals. |
| 1005 | ★ | Maximize Sum Of Array After K Negations |  | Given an array and `k`, perform exactly `k` operations, each negating one element (the same index may be chosen repeatedly), to maximize the array sum. |
| 1094 | ★ | Car Pooling |  | Determine if a car pool trip is feasible given passenger pick-up and drop-off locations. |
| 1272 | ★ | Remove Interval |  | Given a sorted list of disjoint intervals and an interval `toBeRemoved`, return the set of intervals after removing every point that lies inside `toBeRemoved`. |
| 1326 | ★ | Minimum Number of Taps to Open to Water a Garden |  | Find the minimum number of taps to open to water the entire garden. |
| 1353 | ★ | Maximum Number of Events That Can Be Attended |  | Find the maximum number of events you can attend (one per day). |
| 1488 | ★ | Avoid Flood in The City |  | Schedule drying days to prevent flooding given a list of rains. |

## Dynamic Programming  (86 problems, 86 templated)

| # | ★ | Name | Complexity | Description |
|---|---|---|---|---|
| 5 | ★ | Longest Palindromic Substring | O(n^2) / O(1) | Find the longest palindromic substring within a given string. |
| 10 | ★ | Regular Expression Matching | O(mn) / O(mn) | Implement regular expression matching with '.' (any single char) and '*' (zero or more of preceding). Must match entire string. |
| 44 | ★ | Wildcard Matching |  | Match a string against a pattern with '?' (any single char) and '*' (any sequence including empty). |
| 53 | ★ | Maximum Subarray |  | Find the contiguous subarray with the largest sum (at least one element). |
| 62 | ★ | Unique Paths | O(mn) / O(n) | Count distinct paths from the top-left to the bottom-right of an m×n grid (only right or down moves). |
| 63 | ★ | Unique Paths II | O(mn) / O(n) | Count distinct paths in an m×n grid with obstacles (0=open, 1=obstacle). |
| 64 | ★ | Minimum Path Sum | O(mn) / O(1) | Find the path from top-left to bottom-right of a grid with minimum sum. |
| 70 | ★ | Climbing Stairs | O(n) / O(1) | Count the number of ways to climb n stairs, taking 1 or 2 steps at a time. |
| 72 | ★ | Edit Distance | O(mn) / O(mn) | Find the minimum number of edit operations (insert/delete/replace) to convert word1 to word2. |
| 87 | ★ | #87 | O(n³) / O(n^2) | Is s2 a scramble of s1 (recursive splits)? |
| 91 | ★ | Decode Ways | O(n) / O(1) | Count the number of ways to decode a string of digits into letters (A=1 … Z=26). |
| 96 | ★ | Unique Binary Search Trees | O(n^2) / O(n) | Count the number of structurally unique BSTs with exactly n nodes. |
| 97 | ★ | Interleaving String |  | Determine if s3 is formed by interleaving s1 and s2. |
| 115 | ★ | Distinct Subsequences | O(mn) / O(mn) | Count distinct subsequences of s that equal t. |
| 120 | ★ | Triangle |  | Find the minimum path sum from top to bottom of a triangle, moving to adjacent numbers on the row below. |
| 121 | ★ | Best Time to Buy and Sell Stock | O(n) / O(1) | Given daily stock prices, find the maximum profit from one buy-sell transaction (buy before sell). |
| 122 | ★ | Best Time to Buy and Sell Stock II | O(n) / O(1) | Maximize profit by completing as many buy-sell transactions as desired (no simultaneous holdings). |
| 123 | ★ | Best Time to Buy and Sell Stock III | O(n) / O(1) | Maximize profit with at most two buy-sell transactions (no simultaneous holdings). |
| 131 | ★ | Palindrome Partitioning | O(n2^n) / O(n) | Partition a string into all possible subsets where every substring is a palindrome. |
| 132 | ★ | Palindrome Partitioning II |  | Find the minimum number of cuts to partition a string so every part is a palindrome. |
| 139 | ★ | Word Break | O(n^2) / O(n) | Determine if a string can be segmented into space-separated words from a dictionary. |
| 140 | ★ | Word Break II |  | Return all ways to segment a string into space-separated words from a dictionary. |
| 152 | ★ | Maximum Product Subarray |  | Find the contiguous subarray with the largest product. |
| 174 | ★ | Dungeon Game |  | Find the minimum initial health to traverse a dungeon grid from top-left to bottom-right. |
| 188 | ★ | Best Time to Buy and Sell Stock IV |  | Maximize stock profit with at most k buy-sell transactions. |
| 198 | ★ | House Robber | O(n) / O(1) | Maximize the amount stolen from houses in a row; cannot rob two adjacent houses. |
| 213 | ★ | House Robber II | O(n) / O(1) | Maximize robbery from a circular row of houses (first and last are adjacent). |
| 221 | ★ | Maximal Square | O(mn) / O(mn) | Find the largest square containing only 1s in a binary matrix. Return its area. |
| 264 | ★ | Ugly Number II |  | Find the nth ugly number (positive number whose prime factors are only 2, 3, 5). |
| 279 | ★ | Perfect Squares | O(n√n) / O(n) | Find the minimum number of perfect squares summing to n. |
| 300 | ★ | Longest Increasing Subsequence | O(n^2) / O(n) | Find the length of the longest strictly increasing subsequence. |
| 309 | ★ | Best Time to Buy and Sell Stock with Cooldown | O(n) / O(1) | Find the maximum profit from stock with a 1-day cooldown after selling. |
| 312 | ★ | Burst Balloons | O(n³) / O(n^2) | Burst all balloons to maximize collected coins. Coins = left * burst * right. |
| 313 | ★ | Super Ugly Number |  | Find the nth super ugly number (prime factors only from a given list). |
| 322 | ★ | Coin Change | O(amount) / O(amount) | Find the minimum number of coins to make a given amount (coins can be reused). |
| 337 | ★ | House Robber III |  | Find the maximum amount you can rob from a binary tree of houses (no two adjacent nodes). |
| 343 | ★ | Integer Break |  | Break n into at least two positive integers to maximize their product. |
| 368 | ★ | Largest Divisible Subset | O(n^2) / O(n) | Find the largest subset where every pair has the larger divisible by the smaller. |
| 375 | ★ | Guess Number Higher or Lower II |  | Find the minimum cost to guarantee finding a number in range [1,n] using a guessing game. |
| 376 | ★ | Wiggle Subsequence |  | Find the length of the longest wiggle subsequence (alternating up-down differences). |
| 377 | ★ | Combination Sum IV | O(target) / O(target) | Count the number of possible combinations that add up to a target (order matters). |
| 413 | ★ | Arithmetic Slices |  | Count the number of arithmetic slices (subarrays of length 3 with equal differences). |
| 416 | ★ | Partition Equal Subset Sum | O(n) / O(sum) | Determine if an integer array can be partitioned into two subsets with equal sum. |
| 446 | ★ | Arithmetic Slices II - Subsequence |  | Count the number of arithmetic slices that are subsequences of an array. |
| 474 | ★ | #474 | O(l) / O(mn) | Max strings from list fitting within m zeros and n ones. |
| 486 | ★ | Predict the Winner |  | Two players alternately pick from either end of an array; determine if the first player wins. |
| 494 | ★ | Target Sum | O(n) / O(sum) | Count the number of ways to assign + or - to array elements to reach a target sum. |
| 509 | ★ | Fibonacci Number |  | Compute the nth Fibonacci number. |
| 516 | ★ | Longest Palindromic Subsequence | O(n^2) / O(n^2) | Find the length of the longest palindromic subsequence in a string. |
| 518 | ★ | Coin Change 2 | O(amount) / O(amount) | Count the number of combinations of coins that sum to an amount (coins may be reused). |
| 552 | ★ | Student Attendance Record II |  | Count valid attendance records of length n (at most 1 absence, never 3+ consecutive lates). |
| 576 | ★ | Out of Boundary Paths |  | Count paths from a given cell that leave an m×n grid in exactly maxMove steps. |
| 583 | ★ | Delete Operation for Two Strings | O(mn) / O(mn) | Find the minimum number of deletions to make two strings equal. |
| 600 | ★ | Non-negative Integers without Consecutive Ones |  | Count integers in `[0, n]` whose binary representation has no two adjacent 1 bits. |
| 629 | ★ | K Inverse Pairs Array |  | Count permutations of 1..n with exactly k inverse pairs. |
| 638 | ★ | Shopping Offers |  | Minimize the cost to purchase items given special-offer bundles. |
| 639 | ★ | Decode Ways II |  | Count decodings of a digit string where `*` is a wildcard for digits 1-9, modulo 1e9+7. |
| 647 | ★ | Palindromic Substrings | O(n^2) / O(1) | Count all substrings of a string that are palindromes. |
| 650 | ★ | 2 Keys Keyboard |  | Find minimum steps to get exactly n 'A's on a screen using only Copy All and Paste. |
| 673 | ★ | Number of Longest Increasing Subsequence |  | Find the number of longest increasing subsequences. |
| 674 | ★ | Longest Continuous Increasing Subsequence |  | Find the length of the longest continuous (contiguous) strictly increasing subarray. |
| 688 | ★ | Knight Probability in Chessboard |  | Find the probability that a knight stays on an n×n board after exactly k moves. |
| 714 | ★ | Best Time to Buy and Sell Stock with Transaction Fee | O(n) / O(1) | Find the maximum profit from unlimited transactions with a transaction fee per trade. |
| 718 | ★ | Maximum Length of Repeated Subarray |  | Find the maximum length of a subarray that appears in both arrays. |
| 740 | ★ | Delete and Earn |  | Delete and earn: delete nums[i] to earn nums[i] points, but must delete all adjacent values. |
| 746 | ★ | Min Cost Climbing Stairs | O(n) / O(1) | Find the minimum cost to climb a staircase (pay to step on, can skip one). |
| 787 | ★ | Cheapest Flights Within K Stops | O(E log E) / O(V+E) | Find the cheapest flight from src to dst with at most k stops. |
| 873 | ★ | Length of Longest Fibonacci Subsequence |  | Find the length of the longest Fibonacci-like subsequence in a sorted array. |
| 887 | ★ | Super Egg Drop |  | Find the minimum number of moves to determine the critical floor for egg drops. |
| 918 | ★ | Maximum Sum Circular Subarray |  | Find the maximum subarray sum where the array is circular (subarray may wrap around). |
| 931 | ★ | #931 | O(mn) / O(1) | Min sum of a falling path through an n×n matrix. |
| 935 | ★ | Knight Dialer |  | Count distinct phone numbers of length n that a knight can dial. |
| 983 | ★ | Minimum Cost For Tickets |  | Find the minimum cost to cover all travel days using 1-, 7-, or 30-day passes. |
| 1027 | ★ | Longest Arithmetic Subsequence |  | Find the length of the longest arithmetic subsequence in an array. |
| 1048 | ★ | Longest String Chain |  | Find the longest string chain where each word is a predecessor of the next. |
| 1049 | ★ | #1049 | O(n) / O(sum) | Smallest possible weight of last remaining stone. |
| 1137 | ★ | N-th Tribonacci Number |  | Return the nth Tribonacci number (each term is the sum of the previous three). |
| 1143 | ★ | Longest Common Subsequence | O(mn) / O(mn) | Find the length of the longest common subsequence of two strings. |
| 1216 | ★ | Valid Palindrome III |  | Check if a string is a k-palindrome (palindrome after removing at most k chars). |
| 1218 | ★ | Longest Arithmetic Subsequence of Given Difference |  | Find the longest arithmetic subsequence with a given difference. |
| 1269 | ★ | Number of Ways to Stay in the Same Place After Some Steps |  | Count the number of ways to stay at position 0 after exactly n steps on an array of length arrLen. |
| 1312 | ★ | #1312 | O(n^2) / O(n^2) | Min insertions to make string a palindrome. |
| 1395 | ★ | Count Number of Teams |  | Count triplets `(i, j, k)` with `i < j < k` whose ratings are strictly increasing or strictly decreasing. |
| 1567 | ★ | Maximum Length of Subarray With Positive Product |  | Find the maximum length subarray with a positive product. |
| 1696 | ★ | Jump Game VI |  | Find the maximum score reaching the last index, jumping 1 to k steps. |
| 1884 | ★ | Egg Drop With 2 Eggs and N Floors |  | Find minimum moves to determine a critical floor using 2 eggs and n floors. |

## Trie  (8 problems, 8 templated)

| # | ★ | Name | Complexity | Description |
|---|---|---|---|---|
| 208 | ★ | Implement Trie (Prefix Tree) | O(L) / O(n) | Implement a Trie with insert, search, and startsWith operations. |
| 211 | ★ | Design Add and Search Words Data Structure | O(L) / O(n) | Design a data structure supporting addWord and search (with '.' wildcard) for words. |
| 212 | ★ | Word Search II | O(mn4\^L) / O(L) | Find all words from a dictionary that exist in an m×n character board (adjacent cells, no reuse). |
| 336 | ★ | Palindrome Pairs |  | Find all palindrome pairs among a list of unique words. |
| 648 | ★ | Replace Words |  | Given a sentence and a list of roots, replace each word with its root if one exists. |
| 676 | ★ | Implement Magic Dictionary |  | Design a data structure with addWord and search supporting '.' wildcard. |
| 720 | ★ | Longest Word in Dictionary |  | Find the longest word in a dictionary that can be built one character at a time. |
| 1233 | ★ | Remove Sub-Folders from the Filesystem |  | Given a list of folder paths, remove all sub-folders so only top-level folders remain. `"/a/b"` is a sub-folder of `"/a"`. |

## Bit Manipulation  (16 problems, 16 templated)

| # | ★ | Name | Complexity | Description |
|---|---|---|---|---|
| 136 | ★ | Single Number | O(n) / O(1) | Find the single element in an array where every other element appears exactly twice. |
| 137 | ★ | Single Number II |  | Find the single element in an array where every other element appears exactly three times. |
| 190 | ★ | Reverse Bits |  | Reverse all bits of a 32-bit unsigned integer. |
| 191 | ★ | Number of 1 Bits | O(1) / O(1) | Count the number of '1' bits in a 32-bit integer (Hamming weight). |
| 201 | ★ | #201 | O(log n) / O(1) | Bitwise AND of all numbers in range [left, right]. |
| 231 | ★ | Power of Two | O(1) / O(1) | Determine if a number is a power of two. |
| 260 | ★ | Single Number III | O(n) / O(1) | Find two non-repeating numbers in an array where all others appear twice. |
| 268 | ★ | Missing Number | O(n) / O(1) | Find the single missing number in an array of n distinct integers in range [0, n]. |
| 318 | ★ | Maximum Product of Word Lengths |  | Find the maximum product of lengths of two words with no common letters. |
| 338 | ★ | Counting Bits | O(n) / O(n) | Return an array counting the number of 1 bits for each integer from 0 to n. |
| 342 | ★ | Power of Four | O(1) / O(1) | Determine if a number is a power of four. |
| 371 | ★ | Sum of Two Integers |  | Add two integers without using + or - operators. |
| 405 | ★ | Convert a Number to Hexadecimal |  | Given an integer `num`, return its hexadecimal representation as a lowercase string. For negative numbers use two's complement. |
| 461 | ★ | Hamming Distance |  | Calculate Hamming distance between two integers (positions where bits differ). |
| 476 | ★ | Number Complement |  | Find the complement of an integer (flip all bits up to the most significant bit). |
| 957 | ★ | Prison Cells After N Days |  | Find the prison cell configuration after n days of simultaneous updates. |

## Design  (25 problems, 25 templated)

| # | ★ | Name | Complexity | Description |
|---|---|---|---|---|
| 146 | ★ | LRU Cache | O(1) / O(capacity) | Design an LRU (Least Recently Used) Cache with O(1) get and put operations. |
| 170 | ★ | Two Sum III - Data structure design |  | Design a Two Sum data structure with add() and find() operations. |
| 173 | ★ | Binary Search Tree Iterator |  | Implement a Binary Search Tree iterator with hasNext() and next() using O(h) memory. |
| 244 | ★ | Shortest Word Distance II |  | Design data structure for finding shortest word distance between two words in a list, supporting repeated queries. |
| 245 | ★ | Shortest Word Distance III |  | Given a word list and two words (which may be equal), return the shortest index distance. When `word1 == word2`, find the closest pair of distinct occurrences of that word. |
| 251 | ★ | Flatten 2D Vector |  | Design an iterator over a 2D vector with `next()` and `hasNext()` that yields all elements in row-major order. |
| 281 | ★ | Zigzag Iterator |  | Given two lists, design an iterator that returns elements alternating between them; when one is exhausted, continue with the other. |
| 341 | ★ | Flatten Nested List Iterator |  | Implement an iterator that flattens a nested list of integers. |
| 346 | ★ | Moving Average from Data Stream |  | Compute the moving average from a stream of integers given a window size. |
| 348 | ★ | Design Tic-Tac-Toe |  | Design a Tic-Tac-Toe game that detects a winner in O(1) per move. |
| 380 | ★ | Insert Delete GetRandom O(1) |  | Design a set with O(1) insert, remove, and random element retrieval. |
| 381 | ★ | Insert Delete GetRandom O(1) - Duplicates allowed |  | Same as 380 but allows duplicates. |
| 460 | ★ | LFU Cache | O(1) / O(capacity) | Design an LFU (Least Frequently Used) Cache with O(1) get and put. |
| 519 | ★ | Random Flip Matrix |  | Design a matrix with random flip and reset; each 0-cell can be flipped to 1 exactly once. |
| 622 | ★ | Design Circular Queue |  | Design a circular queue (ring buffer) with fixed capacity. |
| 641 | ★ | Design Circular Deque |  | Design a double-ended circular queue with maxSize capacity. |
| 705 | ★ | Design HashSet |  | Design a HashSet with add, remove, and contains operations. |
| 706 | ★ | Design HashMap |  | Design a HashMap with put, get, and remove operations. |
| 707 | ★ | Design Linked List |  | Design a doubly linked list with index-based get, addAtHead, addAtTail, addAtIndex, deleteAtIndex. |
| 729 | ★ | 我的日程安排表 I |  | Book time intervals on a calendar; return false if overlap exists. |
| 731 | ★ | 我的日程安排表 II |  | Book events; return number of existing bookings overlapping the new booking. |
| 732 | ★ | My Calendar III |  | Book events; return the maximum k-booking (k events overlap at same time). |
| 745 | ★ | #745 | O(L) / O(n) | Prefix and suffix search --- find word with given prefix and suffix. |
| 933 | ★ | Number of Recent Calls |  | Find the number of requests made in the last 3000 milliseconds. |
| 1570 | ★ | Dot Product of Two Sparse Vectors |  | Compute the dot product of two sparse vectors efficiently. |

## Math  (57 problems, 57 templated)

| # | ★ | Name | Complexity | Description |
|---|---|---|---|---|
| 9 | ★ | Palindrome Number | O(log n) / O(1) | Determine whether an integer reads the same forward and backward. Negative numbers are never palindromes. |
| 29 | ★ | Divide Two Integers |  | Divide two integers without using multiplication, division, or mod. Clamp to 32-bit signed range. |
| 50 | ★ | Pow(x, n) | O(log n) / O(1) | Implement pow(x, n) --- raise x to the power n (n can be negative). |
| 59 | ★ | Spiral Matrix II |  | Given `n`, generate an `n x n` matrix filled with the numbers `1` to `n*n` in spiral order. |
| 66 | ★ | Plus One |  | Increment a large integer represented as an array of digits. |
| 118 | ★ | Pascal's Triangle |  | Generate Pascal's triangle up to numRows rows. |
| 119 | ★ | Pascal's Triangle II |  | Return the kth row of Pascal's triangle using O(k) space. |
| 149 | ★ | Max Points on a Line |  | Find the maximum number of points that lie on the same straight line. |
| 172 | ★ | Factorial Trailing Zeroes |  | Count trailing zeroes in n! (count factors of 5). |
| 202 | ★ | Happy Number |  | Determine if a number eventually reaches 1 by repeatedly replacing it with the sum of squares of its digits. |
| 204 | ★ | Count Primes | O(n log log n) / O(n) | Count prime numbers less than a non-negative integer n. |
| 223 | ★ | Rectangle Area |  | Given the coordinates of two axis-aligned rectangles, return the total area they cover (counting the overlap once). |
| 233 | ★ | Number of Digit One |  | Count total occurrences of digit 1 in all integers from 1 to n. |
| 243 | ★ | Shortest Word Distance |  | Given an array of words and two distinct words, return the shortest distance (in indices) between any occurrence of the two words. |
| 258 | ★ | Add Digits |  | Repeatedly sum digits until a single digit remains (digital root). |
| 263 | ★ | Ugly Number |  | Check if a number is an ugly number (prime factors only 2, 3, 5). |
| 292 | ★ | Nim Game |  | In Nim game, you and opponent alternate removing 1--3 stones; player who takes last stone wins. Can you win? |
| 319 | ★ | Bulb Switcher |  | n bulbs toggled by n rounds (round i toggles every ith bulb). Count bulbs on after all rounds. |
| 326 | ★ | Power of Three |  | Check if a number is a power of three. |
| 357 | ★ | Count Numbers with Unique Digits |  | Given `n`, count all numbers `x` with `0 <= x < 10^n` that have no repeated digits. |
| 365 | ★ | Water and Jug Problem |  | Given two jugs of capacities `x` and `y` and a target `target`, determine if you can measure exactly `target` liters using fill/empty/pour operations. |
| 367 | ★ | Valid Perfect Square |  | Given a positive integer `num`, return whether it is a perfect square, without using any built-in sqrt function. |
| 372 | ★ | Super Pow | O(log n) / O(1) | Compute `a^b mod 1337` where `b` is given as an array of digits (so `b` may be astronomically large). |
| 397 | ★ | Integer Replacement |  | Find the minimum steps to reduce a number to 1 (even: n/2, odd: n+1 or n-1). |
| 398 | ★ | Random Pick Index |  | Pick a random index from those matching a target value (unknown total size). |
| 400 | ★ | Nth Digit |  | Given `n`, return the `n`-th digit in the infinite sequence of concatenated positive integers `123456789101112...`. |
| 412 | ★ | Fizz Buzz |  | Print numbers 1--n, replacing multiples of 3 with 'Fizz', 5 with 'Buzz', both with 'FizzBuzz'. |
| 441 | ★ | Arranging Coins |  | You have `n` coins to form a staircase where the `k`-th row has exactly `k` coins; return the number of complete rows. |
| 453 | ★ | Minimum Moves to Equal Array Elements |  | In one move you increment `n-1` elements of the array by 1; return the minimum moves to make all elements equal. |
| 458 | ★ | Poor Pigs |  | With `buckets` buckets one of which is poisoned, `minutesToDie` for poison to act, and `minutesToTest` total time, return the minimum pigs needed to find the poisoned bucket. |
| 470 | ★ | Implement Rand10() Using Rand7() |  | Implement rand10() using only rand7(). |
| 492 | ★ | Construct the Rectangle |  | Given a target `area`, return the dimensions `[L, W]` with `L >= W`, `L * W == area`, and `L - W` minimized. |
| 495 | ★ | Teemo Attacking |  | Given sorted attack `timeSeries` and a poison `duration`, return the total time the target is poisoned (overlaps counted once). |
| 528 | ★ | Random Pick with Weight |  | Randomly pick an index proportional to its weight. |
| 593 | ★ | Valid Square |  | Given four points, return whether they form a valid square (positive area). |
| 598 | ★ | Range Addition II |  | Count cells in the intersection of all rectangles defined by range addition operations. |
| 633 | ★ | Sum of Square Numbers |  | Given a non-negative integer `c`, decide whether there exist non-negative integers `a, b` with `a*a + b*b == c`. |
| 656 | ★ | Coin Path |  | Given `coins` (cost per index, `-1` blocked) and a max jump `maxJump`, find the lexicographically smallest cheapest path of indices from index 0 to the last. |
| 781 | ★ | Rabbits in Forest |  | Each surveyed rabbit reports how many other rabbits share its color; given the `answers`, return the minimum number of rabbits in the forest. |
| 789 | ★ | Escape The Ghosts |  | Starting at the origin with a `target`, and given `ghosts` positions, you all move simultaneously in Manhattan steps; return whether you can reach the target before any ghost catches you. |
| 792 | ★ | Number of Matching Subsequences |  | Given a string `s` and an array of `words`, return how many words are subsequences of `s`. |
| 829 | ★ | Consecutive Numbers Sum |  | Find the number of ways to write n as a sum of consecutive positive integers. |
| 836 | ★ | Rectangle Overlap |  | Check if two axis-aligned rectangles overlap. |
| 858 | ★ | Mirror Reflection |  | Given clock hands at h:m, find the minimum angle between them. |
| 869 | ★ | Reordered Power of 2 |  | Check if any permutation of n's digits is a power of 2. |
| 939 | ★ | Minimum Area Rectangle |  | Find the minimum area rectangle from a set of points in an axis-aligned grid. |
| 963 | ★ | Minimum Area Rectangle II |  | Find the minimum area rectangle aligned to any angle from a set of points. |
| 1041 | ★ | Robot Bounded In Circle |  | Determine if a robot following instructions stays within a bounded circle. |
| 1160 | ★ | Find Words That Can Be Formed by Characters |  | Given `words` and a string `chars`, return the total length of words that can be formed using letters of `chars` (each letter used at most as often as it appears). |
| 1201 | ★ | Ugly Number III | O(log(min)) / O(1) | Find the nth positive integer that is divisible by at least one of `a`, `b`, or `c`. |
| 1304 | ★ | Find N Unique Integers Sum up to Zero |  | Find n unique integers that sum to zero. |
| 1344 | ★ | Angle Between Hands of a Clock |  | Calculate the angle between clock hands at a given time. |
| 1583 | ★ | Count Unhappy Friends |  | Count the number of unhappy friends after pairing. |
| 1588 | ★ | Sum of All Odd Length Subarrays |  | Compute the sum of all odd-length subarray sums. |
| 1646 | ★ | Get Maximum in Generated Array |  | Generate an array from a given sequence and return the max element. |
| 1823 | ★ | Find the Winner of the Circular Game |  | `n` friends in a circle eliminate every `k`-th friend repeatedly; return the 1-indexed winner (Josephus problem). |
| 1969 | ★ | Minimum Non-Zero Product of the Array Elements |  | Find the minimum non-zero product of array elements after swaps. |

## Concurrency (no dedicated template)  (2 problems, 0 templated)

| # | ★ | Name | Complexity | Description |
|---|---|---|---|---|
| 1114 |  | Print in Order |  |  |
| 1115 |  | Print FooBar Alternately |  |  |

---

*Total: 737 problems indexed across 15 categories.*
