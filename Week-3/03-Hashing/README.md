# Hashing

[Home](../../README.md) > [Week 3](../README.md) > Hashing

> Week 3 · Topic 3 of 4 · Prerequisites: [Arrays](../../Week-1/04-Arrays/README.md), [STL](../../Week-1/03-STL/README.md)

---

## Why This Topic Now

Binary search gives you O(log n) lookup. Divide & Conquer gives you O(n log n) processing. Hashing gives you **O(1) average lookup** - the fastest possible. It does this by trading memory for speed: instead of searching for a key, you compute exactly where it is stored.

Hashing is behind `unordered_map`, `unordered_set`, Python's `dict` and `set`, and Java's `HashMap`. You have already used these containers. This section explains how they work internally and what can go wrong.

---

## How Hashing Works

A **hash function** takes a key and returns an index for the hash table. Given `{ "al", "dm", "ghe" }` and a table of size 7:

**Step 1 - Map characters to numbers** (a=1, b=2, ..., z=26)

**Step 2 - Sum character values**

| String | Calculation | Sum |
|---|---|---|
| `"al"` | 1 + 12 | 13 |
| `"dm"` | 4 + 13 | 17 |
| `"ghe"` | 7 + 8 + 5 | 20 |

**Step 3 - Apply the hash function**

```
hash_index = sum % table_size
```

| String | Computation | Index |
|---|---|---|
| `"al"` | 13 % 7 | 6 |
| `"dm"` | 17 % 7 | 3 |
| `"ghe"` | 20 % 7 | 6 |

Both `"al"` and `"ghe"` map to index 6 - this is called a **collision**.

---

## Components of Hashing

| Component | Description |
|---|---|
| **Key** | The input value (string, integer, etc.) fed into the hash function |
| **Hash Function** | Takes the key and returns an index for the hash table |
| **Hash Table** | An array-based structure that stores values at computed indices |

---

## Collision

A **collision** occurs when two different keys produce the same hash index. For example, `"ab"` and `"ba"` both have a character sum of 3, so they hash to the same index.

Collisions are unavoidable in practice. Two standard strategies to handle them:

---

## Load Factor and Rehashing

The **load factor** measures how full the hash table is:
```
Load Factor = Total elements / Size of hash table
```

When the load factor exceeds a threshold (default: **0.75**), the table is **rehashed**:
1. A new array of **double the size** is created.
2. All existing elements are **re-inserted** using the new hash function.

This keeps operations near O(1).

---

## HashMap (Key-Value Store)

**Python**
```python
hashmap = {}
hashmap["apple"] = 3
hashmap["banana"] = 5
hashmap["orange"] = 2

print(hashmap["banana"])  # 5

if "apple" in hashmap:
    print("Apple is present.")

del hashmap["orange"]

for key, value in hashmap.items():
    print(f"{key}: {value}")
```

**Java**
```java
import java.util.HashMap;

HashMap<String, Integer> hashmap = new HashMap<>();
hashmap.put("apple", 3);
hashmap.put("banana", 5);
hashmap.put("orange", 2);

System.out.println(hashmap.get("banana"));  // 5

if (hashmap.containsKey("apple"))
    System.out.println("Apple is present.");

hashmap.remove("orange");

for (var entry : hashmap.entrySet())
    System.out.println(entry.getKey() + ": " + entry.getValue());
```

**C++**
```cpp
#include <bits/stdc++.h>
using namespace std;

unordered_map<string, int> hashmap;
hashmap["apple"] = 3;
hashmap["banana"] = 5;
hashmap["orange"] = 2;

cout << hashmap["banana"] << endl;  // 5

if (hashmap.count("apple"))
    cout << "Apple is present." << endl;

hashmap.erase("orange");

for (auto& [key, value] : hashmap)
    cout << key << ": " << value << endl;
```

---

## Index Mapping (Trivial Hashing)

The simplest form of hashing: the key itself is the index. Works when keys are integers within a known, bounded range.

