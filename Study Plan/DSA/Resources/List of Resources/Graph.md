# Graph

Priority: High
Status: Not started

Perfect! Let’s begin with **Graphs**, **BFS**, and **DFS** in Java — all explained FAANG-style with clean code, dry-run examples, edge cases, and interview-ready insights.

---

## 🔹 1. What is a Graph?

- A **graph** is a collection of nodes (**vertices**) connected by edges.
- Graphs can be:
    - **Directed or Undirected**
    - **Weighted or Unweighted**
    - **Cyclic or Acyclic**
    - **Connected or Disconnected**

### 🔸 Java Representation

### ➤ **Adjacency List** (Most used)

```java
Map<Integer, List<Integer>> graph = new HashMap<>();

```

### ➤ **Adjacency Matrix** (Used for dense graphs)

```java
int[][] graph = new int[n][n];

```

---

## 🔹 2. Building an Undirected Graph (Unweighted)

```java
public class GraphBuilder {
    public static Map<Integer, List<Integer>> buildGraph(int[][] edges, int n) {
        Map<Integer, List<Integer>> graph = new HashMap<>();

        for (int i = 0; i < n; i++) {
            graph.put(i, new ArrayList<>());
        }

        for (int[] edge : edges) {
            int u = edge[0], v = edge[1];
            graph.get(u).add(v);
            graph.get(v).add(u); // Omit this for a directed graph
        }

        return graph;
    }
}

```

---

## 🔹 3. **DFS (Depth-First Search)**

### ➤ Recursive DFS

```java
public class DFS {
    public static void dfs(int node, Map<Integer, List<Integer>> graph, Set<Integer> visited) {
        if (visited.contains(node)) return;

        visited.add(node);
        System.out.print(node + " ");

        for (int neighbor : graph.get(node)) {
            dfs(neighbor, graph, visited);
        }
    }
}

```

---

## 🔹 4. **BFS (Breadth-First Search)**

```java
public class BFS {
    public static void bfs(int start, Map<Integer, List<Integer>> graph) {
        Set<Integer> visited = new HashSet<>();
        Queue<Integer> queue = new LinkedList<>();

        visited.add(start);
        queue.offer(start);

        while (!queue.isEmpty()) {
            int current = queue.poll();
            System.out.print(current + " ");

            for (int neighbor : graph.get(current)) {
                if (!visited.contains(neighbor)) {
                    visited.add(neighbor);
                    queue.offer(neighbor);
                }
            }
        }
    }
}

```

---

## 🔹 5. Example Usage (Dry Run Ready)

### Input:

```java
int[][] edges = {
    {0, 1}, {0, 2}, {1, 2}, {2, 3}, {3, 4}
};
int n = 5;

```

### Main:

```java
public class Main {
    public static void main(String[] args) {
        int[][] edges = {{0,1},{0,2},{1,2},{2,3},{3,4}};
        int n = 5;

        Map<Integer, List<Integer>> graph = GraphBuilder.buildGraph(edges, n);

        System.out.println("DFS Traversal:");
        DFS.dfs(0, graph, new HashSet<>());

        System.out.println("\nBFS Traversal:");
        BFS.bfs(0, graph);
    }
}

```

### Output:

```
DFS Traversal:
0 1 2 3 4
BFS Traversal:
0 1 2 3 4

```

---

## 🧠 FAANG Insights

| Concept | Insight |
| --- | --- |
| DFS | Good for detecting cycles, exploring paths, backtracking |
| BFS | Good for shortest path in unweighted graphs |
| Space | DFS uses call stack (O(N)), BFS uses queue (O(N)) |
| Graph Type | Code works for undirected. For directed, skip the reverse edge. |
| Common Mistake | Not marking nodes as visited early in BFS — leads to duplicates |

---

---

## 🔹  Cycle Detection in **Undirected Graph**

### 🔸 🔍 Core Idea (DFS Approach):

If you visit a node already visited **and it’s not the parent**, a cycle exists.

### ✅ Code (DFS for Undirected Graph):

```java
public class CycleUndirectedDFS {
    public static boolean hasCycle(Map<Integer, List<Integer>> graph, int node, int parent, Set<Integer> visited) {
        visited.add(node);

        for (int neighbor : graph.get(node)) {
            if (!visited.contains(neighbor)) {
                if (hasCycle(graph, neighbor, node, visited)) {
                    return true;
                }
            } else if (neighbor != parent) {
                return true; // Cycle detected
            }
        }

        return false;
    }

    public static boolean detectCycle(Map<Integer, List<Integer>> graph, int n) {
        Set<Integer> visited = new HashSet<>();
        for (int i = 0; i < n; i++) {
            if (!visited.contains(i)) {
                if (hasCycle(graph, i, -1, visited)) return true;
            }
        }
        return false;
    }
}

```

