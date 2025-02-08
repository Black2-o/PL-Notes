# Pairs

### Description
A `pair` holds two related values, often used to store and access data efficiently. Useful for mapping keys to values or managing coordinate pairs.

### Syntax & Operations
- **Create a Pair:**
  ```cpp
  pair<int, char> p = {1, 'A'};
  ```
- **Access Elements:**
  ```cpp
  int x = p.first;  // Access first element
  char y = p.second; // Access second element
  ```
- **Modify Elements:**
  ```cpp
  p.first = 100;
  p.second = 'Z';
  ```
- **Use make_pair:**
  ```cpp
  auto q = make_pair(10, 'X');
  ```

### Vector of Pairs
Storing multiple pairs is common using vectors.
```cpp
vector<pair<int, int>> vp;

int n = 3;
int d[] = {1, 3, 5};
int p[] = {2, 4, 6};

for(int i = 0; i < n; i++) {
    vp.push_back(make_pair(d[i], p[i]));
}

// Access and print pairs from the vector
for (const auto& pr : vp) {
    cout << pr.first << ", " << pr.second << endl;
}
```
**Summary:** This example demonstrates how to store pairs in a vector and efficiently iterate through them for access and display.

