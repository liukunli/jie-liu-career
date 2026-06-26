# DFS Templates

DFS appears in five forms. The pattern determines naming, return type, and where the answer is built.

---

## Quick Reference Table

| # | Name | Description | Pattern | Returns | Global var |
|---|---|---|---|---|---|
| 104 | Max Depth | Maximum depth of binary tree | Tree — return up | depth int | No |
| 543 | Diameter | Longest path between any two nodes | Tree — return up | height int | Yes (`diameter`) |
| 124 | Max Path Sum | Max sum path between any two nodes | Tree — return up | best single-arm int | Yes (`maxSum`) |
| 110 | Balanced Tree | Is tree height-balanced? | Tree — return up | height or -1 | No |
| 226 | Invert Tree | Mirror a binary tree | Tree — return up | TreeNode | No |
| 112 | Path Sum | Any root-to-leaf path summing to target? | Tree — pass down | boolean | No |
| 113 | Path Sum II | All root-to-leaf paths summing to target | Tree — pass down + backtrack | void | No |
| 257 | Binary Tree Paths | All root-to-leaf paths as strings | Tree — pass down + backtrack | void | No |
| 129 | Sum Root to Leaf | Sum of all root-to-leaf numbers | Tree — pass down | int | No |
| 200 | Number of Islands | Count connected land regions in grid | Grid DFS | void | No |
| 695 | Max Area of Island | Largest island area | Grid DFS | int (area) | No |
| 207 | Course Schedule | Can all courses be finished (no cycle)? | Graph DFS 3-color | boolean | No |
| 210 | Course Schedule II | Return valid course order | Graph DFS 3-color | void → post-order | No |
| 46 | Permutations | All permutations of distinct integers | Backtrack — no start, used[] | void | No |
| 78 | Subsets | All subsets of distinct integers | Backtrack — start, no used[] | void | No |
| 39 | Combination Sum | All combos summing to target (reuse allowed) | Backtrack — start, reuse i | void | No |
| 40 | Combination Sum II | All combos summing to target (no reuse) | Backtrack — start, skip dups | void | No |
| 79 | Word Search | Does word exist in board? | Grid backtrack — restore cell | boolean | No |
| 131 | Palindrome Partitioning | All palindrome partitions of string | Backtrack — start, check palindrome | void | No |
| 98 | Validate Binary Search Tree | Check if a binary tree is a valid BST | Pass min/max bounds down recursively; every node must satisfy both constraints | **Pass bounds down**: validate(node, min, max) with long bounds to handle INT_MIN/INT_MAX | O(n) | O(h) |
| 230 | Kth Smallest Element in a BST | Find kth smallest element | Inorder traversal (left→node→right) counts ascending; stop at kth | **Inorder + counter**: global count/result; return early when count == k | O(k) | O(h) |
| 270 | Closest BST Value | Find value in BST closest to target | BST search: go left if target < node, right if target > node; track closest | **BST binary search**: use BST structure to traverse in O(h) | O(h) | O(1) |
| 285 | Inorder Successor in BST | Find the smallest node greater than p | BST traversal: if root > p it could be successor; else go right | **BST successor search**: save candidate when going left | O(h) | O(1) |
| 687 | Longest Univalue Path | Longest path where all nodes have same value | Post-order DFS; at each node, extend path from children only if values match | **Conditional extend**: leftPath = (left.val==node.val) ? left+1 : 0 | O(n) | O(h) |

---

## All Templates

