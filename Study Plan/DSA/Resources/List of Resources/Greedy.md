# Greedy

Priority: High
Status: Not started

All greedy patterns:

| Category | Subtopics Covered |
| --- | --- |
| Basic Greedy | Sorting, Ratios, Coverage, Jumping |
| Intervals | Merging, Scheduling, Covering, Insertion [https://medium.com/@timpark0807/leetcode-is-easy-the-interval-pattern-d68a7c1c841](https://medium.com/@timpark0807/leetcode-is-easy-the-interval-pattern-d68a7c1c841) |
| Line Sweep | Events, Count Overlaps, Skyline |
| Heap-based | Job/Course Scheduling, Resource Tracking |
| Game Theory | Stones, Pick Wner |

---

# 1. Basic Greedy — In Depth

## 1.1 Sorting Based Greedy

### What is it?

Sorting based greedy means **sorting the input data by some key (usually ascending or descending)** and then making decisions **in one pass**, assuming that the order helps make locally optimal choices that lead to global optimum.

### Why does it work?

Because the problem has an **optimal substructure** where sorting helps expose the natural order of picking elements. For example:

- Scheduling intervals by earliest finishing time ensures maximum non-overlapping intervals.
- Assigning cookies sorted by size ensures each child can get the smallest cookie possible.

### How to approach?

1. Identify the property to sort by (deadline, start time, value).
2. Sort the array/list based on that property.
3. Traverse once and make greedy decisions:
    - Accept/reject
    - Update counters or pointers

### Example: Assign Cookies (LeetCode 455)

**Problem**: Given arrays `g` (children's greed factors) and `s` (cookie sizes), assign cookies to maximize children satisfied (`cookie >= greed`).

**Why greedy?** Sort both arrays ascending. Give smallest cookie to least greedy child. If cookie fits, assign and move to next child and cookie.

### Code (Java):

```java
public int findContentChildren(int[] g, int[] s) {
    Arrays.sort(g);
    Arrays.sort(s);
    int i = 0, j = 0; // i for children, j for cookies
    while (i < g.length && j < s.length) {
        if (s[j] >= g[i]) {
            i++;
        }
        j++;
    }
    return i;
}

```

---

## 1.2 Ratio-Based Greedy

### What is it?

Used in problems where items have **two parameters** (e.g., value and weight), and the goal is to maximize value with a constraint (like capacity). You sort by **value/weight ratio** and pick items with the highest ratio first.

### Why does it work?

Taking items with the best value per unit weight maximizes total value if fractional picks are allowed (fractional knapsack).

### How to approach?

1. Compute ratio for each item.
2. Sort items by decreasing ratio.
3. Pick items fully or partially until capacity ends.

### Example: Fractional Knapsack

Given items with weights and values, and capacity `W`, maximize value by picking fractions.

### Code (Java):

```java
class Item {
    int value, weight;
    double ratio;
    Item(int v, int w) {
        value = v; weight = w;
        ratio = (double) v / w;
    }
}

public double fractionalKnapsack(Item[] items, int W) {
    Arrays.sort(items, (a, b) -> Double.compare(b.ratio, a.ratio));
    double totalValue = 0;
    int capacity = W;

    for (Item item : items) {
        if (capacity == 0) break;
        if (item.weight <= capacity) {
            totalValue += item.value;
            capacity -= item.weight;
        } else {
            totalValue += item.ratio * capacity;
            capacity = 0;
        }
    }
    return totalValue;
}

```

---

## 1.3 Coverage-Based Greedy

### What is it?

Used in problems where you want to **cover or jump across a range** with the minimum steps or intervals, by greedily extending your current coverage.

### Why does it work?

At each point, pick the option that extends coverage as far as possible to minimize steps.

### How to approach?

1. Maintain variables for current coverage end, farthest reachable point, and steps taken.
2. Iterate through intervals or jumps:
    - Update the farthest reachable point.
    - When you reach the current coverage end, increase steps and set new coverage end to farthest.

### Example: Jump Game II (LeetCode 45)

Find minimum jumps to reach the last index.

### Code (Java):

```java
public int jump(int[] nums) {
    int jumps = 0, end = 0, farthest = 0;
    for (int i = 0; i < nums.length - 1; i++) {
        farthest = Math.max(farthest, i + nums[i]);
        if (i == end) {
            jumps++;
            end = farthest;
        }
    }
    return jumps;
}

```

---

## 1.4 Jumping Greedy (Reachability)

### What is it?

Decide if you can reach the last index (or some target) by jumping from positions in the array.

### Why does it work?

By greedily tracking the farthest reachable index, if you can reach or exceed the last index, return true.

### How to approach?

1. Maintain a variable `maxReach` to track the farthest position you can jump to.
2. Iterate over the array:
    - Update `maxReach`.
    - If current index exceeds `maxReach`, return false (you can't jump further).
3. If loop finishes, return true.

### Example: Jump Game I (LeetCode 55)

Check if you can reach the last index.

### Code (Java):

```java
public boolean canJump(int[] nums) {
    int maxReach = 0;
    for (int i = 0; i < nums.length; i++) {
        if (i > maxReach) return false;
        maxReach = Math.max(maxReach, i + nums[i]);
    }
    return true;
}

```

---

# How to Breakdown Basic Greedy Problems?

1. **Identify if greedy applies**: Is a local optimal choice sufficient? (No overlapping dependencies)
2. **Find the sorting or scanning order**: Sort inputs by a key (value, deadline, start) or process sequentially.
3. **Determine the greedy choice**: What is the locally optimal choice at each step? (earliest finish, furthest jump, best ratio)
4. **Implement in one pass**: Use pointers, counters, or priority queues as needed.
5. **Verify correctness with examples**: Walk through small examples to validate logic.

---

# Summary Table for Basic Greedy

| Subtopic | Core Concept | When to Use | Java Template Core |
| --- | --- | --- | --- |
| Sorting | Sort + iterate | Ordering tasks or events | `Arrays.sort()`, loop |
| Ratios | Sort by ratio | Fractional knapsack | Custom comparator for ratio |
| Coverage | Extend coverage greedily | Minimum jumps or intervals | Track `end`, `farthest`, `steps` |
| Jumping | Track max reachable | Reachability checks | Track `maxReach`, early exit |

---

---

# 2. Intervals — Merging, Scheduling, Covering, Insertion

---

## What Are Interval Problems?

An **interval** is typically represented by a pair `[start, end]`, indicating a continuous range (e.g., a meeting from 9:00 to 10:00). Interval problems ask questions like:

- How to **merge overlapping intervals**?
- How to **schedule the maximum number of non-overlapping intervals**?
- How to **insert a new interval** and adjust accordingly?
- How to **cover a timeline with the fewest intervals**?

---

## Why Are Interval Problems Important?

- Real-world scheduling: meetings, CPU jobs, video segments
- Timeline optimization, calendar apps
- Resource allocation in time

Most interval problems can be solved efficiently by **sorting intervals by start or end times** and then greedily making decisions as you scan.

---

## Common Subtypes of Interval Problems

| Subtopic | Description | Typical Approach |
| --- | --- | --- |
| Merging | Combine all overlapping intervals | Sort by start, merge overlaps in one pass |
| Scheduling | Maximize non-overlapping intervals | Sort by end time, greedily pick earliest end |
| Covering | Minimum intervals covering a target range | Sort and greedily select intervals |
| Insertion | Insert interval & merge overlaps | Insert, then merge |

---

## How to Approach Interval Problems (General Steps)

1. **Sort intervals**: usually by start time or end time depending on problem.
2. **Iterate intervals**: maintain current interval or coverage.
3. **Greedy decision**:
    - Merge if overlapping
    - Select if non-overlapping (earliest finish)
    - Extend coverage if covering range
4. **Output**: merged intervals, max count, or coverage count.

---

# Detailed Explanation & Code Templates (Java)

---

## 2.1 Merging Intervals

### Problem: Merge all overlapping intervals

**Example:**

Input: `[[1,3],[2,6],[8,10],[15,18]]`

Output: `[[1,6],[8,10],[15,18]]`

### Intuition

Sort intervals by start time, then for each interval:

- If it overlaps with the last merged interval, merge them (update end).
- Else, add new interval.

### Java Code:

```java
public int[][] merge(int[][] intervals) {
    if (intervals.length <= 1) return intervals;

    Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));

    List<int[]> merged = new ArrayList<>();
    int[] current = intervals[0];
    merged.add(current);

    for (int[] interval : intervals) {
        if (interval[0] <= current[1]) {
            // Overlapping - merge
            current[1] = Math.max(current[1], interval[1]);
        } else {
            // No overlap - add new interval
            current = interval;
            merged.add(current);
        }
    }

    return merged.toArray(new int[merged.size()][]);
}

```

---

## 2.2 Interval Scheduling (Max Non-overlapping Intervals)

### Problem: Find max number of non-overlapping intervals

**Example:**

Input: `[[1,3],[2,4],[3,5]]`

Output: `2` (Intervals `[1,3]` and `[3,5]`)

### Intuition

Sort intervals by **end time** (not start!). Then greedily pick intervals that finish earliest, so more intervals can fit.

### Java Code:

```java
public int eraseOverlapIntervals(int[][] intervals) {
    if (intervals.length == 0) return 0;

    Arrays.sort(intervals, (a, b) -> Integer.compare(a[1], b[1]));

    int count = 1;
    int end = intervals[0][1];

    for (int i = 1; i < intervals.length; i++) {
        if (intervals[i][0] >= end) {
            count++;
            end = intervals[i][1];
        }
    }
    return count;
}

```

---

## 2.3 Interval Covering (Minimum Number of Intervals to Cover Range)

### Problem: Given intervals and a target `[0, T]`, cover entire range with minimum intervals.

**Example:**

Intervals: `[[0,2],[4,6],[8,10],[1,9],[1,5],[5,9]]`

Target: `[0,10]`

Output: `3` (Choose `[0,2]`, `[1,9]`, `[8,10]`)

### Intuition

Sort intervals by start. At each step, pick the interval that starts before or at current coverage end and extends coverage farthest.

### Java Code:

```java
public int minCoverIntervals(int[][] intervals, int T) {
    Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));

    int count = 0, i = 0, coveredEnd = 0, farthest = 0;

    while (coveredEnd < T) {
        while (i < intervals.length && intervals[i][0] <= coveredEnd) {
            farthest = Math.max(farthest, intervals[i][1]);
            i++;
        }
        if (farthest == coveredEnd) return -1; // can't cover full range

        count++;
        coveredEnd = farthest;
    }
    return count;
}

```

---

## 2.4 Interval Insertion and Merging

### Problem: Insert new interval, merge overlaps

**Example:**

Input: `[[1,3],[6,9]]`, insert `[2,5]`

Output: `[[1,5],[6,9]]`

### Intuition

Iterate intervals, add all intervals before new interval. Then merge all overlapping intervals with new interval. Finally, add all intervals after new interval.

### Java Code:

```java
public int[][] insert(int[][] intervals, int[] newInterval) {
    List<int[]> result = new ArrayList<>();

    int i = 0;
    // Add all intervals before newInterval
    while (i < intervals.length && intervals[i][1] < newInterval[0]) {
        result.add(intervals[i++]);
    }

    // Merge overlapping intervals
    while (i < intervals.length && intervals[i][0] <= newInterval[1]) {
        newInterval[0] = Math.min(newInterval[0], intervals[i][0]);
        newInterval[1] = Math.max(newInterval[1], intervals[i][1]);
        i++;
    }
    result.add(newInterval);

    // Add remaining intervals
    while (i < intervals.length) {
        result.add(intervals[i++]);
    }

    return result.toArray(new int[result.size()][]);
}

```

---

# How to Break Down Interval Problems

1. **Sort intervals** — usually by start time, sometimes by end time (depends on problem).
2. **Understand what you want**:
    - Merge overlapping (merge all overlaps)
    - Schedule max (select earliest finishing intervals)
    - Cover range (greedily extend coverage)
    - Insert and merge (split into before, overlapping, after)
3. **Iterate intervals** — maintain pointers or variables for coverage.
4. **Make greedy decisions**:
    - Merge if overlapping
    - Pick if non-overlapping
    - Extend coverage
5. **Return final intervals or count**

---

# Summary Table for Intervals

| Subtopic | Key Sorting | Greedy Step | Return Value |
| --- | --- | --- | --- |
| Merge | start | Merge intervals if overlap | List of merged intervals |
| Scheduling | end | Pick earliest finishing | Max count |
| Covering | start | Extend coverage farthest | Min intervals to cover |
| Insertion | start | Add before, merge overlapping | Merged intervals list |

---

---

# 3. Line Sweep Algorithm

---

## What is Line Sweep?

**Line Sweep** (or Sweep Line) is an algorithmic technique where you imagine a vertical or horizontal line "sweeping" across a plane or timeline, stopping at important events (like start or end points). You process these events in sorted order and maintain a data structure to track active elements (intervals, points, etc.) at each event.

---

## Why is it useful?

- Efficiently handles interval overlap problems.
- Helps count active intervals or objects dynamically.
- Solves problems like counting overlaps, skyline silhouette, and interval union length.
- Handles complex event-based problems in O(N log N).

---

## Key Idea

- Extract **events** from input — typically interval start and end points.
- Sort events by position.
- Traverse sorted events from left to right:
    - When encountering a **start event**, add interval/object to active set.
    - When encountering an **end event**, remove interval/object.
- Maintain active intervals count or other info at each event.

---

## Common Data Structures Used

- Balanced BST / TreeSet / PriorityQueue — to track active intervals if needed.
- Simple counters — for counting overlaps.

---

# Common Subproblems & How to Solve

| Problem Type | Description | Key Idea |
| --- | --- | --- |
| Counting Overlaps | Count max number of overlapping intervals | Track active count at start/end |
| Skyline Problem | Find silhouette formed by buildings | Use events with heights |
| Interval Union Length | Total length covered by intervals | Track active intervals, sum lengths |
| Meeting Rooms | Count minimum rooms required | Count max overlaps |

---

# How to Approach Line Sweep Problems

1. **Convert intervals to events**:
    - Create `start` event with coordinate and +1 (add to active set)
    - Create `end` event with coordinate and -1 (remove from active set)
2. **Sort events by coordinate** (tie-break: start before end to handle touching intervals)
3. **Sweep through events in order**, maintain active count or data structure:
    - Add or remove intervals as events happen.
4. **Calculate required metric** (max overlap, skyline height changes, union length).

---

# Detailed Example & Java Template

---

## Example 1: Maximum Number of Overlapping Intervals

**Problem:** Given intervals, find the maximum number overlapping at any point.

### Intuition:

- For each interval, create two events: start (+1) and end (-1).
- Sort all events.
- Sweep line, keep track of active intervals.
- Max active intervals = max overlap.

### Java Code:

```java
public int maxOverlap(int[][] intervals) {
    // Create events: [time, type], type: +1 start, -1 end
    int n = intervals.length;
    int[][] events = new int[n * 2][2];

    for (int i = 0; i < n; i++) {
        events[2 * i] = new int[]{intervals[i][0], 1};    // start event
        events[2 * i + 1] = new int[]{intervals[i][1], -1}; // end event
    }

    // Sort events by time, tie-break: start before end
    Arrays.sort(events, (a, b) -> a[0] == b[0] ? b[1] - a[1] : a[0] - b[0]);

    int maxOverlap = 0, active = 0;

    for (int[] event : events) {
        active += event[1];          // +1 for start, -1 for end
        maxOverlap = Math.max(maxOverlap, active);
    }

    return maxOverlap;
}

```

---

## Example 2: Skyline Problem (LeetCode 218)

**Problem:** Given buildings represented as `[left, right, height]`, return the skyline formed by these buildings.

### Intuition:

- Create events for building start (+height) and end (-height).
- Sort events.
- Sweep line keeps track of active building heights.
- When max height changes, record new point in skyline.

### Key Data Structure:

- Max-heap (PriorityQueue) to track tallest building.

### High-Level Steps:

1. Create events: start with height positive, end with height negative.
2. Sort events by coordinate.
3. Sweep:
    - Add height to max-heap on start.
    - Remove height on end.
4. Track max height changes to record skyline points.

---

# How to Break Down Line Sweep Problems

1. **Identify events** — start and end points, sometimes special points.
2. **Create an event list** with appropriate data (coordinate, type, height).
3. **Sort events** by coordinate (handle ties carefully).
4. **Use a data structure** to maintain active elements (counter, heap, BST).
5. **Process events sequentially** — update data structure and calculate results.
6. **Return final answer** after sweeping all events.

---

# Summary Table for Line Sweep

| Subtopic | Key Data Structure | Typical Sort Key | Core Operation | Result Type |
| --- | --- | --- | --- | --- |
| Count Overlaps | Simple counter | coordinate | +1 start, -1 end | Max overlaps (int) |
| Skyline | Max-heap | coordinate | Add/remove height | Skyline points (list) |
| Union Length | Counter + previous point | coordinate | Track coverage length | Total length (int) |
| Meeting Rooms | Counter or min-heap | coordinate | Track room count | Min rooms required (int) |

---

---

# 4. Heap-Based Greedy Algorithms

---

## What Are Heap-Based Greedy Algorithms?

Heap-based greedy algorithms use **priority queues (heaps)** to efficiently track the “best” candidate among many, based on some priority — often the smallest or largest value.

Common use cases:

- Scheduling jobs or courses by deadlines
- Tracking resources (like rooms, machines)
- Merging sorted lists or intervals
- Dynamic selection based on earliest finishing times or minimum cost

---

## Why Use Heaps?

- Heaps allow quick access to the minimum or maximum element in O(log n).
- Enables efficient real-time selection and updating of active elements.
- Suits problems where you need to repeatedly pick the “best candidate” dynamically.

---

## Common Subtopics & Problem Types

| Subtopic | Description | Key Idea |
| --- | --- | --- |
| Job Scheduling | Schedule jobs maximizing profit or count | Sort by deadline, use heap to track end times |
| Course Schedule III | Maximize number of courses within deadlines | Use max heap to remove longest course when over capacity |
| Resource Tracking | Track active resources (rooms, machines) | Min-heap to track earliest finishing time |
| Merge Intervals/Lists | Merge multiple sorted inputs | Min-heap to pick next smallest element |

---

# How to Approach Heap-Based Greedy Problems

1. **Sort input** by a relevant key (e.g., start time, deadline).
2. **Initialize a priority queue (min or max heap)** to track ongoing tasks or resources.
3. **Iterate over sorted input**:
    - Add current task/resource to heap.
    - Check heap conditions (capacity, conflicts).
    - Remove tasks that don’t fit or resolve conflicts using heap operations.
4. **Return result** based on heap size or accumulated value.

---

# Detailed Examples & Java Templates

---

## 4.1 Job Scheduling / Course Schedule III (LeetCode 630)

### Problem

Given courses with durations and deadlines, find max number of courses that can be completed without missing deadlines.

### Intuition

- Sort courses by deadline.
- Use a max heap to keep track of the durations of courses taken.
- When total time exceeds current course’s deadline, remove the longest course taken (from max heap).

### Java Code:

```java
public int scheduleCourse(int[][] courses) {
    Arrays.sort(courses, (a, b) -> Integer.compare(a[1], b[1]));
    PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
    int time = 0;

    for (int[] course : courses) {
        time += course[0];
        maxHeap.offer(course[0]);

        if (time > course[1]) {
            time -= maxHeap.poll(); // remove longest course
        }
    }
    return maxHeap.size();
}

```

---

## 4.2 Meeting Rooms II (LeetCode 253)

### Problem

Given intervals of meeting times, find minimum number of meeting rooms required.

### Intuition

- Sort intervals by start time.
- Use a min heap to track end times of meetings currently occupying rooms.
- For each new meeting:
    - If earliest ending room is free (heap’s min end time ≤ current start), reuse it (pop heap).
    - Else, allocate new room (push current end).
- Size of heap = number of rooms needed.

### Java Code:

```java
public int minMeetingRooms(int[][] intervals) {
    Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();

    for (int[] interval : intervals) {
        if (!minHeap.isEmpty() && minHeap.peek() <= interval[0]) {
            minHeap.poll();  // room freed
        }
        minHeap.offer(interval[1]);  // allocate room (new or reused)
    }
    return minHeap.size();
}

```

---

## 4.3 Merge K Sorted Lists (LeetCode 23)

### Problem

Given K sorted lists, merge into one sorted list.

### Intuition

- Use a min heap to keep track of current smallest elements from each list.
- Pop smallest, add to merged list, then push next element from that list.
- Repeat until all lists exhausted.

### Java Code (Outline):

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int v) { val = v; }
}

public ListNode mergeKLists(ListNode[] lists) {
    PriorityQueue<ListNode> minHeap = new PriorityQueue<>(Comparator.comparingInt(n -> n.val));
    for (ListNode node : lists) {
        if (node != null) minHeap.offer(node);
    }
    ListNode dummy = new ListNode(0);
    ListNode tail = dummy;

    while (!minHeap.isEmpty()) {
        ListNode curr = minHeap.poll();
        tail.next = curr;
        tail = tail.next;
        if (curr.next != null) minHeap.offer(curr.next);
    }
    return dummy.next;
}

```

---

# How to Break Down Heap-Based Problems

1. **Sort input** based on deadline, start time, or priority.
2. **Initialize heap** (min or max depending on problem).
3. **Iterate through input** and dynamically update heap:
    - Add current task/resource.
    - Check for conflicts or capacity; remove or adjust using heap.
4. **Result** is often size of heap or accumulated value.

---

# Summary Table for Heap-Based Greedy

| Subtopic | Heap Type | Sort Key | Heap Use | Result Type |
| --- | --- | --- | --- | --- |
| Job Scheduling | Max Heap | Deadline | Remove longest duration if over | Max courses scheduled |
| Meeting Rooms | Min Heap | Start time | Track earliest finishing room | Min rooms required |
| Merge Sorted | Min Heap | Values | Merge k sorted lists | Merged sorted list |
| Resource Tracking | Min Heap | Start time / End time | Track resource allocation | Resource count |

---

# Greedy Problem List

---

## EASY

| Problem Name | Problem # |
| --- | --- |
| Jump Game | 55 |
| Gas Station | 134 |
| Lemonade Change | 860 |
| Assign Cookies | 455 |
| Remove Covered Intervals | 1288 |
| Non-overlapping Intervals  | 435 |
| Minimum Number of Arrows to Burst Balloons | 452 |
| Valid Parenthesis String | 678 |
| Partition Labels | 763 |
| Valid Palindrome II | 680 |
| Can Place Flowers | 605 |
| Maximum Number of Events That Can Be Attended  | 1353 |
| Path With Maximum Gold  | 1219 |
| Check If It Is a Straight Line | 1232 |
| Car Pooling | 1094 |
| Boats to Save People | 881 |
| Number of Burgers With No Waste of Ingredients | 1276 |
| Play With Chips | 1217 |
| Previous Permutation With One Swap | 1053 |
| Bag of Tokens | 948 |

---

## MEDIUM

| Problem Name | Problem # |
| --- | --- |
| Queue Reconstruction by Height  | 406 |
| Minimum Number of Platforms | 185 |
| Task Scheduler | 621 |
| Russian Doll Envelopes | 354 |
| Jump Game II | 45 |
| Wiggle Subsequence | 376 |
| Minimum Number of Refueling Stops | 871 |
| Car Pooling | 1094 |
| Largest Number == | 179 |
| Best Time to Buy and Sell Stock with Cooldown | 309 |
| Jump Game III | 1306 |
| Maximum Number of Non-overlapping Substrings | 1520 |
| Remove K Digits | 402 |
| Partition Labels | 763 |
| Minimum Increment to Make Array Unique == | 945 |
| Maximum Length of Pair Chain | 646 |
| Minimum Number of Arrows to Burst Balloons | 452 |
| Assign Tasks to Workers | 1723 |
| Minimum Number of Taps to Open to Water a Garden  | 1326 |
| Remove Covered Intervals | 1288 |
| Bag of Tokens | 948 |
| Divide Array in Sets of K Consecutive Numbers | 1296 |
| Group the People Given the Group Size They Belong To | 1282 |
| Cinema Seat Allocation | 1386 |
| Construct K Palindrome Strings | 1400 |
| Advantage Shuffle | 870 |
| Reorganize String | 767 |
| String Without AAA or BBB | 984 |
| Check If a String Can Break Another String | 1433 |
| Remove Duplicate Letters | 316 |

---

## HARD

| Problem Name | Problem # |
| --- | --- |
| Task Scheduler II | 358 |
| Find the Shortest Superstring | 943 |
| Largest Rectangle in Histogram | 84 |
| Trapping Rain Water | 42 |
| Maximum Gap | 164 |
| Minimum Number of Arrows to Burst Balloons | 452 |
| Jump Game IV | 1345 |
| Jump Game VI | 1696 |
| Maximum Number of Events That Can Be Attended II | 1751 |
| Car Pooling | 1094 |
| Last Stone Weight | 1046 |
| Reduce Array Size to The Half | 1338 |
| Minimum Add to Make Parentheses Valid | 921 |
| Merge Intervals | 56 |
| Insert Interval | 57 |
| Meeting Rooms | 252 |
| Meeting Rooms II | 253 |
| Interval List Intersections | 986 |
| Employee Free Time | 759 |
| Single Threaded CPU | 1834 |

---