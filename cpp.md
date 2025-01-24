# C++ Notes

---
### User Input / Output
- **Input**: `cin` is used for taking input.
  ```cpp
  int x;
  cin >> x;
  ```
- **Output**: `cout` is used for printing output.
  ```cpp
  cout << "Value: " << x << endl;
  ```

---
### Data Types
- **Basic types**:
  - `int` (integer numbers)
  - `float` (decimal numbers)
  - `double` (large decimal numbers)
  - `char` (single character)
  - `bool` (true/false)
  - `string` (text - needs `#include<string>`) 

---
### If-Else Statements
- **Syntax**:
  ```cpp
  if (condition) {
      // code when condition is true
  } else {
      // code when condition is false
  }
  ```

---
### Switch Statement
- **Syntax**:
  ```cpp
  switch (variable) {
      case value1:
          // code for value1
          break;
      case value2:
          // code for value2
          break;
      default:
          // default code
  }
  ```

---
### Arrays and Strings
- **Arrays**: Collection of elements of the same type.
  ```cpp
  int arr[5] = {1, 2, 3, 4, 5};
  ```
- **Strings**: Sequence of characters. Requires `#include<string>`.
  ```cpp
  string name = "John";
  ```

---
### For Loops
- **Syntax**:
  ```cpp
  for (int i = 0; i < n; i++) {
      // code block
  }
  ```
  Example:
  ```cpp
  for (int i = 1; i <= 5; i++) {
      cout << i << endl;
  }
  ```

---
### While Loops
- **Syntax**:
  ```cpp
  while (condition) {
      // code block
  }
  ```
  Example:
  ```cpp
  int i = 1;
  while (i <= 5) {
      cout << i << endl;
      i++;
  }
  ```

---
### Functions (Pass by Reference and Value)
- **Pass by Value**: The function gets a copy of the argument.
  ```cpp
  void display(int x) {
      cout << x << endl;
  }
  ```
- **Pass by Reference**: The function gets the reference to the argument.
  ```cpp
  void update(int &x) {
      x = x + 10;
  }
  ```

---
### Time Complexity Basics
- **Basics**:
  - Constant operations: `O(1)`
  - Loops:
    - Simple loop: `O(n)`
    - Nested loop: `O(n^2)`
- **Examples**:
  ```cpp
  // Example 1: O(n)
  for (int i = 0; i < n; i++) {
      cout << i << endl;
  }

  // Example 2: O(n^2)
  for (int i = 0; i < n; i++) {
      for (int j = 0; j < n; j++) {
          cout << i << " " << j << endl;
      }
  }
  ```

