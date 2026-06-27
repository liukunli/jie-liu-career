# BFS Templates — Tree

Core structure: `Queue<TreeNode> queue = new ArrayDeque<>()`.  
One template: snapshot the level size, then drain exactly that many nodes per level.

---

## The Template — Level-Aware BFS

**Variables:** `queue` = nodes waiting to be processed · `size` = level snapshot (count of nodes in the current level) · `level` = current depth counter · `node` = node polled this step · `i` = index within the level
**Pseudocode:**
```
make an empty queue
put root in the queue
level = 0
while the queue is not empty:
    size = how many nodes are in the queue right now (one whole level)
    level = level + 1
    repeat size times (index i = 0..size-1):
        node = take the front of the queue
        process node (level known; i==0 -> first, i==size-1 -> last)
        if node has a left child, add it to the queue
        if node has a right child, add it to the queue
```

```java
// LEVEL-AWARE PROCESSING — snapshot size to make per-level decisions
// the queue holds exactly one full level; freeze its size, then drain just that many.  — WHEN: "level by level", "per row", "rightmost/leftmost in level", "min depth"
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
```

Always snapshot `size` first — it's how you know where each level ends. (If you truly don't need levels, just drop the `size` loop and poll node-by-node.)

## When to Use — Signal → Pattern

| Problem signal phrase | Pattern / group |
|---|---|
| "level order", "values per level", "each row" | Group 1 — collect entire level |
| "average / max / sum of each level" | Group 2 — aggregate per level |
| "right side view" (last in level), "bottom-left" (first in level) | Group 2 — record boundary node (`i==size-1` / `i==0`) |
| "minimum depth", "first level that satisfies X" | Group 3 — early return on condition |
| "connect next pointers at the same level" | Group 4 — wire nodes within a level |
| "same depth, different parent" (cousins), per-node metadata | Group 5 — track per-node metadata |
| "maximum width of a level" (counting null gaps) | Group 6 — position indexing |

## The One Rule — Snapshot Level Size First

```
Always snapshot the level size BEFORE the inner for loop:
    int size = queue.size();
    for (int i = 0; i < size; i++) { ... }

Without the snapshot, newly added children mix with the current level
and i == size-1 / i == 0 checks become meaningless.
```

---

## Quick Reference Table

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

## Group 1 — Collect Entire Level

### #102 Binary Tree Level Order Traversal

**Description:** Return all node values level by level, left to right.

**Variables:** `result` = list of levels · `queue` = BFS queue · `size` = level snapshot · `level` = values collected for this level · `node` = node polled · `i` = index within level
**Pseudocode:**
```
result = empty list
if root is null, return result
queue = new queue, put root in it
while queue not empty:
    size = current queue size (this whole level)
    level = empty list
    repeat size times (i = 0..size-1):
        node = poll front of queue
        append node value to level
        if node.left  exists, add to queue
        if node.right exists, add to queue
    append level to result
return result
```

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) return result;
        Queue<TreeNode> queue = new ArrayDeque<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> level = new ArrayList<>();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                level.add(node.val);
                if (node.left  != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
            result.add(level);
        }
        return result;
    }
}
```
**Time** O(n) | **Space** O(n)

---

### #107 Binary Tree Level Order Traversal II

**Description:** Same as #102 but return levels from bottom to top.  
**Key:** `LinkedList` as result — `addFirst` prepends each level, producing bottom-up order without a final reverse.

**Variables:** `result` = LinkedList of levels (prepended) · `queue` = BFS queue · `size` = level snapshot · `level` = values for this level · `node` = node polled · `i` = index within level
**Pseudocode:**
```
result = empty linked list
if root is null, return result
queue = new queue, put root in it
while queue not empty:
    size = current queue size (this whole level)
    level = empty list
    repeat size times (i = 0..size-1):
        node = poll front of queue
        append node value to level
        if node.left  exists, add to queue
        if node.right exists, add to queue
    prepend level to result (addFirst -> bottom-up order)