---

## 🔹  Cycle Detection in **Directed Graph**

### 🔸 🔍 Core Idea:

Use **DFS with recursion stack** to detect back edges.

### ✅ Code (DFS + RecStack for Directed Graph):

```java
public class CycleDirectedDFS {
    public static boolean hasCycle(int node, Map<Integer, List<Integer>> graph, Set<Integer> visited, Set<Integer> recStack) {
        visited.add(node);
        recStack.add(node);

        for (int neighbor : graph.get(node)) {
            if (!visited.contains(neighbor)) {
                if (hasCycle(neighbor, graph, visited, recStack)) {
                    return true;
                }
            } else if (recStack.contains(neighbor)) {
                return true; // Back edge → cycle
            }
        }

        recStack.remove(node);
        return false;
    }

    public static boolean detectCycle(Map<Integer, List<Integer>> graph, int n) {
        Set<Integer> visited = new HashSet<>();
        Set<Integer> recStack = new HashSet<>();

        for (int i = 0; i < n; i++) {
            if (!visited.contains(i)) {
                if (hasCycle(i, graph, visited, recStack)) return true;
            }
        }

        return false;
    }
}

```

---

## 🧪 Example

```java
public class Main {
    public static void main(String[] args) {
        int[][] undirectedEdges = {
            {0, 1}, {1, 2}, {2, 0}
        };
        int[][] directedEdges = {
            {0, 1}, {1, 2}, {2, 0}
        };
        int n = 3;

        Map<Integer, List<Integer>> undirectedGraph = GraphBuilder.buildGraph(undirectedEdges, n);
        Map<Integer, List<Integer>> directedGraph = GraphBuilder.buildGraphDirected(directedEdges, n);

        System.out.println("Undirected Cycle? " + CycleUndirectedDFS.detectCycle(undirectedGraph, n));
        System.out.println("Directed Cycle? " + CycleDirectedDFS.detectCycle(directedGraph, n));
    }
}

```

### ➤ Output:

```
Undirected Cycle? true
Directed Cycle? true

```

---

## 🔹 Utility for Directed Graph Build

```java
public class GraphBuilder {
    public static Map<Integer, List<Integer>> buildGraph(int[][] edges, int n) {
        Map<Integer, List<Integer>> graph = new HashMap<>();
        for (int i = 0; i < n; i++) graph.put(i, new ArrayList<>());
        for (int[] edge : edges) {
            graph.get(edge[0]).add(edge[1]);
            graph.get(edge[1]).add(edge[0]); // remove this for directed
        }
        return graph;
    }

    public static Map<Integer, List<Integer>> buildGraphDirected(int[][] edges, int n) {
        Map<Integer, List<Integer>> graph = new HashMap<>();
        for (int i = 0; i < n; i++) graph.put(i, new ArrayList<>());
        for (int[] edge : edges) {
            graph.get(edge[0]).add(edge[1]); // Only one direction
        }
        return graph;
    }
}

```

---

## 🧠 FAANG Tips

| Topic | Insight |
| --- | --- |
| Undirected Graph | Use `parent` tracking to ignore false cycles |
| Directed Graph | Use recursion stack to track the current DFS path |
| Common Mistake | Forgetting to backtrack from `recStack` in directed detection |
| Edge Case | Disconnected components → always loop over all `n` nodes |
| Follow Up | Modify to return the cycle path instead of just true/false |

---

---

# ✅ Topological Sort in Directed Graphs

## 💡 Definition:

A **topological sort** of a **Directed Acyclic Graph (DAG)** is a **linear ordering of its vertices** such that for every directed edge `u → v`, node `u` appears **before** `v` in the ordering.

---

## 🔧 When is it used?

- Course scheduling (Leetcode: *Course Schedule II*)
- Task scheduling with dependencies
- Build systems (e.g., compile order of files)
- Package manager dependency resolution

---

## 🛠️ Two Algorithms:

### 1. **DFS-Based Topological Sort** (Reverse Post-order)

### 2. **Kahn’s Algorithm** (BFS + In-degree)

---

## 🔹 1. DFS-Based Topological Sort

### 🔸 Idea:

