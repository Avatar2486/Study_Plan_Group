# Kadane

Priority: High
Status: Done

---

# 🔥 Kadane’s Algorithm - Full Guide for FAANG Preparation

## 📌 Core Concept

### What is Kadane’s Algorithm?

Kadane’s Algorithm is used to find the **maximum sum subarray** in **O(n)** time. This is a classic **Dynamic Programming** problem but simplified into a greedy approach.

---

## 💡 Key Idea

At each index, you have two options:

1. **Extend the previous subarray** by including the current element.
2. **Start a new subarray** starting from the current element.

The goal is to **maximize the sum** at each step.

The final answer will be the **maximum sum encountered across all indices**.

---

## 🔥 Formula

Let:

- `arr[i]` = current element
- `currSum` = maximum sum ending at index `i`
- `maxSum` = maximum sum found so far

**Recurrence relation (Greedy Decision):**

`currSum = max(arr[i], currSum + arr[i])`

`maxSum = max(maxSum, currSum)`

---

# ⚡️ FAANG-Level Tips & Tricks

### ✅ Tip 1: Initialization

Start with:

- `currSum = arr[0]` (subarray starts at index 0)
- `maxSum = arr[0]` (maximum sum starts with first element)

---

### ✅ Tip 2: Handle Negative Arrays

If the array contains only negative numbers, Kadane will still work but `maxSum` will be the **largest negative number**.

---

### ✅ Tip 3: Finding Subarray (not just max sum)

If asked to **return the subarray** itself, you can maintain:

- **start index**
- **end index**

Whenever you reset `currSum` (start new subarray), update the `start` index.

---

### ✅ Tip 4: Variants of Kadane

FAANG often asks **Kadane variations** — some popular ones:

| Variation | Example |
| --- | --- |
| 1D Max Sum Subarray | Standard Kadane |
| 2D Max Sum Submatrix | Apply Kadane row-wise |
| Circular Array Max Sum | Modify Kadane to handle wrap-around |
| Min Sum Subarray | Flip sign and use Kadane |
| K-Concat Max Sum | Concatenate array and apply Kadane |
| Maximum Product Subarray | Trick: Track both max and min product |

---

### ✅ Tip 5: Kadane Patterns

Some typical **question patterns** that scream "Kadane":

1. **Maximum sum subarray**
2. **Profit optimization** (stock prices with no limits on transactions)
3. **Maximum sum after one deletion** (modified Kadane with "skip 1 element")
4. **Circular maximum sum** (wrap-around arrays)
5. **Min sum subarray** (negative Kadane)

---

# 💎 Patterns in Questions (How to Identify Kadane)