return result
```

```java
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        LinkedList<List<Integer>> result = new LinkedList<>();
        if (root == null) return result;
        Queue<TreeNode> queue = new ArrayDeque<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> level = new ArrayList<>();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                level.add(node.val);
                if (node.left  != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
            result.addFirst(level);    // prepend → bottom-up order
        }
        return result;
    }
}
```
**Time** O(n) | **Space** O(n)

---

### #103 Binary Tree Zigzag Level Order Traversal

**Description:** Level 1 left-to-right, level 2 right-to-left, alternating.  
**Key:** `LinkedList<Integer>` per level as a deque — `addLast` for left-to-right, `addFirst` for right-to-left. Flip flag after each level.

**Variables:** `result` = list of levels · `queue` = BFS queue · `leftToRight` = direction flag for this level · `size` = level snapshot · `level` = deque of values for this level · `node` = node polled · `i` = index within level
**Pseudocode:**
```
result = empty list
if root is null, return result
queue = new queue, put root in it
leftToRight = true
while queue not empty:
    size = current queue size (this whole level)
    level = empty deque
    repeat size times (i = 0..size-1):
        node = poll front of queue
        if leftToRight: append node value to back of level
        else:           append node value to front of level
        if node.left  exists, add to queue
        if node.right exists, add to queue
    append level to result
    flip leftToRight
return result
```

```java
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) return result;
        Queue<TreeNode> queue = new ArrayDeque<>();
        queue.offer(root);
        boolean leftToRight = true;
        while (!queue.isEmpty()) {
            int size = queue.size();
            LinkedList<Integer> level = new LinkedList<>();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                if (leftToRight) {
                    level.addLast(node.val);
                } else {
                    level.addFirst(node.val);
                }
                if (node.left  != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
            result.add(level);
            leftToRight = !leftToRight;
        }
        return result;
    }
}
```
**Time** O(n) | **Space** O(n)

---

### #637 Average of Levels in Binary Tree

**Description:** Return the average value of nodes at each level.

**Variables:** `result` = list of per-level averages · `queue` = BFS queue · `size` = level snapshot (also the divisor) · `sum` = running sum of this level · `node` = node polled · `i` = index within level
**Pseudocode:**
```
result = empty list
queue = new queue, put root in it
while queue not empty:
    size = current queue size (this whole level)
    sum = 0
    repeat size times (i = 0..size-1):
        node = poll front of queue
        sum = sum + node value
        if node.left  exists, add to queue
        if node.right exists, add to queue
    append sum / size to result
return result
```

```java
class Solution {
    public List<Double> averageOfLevels(TreeNode root) {
        List<Double> result = new ArrayList<>();
        Queue<TreeNode> queue = new ArrayDeque<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            double sum = 0;
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                sum += node.val;
                if (node.left  != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
            result.add(sum / size);
        }
        return result;
    }
}
```
**Time** O(n) | **Space** O(n)

---

## Group 2 — Record First / Last / Max in Each Level

All share the same outer loop. Only the `if` inside the `for` changes.

### #199 Binary Tree Right Side View

**Description:** Return the value of the rightmost node at each level.  
**Key:** record when `i == size - 1`.

**Variables:** `result` = rightmost value per level · `queue` = BFS queue · `size` = level snapshot · `node` = node polled · `i` = index within level (record when `i == size-1`, the last node)
**Pseudocode:**
```
result = empty list
if root is null, return result
queue = new queue, put root in it
while queue not empty:
    size = current queue size (this whole level)
    repeat size times (i = 0..size-1):
        node = poll front of queue
        if i == size-1: append node value to result   (last in level)
        if node.left  exists, add to queue
        if node.right exists, add to queue
return result
```

```java
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;
        Queue<TreeNode> queue = new ArrayDeque<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                if (i == size - 1) result.add(node.val);   // last in level
                if (node.left  != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
        }
        return result;
    }
}
```
**Time** O(n) | **Space** O(n)

---

### #513 Find Bottom Left Tree Value

**Description:** Return the leftmost value in the last level (deepest row).  
**Key:** record when `i == 0` every level — after the loop, `bottomLeft` holds the first node of the final level.

**Variables:** `queue` = BFS queue · `bottomLeft` = first value of the latest level seen (overwritten each level) · `size` = level snapshot · `node` = node polled · `i` = index within level (record when `i == 0`, the first node)
**Pseudocode:**
```
queue = new queue, put root in it
bottomLeft = root value
while queue not empty:
    size = current queue size (this whole level)
    repeat size times (i = 0..size-1):
        node = poll front of queue
        if i == 0: bottomLeft = node value   (first in level, overwritten each level)
        if node.left  exists, add to queue
        if node.right exists, add to queue