```java
// 1. TREE — RETURN UP (post-order: process children first, combine at node)
private int dfs(TreeNode node) {
    if (node == null) return BASE;          // 0 for depth, true for balanced
    int left  = dfs(node.left);
    int right = dfs(node.right);
    // combine left, right, node.val → answer propagates up
    return ...;
}

// 2. TREE — PASS DOWN (pre-order: use parent state at current node)
private void dfs(TreeNode node, int accumulated) {
    if (node == null) return;
    accumulated += node.val;                // update state on way down
    if (isLeaf(node)) { /* record */ return; }
    dfs(node.left,  accumulated);
    dfs(node.right, accumulated);
    // backtrack: no undo needed for primitive; undo List.add if using collection
}

// 3. TREE — GLOBAL ANSWER (return up the best single arm; update global across both arms)
int answer = Integer.MIN_VALUE;
private int dfs(TreeNode node) {
    if (node == null) return 0;
    int left  = Math.max(0, dfs(node.left));   // clamp negative
    int right = Math.max(0, dfs(node.right));
    answer = Math.max(answer, left + right + node.val);   // cross-node path
    return Math.max(left, right) + node.val;              // single arm up
}

// 4. GRID DFS — mark visited by mutating grid; 4-directional flood fill
private void dfs(int[][] grid, int r, int c) {
    if (r < 0 || r >= grid.length || c < 0 || c >= grid[0].length) return;
    if (grid[r][c] != TARGET) return;
    grid[r][c] = VISITED;
    dfs(grid, r+1, c); dfs(grid, r-1, c);
    dfs(grid, r, c+1); dfs(grid, r, c-1);
}

// 5. GRAPH DFS — 3-color visited: 0=unseen 1=in-stack 2=done
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

# Part 1 — Tree DFS

## Tree Return-Up Pattern

Recurse into children first, then combine results at the current node. Answer propagates upward.

### #104 Maximum Depth of Binary Tree

**Description:** Maximum number of nodes along the longest root-to-leaf path.

```java
class Solution {
    public int maxDepth(TreeNode root) {
        return dfs(root);
    }
    private int dfs(TreeNode node) {
        if (node == null) return 0;
        int left  = dfs(node.left);
        int right = dfs(node.right);
        return Math.max(left, right) + 1;
    }
}
```

---

### #543 Diameter of Binary Tree

**Description:** Length of the longest path between any two nodes (path does not need to pass through root).  
**Key:** the path through a node = `left height + right height`. Track global max; return only the single best arm up.

```java
class Solution {
    int diameter = 0;
    public int diameterOfBinaryTree(TreeNode root) {
        dfs(root);
        return diameter;
    }
    private int dfs(TreeNode node) {
        if (node == null) return 0;
        int left  = dfs(node.left);
        int right = dfs(node.right);
        diameter = Math.max(diameter, left + right);   // cross-node path
        return Math.max(left, right) + 1;              // single arm up
    }
}
```

---

### #124 Binary Tree Maximum Path Sum

**Description:** Maximum sum of any path between any two nodes. Values can be negative.  
**Key:** clamp negative arms to 0 (`Math.max(0, ...)`). Global tracks the best `left + right + node.val`; return only `max(left, right) + node.val` upward.

```java
class Solution {
    int maxSum = Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root) {
        dfs(root);
        return maxSum;
    }
    private int dfs(TreeNode node) {
        if (node == null) return 0;
        int left  = Math.max(0, dfs(node.left));
        int right = Math.max(0, dfs(node.right));
        maxSum = Math.max(maxSum, left + right + node.val);
        return Math.max(left, right) + node.val;
    }
}
```

---

### #110 Balanced Binary Tree

**Description:** Is every node's left and right subtree within 1 height of each other?  
**Key:** return -1 as a sentinel for "unbalanced"; short-circuit immediately on -1.

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        return dfs(root) != -1;
    }
    private int dfs(TreeNode node) {
        if (node == null) return 0;
        int left  = dfs(node.left);
        if (left  == -1) return -1;
        int right = dfs(node.right);
        if (right == -1) return -1;
        if (Math.abs(left - right) > 1) return -1;
        return Math.max(left, right) + 1;
    }
}
```

---

### #226 Invert Binary Tree

**Description:** Mirror a binary tree — swap left and right subtrees at every node.

```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        TreeNode left  = invertTree(root.left);
        TreeNode right = invertTree(root.right);
        root.left  = right;
        root.right = left;
        return root;
    }
}
```

---

## Tree Pass-Down Pattern

State is built on the way **down** and consumed at leaves. Use backtracking when state is a mutable collection.

### #112 Path Sum

**Description:** Does any root-to-leaf path sum to `targetSum`?

```java
class Solution {
    public boolean hasPathSum(TreeNode root, int targetSum) {
        return dfs(root, targetSum);
    }
    private boolean dfs(TreeNode node, int remaining) {
        if (node == null) return false;
        remaining -= node.val;
        if (node.left == null && node.right == null) return remaining == 0;
        return dfs(node.left, remaining) || dfs(node.right, remaining);
    }
}
```

---

### #113 Path Sum II

**Description:** Return all root-to-leaf paths that sum to `targetSum`.  
**Key:** pass a mutable `path` list down. **Backtrack** (remove last element) after returning from each child.

