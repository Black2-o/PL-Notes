# Heap

## Max Heap

### Description
A `max heap` is a binary tree where the parent node is always greater than or equal to its children. It is implemented using a priority queue in C++.

### Syntax & Operations

- **Declare a Max Heap:**
  ```cpp
  priority_queue<int> maxHeap;
  ```
- **Insert Elements:**
  ```cpp
  maxHeap.push(10);
  maxHeap.push(20);
  maxHeap.push(5);
  ```
- **Access Maximum Element:**
  ```cpp
  int maxElement = maxHeap.top(); // Retrieves the maximum element
  ```
- **Remove Maximum Element:**
  ```cpp
  maxHeap.pop();
  ```
- **Check If Heap is Empty:**
  ```cpp
  if (maxHeap.empty()) {
      // Heap is empty
  }
  ```
- **Get Heap Size:**
  ```cpp
  int size = maxHeap.size();
  ```

### Notes
- Always retrieves the largest element first.
- Useful in sorting, scheduling, and priority-based operations.

---

## Min Heap

### Description
A `min heap` is a binary tree where the parent node is always smaller than or equal to its children. It is implemented using a priority queue with greater comparator.

### Syntax & Operations

- **Declare a Min Heap:**
  ```cpp
  priority_queue<int, vector<int>, greater<int>> minHeap;
  ```
- **Insert Elements:**
  ```cpp
  minHeap.push(10);
  minHeap.push(20);
  minHeap.push(5);
  ```
- **Access Minimum Element:**
  ```cpp
  int minElement = minHeap.top(); // Retrieves the minimum element
  ```
- **Remove Minimum Element:**
  ```cpp
  minHeap.pop();
  ```
- **Check If Heap is Empty:**
  ```cpp
  if (minHeap.empty()) {
      // Heap is empty
  }
  ```
- **Get Heap Size:**
  ```cpp
  int size = minHeap.size();
  ```

### Notes
- Always retrieves the smallest element first.
- Useful in graph algorithms, merging k sorted lists, and scheduling tasks.

