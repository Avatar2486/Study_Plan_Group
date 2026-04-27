# Heap (Priority Queue)

Priority: High
Status: Not started

---

## 📘 What is a Heap?

A **Heap** is a special **complete binary tree** where:

- **Max-Heap:** Parent node is always **greater than or equal to** its children.
- **Min-Heap:** Parent node is always **less than or equal to** its children.

### ✅ Properties

- **Complete Binary Tree:** All levels filled except possibly the last.
- **Heap Order Property:** Max or Min ordering.
- Implemented efficiently using **array-based structure**.

---

## 🧠 Real-world Use Cases (FAANG-Asked)

| Use Case | Heap Type | Description |
| --- | --- | --- |
| Priority Queue | Min/Max | Efficient access to the highest/lowest priority element. |
| Dijkstra's Algorithm (shortest path) | Min-Heap | To pick node with min distance. |
| Median in a stream | Max + Min | Max-heap for left half, Min-heap for right half. |
| Top K elements | Min-Heap | Size-K min-heap tracks top K largest. |
| Scheduling (OS, CPU, Tasks) | Min-Heap | Schedule based on priority/time. |
| Huffman Coding (Compression) | Min-Heap | Combine lowest frequency nodes. |

---

## 🧱 Java Implementation Using PriorityQueue

Java’s `PriorityQueue` is a **Min-Heap** by default.

```java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());

```

---

## 🔧 Custom Comparator in Java

```java
PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
// Min-Heap based on the 2nd element of array

```

---

## ⚙️ Manual Heap Implementation in Java

```java
class MaxHeap {
    private int[] heap;
    private int size;

    public MaxHeap(int capacity) {
        heap = new int[capacity];
        size = 0;
    }

    private int parent(int i) { return (i - 1) / 2; }
    private int left(int i) { return 2 * i + 1; }
    private int right(int i) { return 2 * i + 2; }

    public void insert(int val) {
        if (size == heap.length) throw new IllegalStateException("Heap full");
        heap[size] = val;
        int current = size++;

        // Bubble up
        while (current > 0 && heap[current] > heap[parent(current)]) {
            swap(current, parent(current));
            current = parent(current);
        }
    }

    public int extractMax() {
        if (size == 0) throw new IllegalStateException("Heap empty");
        int max = heap[0];
        heap[0] = heap[--size];
        heapify(0);
        return max;
    }

    private void heapify(int i) {
        int largest = i;
        int l = left(i), r = right(i);
        if (l < size && heap[l] > heap[largest]) largest = l;
        if (r < size && heap[r] > heap[largest]) largest = r;
        if (largest != i) {
            swap(i, largest);
            heapify(largest);
        }
    }

    private void swap(int i, int j) {
        int tmp = heap[i]; heap[i] = heap[j]; heap[j] = tmp;
    }
}

```

---

## 🧪 FAANG-Level Interview Patterns Using Heaps

### 🔸 1. **Top K Elements**

**Problem:** Find top K frequent elements

**Approach:** Use Min-Heap of size K

**Complexity:** O(N log K)

---

### 🔸 2. **Kth Largest Element in Stream**

- Maintain Min-Heap of size K.

---

### 🔸 3. **Median from Data Stream**

- Max-Heap for left half, Min-Heap for right half.
- Rebalance heaps on insert.

---

### 🔸 4. **Merge K Sorted Lists**

- Use Min-Heap of size K to merge.
- Each heap entry stores value and which list it came from.

---

### 🔸 5. **Sliding Window Maximum**

- Use Max-Heap (or Monotonic Deque).
- Java Heap will be slower than Deque due to O(log N) insert/removal.

---

## 🔍 Time and Space Complexity

| Operation | Heap (Array-Based) | Notes |
| --- | --- | --- |
| Insert | O(log n) | Bubble up |
| Delete (extract) | O(log n) | Heapify down |
| Get Min/Max | O(1) | At root |
| Heapify (build) | O(n) | Not O(n log n)! |

---

## ⚠️ Common Pitfalls

- **Java’s PriorityQueue is Min-Heap**, not Max-Heap.
- Custom comparators must be consistent (`a == b ⇒ cmp = 0`).
- In Java, **duplicate elements are allowed**, but must handle removal carefully.

---

## 🧩 Heap Variants

| Variant | Description |
| --- | --- |
| Binomial Heap | Faster merge operations |
| Fibonacci Heap | Amortized constant time insert/decrease key |
| Pairing Heap | Simplified version of Fibonacci heap |
| d-ary Heap | Each node has d children; used in network routers |
| Min-Max Heap | Support both min and max in O(1) |

---

## 📚 Want to Practice?

Here are **LeetCode problems by difficulty**:

### Easy

- [Min Heap Implementation](https://leetcode.com/problems/kth-largest-element-in-a-stream/)
- [Last Stone Weight](https://leetcode.com/problems/last-stone-weight/)

### Medium

- [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)
- [K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)
- [Merge K Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)
- [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)

### Hard

- [Sliding Window Median](https://leetcode.com/problems/sliding-window-median/)
- [Smallest Range Covering Elements from K Lists](https://leetcode.com/problems/smallest-range-covering-elements-from-k-lists/)

---