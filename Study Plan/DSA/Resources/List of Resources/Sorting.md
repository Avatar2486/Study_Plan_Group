# Sorting

Priority: High
Status: Done

Perfect! Let's begin your **FAANG-level sorting prep in Java**, covering each algorithm deeply: core idea, time/space complexity, real-world use cases, Java code, and where it's useful in interviews or system design.

---

## 🔹 1. Bubble Sort

### 🔍 Concept

- Repeatedly swap adjacent elements if they are in the wrong order.
- Bubble the largest element to the end in each pass.

### ⏱️ Complexity

| Case | Time | Space |
| --- | --- | --- |
| Best | O(n) | O(1) |
| Avg | O(n²) | O(1) |
| Worst | O(n²) | O(1) |

### ✅ When to Use

- Teaching purposes.
- Small datasets.
- Rarely used in production.

### 👨‍💻 Java Code

```java
void bubbleSort(int[] arr) {
    boolean swapped;
    for (int i = 0; i < arr.length - 1; i++) {
        swapped = false;
        for (int j = 0; j < arr.length - 1 - i; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j]; arr[j] = arr[j + 1]; arr[j + 1] = temp;
                swapped = true;
            }
        }
        if (!swapped) break;
    }
}

```

---

## 🔹 2. Selection Sort

### 🔍 Concept

- Repeatedly find the **minimum element** from the unsorted part and place it at the beginning.

### ⏱️ Complexity

| Case | Time | Space |
| --- | --- | --- |
| All | O(n²) | O(1) |

### ✅ When to Use

- Simple implementation.
- Suitable when memory write operations are costly.

### 👨‍💻 Java Code

```java
void selectionSort(int[] arr) {
    for (int i = 0; i < arr.length - 1; i++) {
        int minIdx = i;
        for (int j = i + 1; j < arr.length; j++) {
            if (arr[j] < arr[minIdx]) minIdx = j;
        }
        int temp = arr[i]; arr[i] = arr[minIdx]; arr[minIdx] = temp;
    }
}

```

---

## 🔹 3. Insertion Sort

### 🔍 Concept

- Build the sorted array one item at a time by inserting elements into their correct position.

### ⏱️ Complexity

| Case | Time | Space |
| --- | --- | --- |
| Best | O(n) | O(1) |
| Avg | O(n²) | O(1) |
| Worst | O(n²) | O(1) |

### ✅ When to Use

- Small or nearly sorted datasets.
- Real-time systems where data is arriving in chunks.

### 👨‍💻 Java Code

```java
void insertionSort(int[] arr) {
    for (int i = 1; i < arr.length; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

```

---

## 🔹 4. Merge Sort

### 🔍 Concept

- Divide the array into halves, sort each half, and merge them.

### ⏱️ Complexity

| Case | Time | Space |
| --- | --- | --- |
| All | O(n log n) | O(n) |

### ✅ When to Use

- Stable sort needed.
- Linked lists or external sorting (large datasets).
- Always consistent performance.

### 👨‍💻 Java Code

```java
void mergeSort(int[] arr, int left, int right) {
    if (left < right) {
        int mid = (left + right) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}

void merge(int[] arr, int l, int m, int r) {
    int[] left = Arrays.copyOfRange(arr, l, m + 1);
    int[] right = Arrays.copyOfRange(arr, m + 1, r + 1);
    int i = 0, j = 0, k = l;
    while (i < left.length && j < right.length)
        arr[k++] = (left[i] <= right[j]) ? left[i++] : right[j++];
    while (i < left.length) arr[k++] = left[i++];
    while (j < right.length) arr[k++] = right[j++];
}

```

---

## 🔹 5. Quick Sort

### 🔍 Concept

- Choose a pivot, partition array such that left < pivot < right, and recursively sort both halves.

### ⏱️ Complexity

| Case | Time | Space |
| --- | --- | --- |
| Best | O(n log n) | O(log n) |
| Avg | O(n log n) | O(log n) |
| Worst | O(n²) | O(log n) (with tail recursion) |

### ✅ When to Use

- In-place and fast average case.
- Default in many languages (`Arrays.sort()` in Java uses dual-pivot quicksort for primitives).

### 👨‍💻 Java Code

```java
void quickSort(int[] arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

int partition(int[] arr, int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            int temp = arr[i]; arr[i] = arr[j]; arr[j] = temp;
        }
    }
    int temp = arr[i + 1]; arr[i + 1] = arr[high]; arr[high] = temp;
    return i + 1;
}

```

---

## 🔹 6. Counting Sort

### 🔍 Concept

- Count frequency of elements and use it to place them in correct order.

### ⏱️ Complexity

| Case | Time | Space |
| --- | --- | --- |
| All | O(n + k) | O(k) where k = range of input |

### ✅ When to Use

- Elements in a **small range**, non-negative integers.
- Linear sort when k ≪ n².

### 👨‍💻 Java Code

```java
void countingSort(int[] arr) {
    int max = Arrays.stream(arr).max().getAsInt();
    int[] count = new int[max + 1];
    for (int num : arr) count[num]++;
    int index = 0;
    for (int i = 0; i < count.length; i++) {
        while (count[i]-- > 0) arr[index++] = i;
    }
}

```

---

## 🔹 7. Bucket Sort

### 🔍 Concept

- Divide data into **buckets**, sort each bucket individually, and concatenate.

### ⏱️ Complexity

| Case | Time | Space |
| --- | --- | --- |
| Avg | O(n + k) | O(n + k) |
| Worst | O(n²) | O(n + k) |

### ✅ When to Use

- Uniformly distributed floating-point numbers in range `[0,1)` or fixed range.
- Visual algorithms, histograms.

### 👨‍💻 Java Code

```java
import java.util.*;

public class BucketSort {
    public static void bucketSort(float[] arr) {
        int n = arr.length;
        if (n <= 0) return;

        // 1. Create n empty buckets
        @SuppressWarnings("unchecked")
        List<Float>[] buckets = new ArrayList[n];
        for (int i = 0; i < n; i++) {
            buckets[i] = new ArrayList<>();
        }

        // 2. Put array elements in different buckets
        for (int i = 0; i < n; i++) {
            int bucketIndex = (int) (arr[i] * n); // index in range [0, n-1]
            buckets[bucketIndex].add(arr[i]);
        }

        // 3. Sort individual buckets
        for (List<Float> bucket : buckets) {
            Collections.sort(bucket);
        }

        // 4. Concatenate all buckets into arr[]
        int index = 0;
        for (List<Float> bucket : buckets) {
            for (float value : bucket) {
                arr[index++] = value;
            }
        }
    }

    public static void main(String[] args) {
        float[] arr = {0.897f, 0.565f, 0.656f, 0.1234f, 0.665f, 0.3434f};
        System.out.println("Original array: " + Arrays.toString(arr));
        bucketSort(arr);
        System.out.println("Sorted array:   " + Arrays.toString(arr));
    }
}

```

---