```java
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        List<List<Integer>> result = new ArrayList<>();
        dfs(root, targetSum, new ArrayList<>(), result);
        return result;
    }
    private void dfs(TreeNode node, int remaining, List<Integer> path, List<List<Integer>> result) {
        if (node == null) return;
        path.add(node.val);
        remaining -= node.val;
        if (node.left == null && node.right == null && remaining == 0)
            result.add(new ArrayList<>(path));
        dfs(node.left,  remaining, path, result);
        dfs(node.right, remaining, path, result);
        path.remove(path.size() - 1);   // backtrack
    }
}
```

---

### #257 Binary Tree Paths

**Description:** Return all root-to-leaf paths as strings (`"1->2->5"`).

```java
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> result = new ArrayList<>();
        dfs(root, new StringBuilder(), result);
        return result;
    }
    private void dfs(TreeNode node, StringBuilder path, List<String> result) {
        if (node == null) return;
        int len = path.length();
        if (len > 0) path.append("->");
        path.append(node.val);
        if (node.left == null && node.right == null)
            result.add(path.toString());
        dfs(node.left,  path, result);
        dfs(node.right, path, result);
        path.setLength(len);   // backtrack to before this node
    }
}
```

---

### #129 Sum Root to Leaf Numbers

**Description:** Each root-to-leaf path represents a number (e.g., 1→2→3 = 123). Return the total sum.

```java
class Solution {
    public int sumNumbers(TreeNode root) {
        return dfs(root, 0);
    }
    private int dfs(TreeNode node, int current) {
        if (node == null) return 0;
        current = current * 10 + node.val;
        if (node.left == null && node.right == null) return current;
        return dfs(node.left, current) + dfs(node.right, current);
    }
}
```

---

## 543 vs 124 — Side by Side

Both use the global-variable pattern. One difference:

```
                    #543 Diameter              #124 Max Path Sum
Global tracks:      left + right               left + right + node.val
Clamp negatives?    No (heights >= 0)          Yes (Math.max(0, ...))
Return up:          max(left, right) + 1       max(left, right) + node.val
Base case:          return 0                   return 0
```

---

# Part 2 — Graph DFS

## Grid DFS (4-directional flood fill)

Mark visited by overwriting the cell value. Return the accumulated property (count, area) or void.

### #200 Number of Islands

**Description:** Count the number of islands (connected groups of `'1'`) in a binary grid.

```java
class Solution {
    public int numIslands(char[][] grid) {
        int count = 0;
        for (int r = 0; r < grid.length; r++)
            for (int c = 0; c < grid[0].length; c++)
                if (grid[r][c] == '1') { dfs(grid, r, c); count++; }
        return count;
    }
    private void dfs(char[][] grid, int r, int c) {
        if (r < 0 || r >= grid.length || c < 0 || c >= grid[0].length) return;
        if (grid[r][c] != '1') return;
        grid[r][c] = '0';   // mark visited
        dfs(grid, r+1, c); dfs(grid, r-1, c);
        dfs(grid, r, c+1); dfs(grid, r, c-1);
    }
}
```

---

### #695 Max Area of Island

**Description:** Return the area of the largest island.  
**Key:** same flood fill but DFS returns the area of the connected component.

```java
class Solution {
    public int maxAreaOfIsland(int[][] grid) {
        int max = 0;
        for (int r = 0; r < grid.length; r++)
            for (int c = 0; c < grid[0].length; c++)
                max = Math.max(max, dfs(grid, r, c));
        return max;
    }
    private int dfs(int[][] grid, int r, int c) {
        if (r < 0 || r >= grid.length || c < 0 || c >= grid[0].length) return 0;
        if (grid[r][c] != 1) return 0;
        grid[r][c] = 0;
        return 1 + dfs(grid, r+1, c) + dfs(grid, r-1, c)
                 + dfs(grid, r, c+1) + dfs(grid, r, c-1);
    }
}
```

---

## Graph DFS — 3-Color Cycle Detection

Three states: `0` = unvisited, `1` = in current DFS stack (visiting), `2` = fully processed (safe).  
A back edge (reaching a node with state `1`) means a cycle.

### #207 Course Schedule

**Description:** Can you finish all courses given prerequisites? Return false if there is a cycle.

