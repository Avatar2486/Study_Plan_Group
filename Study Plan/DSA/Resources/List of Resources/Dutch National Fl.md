# Dutch National Fl

Priority: High
Status: Not started

## **Dutch National Flag Problem (FAANG-Level Preparation)**

The **Dutch National Flag Problem (DNFP)** is a classic problem that involves sorting an array with three distinct values efficiently. It was proposed by **Edsger W. Dijkstra** and is commonly asked in **FAANG** interviews to test a candidate’s **two-pointer technique** skills and **in-place sorting ability**.

---

## **Problem Statement**

Given an array `nums` containing `n` objects **colored red, white, or blue**, sort them in-place so that objects of the same color appear adjacent, in the order:

- **Red (0)**
- **White (1)**
- **Blue (2)**

Implement a function without using the in-built sorting function.

### **Example**

```java
java
CopyEdit
Input: nums = [2, 0, 2, 1, 1, 0]
Output: [0, 0, 1, 1, 2, 2]

```

### **Constraints**

- `1 <= nums.length <= 300`
- `nums[i]` is `0`, `1`, or `2`.

---

## **FAANG-Level Explanation (Two-Pointer Approach)**

The optimal way to solve the problem is using **three pointers**:

1. **low (left pointer)** → marks the boundary of `0s`
2. **mid (current pointer)** → iterates through the array
3. **high (right pointer)** → marks the boundary of `2s`

### **Algorithm (3-Way Partitioning)**

1. **Initialize:**
    - `low = 0`, `mid = 0`, `high = n - 1`
2. **Iterate while mid ≤ high**:
    - If `nums[mid] == 0`, swap `nums[low]` and `nums[mid]`, move both `low` and `mid` forward.
    - If `nums[mid] == 1`, move `mid` forward.
    - If `nums[mid] == 2`, swap `nums[mid]` and `nums[high]`, move `high` backward.

### **Dry Run**

### **Initial State**

```
makefile
CopyEdit
Index:      0  1  2  3  4  5
Array:      2  0  2  1  1  0
low=0, mid=0, high=5

```

| Step | nums[mid] | Action | Array State | low | mid | high |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | `2` | Swap `nums[mid]` and `nums[high]` | `[0, 0, 2, 1, 1, 2]` | 0 | 0 | 4 |
| 2 | `0` | Swap `nums[low]` and `nums[mid]`, move both | `[0, 0, 2, 1, 1, 2]` | 1 | 1 | 4 |
| 3 | `0` | Swap `nums[low]` and `nums[mid]`, move both | `[0, 0, 2, 1, 1, 2]` | 2 | 2 | 4 |
| 4 | `2` | Swap `nums[mid]` and `nums[high]` | `[0, 0, 1, 1, 2, 2]` | 2 | 2 | 3 |
| 5 | `1` | Move `mid` forward | `[0, 0, 1, 1, 2, 2]` | 2 | 3 | 3 |
| 6 | `1` | Move `mid` forward | `[0, 0, 1, 1, 2, 2]` | 2 | 4 | 3 |

**Final Output:** `[0, 0, 1, 1, 2, 2]` ✅

---

## **Code Implementation**

### **Java Solution**

```java
java
CopyEdit
class Solution {
    public void sortColors(int[] nums) {
        int low = 0, mid = 0, high = nums.length - 1;

        while (mid <= high) {
            if (nums[mid] == 0) {
                swap(nums, low++, mid++);
            } else if (nums[mid] == 1) {
                mid++;
            } else {
                swap(nums, mid, high--);
            }
        }
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}

```

### **Python Solution**

```python
python

def sortColors(nums):
    low, mid, high = 0, 0, len(nums) - 1

    while mid <= high:
        if nums[mid] == 0:
            nums[low], nums[mid] = nums[mid], nums[low]
            low += 1
            mid += 1
        elif nums[mid] == 1:
            mid += 1
        else:
            nums[mid], nums[high] = nums[high], nums[mid]
            high -= 1

# Example Usage
nums = [2, 0, 2, 1, 1, 0]
sortColors(nums)
print(nums)  # Output: [0, 0, 1, 1, 2, 2]

```

---

## **Difficulty-Wise Categorization**

1. **Easy**
    - **Sort an array of 0s, 1s, and 2s (DNFP)**
    - **Move all zeros to the end (or beginning)**
2. **Medium**
    - **Partition an array into three parts**
    - **Find missing positive integer**
    - **Sort an array with duplicate values in linear time**
    - **Sort colors in a linked list**
3. **Hard**
    - **Four Sum Problem (using 3-way partitioning)**
    - **Minimum swaps to sort an array**
    - **Partition problem in dynamic programming**
    - Wiggle Sort 2

---

## **Common Patterns in FAANG**

### **1. Two Pointers**

- Used in sorting, partitioning, and searching problems.
- Examples: **Three Sum, Container With Most Water, Valid Palindrome**

### **2. In-Place Sorting**

- Problems where you must sort without extra space.
- Examples: **Sort Colors, Wiggle Sort, Merge Sorted Arrays**

### **3. QuickSort & Partitioning**

- The **DNFP solution is a variation of the QuickSort partition step**.
- Examples: **Kth Largest Element, QuickSelect Algorithm**

### **4. Greedy Algorithms**

- Making local optimal choices to get a global solution.

---

## **FAANG-Level Follow-up Questions**

1. **Can you sort a larger range of numbers (e.g., 0-9) using a similar approach?**
2. **Can you modify the algorithm for sorting a linked list instead of an array?**
3. **What if you have k different colors instead of just 3?**
4. **How would you modify the algorithm to sort an array of negative, zero, and positive numbers?**
5. **How does this algorithm compare with Counting Sort and QuickSort?**
6. **Can you implement a recursive version of this algorithm?**

---

### **Key Takeaways**

✅ **Optimal approach:** **O(N) time, O(1) space**

✅ **Uses three pointers:** `low`, `mid`, `high`

✅ **Classic FAANG problem** testing **in-place sorting & two-pointer approach**

✅ **Variations appear in QuickSort, partitioning, and greedy algorithms**