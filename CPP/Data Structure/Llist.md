# List

### Description
A `list` in C++ is a doubly linked list that allows fast insertion and deletion at any position. Unlike arrays or vectors, lists provide efficient modifications but do not allow direct access by index.

### Syntax & Operations

- **Declare a List:**
  ```cpp
  list<int> lst;
  ```
- **Insert Elements at the Back:**
  ```cpp
  lst.push_back(10); // Adds 10 at the end
  lst.push_back(20);
  ```
- **Insert Elements at the Front:**
  ```cpp
  lst.push_front(5); // Adds 5 at the beginning
  ```
- **Remove Elements from the Front:**
  ```cpp
  lst.pop_front(); // Removes the first element
  ```
- **Remove Elements from the Back:**
  ```cpp
  lst.pop_back(); // Removes the last element
  ```
- **Insert at a Specific Position:**
  ```cpp
  auto it = lst.begin();
  advance(it, 1); // Move iterator to second position
  lst.insert(it, 15); // Inserts 15 at the second position
  ```
- **Erase a Specific Element:**
  ```cpp
  lst.erase(it); // Removes the element at iterator position
  ```
- **Iterate Over Elements:**
  ```cpp
  for (auto &val : lst) {
      cout << val << " ";
  }
  ```
- **Check If List is Empty:**
  ```cpp
  if (lst.empty()) {
      // List is empty
  }
  ```
- **Get List Size:**
  ```cpp
  int size = lst.size();
  ```

### List Methods Summary
- `lst.push_back(value)`: Adds an element to the end
- `lst.push_front(value)`: Adds an element to the front
- `lst.pop_back()`: Removes the last element
- `lst.pop_front()`: Removes the first element
- `lst.insert(iterator, value)`: Inserts an element at a given position
- `lst.erase(iterator)`: Removes an element at a given position
- `lst.begin()`, `lst.end()`: Iterators to traverse the list
- `lst.empty()`: Checks if the list is empty
- `lst.size()`: Returns the number of elements in the list

### Notes
- Lists are useful when frequent insertions and deletions are required.
- Unlike vectors, lists do not provide direct access via indexing (i.e., `lst[i]` is not allowed).
- Suitable for implementing stacks, queues, and other linked data structures.

