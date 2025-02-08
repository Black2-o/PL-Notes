# Map

### Description
A `map` is an associative container in C++ that stores key-value pairs in sorted order based on keys. It provides efficient lookups, insertions, and deletions with logarithmic time complexity.

### Syntax & Operations

- **Declare a Map:**
  ```cpp
  map<int, string> m; // Map with integer keys and string values
  ```
- **Insert Elements:**
  ```cpp
  m[1] = "One";  // Inserts key-value pair {1, "One"}
  m.insert({2, "Two"}); // Inserts key-value pair {2, "Two"}
  ```
- **Access Elements:**
  ```cpp
  string val = m[1];  // Accesses value associated with key 1
  ```
- **Modify Elements:**
  ```cpp
  m[1] = "Updated One";  // Modifies the value for key 1
  ```
- **Remove Elements:**
  ```cpp
  m.erase(1);  // Removes element with key 1
  ```
- **Iterate Over Elements:**
  ```cpp
  for (auto &entry : m) {
      cout << entry.first << ": " << entry.second << "\n";
  }
  ```

- **Find Elements:**
  ```cpp
  if (m.find(1) != m.end()) {
      cout << "Key 1 exists\n";
  }
  ```

### Map Methods Summary
- `m[key]`: Accesses or inserts a key-value pair
- `m.at(key)`: Accesses the value associated with the key without insertion
- `m.insert({key, value})`: Inserts a key-value pair
- `m.erase(key)`: Removes element with the given key
- `m.find(key)`: Returns an iterator to the element if found, or `m.end()` if not
- `m.size()`: Returns the number of elements
- `m.empty()`: Checks if the map is empty
- `m.clear()`: Removes all elements
- `m.count(key)`: Returns 1 if the key exists, 0 otherwise
- `m.begin()`, `m.end()`: Iterators to traverse the map

### Notes
- Maps store elements in a sorted order based on keys.
- Best used when ordered data is required.
- Provides logarithmic complexity for insertions, deletions, and lookups.

## Unordered Map

### Description
An `unordered_map` is an associative container in C++ that stores key-value pairs. It provides faster average time complexity due to hashing but does not maintain the order of elements.

### Syntax & Operations

- **Declare an Unordered Map:**
  ```cpp
  unordered_map<int, string> um; // Unordered map with integer keys and string values
  ```
- **Insert Elements:**
  ```cpp
  um[2] = "Two"; // Inserts key-value pair {2, "Two"}
  um.insert({3, "Three"});
  ```
- **Access Elements:**
  ```cpp
  string val = um[2];  // Accesses value associated with key 2
  ```
- **Modify Elements:**
  ```cpp
  um[2] = "Updated Two";  // Modifies the value for key 2
  ```
- **Remove Elements:**
  ```cpp
  um.erase(2);  // Removes element with key 2
  ```
- **Iterate Over Elements:**
  ```cpp
  for (auto &entry : um) {
      cout << entry.first << ": " << entry.second << "\n";
  }
  ```

- **Find Elements:**
  ```cpp
  if (um.find(2) != um.end()) {
      cout << "Key 2 exists\n";
  }
  ```

### Unordered Map Methods Summary
- `um[key]`: Accesses or inserts a key-value pair
- `um.at(key)`: Accesses the value associated with the key without insertion
- `um.insert({key, value})`: Inserts a key-value pair
- `um.erase(key)`: Removes element with the given key
- `um.find(key)`: Returns an iterator to the element if found, or `um.end()` if not
- `um.size()`: Returns the number of elements
- `um.empty()`: Checks if the map is empty
- `um.clear()`: Removes all elements
- `um.count(key)`: Returns 1 if the key exists, 0 otherwise
- `um.begin()`, `um.end()`: Iterators to traverse the unordered map

### Notes
- **unordered_map:** Suitable for fast access where order doesn't matter.
- Offers faster average time complexity compared to `map`.
- Avoid using `unordered_map` when ordering of elements is required.

