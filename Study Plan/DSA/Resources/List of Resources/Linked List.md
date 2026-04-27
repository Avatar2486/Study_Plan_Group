# Linked List

Priority: High
Status: Done

A **Linked List** is a linear data structure where elements (nodes) are stored in non-contiguous memory locations. Each node contains:

1. **Data**
2. **Pointer (Reference) to the next node** (except in the case of Doubly Linked Lists, where there is an additional pointer to the previous node)

### **Types of Linked Lists**:

1. **Singly Linked List** – Each node points to the next node.
2. **Doubly Linked List** – Each node has pointers to both the next and previous nodes.
3. **Circular Linked List** – The last node points back to the first node.

### **Time Complexity Analysis**

| Operation | Singly Linked List | Doubly Linked List |
| --- | --- | --- |
| Access/Search | O(n) | O(n) |
| Insert (at head) | O(1) | O(1) |
| Insert (at tail) | O(n) | O(1) |
| Delete (from head) | O(1) | O(1) |
| Delete (from tail) | O(n) | O(1) |

---

## **💪 FAANG-Level Linked List Problems Categorized by Difficulty**

### **🟢 Easy Problems**

These problems focus on basic operations, traversal, and insertion/deletion in a linked list.

1. **Reverse a Linked List** – Iterative & Recursive
2. **Find Middle of a Linked List** – Fast & Slow Pointers
3. **Delete a Node Without Head Reference** – In-Place Deletion
4. **Detect Cycle in a Linked List** – Floyd’s Cycle Detection Algorithm
5. **Merge Two Sorted Linked Lists** – Two Pointers Merge
6. **Remove Duplicates from Sorted Linked List** – In-Place Deduplication
7. **Check if Linked List is Palindrome** – Reverse & Compare
8. **Intersection of Two Linked Lists** – Finding the merge point
9. **Nth Node from the End** – Two Pointers Approach

---

### **🟡 Medium Problems**

These problems introduce advanced techniques like fast and slow pointers, stack usage, and recursion.

1. **Flatten a Multilevel Doubly Linked List** – DFS/BFS Approach
2. **Add Two Numbers Represented as Linked List** – Reverse & Add
3. **Rotate Linked List** – Break & Attach
4. **Reverse Nodes in k-Group** – Recursive + Iterative
5. **Remove Duplicates from Unsorted Linked List** – HashSet or Sorting
6. **Partition List (Less than X on Left, Greater on Right)** – Two Pointers
7. **Sort Linked List (Merge Sort on LL)** – Merge Sort O(n log n)
8. **Delete Node in a Doubly Linked List** – Handling Previous & Next Pointers
9. **Swapping Nodes in a Linked List** – Find & Swap
10. **Split Linked List in Parts** – Dividing Linked List
11. **Reorder List (1st, last, 2nd, second-last, …)** – Reverse Half & Merge

---

### **🔴 Hard Problems**

These problems require deep understanding and optimization techniques.

1. **Copy List with Random Pointer** – HashMap or O(1) Space Trick
2. **Merge k Sorted Linked Lists** – Heap (Priority Queue) or Divide & Conquer
3. **LRU Cache using Linked List & HashMap** – Doubly Linked List + HashMap
4. **Reverse Nodes Between M and N** – Pointer Manipulation
5. **Find the Sum of Two Numbers in Circular Linked List** – [Tricky Modifications]
6. **Flatten a Linked List with Next and Child Pointers** – Recursive & Iterative Approaches
7. **Maximum Twin Sum in a Linked List** – Reverse Half & Sum
8. **Find Median of a Linked List in O(1) Space** – [Two Pointers]
9. **Design a Cache System using Linked List** – [FAANG System Design Challenge]
10. **Convert Binary Tree to Doubly Linked List** – Inorder Traversal

---

## **🛠 Advanced Techniques to Master**

1. **Two Pointers Approach**
    - Detect cycle (Floyd’s Algorithm)
    - Find middle node
    - Find nth node from the end
2. **Stack Usage**
    - Check if linked list is palindrome
    - Reverse in k-groups
3. **HashMap Optimization**
    - Detect loop (HashSet)
    - LRU Cache
4. **Recursion for Complex Reversals**
    - Reverse between M and N
    - Reverse k-groups