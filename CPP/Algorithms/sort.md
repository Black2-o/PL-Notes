# Sorting Algorithms

## Sorting an Array

### Description
Sorting an array in C++ can be efficiently done using the `sort()` function from the algorithm library. It uses a variation of the QuickSort, HeapSort, and InsertionSort algorithms for optimal performance.

### Syntax & Operations

- **Sort an Integer Array in Ascending Order:**
  ```cpp
  sort(arr, arr + n);
  ```
- **Sort an Integer Array in Descending Order:**
  ```cpp
  sort(arr, arr + n, greater<int>());
  ```
- **Sort a Character Array:**
  ```cpp
  sort(charArr, charArr + n);
  ```

## Sorting a Vector

### Description
Vectors can be sorted similarly using `sort()`.

### Syntax & Operations

- **Sort a Vector in Ascending Order:**
  ```cpp
  sort(vec.begin(), vec.end());
  ```
- **Sort a Vector in Descending Order:**
  ```cpp
  sort(vec.begin(), vec.end(), greater<int>());
  ```

## Sorting a Vector of Pairs

### Description
A vector of pairs can be sorted based on the first or second element using custom comparators.

### Syntax & Operations

- **Sort by First Element (Ascending Order):**
  ```cpp
  sort(vec.begin(), vec.end());
  ```
- **Sort by First Element (Descending Order):**
  ```cpp
  sort(vec.begin(), vec.end(), greater<pair<int, int>>());
  ```
- **Sort by Second Element (Ascending Order):**
  ```cpp
  sort(vec.begin(), vec.end(), [](pair<int, int> a, pair<int, int> b) {
      return a.second < b.second;
  });
  ```
- **Sort by Second Element (Descending Order):**
  ```cpp
  sort(vec.begin(), vec.end(), [](pair<int, int> a, pair<int, int> b) {
      return a.second > b.second;
  });
  ```

## Custom Comparators

### Description
Custom comparators allow sorting based on specific conditions using lambda functions.

### Syntax & Examples

- **Sorting in Increasing Order Based on the Second Value:**
  ```cpp
  auto comp = [](pair<int, int> a, pair<int, int> b) {
      return a.second < b.second;
  };
  sort(vec.begin(), vec.end(), comp);
  ```
- **Sorting in Decreasing Order Based on the First Value:**
  ```cpp
  auto comp = [](pair<int, int> a, pair<int, int> b) {
      return a.first > b.first;
  };
  sort(vec.begin(), vec.end(), comp);
  ```
- **Sorting by Absolute Difference from a Given Value (e.g., x):**
  ```cpp
  int x = 10;
  auto comp = [x](int a, int b) {
      return abs(a - x) < abs(b - x);
  };
  sort(arr, arr + n, comp);
  ```
- **Sorting in Descending Order Using Boolean Function:**
  ```cpp
  bool comp(int a, int b) {
      return a > b;
  }
  sort(arr, arr + n, comp);
  ```

### Notes
- The `sort()` function is highly optimized and provides an average time complexity of **O(n log n)**.
- Comparators help in sorting based on custom logic and specific conditions.
- Sorting vectors of pairs is useful in problems related to scheduling, intervals, and rankings.

