# Two Pointers

Priority: High
Status: Done

## **Two Pointer Technique – FAANG-Level Explanation**

The **Two Pointer** technique is a powerful algorithmic approach that uses two indices (pointers) to traverse data structures like arrays and linked lists efficiently. This technique helps solve problems involving searching, sorting, and partitioning in an optimized manner, often reducing **O(N²) complexity to O(N) or O(N log N)**.

---

## **Types of Two Pointer Approaches**

1. **Opposite Direction (Left-Right)** → One pointer starts from the left and another from the right.
    - Used in **sorted** arrays for problems like finding pairs with a given sum.
2. **Same Direction (Sliding Window)** → Both pointers move in the same direction.
    - Used for **subarray** or **substring** problems, like finding the longest subarray with a condition.
3. **Fast-Slow Pointers (Floyd’s Cycle Detection)** → One pointer moves faster than the other.
    - Used in **linked lists** and **cycle detection** problems.

---

## **Step-by-Step Guide to Using the Two Pointer Technique**

1. **Understand the Problem Statement**
    - Identify if sorting or searching is involved.
    - Check if the problem requires finding pairs, triplets, or subarrays.
2. **Choose the Type of Two Pointer Approach**
    - If the array is **sorted**, try the **opposite direction** approach.
    - If the problem requires tracking a range, try the **sliding window** method.
    - If working with a linked list, try **fast and slow pointers**.
3. **Initialize the Pointers**
    - Decide where to place the pointers initially (start, end, or both at the beginning).
4. **Move the Pointers Efficiently**
    - Define conditions to move one or both pointers.
    - Optimize to avoid redundant calculations.
5. **Optimize with Sorting or Hashing (if needed)**
    - Sorting can help reduce the problem to O(N log N).
    - Hashing can be an alternative to two pointers in some cases.

---

## **Common Tricks and Tips**

✅ **Use Sorting First**: If the array is unsorted and involves pair or triplet problems, **sort it first** to use the two-pointer technique efficiently.

✅ **Avoid Nested Loops**: Instead of `O(N²)`, aim for `O(N log N)` or `O(N)`.

✅ **Check Edge Cases**: Consider empty arrays, arrays with all elements the same, and negative numbers.

✅ **Sliding Window for Continuous Problems**: Use this when working with subarrays or substrings where the sum, count, or length matters.

✅ **Fast-Slow Pointer for Cycles**: Use this when detecting cycles in a linked list or finding the middle node.

✅ **Two Pointers Work Best on Sorted Data**: If the array isn’t sorted, check if sorting is possible without affecting the problem constraints.

---

## **Practice Questions – Categorized**

### **Easy**

1. **Pair Sum in Sorted Array** → Find two numbers in a sorted array that add up to a given target.
    
    **(Leetcode 167: Two Sum II - Input Array Is Sorted)**
    
2. **Move Zeros to End** → Move all zeros to the end while maintaining relative order.
    
    **(Leetcode 283: Move Zeroes)**
    
3. **Reverse a String using Two Pointers**
    
    **(Leetcode 344: Reverse String)**
    

### **Medium**

1. **3Sum Problem** → Find triplets that sum to zero.
    
    **(Leetcode 15: 3Sum)**
    
2. **Container With Most Water** → Find two heights that form the largest container.
    
    **(Leetcode 11: Container With Most Water)**
    
3. **Longest Substring Without Repeating Characters** → Use the sliding window technique.
    
    **(Leetcode 3: Longest Substring Without Repeating Characters)**
    
4. **Find the Middle of a Linked List** → Fast and slow pointer approach.
    
    **(Leetcode 876: Middle of the Linked List)**
    

### **Hard**

1. **Trapping Rain Water** → Find the amount of water trapped between heights.
    
    **(Leetcode 42: Trapping Rain Water)**
    
2. **Sliding Window Maximum** → Find the maximum in each window of size `k`.
    
    **(Leetcode 239: Sliding Window Maximum)**
    
3. **Merge K Sorted Lists** → Use the two-pointer method along with heaps.
    
    **(Leetcode 23: Merge k Sorted Lists)**
    

## **Common Patterns of Two Pointers** 🚀

The **Two Pointer technique** is a powerful and efficient approach used in many algorithmic problems. Below are the most common patterns categorized based on their usage and problem types.

---

## **1️⃣ Opposite Direction (Left-Right)**

### 🔹 **Pattern**

- One pointer starts at the **beginning** (`left`), and the other starts at the **end** (`right`).
- Move them toward each other based on conditions.

### 🔹 **When to Use?**

- Problems involving **sorted arrays** where you need to find pairs or triplets.
- Problems related to **finding a target sum** or **valid subarrays**.

### 🔹 **Common Problems**

1. **Pair Sum in Sorted Array** → **(Leetcode 167: Two Sum II)**
2. **Find if a Palindrome Exists** → **(Leetcode 125: Valid Palindrome)**
3. **Container with Most Water** → **(Leetcode 11)**
4. **Trapping Rain Water (Two Pointer Approach)** → **(Leetcode 42)**

### 🔹 **Example**

```java
java
CopyEdit
// Find if there exists a pair (arr[i], arr[j]) such that arr[i] + arr[j] = target
public boolean twoSumSorted(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    while (left < right) {
        int sum = arr[left] + arr[right];
        if (sum == target) return true;
        else if (sum < target) left++;
        else right--;
    }
    return false;
}

```

---

## **2️⃣ Sliding Window (Same Direction)**

### 🔹 **Pattern**

- Both pointers start from the **beginning**, one expands while the other contracts.
- Used for problems that require **tracking a range** or **subarray properties**.

