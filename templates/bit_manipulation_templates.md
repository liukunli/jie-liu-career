# Bit Manipulation Templates

---

## Quick Reference Table

| # | Name | Description | Algorithm | Variation from Template | Time | Space |
|---|---|---|---|---|---|---|
| 136 | Single Number | One element appears once; rest appear twice | XOR all — pairs cancel | **Standard** | O(n) | O(1) |
| 137 | Single Number II | One element appears once; rest appear three times | XOR state machine with `ones`, `twos` | **mod 3**: two-state machine instead of simple XOR | O(n) | O(1) |
| 260 | Single Number III | Two unique elements; rest appear twice | XOR → split by lowest-diff bit | **Split**: use `xor & (-xor)` to separate into two groups | O(n) | O(1) |
| 191 | Number of 1 Bits | Count set bits in n | Brian Kernighan: `n &= (n-1)` loop | **Standard bit clear** | O(k) k=set bits | O(1) |
| 338 | Counting Bits | Return number of 1 bits for every i in 0..n | DP: `dp[i] = dp[i >> 1] + (i & 1)` | **DP relation**: right-shift halves the number | O(n) | O(n) |
| 268 | Missing Number | Missing number in [0, n] | XOR indices with values | **Index XOR**: XOR i with nums[i] instead of just nums | O(n) | O(1) |
| 190 | Reverse Bits | Reverse all 32 bits of an integer | Shift-and-OR loop 32 times | **Fixed 32 iterations** instead of until zero | O(32) | O(1) |
| 201 | Bitwise AND of Numbers Range | AND of all numbers in [left, right] | Right-shift both until equal; shift back | **Common prefix**: find shared high bits | O(log n) | O(1) |
| 371 | Sum of Two Integers | Add without `+` or `-` | XOR = sum without carry; AND << 1 = carry | **Carry loop**: separate sum and carry bits | O(32) | O(1) |
| 318 | Max Product of Word Lengths | Max product of word lengths with no shared letters | Precompute 26-bit mask per word; check `mask[i] & mask[j] == 0` | **Bitmask as set**: 26 bits represent letter presence | O(n²) | O(n) |
| 231 | Power of Two | Check if n is a power of two | n > 0 && (n & (n-1)) == 0 | **Single bit check**: power of 2 has exactly one set bit | O(1) | O(1) |
| 287 | Find the Duplicate Number | Find duplicate in nums[1..n] with n+1 elements; no extra space | Floyd's cycle detection: treat array as linked list, nums[i] → next node | **Floyd's cycle**: not XOR; use slow/fast pointer cycle detection | O(n) | O(1) |
| 342 | Power of Four | Check if n is a power of four | Power of 2 AND the single set bit is at an even position (0,2,4,...) | **Even bit position**: check (n & 0xAAAAAAAA) == 0 after power-of-2 check | O(1) | O(1) |

---

## Canonical Template

```java
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
int count = 0;
while (n != 0) { count++; n &= (n - 1); }  // n & (n-1) clears lowest set bit

// ── BITMASK AS SET ── 26-bit integer represents presence of 26 letters
int mask = 0;
for (char c : word.toCharArray()) mask |= (1 << (c - 'a'));
// check no overlap between two words:
if ((mask[i] & mask[j]) == 0) { /* no shared letter */ }
```

---

## Variations