Perform DFS, and when a node finishes (all neighbors explored), **push it onto a stack**. Finally, reverse the stack.

### ✅ Java Code:

```java
public class TopoSortDFS {
    public static void topoDFS(int node, Map<Integer, List<Integer>> graph, Set<Integer> visited, Stack<Integer> stack) {
        visited.add(node);

        for (int neighbor : graph.get(node)) {
            if (!visited.contains(neighbor)) {
                topoDFS(neighbor, graph, visited, stack);
            }
        }

        stack.push(node); // Postorder
    }

    public static List<Integer> topologicalSort(Map<Integer, List<Integer>> graph, int n) {
        Set<Integer> visited = new HashSet<>();
        Stack<Integer> stack = new Stack<>();

        for (int i = 0; i < n; i++) {
            if (!visited.contains(i)) {
                topoDFS(i, graph, visited, stack);
            }
        }

        List<Integer> result = new ArrayList<>();
        while (!stack.isEmpty()) {
            result.add(stack.pop());
        }

        return result;
    }
}

```

---

## 🔹 2. Kahn’s Algorithm (BFS + In-degree)

### 🔸 Idea:

- Count **in-degrees** for all nodes.
- Start with nodes with in-degree `0`.
- Remove them and reduce neighbors' in-degrees.
- If any neighbor’s in-degree becomes `0`, add to queue.

### ✅ Java Code:

```java
public class TopoSortKahn {
    public static List<Integer> topologicalSort(Map<Integer, List<Integer>> graph, int n) {
        int[] inDegree = new int[n];

        for (int u : graph.keySet()) {
            for (int v : graph.get(u)) {
                inDegree[v]++;
            }
        }

        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            if (inDegree[i] == 0) queue.offer(i);
        }

        List<Integer> topoOrder = new ArrayList<>();
        while (!queue.isEmpty()) {
            int u = queue.poll();
            topoOrder.add(u);

            for (int v : graph.get(u)) {
                inDegree[v]--;
                if (inDegree[v] == 0) queue.offer(v);
            }
        }

        if (topoOrder.size() != n) {
            throw new RuntimeException("Cycle detected! Topo sort not possible.");
        }

        return topoOrder;
    }
}

```

---

## 🧪 Example

Given edges:

```java
int[][] edges = {
    {5, 2}, {5, 0}, {4, 0}, {4, 1}, {2, 3}, {3, 1}
};

```

Expected Topological Sort (one of them):

```
5 4 2 3 1 0

```

---

## 🔧 Graph Utility (Reusable)

```java
public class GraphBuilder {
    public static Map<Integer, List<Integer>> buildGraphDirected(int[][] edges, int n) {
        Map<Integer, List<Integer>> graph = new HashMap<>();
        for (int i = 0; i < n; i++) graph.put(i, new ArrayList<>());
        for (int[] edge : edges) {
            graph.get(edge[0]).add(edge[1]);
        }
        return graph;
    }
}

```

---

## 🧠 FAANG Interview Tips

| Concept | Insight |
| --- | --- |
| DAG Required | Topo sort is only defined for DAGs |
| DFS | Stack-based (reverse postorder) |
| Kahn’s | Queue-based + in-degree |
| Cycle Detection | If topo sort has fewer than `n` nodes ⇒ cycle |
| Real Use Case | Course prerequisites, task scheduling |

---

---

## 🧭 Dijkstra's Algorithm - Quick Summary

| Feature | Details |
| --- | --- |
| Purpose | Find **shortest path** from source to all nodes |
| Graph Type | Weighted, Directed/Undirected |
| Edge Weights | **Non-negative only** |
| Time Complexity | `O((V + E) log V)` using PriorityQueue |
| Technique | Greedy + Min-Heap (Priority Queue) |

---

## 💡 Intuition

You always **pick the node** with the **smallest known distance** (from the source), and **relax** its neighbors — i.e., try to **improve** their distances if going through this node is better.

---

## ✅ Java Code: Dijkstra using PriorityQueue

