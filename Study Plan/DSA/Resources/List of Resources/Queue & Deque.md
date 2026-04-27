# Queue & Deque

Priority: High
Status: Done

---

## 🔹 QUEUE – In-Depth FAANG-Level Guide

### 📌 What is a Queue?

- **FIFO (First In, First Out)** linear data structure.
- Supports two main operations: `enqueue` (add to rear) and `dequeue` (remove from front).
- Implemented using `LinkedList`, `ArrayDeque`, or `Queue` interface in Java.

---

### 📚 When to Use Queues

| Use Case | Description | Real Example |
| --- | --- | --- |
| **BFS Traversals** | Explore neighbours layer by layer. | Level order traversal of a binary tree |
| **Shortest Path (Unweighted Graphs)** | Dijkstra (if all weights = 1). | Finding minimum steps in a maze |
| **Rate Limiting / Throttling** | Control access rate. | API call limiter |
| **Sliding Window (Fixed-size)** | Track fixed-size window. | Moving average |
| **Task Scheduling** | Execute tasks in order. | OS job scheduler |

---

### 🧠 Queue Patterns

### 1. **Breadth-First Search (BFS)**

```java
Queue<TreeNode> queue = new LinkedList<>();
queue.offer(root);
while (!queue.isEmpty()) {
    int size = queue.size();
    for (int i = 0; i < size; i++) {
        TreeNode node = queue.poll();
        // process node
        if (node.left != null) queue.offer(node.left);
        if (node.right != null) queue.offer(node.right);
    }
}

```

### 2. **Multi-Source BFS**

```java
Queue<int[]> queue = new LinkedList<>();
for (int[] source : sources) queue.offer(source);
while (!queue.isEmpty()) {
    // Normal BFS logic
}

```

### 3. **Sliding Window with Queue**

For monotonic queue, we use a deque (see Deque section below).

---

### ✅ Queue LeetCode Questions

| Difficulty | Problems |
| --- | --- |
| Easy | [933. Number of Recent Calls](https://leetcode.com/problems/number-of-recent-calls/), [225. Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues/) |
| Medium | [542. 01 Matrix](https://leetcode.com/problems/01-matrix/), [207. Course Schedule](https://leetcode.com/problems/course-schedule/) |
| Hard | [847. Shortest Path Visiting All Nodes](https://leetcode.com/problems/shortest-path-visiting-all-nodes/) |

---

## 🔹 DEQUE – In-Depth FAANG-Level Guide

### 📌 What is a Deque?

- **Double-Ended Queue**: allows insertion/removal from both ends.
- Ideal for problems involving **sliding windows**, **monotonic sequences**, **palindromes**, etc.
- In Java: `ArrayDeque<>` or `LinkedList<>`.

---

### 📚 When to Use Deques

| Use Case | Description | Real Example |
| --- | --- | --- |
| **Sliding Window Maximum** | Keep track of max/min in a window. | Stock prices over time |
| **Palindrome Checking** | Compare front & back. | Valid Palindrome II |
| **Monotonic Queue** | Maintain increasing/decreasing order. | Max in window |
| **Two-Pointer-Like Problems** | Efficient front/back processing. | Rotting Oranges |
| **BFS with Priority** | Deque helps simulate 0-1 BFS. | 0-1 BFS Grid traversal |

---

### 🧠 Deque Patterns

### 1. **Monotonic Decreasing Queue for Max Sliding Window**

```java
Deque<Integer> deque = new LinkedList<>();
for (int i = 0; i < nums.length; i++) {
    while (!deque.isEmpty() && deque.peekFirst() < i - k + 1)
        deque.pollFirst();  // Remove out of window
    while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i])
        deque.pollLast();   // Maintain decreasing order
    deque.offerLast(i);
    if (i >= k - 1) result.add(nums[deque.peekFirst()]);
}

```

### 2. **0-1 BFS Using Deque**

```java
Deque<int[]> deque = new ArrayDeque<>();
deque.offerFirst(new int[]{startX, startY});
while (!deque.isEmpty()) {
    int[] curr = deque.pollFirst();
    for (int[] dir : directions) {
        // if move cost is 0 => offerFirst
        // else offerLast
    }
}

```

---

### ✅ Deque LeetCode Questions

| Difficulty | Problems |
| --- | --- |
| Easy | [2390. Removing Stars From a String](https://leetcode.com/problems/removing-stars-from-a-string/) |
| Medium | [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/), [862. Shortest Subarray with Sum at Least K](https://leetcode.com/problems/shortest-subarray-with-sum-at-least-k/) |
| Hard | [1293. Shortest Path in a Grid with Obstacles Elimination](https://leetcode.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/) |

---

## 🧩 Common Mistakes

- **Forgetting to remove out-of-window indices** in sliding window.
- **Not using deque for monotonic structure**, leading to O(nk) time.
- **Incorrect BFS levels (mixing queue size and logic)**.
- **Overusing PriorityQueue instead of deque** when all weights are 0/1.

---

## 🧪 LeetCode Practice Set (Queue & Deque)

### 🟢 Easy

- 
    1. Number of Recent Calls
- 
    1. Implement Stack using Queues
- 
    1. Implement Queue using Stacks

### 🟡 Medium

- 
    1. Course Schedule (Topological Sort)
- 
    1. 01 Matrix (Multi-source BFS)
- 
    1. Rotting Oranges (Multi-source BFS)
- 
    1. Sliding Window Maximum
- 
    1. Moving Average from Data Stream

### 🔴 Hard

- 
    1. Shortest Path in a Grid with Obstacles Elimination
- 
    1. Shortest Subarray with Sum at Least K
- 
    1. Shortest Path Visiting All Nodes
- 
    1. Maximum Number of Robots Within Budget

---