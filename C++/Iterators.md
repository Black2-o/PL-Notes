# **Iterators in C++**

## **Definition**
Iterators are objects that point to elements in a container (like arrays, vectors, or lists) and allow traversal through the container elements.

---

## **Types of Iterators**
1. **Input Iterator:** Reads elements sequentially (e.g., `cin`).
2. **Output Iterator:** Writes elements sequentially (e.g., `cout`).
3. **Forward Iterator:** Moves forward through the container.
4. **Bidirectional Iterator:** Moves both forward and backward (used in lists).
5. **Random Access Iterator:** Allows jumping to any position (used in vectors).

---

## **Common Methods**
| Method         | Description                        |
|----------------|------------------------------------|
| `begin()`      | Points to the first element       |
| `end()`        | Points to one past the last element |
| `rbegin()`     | Points to the last element (reverse) |
| `rend()`       | Points to one before the first (reverse) |
| `advance(it, n)` | Moves the iterator `n` positions  |
| `next(it)`     | Returns the next position of `it`  |
| `prev(it)`     | Returns the previous position      |

---

## **Basic Example**
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {1, 2, 3, 4, 5};

    // Using iterator to traverse
    for (vector<int>::iterator it = v.begin(); it != v.end(); ++it) {
        cout << *it << " "; // Dereference to access value
    }
    cout << endl;

    return 0;
}
```

---

## **Range-based Loops Using Iterators**
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {10, 20, 30, 40};

    for (auto it = v.begin(); it != v.end(); ++it) {
        cout << *it << " ";  // Outputs: 10 20 30 40
    }

    return 0;
}
```

---

## **Reverse Iterators**
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {1, 2, 3, 4, 5};

    for (auto it = v.rbegin(); it != v.rend(); ++it) {
        cout << *it << " ";  // Outputs: 5 4 3 2 1
    }

    return 0;
}
```