return bottomLeft   (first node of the last level)
```

```java
class Solution {
    public int findBottomLeftValue(TreeNode root) {
        Queue<TreeNode> queue = new ArrayDeque<>();
        queue.offer(root);
        int bottomLeft = root.val;
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                if (i == 0) bottomLeft = node.val;         // first in level — overwritten each level
                if (node.left  != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
        }
        return bottomLeft;
    }
}
```
**Time** O(n) | **Space** O(n)

---

### #515 Find Largest Value in Each Tree Row

**Description:** Return the maximum value found at each level.

**Variables:** `result` = max value per level · `queue` = BFS queue · `size` = level snapshot · `max` = running maximum for this level · `node` = node polled · `i` = index within level
**Pseudocode:**
```
result = empty list
if root is null, return result
queue = new queue, put root in it
while queue not empty:
    size = current queue size (this whole level)
    max = negative infinity
    repeat size times (i = 0..size-1):
        node = poll front of queue
        max = larger of (max, node value)
        if node.left  exists, add to queue
        if node.right exists, add to queue
    append max to result
return result
```

```java
class Solution {
    public List<Integer> largestValues(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;
        Queue<TreeNode> queue = new ArrayDeque<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            int max = Integer.MIN_VALUE;
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                max = Math.max(max, node.val);
                if (node.left  != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
            result.add(max);
        }
        return result;
    }
}
```
**Time** O(n) | **Space** O(n)

---

### #1161 Maximum Level Sum of a Binary Tree

**Description:** Return the smallest level number (1-indexed) whose node sum is maximum.

**Variables:** `queue` = BFS queue · `maxSum` = best level sum so far · `maxLevel` = level number of that best sum · `level` = current level (1-indexed) · `size` = level snapshot · `sum` = sum of this level · `node` = node polled · `i` = index within level
**Pseudocode:**
```
queue = new queue, put root in it
maxSum = negative infinity; maxLevel = 1; level = 0
while queue not empty:
    size = current queue size (this whole level)
    level = level + 1
    sum = 0
    repeat size times (i = 0..size-1):
        node = poll front of queue
        sum = sum + node value
        if node.left  exists, add to queue
        if node.right exists, add to queue
    if sum > maxSum: maxSum = sum; maxLevel = level
return maxLevel
```

```java
class Solution {
    public int maxLevelSum(TreeNode root) {
        Queue<TreeNode> queue = new ArrayDeque<>();
        queue.offer(root);
        int maxSum = Integer.MIN_VALUE, maxLevel = 1, level = 0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            level++;
            int sum = 0;
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                sum += node.val;
                if (node.left  != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
            if (sum > maxSum) { maxSum = sum; maxLevel = level; }
        }
        return maxLevel;
    }
}
```
**Time** O(n) | **Space** O(n)

---

## Group 3 — Early Return on Condition

### #111 Minimum Depth of Binary Tree

**Description:** Minimum number of nodes from root to the nearest leaf.  
**Key:** BFS is optimal here (DFS must visit the whole tree). Return `depth` the moment the first leaf is dequeued — that is guaranteed to be the shallowest.  
**Intuition:** BFS reaches nodes in depth order, so the first leaf it dequeues is necessarily the shallowest.

**Variables:** `queue` = BFS queue · `depth` = current level depth (1-indexed) · `size` = level snapshot · `node` = node polled · `i` = index within level
**Pseudocode:**
```
if root is null, return 0
queue = new queue, put root in it
depth = 0
while queue not empty:
    size = current queue size (this whole level)
    depth = depth + 1
    repeat size times (i = 0..size-1):
        node = poll front of queue
        if node has no children: return depth   (first leaf = shallowest)
        if node.left  exists, add to queue
        if node.right exists, add to queue