```java
class Solution {
    int[] state;
    List<List<Integer>> graph;

    public boolean canFinish(int numCourses, int[][] prerequisites) {
        state = new int[numCourses];
        graph = new ArrayList<>();
        for (int i = 0; i < numCourses; i++) graph.add(new ArrayList<>());
        for (int[] p : prerequisites) graph.get(p[1]).add(p[0]);
        for (int i = 0; i < numCourses; i++)
            if (hasCycle(i)) return false;
        return true;
    }
    private boolean hasCycle(int node) {
        if (state[node] == 1) return true;    // back edge → cycle
        if (state[node] == 2) return false;   // already safe
        state[node] = 1;
        for (int neighbor : graph.get(node))
            if (hasCycle(neighbor)) return true;
        state[node] = 2;
        return false;
    }
}
```

---

### #210 Course Schedule II

**Description:** Return a valid order to take all courses. Return `[]` if a cycle exists.  
**Key:** same 3-color DFS. Add node to `order` in **post-order** (after all neighbors done). Reverse at the end → topological order.

```java
class Solution {
    int[] state;
    List<List<Integer>> graph;
    List<Integer> order;

    public int[] findOrder(int numCourses, int[][] prerequisites) {
        state = new int[numCourses];
        order = new ArrayList<>();
        graph = new ArrayList<>();
        for (int i = 0; i < numCourses; i++) graph.add(new ArrayList<>());
        for (int[] p : prerequisites) graph.get(p[1]).add(p[0]);
        for (int i = 0; i < numCourses; i++)
            if (!dfs(i)) return new int[]{};
        Collections.reverse(order);
        return order.stream().mapToInt(Integer::intValue).toArray();
    }
    private boolean dfs(int node) {
        if (state[node] == 1) return false;   // cycle
        if (state[node] == 2) return true;    // already done
        state[node] = 1;
        for (int neighbor : graph.get(node))
            if (!dfs(neighbor)) return false;
        state[node] = 2;
        order.add(node);                      // post-order
        return true;
    }
}
```

---

## 207 vs 210 — Side by Side

```
                    #207 (boolean)             #210 (order)
DFS returns:        boolean (cycle found?)     boolean (cycle found?)
Extra action:       —                          order.add(node)  after neighbors
Post-process:       —                          Collections.reverse(order)
```

---

# Part 3 — Backtracking

**Template:** choose → recurse → undo.  
`start` controls which elements are eligible at each level. `current` is the in-progress candidate.

```java
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

## Backtracking Decision Table

| # | All orderings? | Reuse element? | Has duplicates? | Start index | Skip condition |
|---|---|---|---|---|---|
| 46 Permutations | Yes — `used[]` | No | No | Loop 0..n, `used[i]` | `used[i]` |
| 78 Subsets | No | No | No | `start` → `i+1` | None |
| 39 Combination Sum | No | Yes | No | `start` → `i` | `candidates[i] > remaining` |
| 40 Combination Sum II | No | No | Yes | `start` → `i+1` | `i > start && nums[i] == nums[i-1]` |
| 131 Palindrome Part. | No | No | No | `start` → `end` | `!isPalindrome(sub)` |

---

### #46 Permutations

**Description:** All permutations of distinct integers.  
**Key:** loop always from 0; use `boolean[] used` to avoid reusing elements within one permutation.

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(nums, new boolean[nums.length], new ArrayList<>(), result);
        return result;
    }
    private void backtrack(int[] nums, boolean[] used, List<Integer> current, List<List<Integer>> result) {
        if (current.size() == nums.length) { result.add(new ArrayList<>(current)); return; }
        for (int i = 0; i < nums.length; i++) {
            if (used[i]) continue;
            used[i] = true;
            current.add(nums[i]);
            backtrack(nums, used, current, result);
            current.remove(current.size() - 1);
            used[i] = false;
        }
    }
}
```

---

### #78 Subsets

**Description:** All subsets (power set) of distinct integers.  
**Key:** record at every node (not just leaves). Pass `i+1` — each element used at most once, order enforced by `start`.

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(nums, 0, new ArrayList<>(), result);
        return result;
    }
    private void backtrack(int[] nums, int start, List<Integer> current, List<List<Integer>> result) {
        result.add(new ArrayList<>(current));   // record every prefix (including empty)
        for (int i = start; i < nums.length; i++) {
            current.add(nums[i]);
            backtrack(nums, i + 1, current, result);
            current.remove(current.size() - 1);
        }
    }
}
```

---

### #39 Combination Sum

**Description:** All combinations summing to target. Same element may be used unlimited times. No duplicate combos.  
**Key:** pass `i` (not `i+1`) to allow reuse. Sort + prune when `candidates[i] > remaining`.

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        Arrays.sort(candidates);
        List<List<Integer>> result = new ArrayList<>();
        backtrack(candidates, 0, target, new ArrayList<>(), result);
        return result;
    }
    private void backtrack(int[] candidates, int start, int remaining, List<Integer> current, List<List<Integer>> result) {
        if (remaining == 0) { result.add(new ArrayList<>(current)); return; }
        for (int i = start; i < candidates.length; i++) {
            if (candidates[i] > remaining) break;   // pruning
            current.add(candidates[i]);
            backtrack(candidates, i, remaining - candidates[i], current, result);  // i, not i+1
            current.remove(current.size() - 1);
        }
    }
}
```

