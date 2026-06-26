# Two Pointer Templates

Two patterns — pick based on whether pointers converge or march together.

## Quick Reference Table

| # | Name | Description | Pattern | i init | j init | Loop | Duplicates |
|---|---|---|---|---|---|---|---|
| 167 | Two Sum II | Two numbers in sorted array summing to target | Opposite | `0` | `n-1` | `i < j` | No |
| 15 | 3Sum | All unique triplets summing to 0 | Opposite + fix | `a+1` | `n-1` | `i < j` | Skip after hit |
| 18 | 4Sum | All unique quadruplets summing to target | Opposite + 2 fix | `b+1` | `n-1` | `i < j` | Skip after hit |
| 11 | Container With Most Water | Max water between two vertical lines | Opposite | `0` | `n-1` | `i < j` | No |
| 42 | Trapping Rain Water | Total trapped water between elevation bars | Opposite | `0` | `n-1` | `i < j` | No |
| 27 | Remove Element | Remove all val in-place, return new length | Same dir | `0` (write) | `0` (read) | `j < n` | No |
| 26 | Remove Duplicates | Each element appears at most once in-place | Same dir | `0` (write) | `0` (read) | `j < n` | Compare `nums[i-1]` |
| 80 | Remove Duplicates II | Each element appears at most twice in-place | Same dir | `0` (write) | `0` (read) | `j < n` | Compare `nums[i-2]` |
| 283 | Move Zeroes | Move zeroes to end, preserve relative order | Same dir | `0` (write) | `0` (read) | `j < n` | No |
| 75 | Sort Colors | Sort 0s, 1s, 2s in-place (Dutch Flag) | 3-pointer | `0` (low) | `n-1` (high) | `k <= j` | No |

---

## Pattern 1 — Opposite Two Pointers

```java
int i = 0, j = n - 1;
while (i < j) {
    if      (condition == target) { /* record */ i++; j--; }
    else if (tooSmall)            i++;
    else                          j--;
}
```

Sort first. `i` and `j` converge inward. Used when the array is sorted and you can eliminate half the search space each step.

---

## #167 Two Sum II

**Description:** Sorted array. Find two numbers summing to target. Return 1-based indices.  
**Key:** sum too small → move `i` right. sum too large → move `j` left.

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int i = 0, j = nums.length - 1;
        while (i < j) {
            int sum = nums[i] + nums[j];
            if      (sum == target) return new int[]{i + 1, j + 1};
            else if (sum < target)  i++;
            else                    j--;
        }
        return new int[]{-1, -1};
    }
}
```

---

## #15 3Sum

**Description:** Find all unique triplets summing to 0. No duplicate triplets in output.  
**Key:** sort first, fix `a`, run opposite two pointers on `[a+1, n-1]`. Skip duplicates at all three levels.

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();
        for (int a = 0; a < nums.length - 2; a++) {
            if (a > 0 && nums[a] == nums[a - 1]) continue;   // skip dup a
            int i = a + 1, j = nums.length - 1;
            while (i < j) {
                int sum = nums[a] + nums[i] + nums[j];
                if (sum == 0) {
                    res.add(Arrays.asList(nums[a], nums[i++], nums[j--]));
                    while (i < j && nums[i] == nums[i - 1]) i++;  // skip dup i
                    while (i < j && nums[j] == nums[j + 1]) j--;  // skip dup j
                } else if (sum < 0) i++;
                else                j--;
            }
        }
        return res;
    }
}
```

---

## #18 4Sum

**Description:** Find all unique quadruplets summing to target.  
**Key:** two nested fix loops + same opposite two pointer inner loop. Cast to `long` — sum of 4 ints can overflow.

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();
        int n = nums.length;
        for (int a = 0; a < n - 3; a++) {
            if (a > 0 && nums[a] == nums[a - 1]) continue;
            for (int b = a + 1; b < n - 2; b++) {
                if (b > a + 1 && nums[b] == nums[b - 1]) continue;
                int i = b + 1, j = n - 1;
                while (i < j) {
                    long sum = (long) nums[a] + nums[b] + nums[i] + nums[j];
                    if (sum == target) {
                        res.add(Arrays.asList(nums[a], nums[b], nums[i++], nums[j--]));
                        while (i < j && nums[i] == nums[i - 1]) i++;
                        while (i < j && nums[j] == nums[j + 1]) j--;
                    } else if (sum < target) i++;
                    else                     j--;
                }
            }
        }
        return res;
    }
}
```

---

## #11 Container With Most Water

**Description:** Given heights of vertical lines, find two lines forming the container with most water.  
**Key:** always move the shorter side inward — moving the taller side can only make things worse.

```java
class Solution {
    public int maxArea(int[] height) {
        int i = 0, j = height.length - 1, max = 0;
        while (i < j) {
            max = Math.max(max, Math.min(height[i], height[j]) * (j - i));
            if (height[i] < height[j]) i++;
            else                       j--;
        }
        return max;
    }
}
```

---

## #42 Trapping Rain Water

**Description:** Given elevation heights, compute total water trapped after rain.  
**Key:** water above position `x` = `min(maxLeft, maxRight) - height[x]`. Track running max from each side.

```java
class Solution {
    public int trap(int[] height) {
        int i = 0, j = height.length - 1, water = 0;
        int maxI = 0, maxJ = 0;
        while (i < j) {
            if (height[i] <= height[j]) {
                maxI = Math.max(maxI, height[i]);
                water += maxI - height[i];
                i++;
            } else {
                maxJ = Math.max(maxJ, height[j]);
                water += maxJ - height[j];
                j--;
            }
        }
        return water;
    }
}
```

---

## Pattern 2 — Same Direction (Write Pointer)

```java
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

