# Prefix Sum

Priority: High
Status: Done

# ⚡ What is Prefix Sum?

It’s a **precomputed array** where each position `i` stores the **cumulative sum** of all elements from the start up to `i`.

For array:

```

nums = [3, 2, 7, 1, 8]

```

The prefix sum array:

```

prefix = [3, 5, 12, 13, 21]

```

- `prefix[0] = nums[0]`
- `prefix[1] = nums[0] + nums[1]`
- `prefix[2] = nums[0] + nums[1] + nums[2]`
- And so on…

---

# ❓ Why Use Prefix Sum?

✅ To compute **range sums** super fast

✅ Convert repeated work into **O(1)** lookups

✅ Helps in **sliding window** and **subarray sum** problems

✅ Often combined with **hashmaps** (for fast lookups)

## 2D Prefix Sum

### **1. Approach**

- **Precompute Prefix Sum:**prefix[i][j]=arr[i][j]+prefix[i−1][j]+prefix[i][j−1]−prefix[i−1][j−1]
    
    prefix[i][j]=arr[i][j]+prefix[i−1][j]+prefix[i][j−1]−prefix[i−1][j−1]\text{prefix}[i][j] = \text{arr}[i][j] + \text{prefix}[i-1][j] + \text{prefix}[i][j-1] - \text{prefix}[i-1][j-1]
    
- **Query Sum in O(1):**sum=prefix[r2][c2]−prefix[r1−1][c2]−prefix[r2][c1−1]+prefix[r1−1][c1−1]
    
    sum=prefix[r2][c2]−prefix[r1−1][c2]−prefix[r2][c1−1]+prefix[r1−1][c1−1]\text{sum} = \text{prefix}[r2][c2] - \text{prefix}[r1-1][c2] - \text{prefix}[r2][c1-1] + \text{prefix}[r1-1][c1-1]
    

---

### **2. Java Implementation**

```java
public class PrefixSum2D {

    private int[][] prefix;

    // Constructor to build prefix sum matrix
    public PrefixSum2D(int[][] matrix) {
        int rows = matrix.length;
        int cols = matrix[0].length;
        prefix = new int[rows][cols];

        // Compute prefix sum
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                prefix[i][j] = matrix[i][j];

                if (i > 0) prefix[i][j] += prefix[i - 1][j];
                if (j > 0) prefix[i][j] += prefix[i][j - 1];
                if (i > 0 && j > 0) prefix[i][j] -= prefix[i - 1][j - 1];
            }
        }
    }

    // Query sum of submatrix from (r1, c1) to (r2, c2)
    public int querySum(int r1, int c1, int r2, int c2) {
        int total = prefix[r2][c2];

        if (r1 > 0) total -= prefix[r1 - 1][c2];
        if (c1 > 0) total -= prefix[r2][c1 - 1];
        if (r1 > 0 && c1 > 0) total += prefix[r1 - 1][c1 - 1];

        return total;
    }

    // Main method to test the implementation
    public static void main(String[] args) {
        int[][] matrix = {
            {1, 2, 3},
            {4, 5, 6},
            {7, 8, 9}
        };

        PrefixSum2D ps = new PrefixSum2D(matrix);

        // Query sum from (1,1) to (2,2) → 5 + 6 + 8 + 9 = 28
        System.out.println(ps.querySum(1, 1, 2, 2)); // Output: 28
    }
}

```

---

### **3. Complexity Analysis**

- **Preprocessing Time:** O(N×M)
    
    O(N×M)O(N \times M)
    
- **Query Time:** O(1)
    
    O(1)O(1)
    
- **Space Complexity:** O(N×M) for the `prefix` array.
    
    O(N×M)O(N \times M)
    

# 📋 **LeetCode Prefix Sum Problem List (Difficulty Wise)**

---

## ✅ Easy Problems — Beginner Friendly

| # | Problem | Link |
| --- | --- | --- |
| 1480 | Running Sum of 1d Array | LeetCode 1480 |
| 724 | Find Pivot Index | LeetCode 724 |
| 303 | Range Sum Query - Immutable | LeetCode 303 |
| 1588 | Sum of All Odd Length Subarrays | LeetCode 1588 |

---

## ✅ Medium Problems — Real Patterns Start Here

