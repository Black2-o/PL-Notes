# Queue

### Description
A `queue` is a container in C++ that follows the First In, First Out (FIFO) principle. Elements are added at the back and removed from the front.

### Syntax & Operations

- **Declare a Queue:**
  ```cpp
  queue<int> q;
  ```
- **Push Elements:**
  ```cpp
  q.push(10); // Adds 10 to the back of the queue
  q.push(20);
  ```
- **Pop Elements:**
  ```cpp
  q.pop(); // Removes the front element
  ```
- **Access Front Element:**
  ```cpp
  int frontElement = q.front(); // Retrieves the front element
  ```
- **Access Back Element:**
  ```cpp
  int backElement = q.back(); // Retrieves the last element
  ```
- **Check If Queue is Empty:**
  ```cpp
  if (q.empty()) {
      // Queue is empty
  }
  ```
- **Get Queue Size:**
  ```cpp
  int size = q.size();
  ```

### Queue Methods Summary
- `q.push(value)`: Adds an element to the back of the queue
- `q.pop()`: Removes the front element
- `q.front()`: Returns the front element
- `q.back()`: Returns the back element
- `q.empty()`: Checks if the queue is empty
- `q.size()`: Returns the number of elements in the queue

### Notes
- A queue follows FIFO (First In, First Out) order.
- Useful in scheduling problems, breadth-first search, and buffering.
