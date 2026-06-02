# Standard Libraries of DSA

[Home](../../README.md) > [Week 1](../README.md) > Standard Libraries

> Week 1 · Topic 3 of 5 · Prerequisites: [Syntax & I/O](../01-Syntax-IO/README.md), [Time & Space Complexity](../02-Complexity/README.md)

---

## Why This Topic Now

You know the language syntax and you can reason about efficiency. Now you need tools. Every language ships with pre-built, production-quality data structures. You should know how to use them fluently before you need to use them in a problem - otherwise you will waste time re-implementing something that already exists.

---

## Which Container to Use?

Before diving into implementation, here is a quick decision guide:

| I need to... | Use |
|---|---|
| Store and resize a list | Vector / ArrayList / list |
| Process in LIFO order (undo, DFS) | Stack |
| Process in FIFO order (BFS, scheduling) | Queue |
| Always get the min or max quickly | Priority Queue (heap) |
| Store unique values in sorted order | Set / TreeSet |
| Store unique values with O(1) lookup | Unordered Set / HashSet |
| Map keys to values in sorted key order | Map / TreeMap |
| Map keys to values with O(1) lookup | Unordered Map / HashMap |
| Insert/delete efficiently at both ends | Deque |
| Insert/delete efficiently in the middle | List (Linked List) |

---

## Containers

### Sequence Containers

#### Vector (Dynamic Array)

Your go-to container for most problems. Use when you need a resizable array with fast random access. Perfect for storing results, BFS/DFS visited nodes, or any list whose size you do not know in advance.

When full and a new element is added, the vector doubles its capacity - all previous elements are copied to a new allocation.

**C++**
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;
    v.push_back(1);
    v.push_back(2);
    v.push_back(3);

    cout << v.at(2) << " or " << v[2] << endl;  // access element at index 2
    cout << v.front() << endl;                    // first element
    cout << v.back() << endl;                     // last element

    v.pop_back();   // remove last element
    v.clear();      // remove all elements

    vector<int> a(5);       // 5 elements initialized to 0
    vector<int> b(5, 1);    // 5 elements initialized to 1
    vector<int> last(a);    // copy of a
}
```

**Java**
```java
import java.util.ArrayList;
import java.util.Collections;

ArrayList<Integer> v = new ArrayList<>();
v.add(1);
v.add(2);
v.add(3);

System.out.println(v.get(2));                    // at(2)
System.out.println(v.get(0));                    // front
System.out.println(v.get(v.size() - 1));         // back
v.remove(v.size() - 1);                          // pop_back
v.clear();

ArrayList<Integer> a = new ArrayList<>(Collections.nCopies(5, 0));
ArrayList<Integer> b = new ArrayList<>(Collections.nCopies(5, 1));
ArrayList<Integer> last = new ArrayList<>(a);
```

**Python**
```python
v = []
v.append(1)
v.append(2)
v.append(3)

print(v[2])       # at(2)
print(v[0])       # front
print(v[-1])      # back
v.pop()           # pop_back
v.clear()