```java
// VARIATION 1: mod-3 state machine (Single Number II)
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

# Part 1 — XOR Cancel

## #136 Single Number

**Description:** Array where every element appears twice except one. Find it.  
**Algorithm:** XOR all — every pair cancels (`a ^ a = 0`), leaving the single element.

```java
class Solution {
    public int singleNumber(int[] nums) {
        int result = 0;
        for (int num : nums) result ^= num;   // pairs cancel; lone element survives
        return result;
    }
}
```
**Time** O(n) | **Space** O(1)

---

## #268 Missing Number

**Description:** Array of n distinct numbers from [0, n] with one missing. Find it.  
**Variation:** XOR each index `i` with `nums[i]`. Indices 0..n XOR'd with the n elements — the missing index has no pair.

```java
class Solution {
    public int missingNumber(int[] nums) {
        int result = nums.length;                             // start with n (last index)
        for (int i = 0; i < nums.length; i++)
            result ^= i ^ nums[i];                           // ← VARIATION: XOR index with value
        return result;
    }
}
```
**Time** O(n) | **Space** O(1)

---

## #137 Single Number II

**Description:** Every element appears three times except one. Find it.  
**Variation:** Two-state XOR machine. `ones` tracks bits seen 1 mod 3 times, `twos` tracks bits seen 2 mod 3 times. When a bit reaches 3, it clears from both.

```java
class Solution {
    public int singleNumber(int[] nums) {
        int ones = 0, twos = 0;
        for (int num : nums) {
            ones = (ones ^ num) & ~twos;    // ← VARIATION: add to ones only if not in twos
            twos = (twos ^ num) & ~ones;    // ← VARIATION: add to twos only if not in ones
        }
        return ones;                         // ones holds the element seen exactly once
    }
}
```
**Time** O(n) | **Space** O(1)

---

## #260 Single Number III

**Description:** Two elements appear exactly once; all others appear twice. Find both.  
**Variation:** XOR all → get `a ^ b`. Use lowest set bit of `a ^ b` to partition nums into two groups (one containing `a`, one containing `b`). XOR each group independently.

```java
class Solution {
    public int[] singleNumber(int[] nums) {
        int xor = 0;
        for (int num : nums) xor ^= num;       // xor = a ^ b

        int diff = xor & (-xor);               // ← VARIATION: isolate lowest bit that differs
        int a = 0;
        for (int num : nums)
            if ((num & diff) != 0) a ^= num;   // ← VARIATION: XOR only one group
        return new int[]{a, xor ^ a};           // b = (a^b) ^ a
    }
}
```
**Time** O(n) | **Space** O(1)

---

# Part 2 — Bit Counting

## #191 Number of 1 Bits

**Description:** Return the number of set bits in an unsigned integer.  
**Algorithm:** Brian Kernighan — `n & (n-1)` clears the lowest set bit each iteration.

```java
public class Solution {
    public int hammingWeight(int n) {
        int count = 0;
        while (n != 0) {
            count++;
            n &= (n - 1);    // ← clears lowest set bit; loop runs exactly hamming-weight times
        }
        return count;
    }
}
```
**Time** O(k) k = number of set bits | **Space** O(1)

---

## #338 Counting Bits

**Description:** Return an array `result` where `result[i]` = number of 1 bits in `i`, for i in [0, n].  
**Variation:** DP relation — `i >> 1` is `i` with last bit removed (already computed), plus the last bit `i & 1`.

```java
class Solution {
    public int[] countBits(int n) {
        int[] dp = new int[n + 1];
        for (int i = 1; i <= n; i++)
            dp[i] = dp[i >> 1] + (i & 1);   // ← VARIATION: dp[i/2] + last bit
        return dp;
    }
}
```
**Time** O(n) | **Space** O(n)

---

## #190 Reverse Bits

**Description:** Reverse the 32 bits of an unsigned integer.  
**Variation:** Fixed 32 iterations — each time take the LSB of `n`, append it to `result`, then shift both.

```java
public class Solution {
    public int reverseBits(int n) {
        int result = 0;
        for (int i = 0; i < 32; i++) {      // ← VARIATION: always 32 iterations (fixed-width)
            result = (result << 1) | (n & 1); // append LSB of n to result
            n >>= 1;
        }
        return result;
    }
}
```
**Time** O(32) = O(1) | **Space** O(1)

---

# Part 3 — Range / Arithmetic

## #201 Bitwise AND of Numbers Range

**Description:** Return the AND of all numbers in `[left, right]`.  
**Key insight:** any two adjacent numbers in the range differ in at least the lowest bit. AND of a range clears all bits that differ across any pair in the range. The result is the common high-bit prefix of `left` and `right`.  
**Variation:** right-shift both until equal to find shared prefix; shift back.

```java
class Solution {
    public int rangeBitwiseAnd(int left, int right) {
        int shift = 0;
        while (left != right) {             // ← VARIATION: shift until common prefix found
            left  >>= 1;
            right >>= 1;
            shift++;
        }
        return left << shift;               // ← restore to original magnitude
    }
}
```
**Time** O(log n) | **Space** O(1)

---

## #371 Sum of Two Integers

**Description:** Return `a + b` without using `+` or `-`.  
**Variation:** XOR computes bit sum without carry; AND shifted left computes carry. Repeat until no carry.

```java
class Solution {
    public int getSum(int a, int b) {
        while (b != 0) {
            int carry = a & b;              // ← VARIATION: carry = bits where both are 1
            a = a ^ b;                      // ← VARIATION: partial sum (no carry propagation)
            b = carry << 1;                 // ← VARIATION: carry propagates one bit left
        }
        return a;
    }
}
```
**Time** O(32) = O(1) | **Space** O(1)

---

# Part 4 — Bitmask as Set

## #318 Maximum Product of Word Lengths

**Description:** Given a list of words, find the maximum product `len(a) * len(b)` where `a` and `b` share no common letters.  
**Variation:** encode each word as a 26-bit integer where bit `i` = 1 if letter `'a' + i` appears. Two words share a letter iff their bitmasks have any common bit (`mask[i] & mask[j] != 0`).

```java
class Solution {
    public int maxProduct(String[] words) {
        int n = words.length;
        int[] masks = new int[n];
        for (int i = 0; i < n; i++)
            for (char c : words[i].toCharArray())
                masks[i] |= (1 << (c - 'a'));    // ← VARIATION: 26-bit bitmask per word

        int max = 0;
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)
                if ((masks[i] & masks[j]) == 0)  // ← VARIATION: no shared letters = AND is zero
                    max = Math.max(max, words[i].length() * words[j].length());
        return max;
    }
}
```
**Time** O(n² + n·k) k = avg word length | **Space** O(n)

---

## Bit Trick Cheat Sheet

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
```