---

### #40 Combination Sum II

**Description:** Each element used at most once. Input may have duplicates. No duplicate combos in output.  
**Key:** sort first. Skip `candidates[i] == candidates[i-1]` when `i > start` — avoids duplicate combos at the same recursion level. Pass `i+1` — no reuse.

```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        Arrays.sort(candidates);
        List<List<Integer>> result = new ArrayList<>();
        backtrack(candidates, 0, target, new ArrayList<>(), result);
        return result;
    }
    private void backtrack(int[] candidates, int start, int remaining, List<Integer> current, List<List<Integer>> result) {
        if (remaining == 0) { result.add(new ArrayList<>(current)); return; }
        for (int i = start; i < candidates.length; i++) {
            if (candidates[i] > remaining) break;
            if (i > start && candidates[i] == candidates[i - 1]) continue;  // skip dup at same level
            current.add(candidates[i]);
            backtrack(candidates, i + 1, remaining - candidates[i], current, result);  // i+1, no reuse
            current.remove(current.size() - 1);
        }
    }
}
```

---

### #79 Word Search

**Description:** Given a board of characters, return true if the word exists as a connected path (no cell reused).  
**Key:** mark cell as visited by overwriting, then restore after recursion (backtrack).

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        for (int r = 0; r < board.length; r++)
            for (int c = 0; c < board[0].length; c++)
                if (dfs(board, word, r, c, 0)) return true;
        return false;
    }
    private boolean dfs(char[][] board, String word, int r, int c, int idx) {
        if (idx == word.length()) return true;
        if (r < 0 || r >= board.length || c < 0 || c >= board[0].length) return false;
        if (board[r][c] != word.charAt(idx)) return false;
        char temp = board[r][c];
        board[r][c] = '#';   // mark visited
        boolean found = dfs(board, word, r+1, c, idx+1) || dfs(board, word, r-1, c, idx+1)
                     || dfs(board, word, r, c+1, idx+1) || dfs(board, word, r, c-1, idx+1);
        board[r][c] = temp;  // restore (backtrack)
        return found;
    }
}
```

---

### #131 Palindrome Partitioning

**Description:** Partition string `s` such that every substring is a palindrome. Return all such partitions.

```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> result = new ArrayList<>();
        backtrack(s, 0, new ArrayList<>(), result);
        return result;
    }
    private void backtrack(String s, int start, List<String> current, List<List<String>> result) {
        if (start == s.length()) { result.add(new ArrayList<>(current)); return; }
        for (int end = start + 1; end <= s.length(); end++) {
            String sub = s.substring(start, end);
            if (!isPalindrome(sub)) continue;
            current.add(sub);
            backtrack(s, end, current, result);
            current.remove(current.size() - 1);
        }
    }
    private boolean isPalindrome(String s) {
        int i = 0, j = s.length() - 1;
        while (i < j) if (s.charAt(i++) != s.charAt(j--)) return false;
        return true;
    }
}
```

---

## 39 vs 40 — The One Difference

```
                    #39 (reuse OK)                  #40 (no reuse, has dups)
