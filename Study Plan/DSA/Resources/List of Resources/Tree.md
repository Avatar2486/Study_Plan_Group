# Tree

Priority: High
Status: In progress

## ✅ 1. Core Concepts

### 🔷 Tree vs Binary Tree vs BST

| Concept | Description |
| --- | --- |
| **Tree** | A hierarchical data structure. |
| **Binary Tree** | Each node has ≤ 2 children. |
| **BST** (Binary Search Tree) | A Binary Tree with ordering: Left < Root < Right. |

---

## ✅ 2. Tree Traversals

### 🔹 2.1 Inorder Traversal (Left, Root, Right)

- **BST Inorder ⇒ Sorted Order**
- Recursive: `inorder(root.left), visit root, inorder(root.right)`
- Iterative with stack.
- **Morris Traversal** (O(1) space): Threaded binary tree.

### 🔹 2.2 Preorder Traversal (Root, Left, Right)

- Used to **clone trees**, prefix notation.
- Recursive: `visit root, preorder(left), preorder(right)`
- Iterative with stack.

### 🔹 2.3 Postorder Traversal (Left, Right, Root)

- Used to **delete a tree**.
- Recursive or with two stacks.

### 🔹 2.4 Level Order (BFS)

- Queue-based.
- Used for **shortest path in unweighted trees**, etc.

---

## ✅ 3. Morris Traversal (O(1) space)

- Rewires tree to avoid recursion/stack.
- **Used for:** Inorder or Preorder traversal in O(n) time & O(1) space.
- [Key Idea] Establish temporary thread from predecessor to current.

---

## ✅ 4. Problem-Solving Patterns

| Pattern Name | Description | Problems Covered |
| --- | --- | --- |
| **Traversal-based** | DFS/BFS to visit nodes in order | All traversal problems |
| **Subtree recursion** | Return info from subtrees | Diameter, Balanced, LCA |
| **Path Pattern** | Carry path/accumulated values | Path Sum, All Root-to-Leaf Paths |
| **Boundary/Binary Views** | Views from sides/top/bottom | Top View, Bottom View, Left/Right View |
| **Ancestor Pattern** | Recursively find LCA | LCA of Binary Tree/BST |
| **Tree Construction** | Build tree from preorder/inorder | Reconstruct Binary Tree |
| **Serialization** | Convert to and from string | Serialize/Deserialize Binary Tree |
| **BST Properties** | Utilize sorted nature | Validate BST, Kth smallest, BST to DLL |
| **Morris Traversal** | Space-efficient traversal | Inorder traversal w/o stack/recursion |

---

---

## ✅ 5. Code Patterns (Java)

### Inorder Traversal (Iterative)

```java
java
CopyEdit
public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    Stack<TreeNode> stack = new Stack<>();
    while (root != null || !stack.isEmpty()) {
        while (root != null) {
            stack.push(root);
            root = root.left;
        }
        root = stack.pop();
        res.add(root.val);
        root = root.right;
    }
    return res;
}

```

### Lowest Common Ancestor (Subtree Pattern)

```java
java
CopyEdit
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null || root == p || root == q) return root;
    TreeNode left = lowestCommonAncestor(root.left, p, q);
    TreeNode right = lowestCommonAncestor(root.right, p, q);
    if (left != null && right != null) return root;
    return left != null ? left : right;
}

```

### Validate BST

```java
java
CopyEdit
public boolean isValidBST(TreeNode root) {
    return validate(root, Long.MIN_VALUE, Long.MAX_VALUE);
}
private boolean validate(TreeNode node, long min, long max) {
    if (node == null) return true;
    if (node.val <= min || node.val >= max) return false;
    return validate(node.left, min, node.val) && validate(node.right, node.val, max);
}

```

### Morris Inorder Traversal

```java
java
CopyEdit
public List<Integer> morrisInorder(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    while (root != null) {
        if (root.left == null) {
            res.add(root.val);
            root = root.right;
        } else {
            TreeNode pre = root.left;
            while (pre.right != null && pre.right != root)
                pre = pre.right;
            if (pre.right == null) {
                pre.right = root;
                root = root.left;
            } else {
                pre.right = null;
                res.add(root.val);
                root = root.right;
            }
        }
    }
    return res;
}

```

### 🟢 **Easy**

1. 94. Binary Tree Inorder Traversal
2. 144. Binary Tree Preorder Traversal
3. 145. Binary Tree Postorder Traversal
4. 101. Symmetric Tree
5. 226. Invert Binary Tree
6. 112. Path Sum
7. 617. Merge Two Binary Trees
8. 938. Range Sum of BST
9. 104. Maximum Depth of Binary Tree
10. [783. Minimum Distance Between BST Nodes](https://leetcode.com/problems/minimum-distance-between-bst-nodes/)

---

### 🟡 **Medium**

1. 102. Binary Tree Level Order Traversal
2. 103. Binary Tree Zigzag Level Order Traversal
3. 105. Construct Binary Tree from Preorder and Inorder Traversal
4. 106. Construct Binary Tree from Inorder and Postorder Traversal
5. 114. Flatten Binary Tree to Linked List
6. 116. Populating Next Right Pointers in Each Node
7. 117. Populating Next Right Pointers in Each Node II
8. 199. Binary Tree Right Side View
9. 230. Kth Smallest Element in a BST
10. 236. Lowest Common Ancestor of a Binary Tree
11. 543. Diameter of Binary Tree
12. 129. Sum Root to Leaf Numbers
13. 437. Path Sum III
14. 173. Binary Search Tree Iterator
15. [863. All Nodes Distance K in Binary Tree](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/)
16. [1530. Number of Good Leaf Nodes Pairs](https://leetcode.com/problems/number-of-good-leaf-nodes-pairs/)
17. [669. Trim a Binary Search Tree](https://leetcode.com/problems/trim-a-binary-search-tree/)
18. 1448. Count Good Nodes in Binary Tree
19. Vertical order traversal

---

### 🔴 **Hard**

1. 124. Binary Tree Maximum Path Sum
2. [297. Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)
3. 652. Find Duplicate Subtrees
4. 968. Binary Tree Cameras
5. 979. Distribute Coins in Binary Tree
6. 1372. Longest ZigZag Path in a Binary Tree
7. 1457. Pseudo-Palindromic Paths in a Binary Tree
8. 426. Convert Binary Search Tree to Sorted Doubly Linked List
9. 1245. Tree Diameter
10. 2246. Longest Path with Different Adjacent Characters
11. [834. Sum of Distances in Tree](https://leetcode.com/problems/sum-of-distances-in-tree/)