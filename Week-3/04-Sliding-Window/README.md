# Sliding Window

[Home](../../README.md) > [Week 3](../README.md) > Sliding Window

> Week 3 · Topic 4 of 4 · Prerequisites: [Two Pointers](../../Week-2/02-Two-Pointers/README.md), [Hashing](../03-Hashing/README.md)

---

## Why This Topic Now

You know two pointers and hashing. The sliding window technique combines both: two pointers define the window boundaries, and hashing (or a running sum) tracks the window's state.

The result is an O(n) solution to problems that would naively take O(n²) or O(n×k). This pattern appears in the majority of hard string and subarray problems - it is the culmination of Week 3.

---

## What is a Sliding Window?

A **sliding window** is a subarray or substring of fixed or variable size that moves through the data structure. Instead of recomputing information for overlapping ranges, you maintain the window state and update it incrementally as elements enter and leave.

```
Naive:  recompute everything for every subarray   -> O(n²) or O(n×k)
Window: reuse previous computation, update by one -> O(n)
```

---

## Fixed vs Variable Window - How to Choose

**Fixed Size (window size = K):**
- The problem specifies an exact window size: "subarrays of size k", "every window of size k"
- Compute the answer for the first k elements, then slide by adding the incoming element and removing the outgoing one

**Variable Size:**
- The problem asks for the longest/shortest subarray satisfying a condition
- Use two pointers: expand `right` to grow the window, shrink from `left` when the condition is violated

---

## Fixed Size Window - Example

**Maximum Sum Subarray of Size K:**

### Naive - O(n × k)
```cpp
int maxSum(vector<int>& arr, int k) {
    int n = arr.size(), max_sum = INT_MIN;
    for (int i = 0; i <= n - k; i++) {
        int current_sum = 0;
        for (int j = 0; j < k; j++)
            current_sum += arr[i + j];
        max_sum = max(max_sum, current_sum);
    }
    return max_sum;
}
```

### Sliding Window - O(n)

Key insight: consecutive windows overlap in k-1 elements.
```
Window [5, 2, -1] -> sum = 6
Next   [2, -1, 0] -> sum = 6 - 5 + 0 = 1  (subtract outgoing, add incoming)
```

```cpp
int maxSum(vector<int>& arr, int k) {
    int n = arr.size();
    if (n < k) return -1;

    int window_sum = 0;
    for (int i = 0; i < k; i++)
        window_sum += arr[i];

    int max_sum = window_sum;

    for (int i = k; i < n; i++) {
        window_sum += arr[i];        // add incoming
        window_sum -= arr[i - k];   // remove outgoing
        max_sum = max(max_sum, window_sum);
    }

    return max_sum;
}
```

**Time:** O(n) - each element enters and leaves the window exactly once.
**Space:** O(1).

---

## Variable Size Window - Example

**Longest Subarray with Sum ≤ k:**

```cpp
int longestSubarray(vector<int>& arr, int k) {
    int left = 0, currentSum = 0, maxLen = 0;

    for (int right = 0; right < arr.size(); right++) {
        currentSum += arr[right];         // expand right

        while (currentSum > k) {          // shrink left until valid
            currentSum -= arr[left];
            left++;
        }

        maxLen = max(maxLen, right - left + 1);
    }

    return maxLen;
}
```

**Why O(n):** `right` moves forward n times. `left` also only moves forward - never backward. Total movements ≤ 2n.

---

## Fixed Size - General Steps

1. Determine window size K.
2. Compute the answer for the first window (indices 0 to K-1).
3. Slide by one position: subtract the outgoing element (index `i - K`), add the incoming element (index `i`).
4. Update the answer.

**Examples:**
- Maximum sum subarray of size K
- First negative number in every window of size K
- Maximum element in every window of size K

---

## Variable Size - General Steps

1. Expand `right` by one (add `arr[right]` to window state).
2. While the window violates the condition, shrink from `left`.
3. Update the answer.
4. Repeat until `right` reaches the end.

**Examples:**
- Longest substring without repeating characters
- Smallest subarray with sum >= K
- Longest subarray with at most K distinct characters
- Minimum window substring

---

## How to Recognize a Sliding Window Problem

A problem is likely a sliding window problem if:

- It involves **contiguous elements** - subarrays, substrings, continuous segments
- It asks for **maximum or minimum**: longest, shortest, max sum, min length
- A naive solution would use **nested loops** (O(n²) or O(n×k))
- Input constraints are large (n ≤ 10^5 or 10^6), requiring an O(n) solution

---

## Before You Move On

- Can you implement the fixed-size sliding window for max sum subarray?
- Do you understand why `right - left + 1` gives the current window length?
- Can you identify whether a problem needs a fixed or variable window?
- Can you combine a sliding window with a hash map to track character counts?

---

## Resources

- [Sliding Window - GeeksforGeeks](https://www.geeksforgeeks.org/dsa/top-problems-on-sliding-window-technique-for-interviews/)
- [Sliding Window Overview - Stack Overflow](http://stackoverflow.com/questions/8269916/what-is-sliding-window-algorithm-examples)

### Video Resources

- [Sliding Window Playlist - Aditya Verma](https://www.youtube.com/playlist?list=PL_z_8CaSLPWeM8BDJmIYDaoQ5zuwyxnfj)
- [Sliding Window - Striver (takeUforward)](https://www.youtube.com/playlist?list=PLgUwDviBIf0q7vrFA_HEWcqRqMpCXzYAL)
- [Sliding Window - NeetCode](https://www.youtube.com/playlist?list=PLot-Xpze53leOBgcVsJBEGrHPd_7x_koV)

---

[Previous: Hashing](../03-Hashing/README.md) | [Week 3 Overview](../README.md) | Next: Week 4 (Coming Soon)