| # | Problem | Link |
| --- | --- | --- |
| 560 | Subarray Sum Equals K | LeetCode 560 |
| 1248 | Count Number of Nice Subarrays | LeetCode 1248 |
| 974 | Subarray Sums Divisible by K | LeetCode 974 |
| 930 | Binary Subarrays With Sum | LeetCode 930 |
| 1314 | Matrix Block Sum (2D Prefix) | LeetCode 1314 |
| 523 | Continuous Subarray Sum | LeetCode 523 |
| 238 | Product of Array Except Self (Modified Prefix Product) | LeetCode 238 |
| 1074 | Number of Submatrices That Sum to Target | LeetCode 1074 |

---

## ✅ Hard Problems — FAANG-Level Challenges

| # | Problem | Link |
| --- | --- | --- |
| 992 | Subarrays with K Different Integers | LeetCode 992 |
| 1292 | Maximum Side Length of Square with Sum ≤ Threshold | LeetCode 1292 |
| 1031 | Maximum Sum of Two Non-Overlapping Subarrays | LeetCode 1031 |
| 1524 | Number of Subarrays With Odd Sum | LeetCode 1524 |
| 1746 | Maximum Subarray Sum After One Operation | LeetCode 1746 |
| 363 | Max Sum of Rectangle No Larger Than K (2D Prefix + Set) | LeetCode 363 |

### **Difference Array Concept**

A **Difference Array** is a technique used to efficiently perform multiple range update operations on an array in constant time O(1). It is particularly useful when performing **increment or decrement operations over a range of indices**.

---

## **1. Basic Idea**

Instead of directly modifying the original array for every update operation (which would be O( per update), we use a **difference array** where updates are made in constant time.

For an original array `arr[]` of size `N`, we construct a **difference array `diff[]`** where:

- `diff[i] = arr[i] - arr[i-1]` (for `i > 0`)
- `diff[0] = arr[0]`

Using `diff[]`, we can apply range updates efficiently.

---

## **2. Operations Using Difference Array**

### **(a) Range Increment Operation (O(1))**

To add `x` to all elements in the range `[l, r]`:

1. **Increment `diff[l]` by `x`** (starting point).
2. **Decrement `diff[r+1]` by `x`** (ending point).

### **(b) Reconstructing the Original Array (O(N))**

Once all updates are applied to `diff[]`, we compute the **prefix sum** to obtain the final array.

---

## **3. Example**

### **Without Difference Array (Naïve Approach) - O(N) per update**

```java
java
int[] arr = {10, 5, 20, 40};
int l = 1, r = 3, x = 5;  // Increase elements from index 1 to 3 by 5

for (int i = l; i <= r; i++) {
    arr[i] += x;
}

// arr[] becomes {10, 10, 25, 45}

```

**Problem:** If multiple updates are needed, this approach is inefficient.

---

### **With Difference Array (Efficient Approach) - O(1) per update**

### **Step 1: Construct the Difference Array**

For `arr[] = {10, 5, 20, 40}`, we create:

```
rust
CopyEdit
diff[0] = arr[0]
diff[i] = arr[i] - arr[i-1] (for i > 0)

```

So, `diff[]` becomes:

```
cpp
CopyEdit
diff[] = {10, -5, 15, 20, 0}  // Extra 0 to handle boundary case

```

### **Step 2: Apply the Range Update in O(1)**

To add `x = 5` to the range `[1,3]`:

```java
java
CopyEdit
diff[1] += 5;  // Increment start
diff[4] -= 5;  // Decrement after end

```

Updated `diff[]`:

```
CopyEdit
{10, 0, 15, 20, -5}

```

### **Step 3: Compute the Final Array (Prefix Sum)**

```java
java
CopyEdit
for (int i = 1; i < arr.length; i++) {
    arr[i] = arr[i - 1] + diff[i];
}

```

Final `arr[]` after updates:

```
CopyEdit
{10, 10, 25, 45}

```

---

## **4. Time Complexity**

- **Initialization of `diff[]`** → O(N)
    
    O(N)O(N)
    
- **Each Range Update** → O(1)
    
    O(1)O(1)
    
- **Final Array Reconstruction** → O(N)
    
    O(N)O(N)
    

Total complexity for multiple updates:

**O(N+U)O(N + U)O(N+U) where UUU is the number of updates** (better than O(N×U)O(N \times U)O(N×U) in the naïve approach).