```java
import java.util.*;

class Pair {
    int node, dist;
    Pair(int node, int dist) {
        this.node = node;
        this.dist = dist;
    }
}

public class Dijkstra {

    public static int[] dijkstra(int V, List<List<Pair>> adj, int src) {
        int[] dist = new int[V];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[src] = 0;

        PriorityQueue<Pair> pq = new PriorityQueue<>((a, b) -> a.dist - b.dist);
        pq.offer(new Pair(src, 0));

        while (!pq.isEmpty()) {
            Pair current = pq.poll();
            int u = current.node;

            for (Pair neighbor : adj.get(u)) {
                int v = neighbor.node;
                int weight = neighbor.dist;

                if (dist[u] + weight < dist[v]) {
                    dist[v] = dist[u] + weight;
                    pq.offer(new Pair(v, dist[v]));
                }
            }
        }

        return dist;
    }

    public static void main(String[] args) {
        int V = 5;
        List<List<Pair>> adj = new ArrayList<>();
        for (int i = 0; i < V; i++) adj.add(new ArrayList<>());

        // Undirected weighted edges
        adj.get(0).add(new Pair(1, 2));
        adj.get(1).add(new Pair(0, 2));

        adj.get(0).add(new Pair(2, 4));
        adj.get(2).add(new Pair(0, 4));

        adj.get(1).add(new Pair(2, 1));
        adj.get(2).add(new Pair(1, 1));

        adj.get(1).add(new Pair(3, 7));
        adj.get(3).add(new Pair(1, 7));

        adj.get(2).add(new Pair(4, 3));
        adj.get(4).add(new Pair(2, 3));

        int[] dist = dijkstra(V, adj, 0);

        System.out.println("Node\tDistance from Source");
        for (int i = 0; i < V; i++) {
            System.out.println(i + "\t" + dist[i]);
        }
    }
}

```

---

## 🧪 Output

```
Node    Distance from Source
0       0
1       2
2       3
3       9
4       6

```

---

## 🔍 Explanation of Core Logic:

1. **PriorityQueue (Min Heap)**:
    
    Always extracts the node with the smallest distance seen so far.
    
2. **Relaxation**:
    
    When you visit neighbors, check if going through the current node improves their known distance.
    
3. **No Revisiting**:
    
    Once a node's distance is finalized (extracted from PQ), we don’t revisit it for better paths.
    

---

## ❗ Important Notes

| Concept | Explanation |
| --- | --- |
| **Only non-negative weights** | For negative weights, use **Bellman-Ford** |
| **Works for directed/undirected** | Adjust edge addition accordingly |
| **Avoid revisiting** | You can use a visited[] if needed for optimization |
| **Dijkstra for single source** | If all-pairs shortest paths needed → use **Floyd-Warshall** |

---

---

## 🔍 When to Use Bellman-Ford

| Feature | Detail |
| --- | --- |
| Graph Type | Directed/Undirected (converted properly) |
| Edge Weights | ✅ Supports **negative weights** |
| Detect Negative Cycle | ✅ Yes |
| Shortest Path | From single source to all vertices |
| Time Complexity | `O(V * E)` |
| Works on | Sparse graphs or graphs with negatives |

---

## 🧠 Intuition

Bellman-Ford **relaxes all edges V-1 times**, ensuring that the shortest paths (even via negative weights) are correctly updated. If we can still **relax any edge in the V-th iteration**, a **negative cycle** exists.

---

## ✅ Java Implementation

```java
import java.util.*;

class Edge {
    int src, dest, weight;
    Edge(int s, int d, int w) {
        this.src = s;
        this.dest = d;
        this.weight = w;
    }
}

public class BellmanFord {

    public static void bellmanFord(List<Edge> edges, int V, int src) {
        int[] dist = new int[V];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[src] = 0;

        // Relax all edges V-1 times
        for (int i = 0; i < V - 1; i++) {
            for (Edge edge : edges) {
                if (dist[edge.src] != Integer.MAX_VALUE &&
                    dist[edge.src] + edge.weight < dist[edge.dest]) {
                    dist[edge.dest] = dist[edge.src] + edge.weight;
                }
            }
        }

        // Check for negative weight cycle
        for (Edge edge : edges) {
            if (dist[edge.src] != Integer.MAX_VALUE &&
                dist[edge.src] + edge.weight < dist[edge.dest]) {
                System.out.println("Negative Weight Cycle Detected!");
                return;
            }
        }

        System.out.println("Vertex\tDistance from Source");
        for (int i = 0; i < V; i++) {
            System.out.println(i + "\t" + dist[i]);
        }
    }

    public static void main(String[] args) {
        int V = 5;
        List<Edge> edges = new ArrayList<>();

        // Add directed edges: from, to, weight
        edges.add(new Edge(0, 1, -1));
        edges.add(new Edge(0, 2, 4));
        edges.add(new Edge(1, 2, 3));
        edges.add(new Edge(1, 3, 2));
        edges.add(new Edge(1, 4, 2));
        edges.add(new Edge(3, 2, 5));
        edges.add(new Edge(3, 1, 1));
        edges.add(new Edge(4, 3, -3));

        bellmanFord(edges, V, 0);
    }
}

```

