# Backtracking

Priority: Medium
Status: Not started

---

Backtracking problems can be broken down into several core **patterns**. Here's how to master them across **difficulty levels**.

[https://www.youtube.com/watch?v=DKCbsiDBN6c&t=351s&ab_channel=AbdulBari](https://www.youtube.com/watch?v=DKCbsiDBN6c&t=351s&ab_channel=AbdulBari)

---

### 🔹 BACKTRACKING CORE PATTERNS

| Pattern | Description |
| --- | --- |
| **1. Subsets** | Include/exclude decision at each step |
| **2. Permutations** | All arrangements of elements |
| **3. Combinations** | Select `k` items from `n` |
| **4. Palindromes** | Partitioning or checking strings |
| **5. N-Queens / Grid Search** | Placing items on 2D grid with constraints |
| **6. Word/Path Search in Matrix** | DFS + backtracking |
| **7. Expression Add Operators** | Explore math expressions recursively |
| **8. Coloring / Graph State** | Coloring nodes or solving constraint satisfaction |
| **9. Bitmask Backtracking** | Optimize recursive state using bitmask |
| **10. Constraint Pruning** | Add conditions to reduce recursion (e.g., Sudoku) |

---

## 🟢 EASY LEVEL (Start Here)

> Goal: Understand recursion + basic backtracking
> 

| Problem | Pattern | Link |
| --- | --- | --- |
| **78. Subsets** | Subsets | [LeetCode](https://leetcode.com/problems/subsets/) |
| **401. Binary Watch** | Combination | [LeetCode](https://leetcode.com/problems/binary-watch/) |
| **118. Pascal's Triangle** | Variation of Combinations | [LeetCode](https://leetcode.com/problems/pascals-triangle/) |
| **104. Maximum Depth of Binary Tree** | DFS (intro) | [LeetCode](https://leetcode.com/problems/maximum-depth-of-binary-tree/) |

---

## 🟡 MEDIUM LEVEL (Most Asked)

> Goal: Learn pruning, constraints, permutations, 2D board search
> 

| Problem | Pattern | Link |
| --- | --- | --- |
| **46. Permutations** | Permutations | [LeetCode](https://leetcode.com/problems/permutations/) |
| **77. Combinations** | Combinations | [LeetCode](https://leetcode.com/problems/combinations/) |
| **39. Combination Sum** | Subsets + pruning | [LeetCode](https://leetcode.com/problems/combination-sum/) |
| **40. Combination Sum II** | Subsets + avoid duplicates | [LeetCode](https://leetcode.com/problems/combination-sum-ii/) |
| **216. Combination Sum III** | K-combinations | [LeetCode](https://leetcode.com/problems/combination-sum-iii/) |
| **131. Palindrome Partitioning** | Palindromes | [LeetCode](https://leetcode.com/problems/palindrome-partitioning/) |
| **79. Word Search** | Grid Search | [LeetCode](https://leetcode.com/problems/word-search/) |
| **90. Subsets II** | Subsets with Duplicates | [LeetCode](https://leetcode.com/problems/subsets-ii/) |
| **17. Letter Combinations of a Phone Number** | Backtracking + Map | [LeetCode](https://leetcode.com/problems/letter-combinations-of-a-phone-number/) |

---

## 🔴 HARD LEVEL (FAANG-Level)

> Goal: Learn advanced pruning, multi-dimensional state, backtrack + memo/bitmask
> 

| Problem | Pattern | Link |
| --- | --- | --- |
| **51. N-Queens** | Grid Search | [LeetCode](https://leetcode.com/problems/n-queens/) |
| **37. Sudoku Solver** | Constraint Satisfaction | [LeetCode](https://leetcode.com/problems/sudoku-solver/) |
| **282. Expression Add Operators** | Expression Parsing + DFS | [LeetCode](https://leetcode.com/problems/expression-add-operators/) |
| **52. N-Queens II** | Count solutions | [LeetCode](https://leetcode.com/problems/n-queens-ii/) |
| **847. Shortest Path Visiting All Nodes** | Bitmask Backtracking + BFS | [LeetCode](https://leetcode.com/problems/shortest-path-visiting-all-nodes/) |
| **301. Remove Invalid Parentheses** | Backtracking + pruning | [LeetCode](https://leetcode.com/problems/remove-invalid-parentheses/) |
| **212. Word Search II** | Trie + Backtracking | [LeetCode](https://leetcode.com/problems/word-search-ii/) |
| **996. Number of Squareful Arrays** | Permutations + Conditions | [LeetCode](https://leetcode.com/problems/number-of-squareful-arrays/) |

---

## 🧠 BEST PRACTICES FOR FAANG-LEVEL BACKTRACKING

1. **Draw the recursion tree** for intuition.
2. **Prune early** — this is key to improving performance.
3. **Use visited sets or bitmasking** to track state.
4. **Avoid duplicates** in subsets/permutations via sorting and skipping.
5. **Memoization + Backtracking** when state is overlapping (like bitmask + position).

---

## ✅ Checklist to Master Backtracking for Interviews

| Goal | Status |
| --- | --- |
| Understand base case and recursive structure | ⬜ |
| Handle subsets, permutations, combinations | ⬜ |
| Solve grid-based search problems (Word search, N-Queens) | ⬜ |
| Practice constraint pruning (Sudoku, Expression parsing) | ⬜ |
| Apply bitmasking to backtracking (squareful arrays, graphs) | ⬜ |
| Write clean code with tracking (`visited`, `path`, `index`) | ⬜ |

---