Sort:               Yes (pruning)                   Yes (both pruning and dup-skip)
Recurse with:       i     (same index)              i+1   (next index)
Skip dup line:      —                               if (i > start && nums[i] == nums[i-1]) continue
```

## Tree DFS Summary

```
Pattern             When to use                         Answer location
Return up           Combine children at node            return value bubbles up
Pass down           Accumulate state toward leaves      check at leaf
Global variable     Path spans across a node (not up)   int/long field, updated inside dfs
```

---

# Part — BST (Binary Search Tree) Problems

BST key property: `left subtree values < node.val < right subtree values`. This allows O(h) search/insert/delete by binary-searching the tree.

## BST Template: Pass Bounds Down

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

## BST Template: Inorder Traversal = Sorted Order

```java
// BST inorder (left → node → right) visits nodes in ascending order
void inorder(TreeNode node) {
    if (node == null) return;
    inorder(node.left);
    // process node (kth smallest: increment counter, return when k)
    inorder(node.right);
}
```

## BST Template: Binary Search on Tree

```java
// Navigate BST like binary search: go left or right based on comparison
TreeNode search(TreeNode root, int target) {
    while (root != null) {
        if      (root.val == target) return root;
        else if (root.val <  target) root = root.right;
        else                         root = root.left;
    }
    return null;
}
```

---

## #98 Validate Binary Search Tree

**Description:** Determine if a binary tree is a valid BST. Each node's value must be strictly greater than all values in its left subtree and strictly less than all values in its right subtree.

**Variation:** Pass min/max bounds down — each call tightens the valid range. Use `long` to handle `Integer.MIN_VALUE` and `Integer.MAX_VALUE` edge cases.

```java
class Solution {
    public boolean isValidBST(TreeNode root) {
        return validate(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private boolean validate(TreeNode node, long min, long max) {
        if (node == null) return true;
        if (node.val <= min || node.val >= max) return false;  // ← VARIATION: bounds constraint
        return validate(node.left, min, node.val)              // ← VARIATION: tighten max going left
            && validate(node.right, node.val, max);            // ← VARIATION: tighten min going right
    }
}
```
**Time** O(n) | **Space** O(h)

---

## #230 Kth Smallest Element in a BST

**Description:** Find the kth smallest element in a BST (1-indexed).

**Variation:** BST inorder traversal visits nodes in ascending order. Count nodes visited; when count reaches k, record the answer and stop early.

```java
class Solution {
    private int count = 0, result = 0;

    public int kthSmallest(TreeNode root, int k) {
        inorder(root, k);
        return result;
    }

    private void inorder(TreeNode node, int k) {
        if (node == null) return;
        inorder(node.left, k);
        if (++count == k) { result = node.val; return; }  // ← VARIATION: stop at kth node
        inorder(node.right, k);
    }
}
```
**Time** O(k) average, O(n) worst | **Space** O(h)

---

## #270 Closest Binary Search Tree Value

**Description:** Given a BST and a `target` (double), return the value in the BST closest to target.

**Variation:** Use BST structure to navigate in O(h). At each node, compare distance to closest seen so far, then binary-search left or right.

```java
class Solution {
    public int closestValue(TreeNode root, double target) {
        int closest = root.val;
        while (root != null) {
            if (Math.abs(root.val - target) < Math.abs(closest - target))
                closest = root.val;                       // ← VARIATION: track closest during search
            root = root.val < target ? root.right : root.left;  // ← VARIATION: binary search
        }
        return closest;
    }
}
```
**Time** O(h) | **Space** O(1)

---

## #285 Inorder Successor in BST

**Description:** Given a node `p` in a BST, return its inorder successor (the smallest node with value greater than `p.val`). Return null if no such node exists.

**Variation:** Navigate the BST. When `root.val > p.val`, this root is a candidate — save it and go left (to find a smaller valid candidate). When `root.val <= p.val`, go right (must find something larger).

```java
class Solution {
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        TreeNode result = null;
        while (root != null) {
            if (root.val > p.val) {
                result = root;          // ← VARIATION: save as candidate, then search left for closer
                root = root.left;
            } else {
                root = root.right;      // ← VARIATION: must go right to find something > p
            }
        }
        return result;
    }
}
```
**Time** O(h) | **Space** O(1)

---

## #687 Longest Univalue Path

**Description:** Return the length of the longest path in a binary tree where every node along the path has the same value. The path does not need to pass through the root.

**Variation:** Post-order DFS. At each node, extend the left or right path only if the child's value matches. The path through the current node = leftPath + rightPath. Return the max single-direction extension upward.

```java
class Solution {
    private int max = 0;

    public int longestUnivaluePath(TreeNode root) {
        dfs(root);
        return max;
    }

    private int dfs(TreeNode node) {
        if (node == null) return 0;
        int left  = dfs(node.left);
        int right = dfs(node.right);
        int leftPath  = (node.left  != null && node.left.val  == node.val) ? left  + 1 : 0;  // ← VARIATION: only extend if values match
        int rightPath = (node.right != null && node.right.val == node.val) ? right + 1 : 0;  // ← VARIATION: conditional extension
        max = Math.max(max, leftPath + rightPath);   // ← path through this node
        return Math.max(leftPath, rightPath);         // ← return max single direction up
    }
}
```
**Time** O(n) | **Space** O(h)