## Pattern Chooser

| Signal | Technique |
|---|---|
| "appears odd/once, rest appear even/twice" | XOR all |
| "appears once, rest appear 3 times" | mod-3 state machine (`ones`, `twos`) |
| "two unique elements" | XOR → split by `xor & (-xor)` |
| Count set bits | Brian Kernighan `n &= (n-1)` |
| Count bits for all 0..n | DP: `dp[i] = dp[i>>1] + (i&1)` |
| AND of a range | Right-shift to find common prefix |
| Add without `+` | XOR + carry loop |
| "no shared characters between two strings" | 26-bit bitmask, check AND == 0 |
| "is n a power of two?" | `n > 0 && (n & (n-1)) == 0` |
| "is n a power of four?" | Power of 2 AND set bit at even position: `(n & 0xAAAAAAAA) == 0` |
| "find duplicate, no extra space, no modification" | Floyd's cycle detection on array-as-linked-list |

---

# Part 5 — Power Checks & Cycle Detection

## #231 Power of Two

**Description:** Given an integer `n`, return true if it is a power of two.

**Algorithm:** A power of two has exactly one set bit. Check `n > 0` and `n & (n-1) == 0` (clearing the lowest set bit results in 0 only if there was one bit).

```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        return n > 0 && (n & (n - 1)) == 0;  // ← VARIATION: single-bit property of powers of 2
    }
}
```
**Time** O(1) | **Space** O(1)

---

## #342 Power of Four

**Description:** Given an integer `n`, return true if it is a power of four.

**Variation:** Power of four must be power of two (one set bit) AND that bit must be at an even bit position (0, 2, 4, 6, ...). Mask `0xAAAAAAAA` has bits set at ALL odd positions; if `n & 0xAAAAAAAA == 0`, the set bit is at an even position.

```java
class Solution {
    public boolean isPowerOfFour(int n) {
        // 0xAAAAAAAA = 1010 1010 ... 1010 (bits at odd positions 1,3,5,...31)
        return n > 0 && (n & (n-1)) == 0         // ← power of 2: exactly one set bit
                     && (n & 0xAAAAAAAA) == 0;   // ← VARIATION: set bit at even position (4^k has bit at position 2k)
    }
}
```
**Time** O(1) | **Space** O(1)

---

## #287 Find the Duplicate Number

**Description:** Given an array of `n+1` integers where each is in `[1, n]`, find the duplicate. No extra space, no modifying the array.

**Variation:** Floyd's Cycle Detection. Treat the array as a linked list where `nums[i]` is the next node. Since there's a duplicate, two indices point to the same value → creates a cycle. Find cycle entry = duplicate.

```java
class Solution {
    public int findDuplicate(int[] nums) {
        // Phase 1: find intersection point in cycle
        int slow = nums[0], fast = nums[0];
        do {
            slow = nums[slow];              // ← VARIATION: Floyd's cycle, not XOR
            fast = nums[nums[fast]];
        } while (slow != fast);
        // Phase 2: find cycle entry (= duplicate)
        slow = nums[0];
        while (slow != fast) {
            slow = nums[slow];
            fast = nums[fast];
        }
        return slow;
    }
}
```
**Time** O(n) | **Space** O(1)