**Python**
```python
MAX = 1000
has = [[False, False] for _ in range(MAX + 1)]

def insert(arr):
    for x in arr:
        if x >= 0: has[x][0] = True
        else: has[abs(x)][1] = True

def search(x):
    if x >= 0: return has[x][0]
    return has[abs(x)][1]

arr = [-1, 9, -5, -8, -5, -2]
insert(arr)
print("Present" if search(-5) else "Not Present")
```

**C++**
```cpp
#define MAX 1000
bool has[MAX + 1][2];

void insert(int a[], int n) {
    for (int i = 0; i < n; i++) {
        if (a[i] >= 0) has[a[i]][0] = 1;
        else has[abs(a[i])][1] = 1;
    }
}

bool search(int X) {
    if (X >= 0) return has[X][0];
    return has[abs(X)][1];
}
```

---

## Separate Chaining (Collision Resolution)

Each index of the hash table holds a **linked list** of all elements that hash to that index.

When a collision occurs, the new element is appended to the list at that index.

**Python**
```python
class HashMap:
    def __init__(self, size=10):
        self.size = size
        self.table = [[] for _ in range(size)]

    def hash(self, key):
        return hash(key) % self.size

    def insert(self, key, value):
        idx = self.hash(key)
        for pair in self.table[idx]:
            if pair[0] == key:
                pair[1] = value
                return
        self.table[idx].append([key, value])

    def search(self, key):
        idx = self.hash(key)
        for pair in self.table[idx]:
            if pair[0] == key:
                return pair[1]
        return None
```

**C++**
```cpp
class HashMap {
    int size = 10;
    vector<list<pair<int,int>>> table;
public:
    HashMap() : table(10) {}

    int hash(int key) { return key % size; }

    void insert(int key, int value) {
        int idx = hash(key);
        for (auto& p : table[idx])
            if (p.first == key) { p.second = value; return; }
        table[idx].push_back({key, value});
    }

    int search(int key) {
        int idx = hash(key);
        for (auto& p : table[idx])
            if (p.first == key) return p.second;
        return -1;
    }
};
```

---

## Open Addressing (Collision Resolution)

All elements are stored **inside the hash table** - no external chains. When a collision occurs, probe for the next available slot.

| Strategy | Probe Formula |
|---|---|
| Linear Probing | `(hash + i) % size` |
| Quadratic Probing | `(hash + i²) % size` |
| Double Hashing | `(hash + i × hash2(key)) % size` |

**Python - Linear Probing:**
```python
class OpenHashMap:
    def __init__(self, size=10):
        self.size = size
        self.table = [None] * size

    def hash(self, key): return key % self.size

    def insert(self, key):
        idx = self.hash(key)
        while self.table[idx] is not None:
            idx = (idx + 1) % self.size
        self.table[idx] = key

    def search(self, key):
        idx = self.hash(key)
        while self.table[idx] is not None:
            if self.table[idx] == key: return True
            idx = (idx + 1) % self.size
        return False
```

---

## Before You Move On

- Can you explain what a hash function does?
- Do you understand what a collision is and how separate chaining handles it?
- Can you use an unordered_map / HashMap / dict to count character frequencies?
- Do you know when to use `unordered_map` vs `map`?

---

## Resources

- [Hashing - GeeksforGeeks](https://www.geeksforgeeks.org/dsa/hashing-data-structure/)
- [Load Factor and Rehashing - GeeksforGeeks](https://www.geeksforgeeks.org/load-factor-and-rehashing/)
- [Separate Chaining - GeeksforGeeks](https://www.geeksforgeeks.org/separate-chaining-collision-handling-technique-in-hashing/)
- [Open Addressing - GeeksforGeeks](https://www.geeksforgeeks.org/open-addressing-collision-handling-technique-in-hashing/)

### Video Resources

- [Hashing - Striver's A2Z DSA](https://www.youtube.com/watch?v=KEs5UyBJ39g)
- [Hashing Technique - Abdul Bari](https://www.youtube.com/watch?v=mFY0J5W8Udk)
- [HashMaps in Python - Codebagel](https://www.youtube.com/watch?v=RcZsTI5h0kg)

---

[Previous: Divide & Conquer](../02-Divide-and-Conquer/README.md) | [Week 3 Overview](../README.md) | [Next: Sliding Window](../04-Sliding-Window/README.md)
