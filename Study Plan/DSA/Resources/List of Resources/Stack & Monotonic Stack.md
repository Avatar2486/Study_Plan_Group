# Stack & Monotonic Stack

Priority: High
Status: Done

[https://leetcode.com/discuss/post/2347639/a-comprehensive-guide-and-template-for-m-irii/](https://leetcode.com/discuss/post/2347639/a-comprehensive-guide-and-template-for-m-irii/)

## 1. Stack vs Monotonic Stack

### ✅ Stack (General Use Cases)

A **stack** is a LIFO (Last In First Out) data structure used when:

- You need to remember previous elements (like matching brackets)
- Backtracking (like DFS)
- Keeping track of indices or elements in reverse order

### ✅ Monotonic Stack

A **Monotonic Stack** is a special stack where elements are always in **increasing** or **decreasing** order.

- **Monotonically Increasing Stack:** Elements increase from top to bottom
    - Used when you're looking for **next smaller** or **previous smaller**
- **Monotonically Decreasing Stack:** Elements decrease from top to bottom
    - Used when you're looking for **next greater** or **previous greater**

---

## 🔹 2. When to Use Monotonic Stack (Patterns)

### 👉 Spot a Monotonic Stack Problem If:

- You're asked for:
    - Next Greater Element
    - Previous Greater Element
    - Next Smaller Element
    - Previous Smaller Element
- You're scanning an array and need to **find relationships across elements (like nearest bigger/smaller)** in **O(n)** time.
- Brute-force solution would be **O(n²)** (nested loops)

---

## 🔹 3. Java Code Template – Monotonic Stack

### ✅ Next Greater Element (Monotonic Decreasing Stack)

```java
java
CopyEdit
public int[] nextGreaterElements(int[] nums) {
    int n = nums.length;
    int[] result = new int[n];
    Stack<Integer> stack = new Stack<>(); // stores indices

    for (int i = n - 1; i >= 0; i--) {
        while (!stack.isEmpty() && nums[stack.peek()] <= nums[i]) {
            stack.pop();
        }
        result[i] = stack.isEmpty() ? -1 : nums[stack.peek()];
        stack.push(i);
    }

    return result;
}

```

### ✅ Next Smaller Element (Monotonic Increasing Stack)

```java
java
CopyEdit
public int[] nextSmallerElements(int[] nums) {
    int n = nums.length;
    int[] result = new int[n];
    Stack<Integer> stack = new Stack<>(); // stores indices

    for (int i = n - 1; i >= 0; i--) {
        while (!stack.isEmpty() && nums[stack.peek()] >= nums[i]) {
            stack.pop();
        }
        result[i] = stack.isEmpty() ? -1 : nums[stack.peek()];
        stack.push(i);
    }

    return result;
}

```

---

## 🔹 4. LeetCode Problems by Difficulty and Pattern

### 🟢 EASY

| Problem | Pattern |
| --- | --- |
| 20. Valid Parentheses | Basic Stack |
| 496. Next Greater Element I | Monotonic Stack (Decreasing) |
| 844. Backspace String Compare | Stack Simulation |

---

### 🟡 MEDIUM

| Problem | Pattern |
| --- | --- |
| 739. Daily Temperatures | Monotonic Stack (Decreasing) |
| 901. Online Stock Span | Monotonic Stack (Increasing) |
| 503. Next Greater Element II | Monotonic Stack with Circular Array |
| 402. Remove K Digits | Monotonic Increasing Stack |
| 581. Shortest Unsorted Continuous Subarray | Two-Pass Stack |
| 84. Largest Rectangle in Histogram | Monotonic Stack for Span |

---

### 🔴 HARD

| Problem | Pattern |
| --- | --- |
| 42. Trapping Rain Water | Two Pointers OR Monotonic Stack |
| 316. Remove Duplicate Letters | Stack + Greedy |
| 85. Maximal Rectangle | Convert to Histogram + Monotonic Stack |

---

## 🔹 5. Key Patterns to Master

| Pattern | Stack Type | Use Case |
| --- | --- | --- |
| Next Greater Element | Decreasing Stack | 503, 496 |
| Next Smaller Element | Increasing Stack | 402 |
| Largest Rectangle | Increasing Stack | 84 |
| Stock Span | Increasing Stack | 901 |
| Remove Digits | Increasing Stack | 402 |
| Daily Temperatures | Decreasing Stack | 739 |

---

## 🔹 6. Tips to Recognize Monotonic Stack Problems

- 🧠 "Find the **next/previous** greater/smaller element"
- 🧠 "Span of days/temperature/stock where a condition holds"
- 🧠 "Max rectangle/histogram area"
- 🧠 If brute-force is `O(n^2)`, and you're processing **linear structure (array, string)** → think **Monotonic Stack**