---

## 🧪 Output

```
Vertex  Distance from Source
0       0
1       -1
2       2
3       -2
4       1

```

---

## 🔄 Difference from Dijkstra

| Feature | Dijkstra | Bellman-Ford |
| --- | --- | --- |
| Negative Weights | ❌ Not supported | ✅ Supported |
| Negative Cycles | ❌ No check | ✅ Detectable |
| Time Complexity | `O((V+E)logV)` | `O(V*E)` |
| Strategy | Greedy | Dynamic Programming |

---

## 💥 Negative Weight Cycle Detection

If after **V-1 relaxations**, any edge can still be relaxed — that implies a **negative weight cycle** exists.

---

---

## 🧠 What is a Strongly Connected Component (SCC)?

In a **directed graph**, a **strongly connected component (SCC)** is a **maximal set of nodes** such that **every node is reachable from every other node** in that set.

---

## 🚀 Kosaraju's Algorithm — Overview

Kosaraju's Algorithm finds all SCCs in **3 main steps**:

1. **Do DFS** and push nodes to a **stack** in the order of **finishing time**.
2. **Transpose the graph** (reverse all edges).
3. **Pop from the stack** and do DFS on the transposed graph. Each DFS traversal gives **one SCC**.

---

### 🔁 Why this works?

- Original DFS ensures we handle **finish times** in topological order.
- Transposing allows us to walk **backward** to find components that were mutually reachable.

---

## ✅ Java Implementation

```java
import java.util.*;

public class KosarajuSCC {
    private int V;
    private List<List<Integer>> graph;
    private List<List<Integer>> transposed;

    KosarajuSCC(int V) {
        this.V = V;
        graph = new ArrayList<>();
        transposed = new ArrayList<>();
        for (int i = 0; i < V; i++) {
            graph.add(new ArrayList<>());
            transposed.add(new ArrayList<>());
        }
    }

    void addEdge(int u, int v) {
        graph.get(u).add(v);
    }

    void dfs(int u, boolean[] visited, Stack<Integer> stack) {
        visited[u] = true;
        for (int v : graph.get(u)) {
            if (!visited[v])
                dfs(v, visited, stack);
        }
        stack.push(u);
    }

    void dfsTranspose(int u, boolean[] visited, List<Integer> component) {
        visited[u] = true;
        component.add(u);
        for (int v : transposed.get(u)) {
            if (!visited[v])
                dfsTranspose(v, visited, component);
        }
    }

    void transposeGraph() {
        for (int u = 0; u < V; u++) {
            for (int v : graph.get(u)) {
                transposed.get(v).add(u);  // reverse edge
            }
        }
    }

    void findSCCs() {
        Stack<Integer> stack = new Stack<>();
        boolean[] visited = new boolean[V];

        // Step 1: Fill stack with finish times
        for (int i = 0; i < V; i++) {
            if (!visited[i])
                dfs(i, visited, stack);
        }

        // Step 2: Transpose the graph
        transposeGraph();

        // Step 3: DFS on transposed graph
        Arrays.fill(visited, false);
        System.out.println("Strongly Connected Components:");
        while (!stack.isEmpty()) {
            int node = stack.pop();
            if (!visited[node]) {
                List<Integer> component = new ArrayList<>();
                dfsTranspose(node, visited, component);
                System.out.println(component);
            }
        }
    }

    public static void main(String[] args) {
        KosarajuSCC g = new KosarajuSCC(5);
        g.addEdge(1, 0);
        g.addEdge(0, 2);
        g.addEdge(2, 1);
        g.addEdge(0, 3);
        g.addEdge(3, 4);

        g.findSCCs();
    }
}

```

---

## 🔍 Output

```
Strongly Connected Components:
[4]
[3]
[0, 2, 1]

```

---

## 🧩 Time Complexity

- **O(V + E)**:
    - 1 DFS = O(V + E)
    - Transpose = O(E)
    - 2nd DFS = O(V + E)

---

## 💡 Real-Life Use Case

- **Compilers** (dependency analysis)
- **Social Networks** (strong groups)
- **Distributed Systems** (mutual reachability)

---

---

## ✅ 1. 0-1 BFS (for Graphs with Edge Weights 0 or 1)

### 🔍 Problem Type:

- Shortest path in a **graph with only edge weights of 0 or 1**.