### 🔹 **When to Use?**

- **Subarray problems**, longest/shortest subarray constraints.
- **Variable size window** problems.
- **Sum-based or distinct elements problems**.

### 🔹 **Common Problems**

1. **Longest Substring Without Repeating Characters** → **(Leetcode 3)**
2. **Minimum Size Subarray Sum** → **(Leetcode 209)**
3. **Sliding Window Maximum** → **(Leetcode 239)**
4. **Longest Repeating Character Replacement** → **(Leetcode 424)**

### 🔹 **Example**

```java
java
CopyEdit
// Find the longest substring without repeating characters
public int lengthOfLongestSubstring(String s) {
    Set<Character> set = new HashSet<>();
    int left = 0, maxLength = 0;
    for (int right = 0; right < s.length(); right++) {
        while (set.contains(s.charAt(right))) {
            set.remove(s.charAt(left++));
        }
        set.add(s.charAt(right));
        maxLength = Math.max(maxLength, right - left + 1);
    }
    return maxLength;
}

```

---

## **3️⃣ Fast-Slow Pointers (Tortoise & Hare)**

### 🔹 **Pattern**

- One pointer moves **1 step**, while the other moves **2 steps**.
- Used to detect cycles or find middle nodes.

### 🔹 **When to Use?**

- **Cycle detection in linked lists** (Floyd’s Algorithm).
- **Finding the middle node of a linked list**.
- **Detecting cycle in a graph**.

### 🔹 **Common Problems**

1. **Detect Cycle in a Linked List** → **(Leetcode 141)**
2. **Find Middle of Linked List** → **(Leetcode 876)**
3. **Find Start of Cycle in Linked List** → **(Leetcode 142)**

### 🔹 **Example**

```java
java
CopyEdit
// Detect if a linked list has a cycle
public boolean hasCycle(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) return true;
    }
    return false;
}

```

---

## **4️⃣ Merging Two Sorted Lists (Merge Pattern)**

### 🔹 **Pattern**

- Two pointers traverse two sorted lists or arrays.
- Used in **merge sort**, **sorted array intersection**, etc.

### 🔹 **When to Use?**

- **Merging sorted lists** efficiently.
- **Finding common elements between two sorted arrays**.

### 🔹 **Common Problems**

1. **Merge Two Sorted Lists** → **(Leetcode 21)**
2. **Intersection of Two Sorted Arrays** → **(Leetcode 349)**
3. **Median of Two Sorted Arrays** → **(Leetcode 4)**

### 🔹 **Example**

```java
java
CopyEdit
// Merge two sorted linked lists
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0), current = dummy;
    while (l1 != null && l2 != null) {
        if (l1.val < l2.val) {
            current.next = l1;
            l1 = l1.next;
        } else {
            current.next = l2;
            l2 = l2.next;
        }
        current = current.next;
    }
    current.next = (l1 != null) ? l1 : l2;
    return dummy.next;
}

```

---

## **5️⃣ K-Sum (Expanding Two Pointer)**

### 🔹 **Pattern**

- An extension of **Two Sum** where you look for **K numbers** that sum to a target.
- Reduce the problem using **sorting** and **recursion**.

### 🔹 **When to Use?**

- **3Sum, 4Sum, or KSum** problems.
- **Optimizing brute force solutions**.

### 🔹 **Common Problems**

1. **3Sum (Triplets with Zero Sum)** → **(Leetcode 15)**
2. **4Sum** → **(Leetcode 18)**

### 🔹 **Example**

```java
java
CopyEdit
// Find all unique triplets that sum up to zero
public List<List<Integer>> threeSum(int[] nums) {
    Arrays.sort(nums);
    List<List<Integer>> result = new ArrayList<>();
    for (int i = 0; i < nums.length - 2; i++) {
        if (i > 0 && nums[i] == nums[i - 1]) continue;  // Avoid duplicates
        int left = i + 1, right = nums.length - 1;
        while (left < right) {
            int sum = nums[i] + nums[left] + nums[right];
            if (sum == 0) {
                result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                while (left < right && nums[left] == nums[left + 1]) left++;
                while (left < right && nums[right] == nums[right - 1]) right--;
                left++; right--;
            } else if (sum < 0) left++;
            else right--;
        }
    }
    return result;
}

```

---

## **Back-to-Back Pointers (Bidirectional Expansion)**

### 🔹 **Pattern**

- Starts at a **center point** and expands outward in both directions.
- Useful for **finding palindromes, expanding substrings, and range problems**.

### 🔹 **When to Use?**

- **Checking for palindromes**.
- **Expanding substrings** from a center.
- Problems where you **expand in both directions**.

### 🔹 **Common Problems**

1. **Longest Palindromic Substring** → **(Leetcode 5)**
2. **Expand Around Center for Palindromes** → **(Leetcode 647)**
3. **Find the Largest Balanced Substring** → **(Interview Variation: Longest Substring of Balanced Parentheses)**

## **💡 Summary of Two Pointer Patterns**

| **Pattern** | **Best Used For** | **Common Problems** |
| --- | --- | --- |
| **Opposite Direction** | Sorted arrays, sum pairs | Two Sum, 3Sum, Container with Most Water |
| **Sliding Window** | Subarrays, substrings | Longest Substring, Minimum Window Substring |
| **Fast-Slow Pointers** | Cycle detection, middle element | Linked List Cycle, Find Middle of Linked List |
| **Merge Two Lists** | Merging sorted arrays or lists | Merge Sorted Lists, Intersection of Arrays |
| **K-Sum (Expanding)** | Finding multiple numbers that sum to a target | 3Sum, 4Sum |