# Two Pointers

[Home](../../README.md) > [Week 2](../README.md) > Two Pointers

> Week 2 · Topic 2 of 4 · Prerequisites: [Sorting](../../Week-1/05-Sorting/README.md), [Prefix Sum](../01-Prefix-Sum/README.md)

---

## Why This Topic Now

Prefix sum handles static range queries efficiently. Two pointers handles a different class of problem: finding pairs, removing elements, or checking conditions - in a single pass.

The naive solution to most pair problems uses nested loops: for every element, check all other elements → O(n²). Two pointers eliminates the inner loop by using the structure of a sorted array to decide which pointer to move. The result: O(n) instead of O(n²).

---

## What is the Two Pointer Technique?

Two pointers is a pattern where you use **two index variables** that move through a data structure - usually an array or string - to solve a problem efficiently.

The two pointers typically either:
- **Start from opposite ends** and move toward each other
- **Start from the same end** and move at different speeds (slow & fast pointer)

---

## Pattern 1 - Opposite Ends

Both pointers start at the two ends of the array and move inward until they meet.

**Example - Two Sum (Sorted Array):**
Given a sorted array, find two numbers that add up to a target.

```cpp
vector<int> twoSumSorted(vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;

    while (left < right) {
        int currentSum = arr[left] + arr[right];
        if (currentSum == target)
            return {left, right};
        else if (currentSum < target)
            left++;     // need a bigger number, move left pointer right
        else
            right--;    // need a smaller number, move right pointer left
    }

    return {};
}
```

**How we get O(n):**
In the worst case, the two pointers together traverse the entire array once - `left` moves right and `right` moves left, and they never cross. Each element is visited at most once → O(n) time, O(1) space.

---

## Pattern 2 - Same Direction (Slow & Fast)

Both pointers start at the same end but move at different speeds. The fast pointer explores ahead while the slow pointer marks a position.

**Example - Remove Duplicates from Sorted Array:**
Remove duplicates in-place and return the length of the unique part.

```cpp
int removeDuplicates(vector<int>& arr) {
    if (arr.empty()) return 0;

    int slow = 0;  // marks the last unique element

    for (int fast = 1; fast < arr.size(); fast++) {
        if (arr[fast] != arr[slow]) {  // found a new unique element
            slow++;
            arr[slow] = arr[fast];     // place it after the last unique
        }
    }

    return slow + 1;
}
```

**How we get O(n):**
`fast` moves from index 1 to n-1 - exactly one pass through the array. `slow` only moves when a new unique element is found, never exceeding `fast`. Total steps = n → O(n) time, O(1) space (modified in-place).

---

## Pattern 3 - Sliding Window (Variable Size)

A variation where the two pointers define a **window** that expands and shrinks based on a condition.

**Example - Longest Subarray with Sum ≤ k:**

```cpp
int longestSubarray(vector<int>& arr, int k) {
    int left = 0, currentSum = 0, maxLen = 0;

    for (int right = 0; right < arr.size(); right++) {
        currentSum += arr[right];         // expand window

        while (currentSum > k) {          // shrink window if condition violated
            currentSum -= arr[left];
            left++;
        }

        maxLen = max(maxLen, right - left + 1);
    }

    return maxLen;
}
```

**How we get O(n):**
`right` moves forward n times total. `left` also only moves forward - it never goes back. Across the entire run, `left` moves at most n times. Total pointer movements ≤ 2n → O(n) time, O(1) space.

---

## When to Use Two Pointers

| Signal in the problem | Pattern to use |
|-----------------------|----------------|
| Sorted array + find a pair | Opposite ends |
| Remove/count elements in-place | Slow & fast |
| Longest/shortest subarray with a condition | Sliding window |
| Palindrome check | Opposite ends |
| Cycle detection in linked list | Slow & fast (Floyd's) |

---

## Key Tips

- Two pointers almost always requires the array to be **sorted**, or the problem to have a structure that lets you decide which pointer to move
- Always check the loop condition carefully - `left < right` vs `left <= right` matters
- The technique trades the second loop for pointer logic → drops O(n²) to O(n)
- Space is almost always O(1) since you are just maintaining two index variables

---

## Before You Move On

- Can you solve Two Sum on a sorted array in O(n) without extra space?
- Can you remove duplicates from a sorted array in-place?
- Do you understand why two pointers only works when the array is sorted (for opposite-ends pattern)?

---

## Resources

- [GeeksforGeeks - Two Pointer Technique](https://www.geeksforgeeks.org/two-pointers-technique/)
- [ByteByteGo - Introduction to Two Pointers](https://bytebytego.com/courses/coding-patterns/two-pointers/introduction-to-two-pointers)
- [CSES Competitive Programmer's Handbook - Chapter 8](https://cses.fi/book/book.pdf#chapter.8)

### Video Resources

- [Two Pointers - Striver (takeUforward)](https://www.youtube.com/watch?v=-gjxg6Pln50)
- [Two Pointers in 7 minutes - AlgoMasterIO](https://www.youtube.com/watch?v=QzZ7nmouLTI)

---

[Previous: Prefix Sum](../01-Prefix-Sum/README.md) | [Week 2 Overview](../README.md) | [Next: Binary Search](../03-Binary-Search/README.md)
