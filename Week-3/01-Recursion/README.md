# Recursion

[Home](../../README.md) > [Week 3](../README.md) > Recursion

> Week 3 · Topic 1 of 4 · Prerequisites: [Arrays](../../Week-1/04-Arrays/README.md), [Time & Space Complexity](../../Week-1/02-Complexity/README.md)

---

## Why This Topic Now

Every algorithm you have written so far has been iterative - a loop that runs until a condition is met. Recursion is the alternative: a function that calls itself on a smaller version of the same problem.

You need recursion before Divide & Conquer, before trees, before graphs, before backtracking, and before dynamic programming. It is the foundational mental model for the second half of this bootcamp.

---

## What is Recursion?

Recursion is when a function **calls itself** to solve a smaller version of the same problem. Every recursive solution has two parts:

- **Base case** - the condition where the function stops calling itself
- **Recursive case** - where the function breaks the problem down and calls itself

Without a base case, the function calls itself forever → **stack overflow**.

---

## How the Call Stack Works

Every function call gets a **stack frame** - a slot in memory holding its local variables and a return address. With recursion, frames pile up until the base case is hit, then they unwind one by one.

```
factorial(4)
  |
  +-- factorial(3)
        |
        +-- factorial(2)
              |
              +-- factorial(1)
                    |
                    +-- factorial(0)  <- base case, returns 1
                    <- returns 1
              <- returns 2
        <- returns 6
  <- returns 24
```

This is why recursion always uses **O(depth)** stack space.

---

## Pattern 1 - Linear Recursion

One recursive call per function call. The problem shrinks by a fixed amount each time.

**Example - Factorial:**

```cpp
int factorial(int n) {
    if (n == 0) return 1;          // base case
    return n * factorial(n - 1);   // recursive case
}
```

**How we get O(n) time, O(n) space:**
- The function is called for n, n-1, n-2, ..., 1, 0 → n+1 calls → **O(n) time**
- At peak, all n+1 frames sit on the call stack simultaneously → **O(n) space**

---

## Pattern 2 - Binary Recursion

Two recursive calls per function call. The problem splits into two subproblems.

**Example - Fibonacci:**

```cpp
int fibonacci(int n) {
    if (n <= 1) return n;                          // base case
    return fibonacci(n - 1) + fibonacci(n - 2);   // two recursive calls
}
```

**How we get O(2ⁿ) time, O(n) space:**
- Each call spawns 2 more - the call tree doubles at every level → **O(2ⁿ) time**
- Despite the tree being wide, the **depth** is only n (we go left as deep as possible first) → **O(n) space**

> This is very inefficient. Memoization (caching results) brings it down to O(n) time. This is covered in the DP week.

---

## Pattern 3 - Divide and Conquer

The problem is split into roughly equal halves, solved recursively, then combined.

**Example - Binary Search (Recursive):**

```cpp
int binarySearch(vector<int>& arr, int left, int right, int target) {
    if (left > right) return -1;                   // base case: not found

    int mid = left + (right - left) / 2;

    if (arr[mid] == target)      return mid;
    else if (arr[mid] < target)  return binarySearch(arr, mid + 1, right, target);
    else                         return binarySearch(arr, left, mid - 1, target);
}
```

**How we get O(log n) time, O(log n) space:**
- Each call halves the search range → **log₂(n) levels deep** → **O(log n) time**
- Each level has exactly one active stack frame → **O(log n) space** (unlike iteration which is O(1))

---

## Pattern 4 - Backtracking

Try a choice, recurse, and **undo** the choice if it does not lead to a solution. Used when you need to explore all possibilities.

**Example - Generate All Subsets:**

```cpp
void subsets(vector<int>& nums, int index, vector<int>& current, vector<vector<int>>& result) {
    result.push_back(current);              // record current subset

    for (int i = index; i < nums.size(); i++) {
        current.push_back(nums[i]);         // make a choice
        subsets(nums, i + 1, current, result);  // recurse
        current.pop_back();                 // undo the choice (backtrack)
    }
}
```

**How we get O(2ⁿ) time, O(n) space:**
- Every element is either included or not → **2ⁿ subsets** → **O(2ⁿ) time**
- The recursion depth is at most n (one element added per level) → **O(n) space**

---

## Recursion vs Iteration

| | Recursion | Iteration |
|---|-----------|-----------|
| Code clarity | Often cleaner for tree/graph problems | Better for simple loops |
| Space | O(depth) stack space always | O(1) if no extra structures |
| Risk | Stack overflow for deep inputs | No such risk |
| Use when | Problem naturally divides into subproblems | Simple repetition |

---

## Key Tips

- Always define the **base case first** - it is the most important part
- Every recursive call must move **closer to the base case**, otherwise infinite recursion
- If you see repeated subproblems (like Fibonacci), use **memoization** to avoid recomputation
- Recursive space is **O(depth)**, not O(number of total calls) - the stack only holds the current path, not the whole tree
- Most recursive solutions can be converted to iterative using an explicit stack

---

## Before You Move On

- Can you write a recursive factorial function from scratch?
- Can you trace through the call stack for `factorial(4)` on paper?
- Do you understand why naive Fibonacci is O(2ⁿ)?
- Can you identify the base case in a given recursive function?

---

## Resources

- [GeeksforGeeks - Recursion](https://www.geeksforgeeks.org/recursion/)
- [Visualgo - Recursion Tree](https://visualgo.net/en/recursion)
- [LeetCode - Recursion Problems](https://leetcode.com/tag/recursion/)

### Video Resources

- [Recursion Series - Striver (takeUforward)](https://www.youtube.com/watch?v=yVdKa8dnKiE)
- [Recursion Playlist - Aditya Verma](https://www.youtube.com/playlist?list=PL_z_8CaSLPWeT1ffjiImo0sYTcnLzo-wY)

---

[Week 3 Overview](../README.md) | [Next: Divide & Conquer](../02-Divide-and-Conquer/README.md)