return depth
```

```java
class Solution {
    public int minDepth(TreeNode root) {
        if (root == null) return 0;
        Queue<TreeNode> queue = new ArrayDeque<>();
        queue.offer(root);
        int depth = 0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            depth++;
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                if (node.left == null && node.right == null) return depth;  // first leaf
                if (node.left  != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
        }
        return depth;
    }
}
```
**Time** O(n) | **Space** O(n)

---

## Group 4 — Connect Nodes Within a Level

### #116 Populating Next Right Pointers in Each Node

**Description:** Connect each node's `next` to the node immediately to its right at the same level. Tree is a perfect binary tree.  
**Key:** `previous` tracks the last node seen in the current level — wire `previous.next = node` before advancing. Reset `previous = null` at each level start.  
**Intuition:** BFS already visits a level left to right, so just chain each node to the one polled before it.

**Variables:** `queue` = BFS queue · `size` = level snapshot · `previous` = last node seen in this level (reset to null each level) · `node` = node polled · `i` = index within level
**Pseudocode:**
```
if root is null, return null
queue = new queue, put root in it
while queue not empty:
    size = current queue size (this whole level)
    previous = null
    repeat size times (i = 0..size-1):
        node = poll front of queue
        if previous is not null: previous.next = node   (chain within level)
        previous = node
        if node.left  exists, add to queue
        if node.right exists, add to queue
return root
```

```java
class Solution {
    public Node connect(Node root) {
        if (root == null) return null;
        Queue<Node> queue = new ArrayDeque<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            Node previous = null;
            for (int i = 0; i < size; i++) {
                Node node = queue.poll();
                if (previous != null) previous.next = node;
                previous = node;
                if (node.left  != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
        }
        return root;
    }
}
```
**Time** O(n) | **Space** O(n)

---

### #117 Populating Next Right Pointers in Each Node II

**Description:** Same as #116 but the tree can be any binary tree (not necessarily perfect).  
**Key:** the BFS solution is **identical** to #116 — the `size` snapshot handles uneven levels automatically.

**Variables:** `queue` = BFS queue · `size` = level snapshot (handles uneven levels) · `previous` = last node seen in this level (reset to null each level) · `node` = node polled · `i` = index within level
**Pseudocode:**
```
if root is null, return null
queue = new queue, put root in it
while queue not empty:
    size = current queue size (this whole level)
    previous = null
    repeat size times (i = 0..size-1):
        node = poll front of queue
        if previous is not null: previous.next = node   (chain within level)
        previous = node
        if node.left  exists, add to queue
        if node.right exists, add to queue
return root
```

```java
class Solution {
    public Node connect(Node root) {
        if (root == null) return null;
        Queue<Node> queue = new ArrayDeque<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            Node previous = null;
            for (int i = 0; i < size; i++) {
                Node node = queue.poll();
                if (previous != null) previous.next = node;
                previous = node;
                if (node.left  != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
        }
        return root;
    }
}
```
**Time** O(n) | **Space** O(n)

---

## Group 5 — Track Per-Node Metadata

### #993 Cousins in Binary Tree

**Description:** Two nodes `x` and `y` are cousins if they are at the same depth but have different parents. Return true if `x` and `y` are cousins.  
**Key:** for each node polled, check if its children are `x` or `y`. After each full level, if both parents found → check `xParent != yParent`. If only one found → different depths → false.  
**Intuition:** cousins must surface in the *same* BFS level; if only one shows up per level, their depths differ.

**Variables:** `queue` = BFS queue · `size` = level snapshot · `xParent`/`yParent` = parents of x/y found in this level (null if not yet) · `node` = node polled · `i` = index within level
**Pseudocode:**
```
queue = new queue, put root in it
while queue not empty:
    size = current queue size (this whole level)
    xParent = null; yParent = null
    repeat size times (i = 0..size-1):
        node = poll front of queue
        if node.left exists:
            add node.left to queue
            if node.left value == x: xParent = node
            if node.left value == y: yParent = node
        if node.right exists:
            add node.right to queue
            if node.right value == x: xParent = node
            if node.right value == y: yParent = node
    if both parents found: return xParent != yParent   (same depth -> cousins iff different parent)
    if exactly one parent found: return false           (different depths)
return false
```

```java
class Solution {
    public boolean isCousins(TreeNode root, int x, int y) {
        Queue<TreeNode> queue = new ArrayDeque<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            TreeNode xParent = null, yParent = null;
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                if (node.left != null) {
                    queue.offer(node.left);
                    if (node.left.val == x) xParent = node;
                    if (node.left.val == y) yParent = node;
                }
                if (node.right != null) {
                    queue.offer(node.right);
                    if (node.right.val == x) xParent = node;
                    if (node.right.val == y) yParent = node;
                }
            }
            if (xParent != null && yParent != null) return xParent != yParent;
            if (xParent != null || yParent != null) return false;  // one found → different depths
        }
        return false;
    }
}
```
**Time** O(n) | **Space** O(n)

---

## Side-by-Side: 199 vs 513

Both record one node per level. The only difference is which node:

```
                    #199 Right Side View        #513 Bottom Left Value
