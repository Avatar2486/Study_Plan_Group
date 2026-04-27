# Binary Search

Priority: High
Status: Done

[https://leetcode.com/discuss/post/2371234/an-opinionated-guide-to-binary-search-co-1yfw/](https://leetcode.com/discuss/post/2371234/an-opinionated-guide-to-binary-search-co-1yfw/)

---

## 🧠 Core Concept of Binary Search

Binary Search is an efficient **O(log n)** algorithm to find an element in a **sorted** array by repeatedly dividing the search interval in half.

### ✅ Key Requirements:

- Input must be **sorted**
- Works on **monotonic** functions (increasing/decreasing or bitonic)

---

## 🧱 Binary Search - Common Code Template (Java)

```java
int binarySearch(int[] nums, int target) {
    int left = 0, right = nums.length - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;  // Safe mid to avoid overflow

        if (nums[mid] == target)
            return mid;
        else if (nums[mid] < target)
            left = mid + 1;
        else
            right = mid - 1;
    }
    return -1;  // Not found
}

```

---

## 🧮 Variants of Mid Calculation

| Variant | Code | When to Use |
| --- | --- | --- |
| `mid = (l + r) / 2` | ✅ Simple, but may overflow | Small numbers only |
| `mid = l + (r - l) / 2` | ✅ Safe for large `l` and `r` | Preferred everywhere |
| `mid = (l + r + 1) / 2` | ✅ Bias towards right | Use in upper bound patterns |

---

## 🔍 Lower Bound vs Upper Bound

### 🔽 Lower Bound

- First index where element is **greater than or equal to target**
- Also works for **first occurrence**

```java
int lowerBound(int[] nums, int target) {
    int l = 0, r = nums.length;
    while (l < r) {
        int mid = l + (r - l) / 2;
        if (nums[mid] < target)
            l = mid + 1;
        else
            r = mid;
    }
    return l;
}

```

---

### 🔼 Upper Bound

- First index where element is **greater than target**

```java
int upperBound(int[] nums, int target) {
    int l = 0, r = nums.length;
    while (l < r) {
        int mid = l + (r - l) / 2;
        if (nums[mid] <= target)
            l = mid + 1;
        else
            r = mid;
    }
    return l;
}

```

---

## 🔁 Common Binary Search Patterns

| Pattern | Use Case Example |
| --- | --- |
| Exact match | Classic binary search |
| Lower bound (first ≥ target) | First occurrence, search insert position |
| Upper bound (first > target) | Count of target elements, range queries |
| Search in rotated sorted array | [4,5,6,7,0,1,2] |
| Find min/max value satisfying condition | Binary Search on answer (e.g., minimum capacity) |
| Binary Search in 2D matrix | Treat matrix as flattened sorted array |
| Infinite Array | Expanding bounds then applying binary search |

---

## 🧪 FAANG-Level LeetCode Practice

### 🟢 Easy

- [704. Binary Search](https://leetcode.com/problems/binary-search/)
- [35. Search Insert Position](https://leetcode.com/problems/search-insert-position/)
- [852. Peak Index in a Mountain Array](https://leetcode.com/problems/peak-index-in-a-mountain-array/)
- [278. First Bad Version](https://leetcode.com/problems/first-bad-version/) — ✅ Lower Bound

---

### 🟡 Medium

- [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
- [34. Find First and Last Position](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) — ✅ Lower/Upper Bound
- [162. Find Peak Element](https://leetcode.com/problems/find-peak-element/)
- [875. Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) — ✅ Binary Search on Answer
- [410. Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/) — ✅ Binary Search on Answer
- [287. Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/) — ✅ Binary Search with Count
- [240. Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/)

---

### 🔴 Hard

- [4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)
- [668. Kth Smallest Number in Multiplication Table](https://leetcode.com/problems/kth-smallest-number-in-multiplication-table/)
- [154. Find Minimum in Rotated Sorted Array II](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/)
- [1231. Divide Chocolate](https://leetcode.com/problems/divide-chocolate/)
- [1901. Find a Peak Element II](https://leetcode.com/problems/find-a-peak-element-ii/) — ✅ 2D Binary Search

---

## 🔁 Summary of Code Patterns

```java
// 1. Standard Binary Search
while (left <= right) {
    int mid = left + (right - left) / 2;
    if (nums[mid] == target) return mid;
    else if (nums[mid] < target) left = mid + 1;
    else right = mid - 1;
}

// 2. Lower Bound
while (left < right) {
    int mid = left + (right - left) / 2;
    if (nums[mid] < target) left = mid + 1;
    else right = mid;
}

// 3. Upper Bound
while (left < right) {
    int mid = left + (right - left) / 2;
    if (nums[mid] <= target) left = mid + 1;
    else right = mid;
}

```

---

**Binary Search on Answer Space**, often called **“Parametric Search”**. This is a *powerful technique* frequently used in **FAANG interviews**, especially in optimization-type problems.

---

## 🔍 What Is "Binary Search on Answer"?

Unlike traditional binary search on **sorted arrays**, here you:

- Search in a **range of values**, e.g., speeds, capacities, distances, times.
- Each value in that range is **not stored in the array**.
- For a given value (mid), you use a **predicate function** (`can(mid)` or `isValid(mid)`) to **simulate or validate** a condition.

---

## 💡 Core Template in Java

```java
int left = MIN_POSSIBLE; // start of the answer space
int right = MAX_POSSIBLE; // end of the answer space
int answer = -1;

while (left <= right) {
    int mid = left + (right - left) / 2;

    if (isValid(mid)) {
        answer = mid;
        right = mid - 1; // try to find smaller/better
    } else {
        left = mid + 1; // need bigger value
    }
}
return answer;

```

Sometimes for maximization, you'd do:

```java
if (isValid(mid)) {
    answer = mid;
    left = mid + 1; // try bigger
} else {
    right = mid - 1;
}

```

---

## 🤯 But... How Do I Know to Use This?

Ask yourself:

> "Am I looking for a minimum/maximum value that satisfies a constraint?"
> 

If yes, use this.

---

## 🔄 Real World Example

### 🧪 Problem: Koko Eating Bananas

> You’re given an array of banana piles. Koko eats bananas at speed k per hour. You must find the minimum speed k such that she finishes all piles in h hours.
> 

### ➤ Why Binary Search on Answer?

- We’re not searching for a pile.
- We're looking for the **smallest possible `k`** that satisfies:
    
    > totalHours(k) <= h
    > 
- You **simulate the condition** in a helper function (`isValid()`).

---

## 🧱 Break Down the Steps

### Step 1: Identify the Search Space

- `left = 1` (slowest possible speed)
- `right = max(piles)` (fastest — one pile per hour)

---

### Step 2: Design the `isValid(mid)` Function

```java
boolean isValid(int speed) {
    int hours = 0;
    for (int pile : piles) {
        hours += Math.ceil((double)pile / speed);
    }
    return hours <= h;
}

```

---

## 🔁 Common Variants You’ll See

| Pattern Type | Description |
| --- | --- |
| **Minimize the maximum** | Ship capacity, max workload, divide chocolate |
| **Maximize the minimum** | Magnetic force, distance between elements |
| **Minimize a value with conditions** | Smallest divisor, fastest speed |
| **Exact time/resource optimization** | Minimum time to make products or tasks |
| **2D parametric (harder)** | Gas stations, matrix peaks |

---

## 🚦 Two Binary Search Variants

| Use Case | Logic Flow |
| --- | --- |
| **Minimize possible answer** | If `isValid(mid)` → try left |
| **Maximize possible answer** | If `isValid(mid)` → try right |

---

## 🎯 Key Questions to Ask During Interviews

1. Can I simulate/validate a condition for a given number?
2. Can the answer space be bounded (`[low, high]`)?
3. Is the predicate **monotonic**? (if `mid` is valid, then all larger or smaller values are also valid)

If yes, then you can **Binary Search the Answer**.

---

## 🧠 Intuition Builder

Let’s compare two problems:

### ✅ Traditional Binary Search:

```java
Find target in sorted array.

```

Search **on the array**.

---

### ✅ Binary Search on Answer:

```java
Find minimum ship capacity to deliver in D days.

```

Search **on a value not in the array**, validate it via a simulation.

---

## 🏁 Summary Table

| Feature | Traditional BS | BS on Answer |
| --- | --- | --- |
| Searching over | Indices / Elements | Value range (answer space) |
| Needs sorted input? | ✅ Yes | ❌ No |
| Predicate used? | ❌ No | ✅ Yes |
| Output | Index/value | Best possible value |
| Use case | Search/Existence | Optimization |

---

Would you like to deep dive into one problem (like Koko, Shipping Packages, or Divide Chocolate) next with full Java code and dry run?

For each problem, try asking yourself:

> “If I guess a number, can I write a helper function that tells me whether it satisfies the conditions?”
> 

If yes → you can binary search over that number range.

### 🟢 Easy–Medium

1. **875. Koko Eating Bananas**
2. **1011. Capacity To Ship Packages Within D Days**
3. **1283. Find the Smallest Divisor Given a Threshold**

---

### 🟡 Medium

1. **1482. Minimum Number of Days to Make m Bouquets**
2. **1552. Magnetic Force Between Two Balls**
3. **1870. Minimum Speed to Arrive on Time**
4. **2064. Minimized Maximum of Products Distributed to Any Store**

---

### 🔴 Hard

1. **774. Minimize Max Distance to Gas Station**
2. **410. Split Array Largest Sum**
3. **1231. Divide Chocolate**
4. **1901. Find a Peak Element II (2D)**