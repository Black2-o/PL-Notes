🧠 **1. Graphs**

📘 **Concept:**
Graphs are collections of nodes (vertices) connected by edges. They are used to model networks, paths, relationships.

* Types:

  * Directed / Undirected
  * Weighted / Unweighted
  * Cyclic / Acyclic
  * Connected / Disconnected

📋 **Graph Representation:**

```cpp
// Adjacency List
vector<vector<int>> adj(n);
adj[u].push_back(v);

// For weighted graph
vector<pair<int, int>> adj[n];
adj[u].push_back({v, weight});
```

📋 **DFS (Depth-First Search):**

```cpp
void dfs(int u, vector<vector<int>>& adj, vector<bool>& visited) {
    visited[u] = true;
    for (int v : adj[u]) {
        if (!visited[v]) dfs(v, adj, visited);
    }
}
```

📋 **BFS (Breadth-First Search):**

```cpp
void bfs(int start, vector<vector<int>>& adj) {
    queue<int> q;
    vector<bool> visited(adj.size(), false);
    q.push(start);
    visited[start] = true;

    while (!q.empty()) {
        int u = q.front(); q.pop();
        for (int v : adj[u]) {
            if (!visited[v]) {
                visited[v] = true;
                q.push(v);
            }
        }
    }
}
```

📋 **Dijkstra’s Algorithm (Shortest Path):**

```cpp
priority_queue<pair<int,int>, vector<pair<int,int>>, greater<>> pq;
vector<int> dist(n, INF);
dist[src] = 0;
pq.push({0, src});

while (!pq.empty()) {
    auto [d, u] = pq.top(); pq.pop();
    if (d > dist[u]) continue;
    for (auto [v, w] : adj[u]) {
        if (dist[v] > d + w) {
            dist[v] = d + w;
            pq.push({dist[v], v});
        }
    }
}
```

🧠 **Use Cases:**

* Finding paths
* Cycle detection
* Shortest paths (Dijkstra, BFS, Bellman-Ford)
* MST (Prim’s, Kruskal’s)
* Topological Sort

---

💡 **2. Dynamic Programming (DP)**

📘 **Concept:**
Break a problem into overlapping subproblems and use memoization or tabulation to avoid recomputation.

* Top-down: Recursion + memo
* Bottom-up: Iterative DP

📋 **Fibonacci (Top-down):**

```cpp
int dp[100];
int fib(int n) {
    if (n <= 1) return n;
    if (dp[n] != -1) return dp[n];
    return dp[n] = fib(n-1) + fib(n-2);
}
```

📋 **Fibonacci (Bottom-up):**

```cpp
int fib(int n) {
    vector<int> dp(n+1);
    dp[0] = 0, dp[1] = 1;
    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i-1] + dp[i-2];
    }
    return dp[n];
}
```

📋 **0/1 Knapsack:**

```cpp
int dp[n+1][W+1];
for (int i = 0; i <= n; i++) {
    for (int w = 0; w <= W; w++) {
        if (i == 0 || w == 0) dp[i][w] = 0;
        else if (wt[i-1] <= w)
            dp[i][w] = max(val[i-1] + dp[i-1][w - wt[i-1]], dp[i-1][w]);
        else
            dp[i][w] = dp[i-1][w];
    }
}
```

🧠 **Use Cases:**

* Counting paths/ways
* Optimization problems (min/max)
* Subset problems
* Partitioning
* LIS, LCS, Edit Distance

---

🌳 **3. Trees**

📘 **Concept:**
Trees are special graphs with no cycles and one root (in rooted trees).

* Binary tree: Each node has ≤2 children
* BST: Binary tree with ordering property
* Tree DP: DP where nodes depend on subtrees

📋 **DFS on Tree:**

```cpp
void dfs(int u, int parent, vector<vector<int>>& tree) {
    for (int v : tree[u]) {
        if (v != parent) {
            dfs(v, u, tree);
        }
    }
}
```

📋 **Tree Height Calculation:**

```cpp
int height(int u, int parent, vector<vector<int>>& tree) {
    int h = 0;
    for (int v : tree[u]) {
        if (v != parent) {
            h = max(h, 1 + height(v, u, tree));
        }
    }
    return h;
}
```

📋 **Binary Tree Inorder Traversal:**

```cpp
void inorder(TreeNode* root) {
    if (!root) return;
    inorder(root->left);
    cout << root->val << " ";
    inorder(root->right);
}
```

📋 **Lowest Common Ancestor (Binary Tree):**

```cpp
TreeNode* LCA(TreeNode* root, TreeNode* p, TreeNode* q) {
    if (!root || root == p || root == q) return root;
    TreeNode* left = LCA(root->left, p, q);
    TreeNode* right = LCA(root->right, p, q);
    if (left && right) return root;
    return left ? left : right;
}
```

🧠 **Use Cases:**

* Hierarchical data
* Path/ancestor queries
* Subtree queries
* Tree-based DP
* Segment Tree/Fenwick Tree (advanced)

---

✅ **Quick Summary Table:**

| Topic  | Key Techniques                | Time Complexity | Use Cases                       |
| ------ | ----------------------------- | --------------- | ------------------------------- |
| Graphs | DFS, BFS, Dijkstra, Topo Sort | V+E, V log V    | Shortest Path, MST, Cycle Check |
| DP     | Memoization, Tabulation       | Varies (O(N^2)) | Count/optimize, LIS, Knapsack   |
| Trees  | DFS, Recursion, Tree DP       | O(N)            | Subtree, LCA, Tree path queries |