### ⚠️ Why not use Dijkstra?

- Dijkstra works, but uses a **priority queue** and costs `O(E log V)`.
- We can **optimize it to O(V + E)** using a **Deque (Double-Ended Queue)**.

---

### 🚀 Key Idea:

Use a **Deque** instead of a priority queue:

- **If the edge has weight 0 → push node to front of deque**
- **If the edge has weight 1 → push node to back of deque**

This ensures BFS-like level traversal but also accounts for edge weights efficiently.

---

### ✅ Java Implementation:

```java
import java.util.*;

class ZeroOneBFS {
    static class Pair {
        int node, cost;
        Pair(int n, int c) {
            node = n;
            cost = c;
        }
    }

    public static int[] zeroOneBFS(List<List<Pair>> graph, int src, int V) {
        int[] dist = new int[V];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[src] = 0;

        Deque<Integer> dq = new ArrayDeque<>();
        dq.addFirst(src);

        while (!dq.isEmpty()) {
            int u = dq.pollFirst();

            for (Pair edge : graph.get(u)) {
                int v = edge.node;
                int wt = edge.cost;

                if (dist[u] + wt < dist[v]) {
                    dist[v] = dist[u] + wt;
                    if (wt == 0)
                        dq.addFirst(v);
                    else
                        dq.addLast(v);
                }
            }
        }
        return dist;
    }

    public static void main(String[] args) {
        int V = 5;
        List<List<Pair>> graph = new ArrayList<>();
        for (int i = 0; i < V; i++) graph.add(new ArrayList<>());

        // Sample edges (u → v, weight)
        graph.get(0).add(new Pair(1, 0));
        graph.get(0).add(new Pair(2, 1));
        graph.get(1).add(new Pair(2, 0));
        graph.get(2).add(new Pair(3, 1));
        graph.get(1).add(new Pair(3, 1));
        graph.get(3).add(new Pair(4, 0));

        int[] dist = zeroOneBFS(graph, 0, V);
        System.out.println("Shortest distances from node 0: " + Arrays.toString(dist));
    }
}

```

### 🧠 Time Complexity:

- **O(V + E)** — each node and edge processed at most once.

---

## ✅ 2. Multi-Source BFS (Multiple Sources → All Nodes)

### 🔍 Problem Type:

- You have **multiple starting nodes**, and you want to compute the **shortest distance to all nodes**.

### 🔥 Common in:

- Fire spreading from multiple cells.
- Rotting oranges (Leetcode 994).
- Distance from multiple gates (Walls and Gates).

---

### 🚀 Key Idea:

- Instead of one source in BFS, you initialize the queue with **all source nodes**.
- Start BFS from **all of them in parallel**.

---

### ✅ Java Template:

```java
public class MultiSourceBFS {
    public static int[][] bfs(int[][] grid, List<int[]> sources) {
        int m = grid.length, n = grid[0].length;
        int[][] dist = new int[m][n];
        for (int[] row : dist)
            Arrays.fill(row, -1);

        Queue<int[]> q = new LinkedList<>();
        for (int[] source : sources) {
            q.offer(source);
            dist[source[0]][source[1]] = 0;
        }

        int[][] dirs = {{0,1},{1,0},{0,-1},{-1,0}};
        while (!q.isEmpty()) {
            int[] cell = q.poll();
            int x = cell[0], y = cell[1];

            for (int[] d : dirs) {
                int nx = x + d[0], ny = y + d[1];
                if (nx >= 0 && ny >= 0 && nx < m && ny < n &&
                    grid[nx][ny] == 0 && dist[nx][ny] == -1) {
                    dist[nx][ny] = dist[x][y] + 1;
                    q.offer(new int[]{nx, ny});
                }
            }
        }
        return dist;
    }
}

```

---

### 🧠 Time Complexity:

- **O(M × N)** for a grid or `O(V + E)` for a graph — same as normal BFS.

---

## 🧾 Summary:

| Algorithm | Use Case | Time Complexity | Data Structure |
| --- | --- | --- | --- |
| **0-1 BFS** | Shortest path with 0/1 edge weights | `O(V + E)` | Deque |
| **Multi-Source BFS** | Shortest path from multiple sources | `O(V + E)` / `O(M×N)` | Queue |

---

---

## 🧠 What is DSU / Union-Find?

DSU is a data structure that efficiently keeps track of elements partitioned into disjoint (non-overlapping) sets.

Used for:

- **Cycle detection in graphs**
- **Kruskal’s MST**
- **Connected components**
- **Dynamic connectivity queries**