a = [0] * 5
b = [1] * 5
import copy
last = copy.copy(a)
```

---

#### Array (Fixed-Size)

Use when you know the size at compile time. Fastest access, zero overhead. Good for lookup tables, RGB values, or matrix rows.

**C++**
```cpp
#include <array>
array<int, 4> arr = {1, 2, 3, 4};
cout << arr.size() << endl;
cout << arr.at(2) << endl;     // bounds-checked access
cout << arr.front() << endl;
cout << arr.back() << endl;
```

**Java**
```java
int[] arr = {1, 2, 3, 4};
System.out.println(arr.length);
System.out.println(arr[2]);
System.out.println(arr[0]);
System.out.println(arr[arr.length - 1]);
```

**Python**
```python
arr = [1, 2, 3, 4]
print(len(arr))
print(arr[2])
print(arr[0])
print(arr[-1])
```

---

#### Deque (Double-Ended Queue)

Use when you need fast insertion and deletion at **both** ends. Good for sliding window problems, implementing queues with push/pop from both sides, or browser history.

**C++**
```cpp
#include <deque>
deque<int> d;
d.push_back(1);
d.push_front(2);
cout << d.at(1) << endl;
cout << d.front() << endl;
cout << d.back() << endl;
d.pop_back();
d.pop_front();
```

**Java**
```java
import java.util.ArrayDeque;
ArrayDeque<Integer> d = new ArrayDeque<>();
d.addLast(1);
d.addFirst(2);
System.out.println(d.peekFirst());
System.out.println(d.peekLast());
d.removeLast();
d.removeFirst();
```

**Python**
```python
from collections import deque
d = deque()
d.append(1)        # push_back
d.appendleft(2)    # push_front
print(d[0])        # front
print(d[-1])       # back
d.pop()
d.popleft()
```

---

#### List (Doubly Linked List)

Use when you need frequent insertions and deletions in the **middle** of a sequence. Unlike vectors, no shifting is needed. Good for LRU cache, playlist management, or frequent mid-list edits. Avoid if you need random access.

**C++**
```cpp
#include <list>
list<int> l;
l.push_back(2);
l.push_front(1);
l.erase(l.begin());   // erase first element
list<int> n(l);       // copy
```

**Java**
```java
import java.util.LinkedList;
LinkedList<Integer> l = new LinkedList<>();
l.addLast(2);
l.addFirst(1);
l.removeFirst();
LinkedList<Integer> n = new LinkedList<>(l);
```

**Python**
```python
from collections import deque
l = deque()
l.append(2)
l.appendleft(1)
l.popleft()
n = l.copy()
```

---

### Container Adaptors

#### Stack

Follows LIFO (Last In, First Out) order. Use for: balanced parentheses, undo/redo, function call simulation, DFS, next greater element.

**C++**
```cpp
#include <stack>
stack<string> s;
s.push("A");
s.push("B");
s.push("C");
cout << s.top() << endl;   // C - last in, first out
s.pop();
cout << s.top() << endl;   // B
cout << s.empty() << endl;
```

**Java**
```java
import java.util.Stack;
Stack<String> s = new Stack<>();
s.push("A");
s.push("B");
s.push("C");
System.out.println(s.peek());   // C
s.pop();
System.out.println(s.peek());   // B
System.out.println(s.isEmpty());
```

**Python**
```python
s = []
s.append("A")
s.append("B")
s.append("C")
print(s[-1])   # C
s.pop()
print(s[-1])   # B
print(len(s) == 0)
```

---

#### Queue

Follows FIFO (First In, First Out) order. Use for: BFS, task scheduling, printer queue, level-order tree traversal.

**C++**
```cpp
#include <queue>
queue<string> q;
q.push("A");
q.push("B");
q.push("C");
cout << q.front() << endl;   // A - first in, first out
q.pop();
cout << q.front() << endl;   // B
cout << q.empty() << endl;
```

**Java**
```java
import java.util.LinkedList;
import java.util.Queue;
Queue<String> q = new LinkedList<>();
q.add("A");
q.add("B");
q.add("C");
System.out.println(q.peek());   // A
q.poll();
System.out.println(q.peek());   // B
System.out.println(q.isEmpty());
```

**Python**
```python
from collections import deque
q = deque()
q.append("A")
q.append("B")
q.append("C")
print(q[0])       # A
q.popleft()
print(q[0])       # B
print(len(q) == 0)
```

---

#### Priority Queue

Adds and removes elements based on priority. Internally a heap. Use for: Dijkstra's algorithm, heap sort, scheduling by priority, Top-K problems.

**C++**
```cpp
#include <queue>
// max heap (default)
priority_queue<int> maxH;
maxH.push(8);
maxH.push(3);
maxH.push(7);
cout << maxH.top() << endl;   // 8

// min heap
priority_queue<int, vector<int>, greater<int>> minH;
minH.push(3);
minH.push(7);
minH.push(2);
cout << minH.top() << endl;   // 2
```

**Java**
```java
import java.util.PriorityQueue;
import java.util.Collections;

// max heap
PriorityQueue<Integer> maxH = new PriorityQueue<>(Collections.reverseOrder());
maxH.add(8); maxH.add(3); maxH.add(7);
System.out.println(maxH.peek());   // 8

// min heap (default in Java)
PriorityQueue<Integer> minH = new PriorityQueue<>();
minH.add(3); minH.add(7); minH.add(2);
System.out.println(minH.peek());   // 2
```

**Python**
```python
import heapq

# min heap
min_heap = []
heapq.heappush(min_heap, 3)
heapq.heappush(min_heap, 7)
heapq.heappush(min_heap, 2)
print(min_heap[0])   # 2

# max heap - negate values
max_heap = []
heapq.heappush(max_heap, -8)
heapq.heappush(max_heap, -3)
heapq.heappush(max_heap, -7)
print(-max_heap[0])   # 8
```

---

### Associative Containers

#### Set

Stores only unique elements in sorted ascending order. Implemented as a Red-Black Tree - O(log n) operations. Use for removing duplicates, checking membership, and problems requiring sorted unique data.

**C++**
```cpp
#include <set>
set<int> s;
s.insert(5);
s.insert(5);   // duplicate - ignored
s.insert(6);
s.insert(3);
for (auto i : s) cout << i << endl;   // 3 4 5 6

