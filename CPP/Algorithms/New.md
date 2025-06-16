🧠 **1. Binary Search**

📘 **Concept:**
Efficient algorithm to find an element or optimize answer in a sorted space.

* Time complexity: O(log N)
* Works when:

  * Array is sorted
  * Answer space is monotonic

📋 **Template 1: Search in Sorted Array**

```cpp
int binarySearch(vector<int>& a, int target) {
    int low = 0, high = a.size() - 1;
    while (low <= high) {
        int mid = (low + high) / 2;
        if (a[mid] == target) return mid;
        else if (a[mid] < target) low = mid + 1;
        else high = mid - 1;
    }
    return -1; // Not found
}
```

📋 **Template 2: Binary Search on Answer**

```cpp
bool isOk(int mid) {
    // Define your condition here
    return true; // or false
}

int solve() {
    int low = 0, high = 1e9, ans = -1;
    while (low <= high) {
        int mid = (low + high) / 2;
        if (isOk(mid)) {
            ans = mid;
            high = mid - 1; // Minimize
        } else {
            low = mid + 1;
        }
    }
    return ans;
}
```

🧠 **Use Cases:**

* Find min/max that satisfies condition
* Lower/Upper bound
* Partitioning problems
* Classical problems like: Aggressive Cows, EKO (woodcutting), Allocate Books

---

🏃‍♂️ **2. Two Pointers**

📘 **Concept:**
Use two indexes to traverse array efficiently

* Time complexity: O(N) in most cases
* Mostly used in:

  * Subarrays / substrings
  * Pair sum problems
  * Sliding window problems

📋 **Template 1: Sliding Window**

```cpp
int solve(vector<int>& a, int k) {
    int left = 0, sum = 0, ans = 0;
    for (int right = 0; right < a.size(); right++) {
        sum += a[right];
        while (sum > k) {
            sum -= a[left++];
        }
        ans = max(ans, right - left + 1);
    }
    return ans;
}
```

📋 **Template 2: Find Pair with Sum**

```cpp
bool hasPair(vector<int>& a, int target) {
    sort(a.begin(), a.end());
    int i = 0, j = a.size() - 1;
    while (i < j) {
        int sum = a[i] + a[j];
        if (sum == target) return true;
        else if (sum < target) i++;
        else j--;
    }
    return false;
}
```

🧠 **Use Cases:**

* Longest substring with constraints
* Two sum (sorted array)
* Merge intervals
* Trapping rain water

---

⚙️ **3. Bitmasks**

📘 **Concept:**
Use bits to represent sets, states, toggles

* Efficient for subset generation
* Time complexity: usually O(2^N), N ≤ 20–25

📋 **Template 1: Generate All Subsets**

```cpp
int n = 4;
for (int mask = 0; mask < (1 << n); mask++) {
    for (int i = 0; i < n; i++) {
        if (mask & (1 << i)) {
            cout << "Take element " << i << "\n";
        }
    }
}
```

📋 **Bit Tricks:**

```cpp
int setBit(int mask, int i) {
    return mask | (1 << i);
}

int clearBit(int mask, int i) {
    return mask & ~(1 << i);
}

int toggleBit(int mask, int i) {
    return mask ^ (1 << i);
}

bool isBitSet(int mask, int i) {
    return (mask >> i) & 1;
}

int countSetBits(int mask) {
    return __builtin_popcount(mask);  // Built-in function in GCC
}
```

🧠 **Use Cases:**

* Subset generation
* Travelling Salesman (TSP)
* Light toggle puzzles
* State DP (bitmask dp)
* Count number of valid subsets

---

💪 **4. Brute Force**

📘 **Concept:**
Try all possible combinations / permutations

* Acceptable when total operations ≤ 1e7
* Time complexity: depends on approach

📋 **Template 1: Nested Loops**

```cpp
void solve(vector<int>& a) {
    int n = a.size();
    for (int i = 0; i < n; i++) {
        for (int j = i+1; j < n; j++) {
            // Try every pair
            if (a[i] + a[j] == 10) {
                cout << i << " " << j << "\n";
            }
        }
    }
}
```

📋 **Template 2: Try All Subsets**

```cpp
void solve(vector<int>& a) {
    int n = a.size();
    for (int mask = 0; mask < (1 << n); mask++) {
        int sum = 0;
        for (int i = 0; i < n; i++) {
            if (mask & (1 << i)) {
                sum += a[i];
            }
        }
        if (sum == 10) {
            cout << "Subset found with sum 10\n";
        }
    }
}
```

📋 **Template 3: Generate All Permutations**

```cpp
void solve(vector<int>& a) {
    sort(a.begin(), a.end());
    do {
        for (int x : a) cout << x << " ";
        cout << "\n";
    } while (next_permutation(a.begin(), a.end()));
}
```

🧠 **Use Cases:**

* N ≤ 10 or 12
* Small inputs, testing all possibilities
* Subset/permutation problems
* Optimization + pruning

---

✅ **Quick Summary Table:**

| Technique     | Time      | Usage Condition           | Common Use Case                    |
| ------------- | --------- | ------------------------- | ---------------------------------- |
| Binary Search | O(log N)  | Sorted / Monotonic        | Search, Minimize/Maximize problems |
| Two Pointers  | O(N)      | Sorted/Linear Arrays      | Pairs, subarrays, window problems  |
| Bitmasks      | O(2^N)    | N ≤ 20, subset/state prob | TSP, subset-sum, state DP          |
| Brute Force   | ≤ 1e7 ops | Small N / Try all         | All combinations, logic testing    |


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
