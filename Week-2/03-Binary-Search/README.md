# Binary Search

[Home](../../README.md) > [Week 2](../README.md) > Binary Search

> Week 2 · Topic 3 of 4 · Prerequisites: [Sorting](../../Week-1/05-Sorting/README.md), [Two Pointers](../02-Two-Pointers/README.md)

---

## Why This Topic Now

Sorting (Week 1) arranged your data. Two pointers used that arrangement for pair problems. Binary search uses that same arrangement to search in O(log n) instead of O(n).

Think of finding a word in a dictionary - you do not start from page 1. You open to the middle, decide whether the word is in the left half or right half, discard the other half, and repeat. That intuition is exactly what binary search formalizes.

---

## What is Binary Search?

Binary search operates on a **sorted or monotonic search space**, repeatedly dividing it in half to find a target value in **O(log n)** time.

The core idea: at every step, **eliminate half the search space**.

---

## The Algorithm

1. Set `low = 0`, `high = n - 1`.
2. Find `mid = low + (high - low) / 2`.
   > Use this form - not `(low + high) / 2`. It avoids **integer overflow** in Java/C++.
3. If `arr[mid] == target` → return `mid`.
4. If `target < arr[mid]` → answer is in the left half → `high = mid - 1`.
5. If `target > arr[mid]` → answer is in the right half → `low = mid + 1`.
6. Repeat until `low > high`. If not found, return `-1`.

**Dry Run:**

Array: `[2, 5, 8, 12, 16, 23, 38, 56, 72, 91]` | Target: `23`

| Step | low | high | mid | arr[mid] | Action |
|------|-----|------|-----|----------|--------|
| 1 | 0 | 9 | 4 | 16 | 23 > 16 → go right |
| 2 | 5 | 9 | 7 | 56 | 23 < 56 → go left |
| 3 | 5 | 6 | 5 | 23 | Found at index 5 |

---

## Time & Space Complexity

Every step cuts the search space in half. Starting with N elements:

```
After 1 step  ->  N/2 remain
After 2 steps ->  N/4 remain
After k steps ->  N/2^k remain
```

The loop stops when `N/2^k = 1` → `k = log₂(N)`.

| Version | Time | Space |
|---|---|---|
| Iterative | O(log N) | O(1) |
| Recursive | O(log N) | O(log N) - call stack |

---

## Implementation

### Iterative (Preferred)

**Python**
```python
def binary_search(arr, x):
    low, high = 0, len(arr) - 1
    while low <= high:
        mid = low + (high - low) // 2
        if arr[mid] == x:    return mid
        elif arr[mid] < x:   low = mid + 1
        else:                high = mid - 1
    return -1
```

**Java**
```java
static int binarySearch(int[] arr, int x) {
    int low = 0, high = arr.length - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] == x)      return mid;
        else if (arr[mid] < x)  low = mid + 1;
        else                    high = mid - 1;
    }
    return -1;
}
```

**C++**
```cpp
int binarySearch(vector<int>& arr, int x) {
    int low = 0, high = arr.size() - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] == x)      return mid;
        else if (arr[mid] < x)  low = mid + 1;
        else                    high = mid - 1;
    }
    return -1;
}
```

### Recursive

**Python**
```python
def binary_search(arr, low, high, x):
    if high >= low:
        mid = low + (high - low) // 2
        if arr[mid] == x:    return mid
        elif arr[mid] > x:   return binary_search(arr, low, mid - 1, x)
        else:                return binary_search(arr, mid + 1, high, x)
    return -1
```

**Java**
```java
static int binarySearch(int[] arr, int low, int high, int x) {
    if (high >= low) {
        int mid = low + (high - low) / 2;
        if (arr[mid] == x)      return mid;
        if (arr[mid] > x)       return binarySearch(arr, low, mid - 1, x);
        return binarySearch(arr, mid + 1, high, x);
    }
    return -1;
}
```

**C++**
```cpp
int binarySearch(vector<int>& arr, int low, int high, int x) {
    if (high >= low) {
        int mid = low + (high - low) / 2;
        if (arr[mid] == x)      return mid;
        if (arr[mid] > x)       return binarySearch(arr, low, mid - 1, x);
        return binarySearch(arr, mid + 1, high, x);
    }
    return -1;
}
```

> Base case: `high < low` means the search space is empty.

---

## Variations

These are not separate algorithms - they are modifications of the same core idea. Learn them in this order:

### Standard → Lower Bound → Upper Bound → First/Last Occurrence → Binary Search on Answer

---

### Variation 1 - Lower Bound

Finds the **first position where a value >= target exists** - the leftmost index where the target could be inserted while keeping the array sorted.

When `arr[mid] >= target`: record `mid` as a potential answer and continue **left** to check for an earlier valid position.
When `arr[mid] < target`: move right.

**Use cases:** Finding insertion points, first element >= some value, range query boundaries.

> In C++, `std::lower_bound()` does this out of the box.

---

### Variation 2 - Upper Bound

Finds the **first position where a value > target exists**.

When `arr[mid] <= target`: move right.
When `arr[mid] > target`: record `mid` and continue **left**.

A useful property: `upper_bound(target) - lower_bound(target)` gives the **count of occurrences** of the target in O(log N).

**Use cases:** Finding the end boundary of a range, counting occurrences, finding the first element strictly greater than a value.

> In C++, `std::upper_bound()` handles this.

---

### Variation 3 - First and Last Occurrence

Target a specific value and find its exact first or last position in an array with duplicates.

**First occurrence:** When `arr[mid] == target`, record the index and continue **left** to check for an earlier duplicate.

**Last occurrence:** When `arr[mid] == target`, record the index and continue **right** to check for a later duplicate.

**Use cases:** Finding the range `[first, last]` of a repeated element.

---

### Variation 4 - Binary Search on Answer

This variation does not search an array directly. Instead, it searches an abstract **answer space** for the optimal value that satisfies a given condition.

**The pattern:**
- Define a range `[low, high]` of possible answers.
- Write a `isValid(mid)` predicate that returns true or false.
- Since valid and invalid answers are monotonic - all valid on one side, all invalid on the other - binary search finds the exact boundary efficiently.

**Use cases:** Minimizing the maximum, maximizing the minimum, problems with "at least" or "at most" constraints.

---

## Before You Move On

- Can you implement iterative binary search from memory?
- Can you explain why `mid = low + (high - low) / 2` instead of `(low + high) / 2`?
- Do you understand the difference between lower bound and upper bound?
- Can you describe what "binary search on the answer" means?

---

## Resources

- [Binary Search - GeeksforGeeks](https://www.geeksforgeeks.org/dsa/binary-search/)
- [Variants of Binary Search - GeeksforGeeks](https://www.geeksforgeeks.org/dsa/variants-of-binary-search/)
- [Binary Search on Answers - GeeksforGeeks](https://www.geeksforgeeks.org/dsa/binary-search-on-answer-tutorial-with-problems/)
- [Binary Search - InterviewBit](https://www.interviewbit.com/courses/programming/binary-search/)
- [CSES Competitive Programmer's Handbook - Section 3.3](https://cses.fi/book/book.pdf#section.3.3)

### Video Resources


- [Binary Search Series - Striver (playlist)](https://www.youtube.com/playlist?list=PLgUwDviBIf0pMFMWuuvDNMAkoQFi-h0ZF)


---

[Previous: Two Pointers](../02-Two-Pointers/README.md) | [Week 2 Overview](../README.md) | [Next: Strings](../04-Strings/README.md)