Record condition:   i == size - 1 (last)        i == 0 (first)
Update per level:   result.add(node.val)        bottomLeft = node.val  (overwrite)
Return:             List<Integer>               bottomLeft after all levels done
```

## Side-by-Side: 102 vs 103 vs 107

All collect every node in every level. Only the insertion order changes:

```
                    #102 Level Order            #103 Zigzag             #107 Bottom-Up
Level container:    ArrayList<Integer>          LinkedList<Integer>     ArrayList<Integer>
Add node:           level.add(val)              addLast/addFirst        level.add(val)
Add to result:      result.add(level)           result.add(level)       result.addFirst(level)
Extra state:        —                           boolean leftToRight     result is LinkedList
```

## Pattern Summary

| What changes per level | Key variable | Example problems |
|---|---|---|
| Collect all values | `List<Integer> level` | 102, 107, 103 |
| Compute aggregate | `int sum` / `int max` | 637, 515, 1161 |
| Record boundary node | check `i == 0` or `i == size-1` | 199, 513 |
| Return on first match | `return depth` | 111 |
| Wire nodes together | `Node previous` | 116, 117 |
| Track parent metadata | `TreeNode xParent, yParent` | 993 |

## The One Rule (recap)

Snapshot the level size **before** the inner `for` loop — see "The One Rule" at the top of this file for the full explanation.

---

## Group 6 — Position Indexing

### #662 Maximum Width of Binary Tree

**Description:** Return the maximum width of any level of a binary tree. Width is defined as the length between the leftmost and rightmost non-null nodes, including all the null nodes in between.

**Variation:** BFS with position tracking. Assign each node a position: root=1, left child of node at pos `p` gets `2*p`, right child gets `2*p+1`. Width of level = `lastPos - firstPos + 1`. Normalize by subtracting `firstPos` of each level to prevent overflow.

**Variables:** `maxWidth` = best width found · `queue` = BFS queue of nodes · `indices` = parallel queue of heap-style positions · `size` = level snapshot · `first` = leftmost position of this level (normalize against it) · `last` = rightmost normalized position seen · `node` = node polled · `pos` = normalized position of node · `i` = index within level
**Pseudocode:**
```
if root is null, return 0
maxWidth = 0
queue = new queue with root; indices = new queue with position 0
while queue not empty:
    size = current queue size (this whole level)
    first = front position in indices; last = 0
    repeat size times (i = 0..size-1):
        node = poll front of queue
        pos = poll front of indices minus first   (normalize to avoid overflow)
        last = pos
        if node.left  exists: add node.left to queue, add 2*pos     to indices
        if node.right exists: add node.right to queue, add 2*pos+1 to indices
    maxWidth = larger of (maxWidth, last + 1)   (width = last - first(0) + 1)
return maxWidth
```

```java
class Solution {
    public int widthOfBinaryTree(TreeNode root) {
        if (root == null) return 0;
        int maxWidth = 0;
        Queue<TreeNode> queue = new ArrayDeque<>();        // canonical BFS queue + size snapshot
        Queue<Long> indices = new ArrayDeque<>();          // heap-style position per node
        queue.offer(root);
        indices.offer(0L);
        while (!queue.isEmpty()) {
            int size = queue.size();                       // ← snapshot: all nodes at this level
            long first = indices.peek(), last = 0;
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                long pos = indices.poll() - first;         // ← VARIATION: normalize to prevent overflow
                last = pos;
                if (node.left  != null) { queue.offer(node.left);  indices.offer(2 * pos);     } // left  = 2*pos
                if (node.right != null) { queue.offer(node.right); indices.offer(2 * pos + 1); } // right = 2*pos+1
            }
            maxWidth = (int) Math.max(maxWidth, last + 1); // width = lastPos - firstPos(0) + 1
        }
        return maxWidth;
    }
}
```
**Time** O(n) | **Space** O(n)
