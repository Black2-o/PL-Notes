# C++ Notes

---

### Base Structure of a C++ Program

```cpp
// #include <bits/stdc++.h>
#include <iostream>
using namespace std;

int main() {
    // Your code goes here
    return 0;
}
```

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

- **Input an Array Using For Loop**:
  ```cpp
  int arr[5];
  for (int i = 0; i < 5; i++) {
      cin >> arr[i];
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

### Do-While Loop

- **Syntax**:
  ```cpp
  do {
      // code block
  } while (condition);
  ```
  Example:
  ```cpp
  int i = 1;
  do {
      cout << i << endl;
      i++;
  } while (i <= 5);
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

