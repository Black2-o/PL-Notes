# Greedy Algorithms

## Description
Greedy algorithms are a problem-solving approach where the best possible choice is made at each step with the hope of finding the global optimal solution. They do not always guarantee the best solution, but they work well for many optimization problems.

### Key Characteristics
- **Local Optimization:** Greedy algorithms make the best decision at each step without reconsidering past choices.
- **Fast and Efficient:** Usually have a time complexity of **O(n log n)** or **O(n)**.
- **Works for Certain Problems:** Not all problems can be solved optimally using greedy strategies.

## Steps to Solve a Problem Using Greedy Algorithm
1. **Identify the optimal substructure:** Check if the problem can be broken down into subproblems that can be solved greedily.
2. **Choose a greedy strategy:** Find the best choice at each step.
3. **Prove its correctness (if needed):** Some problems require mathematical proof to confirm that a greedy approach works.
4. **Implement the solution:** Use sorting, priority queues, or simple loops to execute the algorithm efficiently.

## Common Greedy Algorithm Problems

### 1. Activity Selection Problem
**Problem:** Given `n` activities with start and end times, select the maximum number of non-overlapping activities.

**Approach:**
- Sort activities based on their finishing time.
- Pick the activity that finishes the earliest and does not overlap with previously chosen activities.

**Implementation:**
```cpp
sort(activities.begin(), activities.end(), [](pair<int, int> a, pair<int, int> b) {
    return a.second < b.second;
});
```

### 2. Fractional Knapsack Problem
**Problem:** Given weights and values of `n` items, put them in a knapsack of capacity `W` to maximize total value. You can take fractional parts of items.

**Approach:**
- Calculate **value/weight** ratio for each item.
- Sort items in decreasing order of ratio.
- Pick items with the highest ratio until the knapsack is full.

**Implementation:**
```cpp
sort(items.begin(), items.end(), [](Item a, Item b) {
    return (double)a.value / a.weight > (double)b.value / b.weight;
});
```

### 3. Huffman Coding (Optimal Prefix Code)
**Problem:** Given `n` characters with frequencies, build an optimal prefix-free encoding.

**Approach:**
- Use a **min heap** to repeatedly merge the two least frequent characters.
- Construct a binary tree where frequently used characters have shorter codes.

**Implementation:**
```cpp
priority_queue<Node*, vector<Node*>, Compare> minHeap;
```

### 4. Minimum Number of Coins (Change Problem)
**Problem:** Given denominations and a total amount, find the minimum number of coins needed.

**Approach:**
- Start with the largest denomination and take as many as possible.
- Move to smaller denominations until the total is reached.

**Implementation:**
```cpp
for (int i = 0; i < coins.size(); i++) {
    while (amount >= coins[i]) {
        amount -= coins[i];
        result.push_back(coins[i]);
    }
}
```

### Notes
- Greedy algorithms work best when **greedy choice property** and **optimal substructure** hold.
- If a problem cannot be solved optimally with a greedy approach, consider **dynamic programming** instead.
- Common data structures used: **Sorting, Priority Queue, Heap, Greedy Sorting**.