| Pattern | Example Problem |
| --- | --- |
| Max Sum Subarray | [Leetcode 53](https://leetcode.com/problems/maximum-subarray/) |
| Min Sum Subarray | Flip signs & Kadane |
| 2D Grid Max Sum | Kadane applied per row/col |
| Circular Array | [Leetcode 918](https://leetcode.com/problems/maximum-sum-circular-subarray/) |
| Maximum Product Subarray | [Leetcode 152](https://leetcode.com/problems/maximum-product-subarray/) |

---

# 📊 Difficulty-Wise Problem List

### 🔰 Easy

| Problem | Type |
| --- | --- |
| Maximum Subarray (LC 53) | Basic Kadane |
| Find Largest Contiguous Sum | Classic |
| Maximum Subarray (Negative Numbers) | Edge case handling |

---

### ⚙️ Medium

| Problem | Type |
| --- | --- |
| Maximum Sum Circular Subarray (LC 918) | Circular Kadane |
| Maximum Product Subarray (LC 152) | Product Variant |
| Maximum Sum after One Deletion (LC 1186) | Modified Kadane |
| Maximum Subarray with At Most K Deletions | Variant |

---

### 🔥 Hard

| Problem | Type |
| --- | --- |
| K-Concatenation Maximum Sum (LC 1191) | Extended Kadane |
| Maximum Sum Rectangle in 2D Matrix (GFG) | 2D Kadane |
| Maximum Alternating Subarray Sum | Modified Rules |
| Maximum Sum of Non-Adjacent Subarrays | Combination of Kadane & DP |

---

# 🚀 Pro-Level Insights

### ✨ Finding Patterns in Questions

If the problem asks for:

- **Maximum contiguous sum** → Think **Kadane** directly.
- **Maximum contiguous product** → Similar, but track both max and min (because of negatives).
- **Circular Array or Wrapping Allowed** → Modified Kadane.
- **Array allowed to delete/skip 1 element** → Modified Kadane with special case handling.

---

# 📝 Template Code (Core Kadane)

```java
public int maxSubArray(int[] nums) {
    int currSum = nums[0];
    int maxSum = nums[0];

    for (int i = 1; i < nums.length; i++) {
        currSum = Math.max(nums[i], currSum + nums[i]);
        maxSum = Math.max(maxSum, currSum);
    }

    return maxSum;
}

```

---

# 🧵 Template Code (Kadane + Start/End Subarray Indices)

```java
public int[] maxSubArrayWithIndices(int[] nums) {
    int currSum = nums[0];
    int maxSum = nums[0];
    int start = 0, end = 0, tempStart = 0;

    for (int i = 1; i < nums.length; i++) {
        if (nums[i] > currSum + nums[i]) {
            currSum = nums[i];
            tempStart = i;   // start new subarray
        } else {
            currSum += nums[i];
        }

        if (currSum > maxSum) {
            maxSum = currSum;
            start = tempStart;
            end = i;   // update final range
        }
    }
    return new int[]{maxSum, start, end};
}

```

---

```jsx
class Solution {
    public int maxSumRectangle(int[][] matrix, int R, int C) {
        int maxSum = Integer.MIN_VALUE;

        // Fix top and bottom rows
        for (int top = 0; top < R; top++) {
            int[] temp = new int[C]; // column-compressed array

            for (int bottom = top; bottom < R; bottom++) {
                // Add current row's values to each column
                for (int col = 0; col < C; col++) {
                    temp[col] += matrix[bottom][col];
                }

                // Run Kadane on the compressed columns
                int currentMax = kadane(temp);
                maxSum = Math.max(maxSum, currentMax);
            }
        }

        return maxSum;
    }

    private int kadane(int[] arr) {
        int maxSoFar = arr[0], currMax = arr[0];
        for (int i = 1; i < arr.length; i++) {
            currMax = Math.max(arr[i], currMax + arr[i]);
            maxSoFar = Math.max(maxSoFar, currMax);
        }
        return maxSoFar;
    }

    public static void main(String[] args) {
        Solution sol = new Solution();
        int[][] matrix = {
            {1, 2, -1, -4, -20},
            {-8, -3, 4, 2, 1},
            {3, 8, 10, 1, 3},
            {-4, -1, 1, 7, -6}
        };
        System.out.println(sol.maxSumRectangle(matrix, 4, 5)); // Output: 29
    }
}

```

# 📚 Practice Set (Must-Solve)

| Platform | Problems |
| --- | --- |
| Leetcode | 53, 152, 918, 1191, 1186 |
| GFG | Max Sum Rectangle |
| Codeforces | Maximum Subarray Sum (with modification rules) |
| InterviewBit | Max Sum Subarray |

---

# 💯 Final Checklist for FAANG

✅ Understand basic Kadane (core logic)

✅ Handle all variants (circular, product, deletion allowed, 2D)

✅ Practice subarray extraction (start, end)

✅ Study negative array edge case

✅ Be ready to modify logic for any twist (sum becomes product, allow deletion, etc.)

---

| Problem | Platform | Category | Link |
| --- | --- | --- | --- |
| Maximum Subarray | Leetcode 53 | Classic Kadane | Link |
| Maximum Product Subarray | Leetcode 152 | Product Variant | Link |
| Maximum Sum Circular Subarray | Leetcode 918 | Circular Array | Link |
| Maximum Sum After One Deletion | Leetcode 1186 | Modified Kadane | Link |
| K-Concatenation Maximum Sum | Leetcode 1191 | Extended Array | Link |
| Maximum Sum Rectangle in 2D Matrix | GFG | 2D Kadane | Link |
| Minimum Sum Subarray | Flip Kadane | Min Sum Variant | Implement on your own |
| Maximum Alternating Subarray Sum | Codeforces/GFG | Modified Kadane | Example |
| Longest Subarray with Sum <= k | InterviewBit | Sliding + Kadane | Link |
| Largest Sum Contiguous Subarray with At Most One Inversion | Custom | Twisted Kadane | I’ll draft if needed |
| Maximum Subarray Sum after Splitting into K Parts | Hard | Segment+Kadane | Ask me if needed |
| Maximum Sum Subarray with Exclusion (skip 1 or more) | Hard | Deletion Kadane | Custom — I can explain |
| Sum of Subarrays | LC 1508 | Sum over All Subarrays | Link |
| Maximum Length Subarray with Sum K | GFG | HashMap + Kadane | Link |
| Count Subarrays with Maximum Sum | Hard | Counting Variation | I can draft this too |