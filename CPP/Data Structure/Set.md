# Set
### Description
A `set` is a container that stores unique elements in a sorted order.

### Syntax & Operations

- **Declare a Set:**
  ```cpp
  set<int> s;
  ```
- **Insert Elements:**
  ```cpp
  s.insert(5);
  s.insert(2);
  s.insert(8);
  s.insert(2); // Duplicate, won't be added
  ```
- **Erase Elements:**
  ```cpp
  s.erase(5);
  ```
- **Check Existence:**
  ```cpp
  if (s.find(2) != s.end()) {
      // Element exists
  }
  ```
- **Iterate Over Elements:**
  ```cpp
  for (auto it = s.begin(); it != s.end(); ++it) {
      // Access *it
  }
  ```

### Notes
- Stores unique elements in sorted order.
- Best for scenarios requiring ordered unique elements.

---

## Multiset (Sorted Duplicate Elements)
### Description
A `multiset` is similar to a `set` but allows duplicate elements.

### Syntax & Operations

- **Declare a Multiset:**
  ```cpp
  multiset<int> ms;
  ```
- **Insert Elements:**
  ```cpp
  ms.insert(5);
  ms.insert(2);
  ms.insert(8);
  ms.insert(2); // Duplicate allowed
  ```
- **Erase One Instance of an Element:**
  ```cpp
  ms.erase(ms.find(2));
  ```
- **Count Occurrences:**
  ```cpp
  int count = ms.count(2);
  ```

### Notes
- Allows duplicate elements.
- Useful for frequency-based data storage.

---

## Unordered Set (Unique Elements, Unsorted Order)
### Description
An `unordered_set` stores unique elements but does not guarantee order.

### Syntax & Operations

- **Declare an Unordered Set:**
  ```cpp
  unordered_set<int> us;
  ```
- **Insert Elements:**
  ```cpp
  us.insert(5);
  us.insert(2);
  us.insert(8);
  us.insert(2); // Duplicate, won't be added
  ```
- **Erase Elements:**
  ```cpp
  us.erase(5);
  ```
- **Check Existence:**
  ```cpp
  if (us.find(2) != us.end()) {
      // Element exists
  }
  ```

### Notes
- Stores unique elements with faster average time complexity.
- Order of elements is not maintained.
- Best for scenarios requiring fast lookups without ordering constraints.

