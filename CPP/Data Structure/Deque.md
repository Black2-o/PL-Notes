# Deque (Double-Ended Queue)

### Description
A `deque` (double-ended queue) allows insertion and deletion from both the front and the back, making it more flexible than a queue.

### Syntax & Operations

- **Declare a Deque:**
  ```cpp
  deque<int> dq;
  ```
- **Push Elements to the Back:**
  ```cpp
  dq.push_back(10); // Adds 10 to the back
  dq.push_back(20);
  ```
- **Push Elements to the Front:**
  ```cpp
  dq.push_front(5); // Adds 5 to the front
  ```
- **Pop Elements from the Front:**
  ```cpp
  dq.pop_front(); // Removes the front element
  ```
- **Pop Elements from the Back:**
  ```cpp
  dq.pop_back(); // Removes the last element
  ```
- **Access Front Element:**
  ```cpp
  int frontElement = dq.front(); // Retrieves the front element
  ```
- **Access Back Element:**
  ```cpp
  int backElement = dq.back(); // Retrieves the last element
  ```
- **Check If Deque is Empty:**
  ```cpp
  if (dq.empty()) {
      // Deque is empty
  }
  ```
- **Get Deque Size:**
  ```cpp
  int size = dq.size();
  ```

### Deque Methods Summary
- `dq.push_front(value)`: Adds an element to the front
- `dq.push_back(value)`: Adds an element to the back
- `dq.pop_front()`: Removes the front element
- `dq.pop_back()`: Removes the last element
- `dq.front()`: Returns the front element
- `dq.back()`: Returns the back element
- `dq.empty()`: Checks if the deque is empty
- `dq.size()`: Returns the number of elements in the deque

### Notes
- A deque supports insertion and deletion from both ends.
- Useful in scenarios where both FIFO and LIFO operations are needed.

