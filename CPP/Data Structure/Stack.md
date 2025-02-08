# Stack

### Description
A `stack` is a container in C++ that follows the Last In, First Out (LIFO) principle. Elements are added and removed only from the top of the stack.

### Syntax & Operations

- **Declare a Stack:**
  ```cpp
  stack<int> st;
  ```
- **Push Elements:**
  ```cpp
  st.push(10); // Pushes 10 onto the stack
  st.push(20);
  ```
- **Pop Elements:**
  ```cpp
  st.pop(); // Removes the top element
  ```
- **Access Top Element:**
  ```cpp
  int topElement = st.top(); // Retrieves the top element
  ```
- **Check If Stack is Empty:**
  ```cpp
  if (st.empty()) {
      // Stack is empty
  }
  ```
- **Get Stack Size:**
  ```cpp
  int size = st.size();
  ```

### Stack Methods Summary
- `st.push(value)`: Pushes an element onto the stack
- `st.pop()`: Removes the top element
- `st.top()`: Returns the top element
- `st.empty()`: Checks if the stack is empty
- `st.size()`: Returns the number of elements in the stack

### Notes
- A stack follows LIFO (Last In, First Out) order.
- Use stacks when you need to process elements in a reverse order.
- Ideal for problems involving recursion, backtracking, and expression evaluation.

