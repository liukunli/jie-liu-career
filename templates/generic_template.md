# Generic Template — Format Guide & Test Harness

Every template file in this folder follows the same two-part structure:

1. **Template algorithm + template code** — the reusable pattern, with specific LeetCode problems used as concrete examples inside the code.
2. **Quick reference table + question/solution** — a table listing every problem (with a *Variation from Template* column), followed by each problem's full solution where deviations are marked `// ← VARIATION: explanation`.

---

## Generic Test Harness

Use this boilerplate to run any single problem locally. Replace `data`/`solve()` with the problem's input and logic.

```java
class Question {

    private int data;

    public Question(int data) {
        this.data = data;
    }

    public void solve() {
        // TODO
    }
}

public class Solution {

    public static void main(String[] args) {
        Question q = new Question(0);
        q.solve();
    }
}
```

---

## Formatting Rules

- **Always brace `if`/`else`** — no inline single-statement bodies, no column-aligned `else`. Every branch uses `{ }` on its own lines:

```java
if (condition) {
    doThis();
} else if (other) {
    doThat();
} else {
    fallback();
}
```

---

## Naming Conventions (enforced across all template files)

| Context | Convention |
|---|---|
| Index variables | `i`, `j`, `k` (never `left`, `right`, `low`, `mid`, `high`) |
| Linked list | `sentinel`, `previous`, `current` |
| Queue | `Queue<Integer> queue = new ArrayDeque<>();` |
| BFS over tree | `Queue<TreeNode> queue = new ArrayDeque<>();` |
| Grid directions | `int[][] dirs = {{-1,0},{1,0},{0,-1},{0,1}};` (UP, DOWN, LEFT, RIGHT) |
| Character frequency | `count[ch - 'a']++;` |
| Digit frequency | `count[ch - '0']++;` |
| Char to integer build | `num = num * 10 + (ch - '0');` |

---

## Template Index

| File | Category | Core Pattern |
|---|---|---|
| `binary_search_templates.md` | Binary Search | Closed `[i,j]`, half-open, minimize/maximize answer space |
| `two_pointer_templates.md` | Two Pointers | Opposite ends, same-direction write pointer, Dutch flag |
| `prefix_sum_hashmap_templates.md` | Prefix Sum | Count/length with HashMap, tree path sums |
| `sorting_templates.md` | Sorting | Merge sort, quick sort, quick select, count-during-merge |
| `sliding_window_templates.md` | Sliding Window | Fixed, max-variable, min-variable windows |
| `linked_list_templates.md` | Linked List | Delete/filter, reversal, fast/slow, merge, composite |
| `dfs_templates.md` | DFS / Backtracking | Tree return-up/pass-down, grid DFS, graph 3-color, backtracking, BST |
| `bfs_templates.md` | BFS | Level-order with size snapshot, position indexing |
| `graph_templates.md` | Graph | BFS shortest path, topo sort, union find, Dijkstra, bipartite, Prim's MST |
| `dp_templates.md` | Dynamic Programming | 1D/2D/grid/interval DP, knapsack, state machine |
| `stack_queue_templates.md` | Stack / Queue / Heap | Monotone stack/deque, two heaps, priority queue |
| `greedy_templates.md` | Greedy | Sort-by-end, sort-by-start, sort + heap, non-interval |
| `string_templates.md` | String | Frequency counting, hashing, bucket sort, expand-from-center |
| `bit_manipulation_templates.md` | Bit Manipulation | XOR cancel, mod-k state machine, bitmask as set, power checks |
| `trie_templates.md` | Trie | Insert/search/startsWith, wildcard DFS, grid pruning |
| `design_templates.md` | Design | HashMap + linked list (LRU), frequency maps (LFU), array + map |
| `math_templates.md` | Math | Fast power, base conversion, sieve, digit manipulation |
