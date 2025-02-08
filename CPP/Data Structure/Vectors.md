# Vectors

### Description

A `vector` is a dynamic array provided by the Standard Template Library (STL) in C++. It can grow or shrink in size and provides fast random access to elements. Vectors are commonly used for efficient storage and retrieval in dynamic scenarios.

### Syntax & Operations

- **Declare a Vector:**
  ```cpp
  vector<int> v;
  ```
- **Insert Elements:**
  ```cpp
  v.push_back(10);  // Adds an element to the end
  ```
- **Access Elements:**
  ```cpp
  int x = v[0];  // Accesses the first element
  ```
- **Modify Elements:**
  ```cpp
  v[1] = 30;  // Modifies the element at index 1
  ```
- **Remove Last Element:**
  ```cpp
  v.pop_back();  // Removes the last element
  ```
- **Iterate Over a Vector:**
  ```cpp
  for(const auto& val : v) {
      cout << val << " ";
  }
  ```

- **Insert and Erase Examples:**
  ```cpp
  vector<int> v = {1, 2, 3, 4};
  v.insert(v.begin() + 2, 10);  // Inserts 10 at index 2
  v.erase(v.begin() + 1);       // Removes element at index 1
  ```

### Vector Methods Summary

- `v.push_back(x)`: Adds element x to the end
- `v.pop_back()`: Removes the last element
- `v.size()`: Returns the number of elements
- `v.empty()`: Checks if the vector is empty
- `v.clear()`: Removes all elements
- `v.insert(it, x)`: Inserts x at position it
- `v.erase(it)`: Removes element at iterator it
- `v.erase(it1, it2)`: Removes range [it1, it2)
- `v.front()`: Accesses the first element
- `v.back()`: Accesses the last element
- `v.resize(n)`: Resizes the vector to contain n elements
- `v.swap(v2)`: Swaps elements of v with v2
- `v.assign(n, x)`: Assigns n copies of x to the vector

### Notes

- Vectors are versatile and commonly used in competitive programming.
- They offer dynamic resizing and support multiple built-in functions for efficient operations.