## #27 Remove Element

**Description:** Remove all occurrences of `val` in-place. Return new length.  
**Keep condition:** `nums[j] != val`

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int i = 0;
        for (int j = 0; j < nums.length; j++)
            if (nums[j] != val) nums[i++] = nums[j];
        return i;
    }
}
```

---

## #26 Remove Duplicates from Sorted Array

**Description:** Remove duplicates in-place so each element appears at most once. Return new length.  
**Keep condition:** `nums[j] != nums[i-1]` — don't write if same as last written.

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int i = 0;
        for (int j = 0; j < nums.length; j++)
            if (i == 0 || nums[j] != nums[i - 1])
                nums[i++] = nums[j];
        return i;
    }
}
```

---

## #80 Remove Duplicates from Sorted Array II

**Description:** Each element may appear at most twice in-place. Return new length.  
**Keep condition:** `nums[j] != nums[i-2]` — don't write if same as two slots back.

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int i = 0;
        for (int j = 0; j < nums.length; j++)
            if (i < 2 || nums[j] != nums[i - 2])
                nums[i++] = nums[j];
        return i;
    }
}
```

---

## #283 Move Zeroes

**Description:** Move all zeroes to end while preserving relative order of non-zero elements.  
**Keep condition:** `nums[j] != 0`. Fill tail with zeros after the write pass.

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int i = 0;
        for (int j = 0; j < nums.length; j++)
            if (nums[j] != 0) nums[i++] = nums[j];
        while (i < nums.length) nums[i++] = 0;
    }
}
```

---

## Pattern 3 — Dutch Flag (3 Pointers)

```java
int i = 0, k = 0, j = n - 1;
while (k <= j) {
    if      (nums[k] == LO) swap(nums, i++, k++);  // confirmed small
    else if (nums[k] == MID) k++;                   // confirmed mid, skip
    else                     swap(nums, k, j--);    // large — don't advance k
}
```

Three regions: `[0, i)` = confirmed small, `[i, k)` = confirmed mid, `(j, n)` = confirmed large. `k` is the frontier.  
Do **not** increment `k` after swapping with `j` — the swapped element is unknown.

---

## #75 Sort Colors

**Description:** Sort array of 0s, 1s, 2s in-place without library sort.  
**Key:** Dutch Flag with LO = 0, MID = 1, HI = 2.

```java
class Solution {
    public void sortColors(int[] nums) {
        int i = 0, k = 0, j = nums.length - 1;
        while (k <= j) {
            if      (nums[k] == 0) swap(nums, i++, k++);
            else if (nums[k] == 1) k++;
            else                   swap(nums, k, j--);
        }
    }
    private void swap(int[] a, int x, int y) {
        int t = a[x]; a[x] = a[y]; a[y] = t;
    }
}
```

---

## Pattern Comparison

| Pattern | Pointers move | Sort needed | Use when |
|---|---|---|---|
| Opposite | `i` right, `j` left, converge | Yes (usually) | Sum/target problems on sorted array |
| Same direction | `j` scans, `i` writes | No | Filter / compact array in-place |
| Dutch Flag | `k` scans, `i` low boundary, `j` high boundary | No | 3-way partition (< / = / >) |

## Duplicate-skip Cheat Sheet (for Opposite pointers after a hit)

```java
// After recording a result at (i, j):
i++; j--;
while (i < j && nums[i] == nums[i - 1]) i++;  // skip duplicate i
while (i < j && nums[j] == nums[j + 1]) j--;  // skip duplicate j
```

Always check `i < j` inside the skip loop to avoid crossing.