---

## 🧩 Core Operations

1. **Find(x)** – returns the representative (leader) of the set containing `x`.
2. **Union(x, y)** – merges the sets containing `x` and `y`.

---

## 🚀 Optimizations for FAANG-level Performance

### ✅ 1. **Path Compression** (Optimizes `find`)

When calling `find(x)`, we recursively point every node on the path to the root, flattening the structure.

### ✅ 2. **Union by Rank / Size**

Instead of always attaching one tree to another arbitrarily:

- Attach the **smaller rank tree** under the **larger one**.
- This minimizes height, making future `find` calls faster.

---

## 🔥 Final Time Complexity

With both optimizations:

- **Almost O(1)** per operation.
- Technically: **O(α(N))**, where α is the inverse Ackermann function, which grows super slowly (≈ 4 for all practical N).

---

## ✅ Java Implementation of DSU with Rank & Path Compression

```java
public class DSU {
    int[] parent, rank;

    public DSU(int n) {
        parent = new int[n];
        rank = new int[n];  // rank[i] = approx. height of tree rooted at i
        for (int i = 0; i < n; i++) parent[i] = i;
    }

    // Find with path compression
    public int find(int x) {
        if (parent[x] != x)
            parent[x] = find(parent[x]); // path compression
        return parent[x];
    }

    // Union by rank
    public boolean union(int x, int y) {
        int px = find(x), py = find(y);
        if (px == py) return false; // already in same set

        if (rank[px] < rank[py]) {
            parent[px] = py;
        } else if (rank[px] > rank[py]) {
            parent[py] = px;
        } else {
            parent[py] = px;
            rank[px]++;
        }
        return true;
    }
}

```

---

## 🔍 Example: Detecting Cycle in Undirected Graph Using DSU

```java
public boolean hasCycle(int V, int[][] edges) {
    DSU dsu = new DSU(V);
    for (int[] edge : edges) {
        int u = edge[0], v = edge[1];
        if (!dsu.union(u, v)) return true; // already connected → cycle
    }
    return false;
}

```

---

## 📌 Use Cases in FAANG Interviews

| Problem Type | DSU Role |
| --- | --- |
| **Cycle Detection (Undirected Graph)** | Detect if 2 nodes already connected |
| **Kruskal's MST** | Prevent cycles while picking edges |
| **Connected Components** | Group elements |
| **Dynamic connectivity** | Add edges and check connectivity fast |
| **Accounts Merge** | Merge accounts with shared emails |
| **Social Network Friend Circles** | Group users by friendship chains |

---

## 🧪 Rank vs Size — Which to Use?

- **Rank** tracks height → good for depth-sensitive unions.
- **Size** tracks set size → helps in count-based unions.

Functionally, both optimize similarly. Choose based on what's more intuitive in your problem.

---

## 🧾 Summary:

| Optimization | Description | Benefit |
| --- | --- | --- |
| **Path Compression** | Flattens tree during `find()` | Fast future lookups |
| **Union by Rank** | Always attach shorter tree to taller one | Keeps tree shallow |
| **Time Complexity** | Amortized O(α(N)) per operation | Practically constant |

---

## Questions:

## Easy Problems

- Flood Fill
- Is Graph Bipartite?
- Clone Graph
- Graph Valid Tree
- Number of Provinces
- **Find Center of Star Graph**

## Medium Problems

- **Detect Cycle in Directed Graph**
- **Detect Cycle in Undirected Graph**
- Pacific Atlantic Water Flow
- Course Schedule
- Word Ladder
- Surrounded Regions
- Bellman-Ford Algorithm Problem
- Minimum Height Trees
- Shortest Bridge
- Minimum Time to Collect All Apples in a Tree
- Number of Operations to Make Network Connected
- Course Schedule II
- Alien Dictionary
- Rotting Oranges
- Network Delay Time
- Cheapest Flights Within K Stops
- Path With Minimum Effort
- Find the City With the Smallest Number of Neighbors at a Threshold Distance
- Number of Ways to Arrive at Destination
- Redundant Connection
- Couples Holding Hands
- Number of Islands II
- **Find Eventual Safe States**
- Satisfiability of Equality Equations
- Min Cost to Connect All Points
- Most Stones Removed with Same Row or Column
- Course Schedule IV
- Walls and Gates
- 01 Matrix
- Minimum Cost to Make at Least One Valid Path in a Grid
- Reorder Routes to Make All Paths Lead to the City Zero
- Water and Jug Problem
- Get Watched Videos by Your Friends
- Bus Routes