s.erase(s.begin());   // remove smallest
cout << s.count(5) << endl;   // 1 if present, 0 if not
auto it = s.find(5);
```

**Java**
```java
import java.util.TreeSet;
TreeSet<Integer> s = new TreeSet<>();
s.add(5); s.add(5); s.add(6); s.add(3);
for (int i : s) System.out.println(i);
s.pollFirst();
System.out.println(s.contains(5) ? 1 : 0);
```

**Python**
```python
from sortedcontainers import SortedList
s = SortedList(set([5, 5, 6, 3]))
for i in s: print(i)
s.pop(0)
print(1 if 5 in s else 0)
```

> For O(1) average lookup (unordered), use `unordered_set` (C++), `HashSet` (Java), or Python's built-in `set`.

---

#### Map

Stores key-value pairs in sorted key order using a Red-Black Tree. O(log n) for all operations. Does not allow duplicate keys. Use for frequency counting with sorted output, ordered dictionaries, and range queries on keys.

**C++**
```cpp
#include <map>
map<int, string> m;
m[1] = "A";
m[3] = "Boy";
m.insert({5, "Good"});
for (auto i : m) cout << i.first << " " << i.second << endl;
cout << m.count(3) << endl;   // 1 if key exists
m.erase(3);
```

**Java**
```java
import java.util.TreeMap;
TreeMap<Integer, String> m = new TreeMap<>();
m.put(1, "A");
m.put(3, "Boy");
m.put(5, "Good");
for (var e : m.entrySet()) System.out.println(e.getKey() + " " + e.getValue());
System.out.println(m.containsKey(3) ? 1 : 0);
m.remove(3);
```

**Python**
```python
d = {}
d[1] = "A"
d[3] = "Boy"
d[5] = "Good"
for key, value in sorted(d.items()): print(key, value)
print(1 if 3 in d else 0)
del d[3]
```

> For O(1) average lookup (unordered), use `unordered_map` (C++), `HashMap` (Java), or Python's built-in `dict`.

---

> For Multiset and Multimap, refer to:
> - [Multiset - GeeksforGeeks](https://www.geeksforgeeks.org/cpp/multiset-in-cpp-stl/)
> - [Multimap - GeeksforGeeks](https://www.geeksforgeeks.org/cpp/multimap-associative-containers-the-c-standard-template-library-stl/)
> - [Unordered variants - GeeksforGeeks](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/)

---

## Algorithms

Algorithms are ready-made functions for common operations: searching, sorting, counting, comparing. In C++ they live in `<algorithm>` and `<numeric>`.

**C++**
```cpp
#include <algorithm>
#include <vector>
vector<int> v = {5, 2, 4, 10};

binary_search(v.begin(), v.end(), 4);           // true/false
lower_bound(v.begin(), v.end(), 6) - v.begin(); // first index >= 6
upper_bound(v.begin(), v.end(), 6) - v.begin(); // first index > 6

int a = 9, b = 7;
cout << max(a, b) << endl;
cout << min(a, b) << endl;
swap(a, b);

string str = "abcd";
reverse(str.begin(), str.end());   // "dcba"

rotate(v.begin(), v.begin() + 1, v.end());   // shift left by 1
sort(v.begin(), v.end());
```

**Java**
```java
import java.util.*;
ArrayList<Integer> v = new ArrayList<>(Arrays.asList(5, 2, 4, 10));
Collections.sort(v);
Collections.binarySearch(v, 4);
Math.max(9, 7);
Math.min(9, 7);
Collections.reverse(v);
new StringBuilder("abcd").reverse().toString();
```

**Python**
```python
from bisect import bisect_left, bisect_right
v = [2, 4, 5, 10]  # sorted

bisect_left(v, 6)    # lower_bound
bisect_right(v, 6)   # upper_bound

max(9, 7)
min(9, 7)
a, b = b, a          # swap

s = "abcd"[::-1]     # reverse string
v.sort()
```

---

## Before You Move On

- Can you push and pop from a stack and queue?
- Can you iterate over a map and print key-value pairs?
- Do you know when to use `unordered_map` vs `map`?
- Can you use a priority queue to get the minimum element?

---

## Resources

- [C++ STL - GeeksforGeeks](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/)
- [Java Collections Framework - GeeksforGeeks](https://www.geeksforgeeks.org/collections-in-java-2/)
- [Python Collections Module - GeeksforGeeks](https://www.geeksforgeeks.org/python-collections-module/)

---

[Previous: Time & Space Complexity](../02-Complexity/README.md) | [Week 1 Overview](../README.md) | [Next: Arrays](../04-Arrays/README.md)
