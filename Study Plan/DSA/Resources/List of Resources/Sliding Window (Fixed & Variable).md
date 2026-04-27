# Sliding Window (Fixed & Variable)

Priority: High
Status: Done

# **🔥 FAANG-Level Sliding Window Mastery 🔥**

The **Sliding Window** technique is one of the most efficient approaches for solving **subarray and substring problems**. It allows us to transform **brute-force `O(n²)` solutions into `O(n)` optimized solutions**, making it a must-know for FAANG interviews.

---

# **📌 When to Use Sliding Window?**

Use the **Sliding Window** technique when:

1. The problem involves **contiguous** subarrays or substrings.
2. You need to find **maximum/minimum**, **count**, or **validate conditions** on a **subset of elements**.
3. The brute-force solution involves **nested loops (`O(n²)`)**, and an **optimized `O(n)` approach** is needed.

---

# **🔹 Types of Sliding Window**

There are **two types** of Sliding Window:

1. **Fixed-Size Sliding Window**
    - Used when the **size of the window remains constant**.
    - Example: **"Find the maximum sum of any subarray of size `k`."**
    - **Complexity:** `O(n)`
2. **Variable-Size Sliding Window**
    - Used when the **size of the window changes dynamically** based on conditions.
    - Example: **"Find the longest substring with unique characters."**
    - **Complexity:** `O(n)`

---

# **🚀 General Templates for Sliding Window**

### **1️⃣ Fixed-Size Sliding Window Template**

Use when the **window size is constant**.

```java
java
CopyEdit
public int fixedSizeSlidingWindow(int[] nums, int k) {
    int windowSum = 0, maxSum = Integer.MIN_VALUE;

    // Compute sum of first window
    for (int i = 0; i < k; i++) {
        windowSum += nums[i];
    }
    maxSum = windowSum;

    // Slide the window
    for (int i = k; i < nums.length; i++) {
        windowSum += nums[i] - nums[i - k]; // Add new, remove old
        maxSum = Math.max(maxSum, windowSum);
    }

    return maxSum;
}

```

---

### **2️⃣ Variable-Size Sliding Window Template**

Use when the **window grows/shrinks based on conditions**.

```java
java
CopyEdit
public int variableSizeSlidingWindow(String s) {
    int left = 0, maxLength = 0;
    HashMap<Character, Integer> map = new HashMap<>();

    for (int right = 0; right < s.length(); right++) {
        char c = s.charAt(right);
        map.put(c, map.getOrDefault(c, 0) + 1);

        while (map.size() > someCondition) { // Adjust window based on condition
            char leftChar = s.charAt(left);
            map.put(leftChar, map.get(leftChar) - 1);
            if (map.get(leftChar) == 0) {
                map.remove(leftChar);
            }
            left++; // Shrink window
        }

        maxLength = Math.max(maxLength, right - left + 1);
    }

    return maxLength;
}

```

---

# **🔹 Common Sliding Window Patterns**

1. **Fixed-Size Window**
    - **Use Case:** Find max/min/sum of a fixed-length subarray.
    - **Key Concept:** Maintain a window of size `k` and slide it.
2. **Expand and Contract (Variable Window)**
    - **Use Case:** Longest substring with a condition (e.g., unique characters).
    - **Key Concept:** Expand window, shrink when condition is violated.
3. **Two-Pointer (Left-Right)**
    - **Use Case:** Find subarrays with a sum constraint.
    - **Key Concept:** Move `right` to expand, `left` to contract.
4. **Deque for Min/Max**
    - **Use Case:** Sliding window maximum/minimum.
    - **Key Concept:** Use a **Deque (double-ended queue)** to store max/min efficiently.

---

# **📝 Categorized FAANG-Level Questions for Practice**

## **🟢 Easy**

| # | Problem | Type |
| --- | --- | --- |
| 1 | Maximum Sum of Subarray of Size K | Fixed |
| 2 | Find All Anagrams in a String | Variable |
| 3 | Permutation in String | Variable |
| 4 | Longest Substring Without Repeating Characters | Variable |

---

## **🟠 Medium**

| # | Problem | Type |
| --- | --- | --- |
| 5 | Longest Repeating Character Replacement | Variable |
| 6 | Sliding Window Maximum | Fixed |
| 7 | Minimum Window Substring | Variable |
| 8 | Count Number of Nice Subarrays | Variable |

---

## **🔴 Hard**

| # | Problem | Type |
| --- | --- | --- |
| 9 | Smallest Subarray with Sum ≥ K | Variable |
| 10 | Number of Subarrays with Bounded Maximum | Variable |
| 11 | Subarrays with K Different Integers | Variable |
| 12 | Longest Subarray with Absolute Diff ≤ Limit | Variable |
| 13 | **Subarrays with K Different Integers** | Variable |

---

# **🔥 FAANG-Level Key Takeaways**

### **🚀 Optimizing Sliding Window**

1. **Avoid unnecessary computations** by adding/removing elements instead of recomputing.
2. **Use HashMap/Set** for tracking unique elements.
3. **Use Deque** for tracking max/min in a window efficiently.
4. **For longest subarray problems, think about shrink-and-expand patterns**.

### **🧐 How to Identify Sliding Window Problems?**

1. **Look for substrings or subarrays** in the problem statement.
2. **The brute-force solution is `O(n²)`** but can be optimized to `O(n)`.
3. **"At most K", "exactly K", "longest/shortest"** often indicate a variable-size window.