## Hard Problems

- Shortest Path Visiting All Nodes
- Word Ladder II
- Tree Diameter
- Sort Items by Groups Respecting Dependencies
- Graph Connectivity With Threshold
- Maximum Score From Removing Stones
- Removing Minimum Number of Magic Beans

EXTRA:

---

# What is Cyclic Swapping?

**Cyclic swapping** (or **cyclic rotation**) means rearranging elements of an array such that elements are rotated or swapped in a cycle. This often involves moving elements to new positions in a circular fashion.

Example:

For array `[1, 2, 3, 4, 5]`, a right cyclic rotation by 2 positions results in `[4, 5, 1, 2, 3]`.

---

# Common Uses of Cyclic Swapping in DSA

- Rotating arrays
- In-place rearrangements without extra space
- Permutation cycles
- Problems involving shifting elements in a cycle

---

# Basic Cyclic Swapping Algorithm in Java

Suppose you want to **rotate an array to the right by k positions**. The cyclic swapping approach involves:

1. Identify the cycle length (GCD of array length and k).
2. For each cycle, move elements within that cycle.
3. Stop when a cycle is complete and move to the next cycle.

---

### Step-by-step Cyclic Rotation (Right rotate by k):

```java
public class CyclicRotation {

    // Function to right rotate array by k positions using cyclic swapping
    public static void rightRotate(int[] arr, int k) {
        int n = arr.length;
        k = k % n;  // In case k > n

        int count = 0;  // count of elements moved
        for (int start = 0; count < n; start++) {
            int current = start;
            int prev = arr[start];

            do {
                int next = (current + k) % n;
                int temp = arr[next];
                arr[next] = prev;
                prev = temp;
                current = next;
                count++;
            } while (start != current);
        }
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};
        int k = 2;

        System.out.println("Original array: ");
        for (int num : arr) System.out.print(num + " ");
        System.out.println();

        rightRotate(arr, k);

        System.out.println("Array after right rotation by " + k + ":");
        for (int num : arr) System.out.print(num + " ");
    }
}

public int miniSwapsArray(int[] row) {
    int res = 0, N = row.length;

    for (int i = 0; i < N; i++) {
		for (int j = row[i]; i != j; j = row[i]) {
			swap(row, i, j);
			res++;
		}
    }

    return res;
}

private void swap(int[] arr, int i, int j) {
    int t = arr[i];
    arr[i] = arr[j];
    arr[j] = t;
}
```

---

### Explanation:

- We rotate by `k` positions.
- We perform cyclic swaps inside cycles. The number of cycles is the gcd of `n` and `k`.
- The do-while loop moves each element in the cycle once.
- This approach works **in-place** with O(1) extra space and O(n) time.

---

# Understanding the Cyclic Swapping Steps:

For arr = `[1,2,3,4,5]`, k=2:

- n=5, k=2
- gcd(5,2) = 1 → only 1 cycle
- Start at index 0:
    - Move element at 0 to (0+2)%5 = 2
    - Move element at 2 to (2+2)%5 = 4
    - Move element at 4 to (4+2)%5 = 1
    - Move element at 1 to (1+2)%5 = 3
    - Move element at 3 to (3+2)%5 = 0, cycle complete.

Result after swaps: `[4,5,1,2,3]`

---

# LeetCode Problems Using Cyclic Swapping:

Here are some problems where cyclic swapping or similar rotation concepts help:

1. **Rotate Array (LeetCode 189)**
    
    Rotate an array to the right by k steps.
    
    [LeetCode 189](https://leetcode.com/problems/rotate-array/)
    
2. **Next Permutation (LeetCode 31)**
    
    Rearrange numbers to get the next lexicographical permutation. Cyclic swaps are used internally.
    
    [LeetCode 31](https://leetcode.com/problems/next-permutation/)
    
3. **Find the Duplicate Number (LeetCode 287)**
    
    Uses cycle detection in array indexing.
    
    [LeetCode 287](https://leetcode.com/problems/find-the-duplicate-number/)
    
4. **Circular Array Loop (LeetCode 457)**
    
    Detect cycles in the array with a cyclic move.
    
    [LeetCode 457](https://leetcode.com/problems/circular-array-loop/)
    

---

# Summary:

- Cyclic swapping involves moving elements along cycles.
- Useful for array rotation and rearrangement problems.
- Implemented with in-place swaps following index cycles.
- Efficient in time (O(n)) and space (O(1)).

---