# **Data Structures Notes in C++**

## **1. Pairs**
- A pair is a container that stores two values of potentially different types.
- Useful for storing related information.

### **Syntax and Usage**
```cpp
#include <iostream>
#include <utility>  // for std::pair
using namespace std;

int main() {
    pair<int, string> p1 = {1, "Alice"};
    cout << p1.first << " " << p1.second << endl;
    return 0;
}
```

---

## **2. Vectors (Dynamic Arrays)**
- Dynamic array that can grow and shrink in size.
- Elements are stored in contiguous memory locations.

## **Common Practices**
1. **Reserve Capacity:**
   Use `v.reserve(n);` to allocate memory in advance and improve efficiency.

2. **Sorting:**
   ```cpp
   #include <algorithm>
   sort(v.begin(), v.end());
   ```

3. **Access Elements:**
   ```cpp
   cout << v[0];    // Access element using index
   cout << v.at(1); // Access with bounds checking
   ```

---

## **Common Methods**
| Method              | Description                                 |
|---------------------|---------------------------------------------|
| `v.push_back(x)`    | Adds element `x` to the end                |
| `v.pop_back()`      | Removes the last element                   |
| `v.size()`          | Returns the number of elements             |
| `v.empty()`         | Checks if the vector is empty              |
| `v.clear()`         | Removes all elements                       |
| `v.insert(it, x)`   | Inserts `x` at position `it`               |
| `v.erase(it)`       | Removes element at iterator `it`           |
| `v.erase(it1, it2)` | Removes range `[it1, it2)`                 |
| `v.front()`         | Accesses the first element                 |
| `v.back()`          | Accesses the last element                  |
| `v.resize(n)`       | Resizes the vector to contain `n` elements |
| `v.swap(v2)`        | Swaps elements of `v` with `v2`            |
| `v.assign(n, x)`    | Assigns `n` copies of `x` to the vector    |

---

## **Declaration and Initialization**
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v; // Empty vector
    vector<int> v2(5, 10); // Vector of size 5, all elements initialized to 10
    vector<int> v3 = {1, 2, 3, 4, 5}; // Initialize with list of values

    return 0;
}
```

---

## **Basic Traversal Example**
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {10, 20, 30, 40, 50};

    for (int i = 0; i < v.size(); ++i) {
        cout << v[i] << " ";
    }

    return 0;
}
```

---

## **Insert and Erase Example**
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {1, 2, 3, 4, 5};

    v.insert(v.begin() + 2, 10); // Insert 10 at index 2
    v.erase(v.begin() + 3); // Remove element at index 3

    for (int x : v) {
        cout << x << " ";
    }

    return 0;
}
```

These vector notes provide a concise reference for common operations and practices in C++.



## **3. Map (Associative Container)**
- Stores key-value pairs in sorted order by key.
- Unique keys.

### **Common Methods**
| Method            | Description |
|-------------------|-------------|
| `map[key] = val`  | Insert or update value at key |
| `insert(pair)`    | Insert key-value pair |
| `emplace(k, v)`   | More efficient than `insert` |
| `erase(it/key)`   | Remove element |
| `find(key)`       | Return iterator to element |
| `count(key)`      | Check presence |
| `size()`          | Return size |
| `clear()`         | Remove all elements |

### **Example: Insert and Traverse**
```cpp
#include <iostream>
#include <map>
using namespace std;

int main() {
    map<int, string> mp;
    mp[0] = "Apple";
    mp.emplace(1, "Banana");
    mp.insert({2, "Cherry"});

    for (auto &p : mp) {
        cout << p.first << ": " << p.second << endl;
    }
    return 0;
}
```

---

## **4. Set (Sorted Unique Elements)**
- Stores unique elements in sorted order.

### **Common Methods**
| Method            | Description |
|-------------------|-------------|
| `insert(val)`     | Insert element |
| `emplace(val)`    | Efficient insertion |
| `find(val)`       | Return iterator if present |
| `erase(it/val)`   | Remove element |
| `count(val)`      | Check existence (0 or 1) |
| `lower_bound(x)`  | Iterator to first element >= x |
| `upper_bound(x)`  | Iterator to first element > x |

### **Example: Insert and Find**
```cpp
#include <iostream>
#include <set>
using namespace std;

int main() {
    set<int> s;
    s.insert(10);
    s.insert(20);
    s.insert(30);

    if (s.find(20) != s.end()) {
        cout << "20 found" << endl;
    }

    for (int x : s) cout << x << " ";
    return 0;
}
```

---

## **5. Deque (Double-ended Queue)**
- Elements can be added or removed from both ends.

### **Common Methods**
| Method            | Description |
|-------------------|-------------|
| `push_back(val)`  | Add element at the back |
| `push_front(val)` | Add element at the front |
| `pop_back()`      | Remove element from the back |
| `pop_front()`     | Remove element from the front |
| `size()`          | Return size |
| `empty()`         | Check if deque is empty |

---

## **6. Stack (LIFO - Last In First Out)**
- Elements added to the top and removed from the top.

### **Common Methods**
| Method            | Description |
|-------------------|-------------|
| `push(val)`       | Add element |
| `pop()`           | Remove top element |
| `top()`           | Access top element |
| `size()`          | Return size |
| `empty()`         | Check if stack is empty |

---

## **7. Queue (FIFO - First In First Out)**
- Elements added at the back and removed from the front.

### **Common Methods**
| Method            | Description |
|-------------------|-------------|
| `push(val)`       | Add element |
| `front()`         | Access front element |
| `back()`          | Access last element |
| `pop()`           | Remove front element |
| `size()`          | Return size |

---

## **8. Priority Queue (Max Heap)**
- Elements arranged in descending order by default.

### **Common Methods**
| Method            | Description |
|-------------------|-------------|
| `push(val)`       | Add element |
| `top()`           | Access maximum element |
| `pop()`           | Remove top element |
| `size()`          | Return size |

---

## **9. Min Heap (Priority Queue)**
- Custom comparator required for ascending order.

### **Example:**
```cpp
#include <iostream>
#include <queue>
using namespace std;

int main() {
    priority_queue<int, vector<int>, greater<int>> pq;
    pq.push(10);
    pq.push(5);
    pq.push(15);

    cout << "Min element: " << pq.top() << endl; // Outputs 5
    return 0;
}
```

---

## **10. List**
- Doubly linked list allowing efficient insertion and deletion.

### **Common Methods**
| Method            | Description |
|-------------------|-------------|
| `push_back(val)`  | Add element at the back |
| `push_front(val)` | Add element at the front |
| `pop_back()`      | Remove element from the back |
| `pop_front()`     | Remove element from the front |
| `insert(it, val)` | Insert element at position |
| `erase(it)`       | Remove element |

---

## **11. Multiset**
- Similar to set but allows duplicate elements.

---

## **12. Unordered Set**
- Stores unique elements but not in sorted order.

---

## **13. Multimap**
- Stores key-value pairs but allows duplicate keys.

---

## **14. Unordered Map**
- Stores key-value pairs without any order.
- Faster access compared to `map` due to hashing.

