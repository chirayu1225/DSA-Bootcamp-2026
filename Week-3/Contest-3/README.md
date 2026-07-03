# Week 3 - Contest 3

[Home](../../README.md) > [Week 3](../README.md) > Contest 3

This contest tested the core Week 3 topics - **sliding window, two pointers, prefix sums, and divide & conquer** - through six problems of increasing difficulty. Below are the problem statements from the contest for your reference. If you didn't get a chance to attempt all of them during the contest, try solving them now - read each problem carefully, pay attention to edge cases, and think about which Week 3 pattern applies before writing code.

---

## Q1. Quiz Competition Teams

### Problem Description

A class has students with various talents, each represented by an integer from `1` to `talentsCount`. You need to form teams for a quiz competition, where each team must have at least one member with each talent.

Teams must be formed from consecutive students in the array. For each possible starting position, determine the minimum number of students needed to form a valid team. If it is not possible to form a team with all talents from a particular starting position, return `-1` for that position.

---

### Function Signature

```cpp
vector<int> teamSize(vector<int> talent, int talentsCount) {
    // Complete the function
}
```

**Parameters:**

- `talent` (`int[n]`) - an array of integers representing the students' talents.
- `talentsCount` (`int`) - the number of talents, represented by integers from `1` to `talentsCount`.

**Returns:**

- `int[n]` - an array where the element at each index represents the minimum size of a valid team starting at that index, or `-1` if a valid team cannot be formed.

---

### Examples

#### Example 1

- **Input:** `talent = [1, 2, 3, 2, 1]`, `talentsCount = 3`
- **Output:** `[3, 4, 3, -1, -1]`

**Explanation:**

- Starting at position 1: The subarray `[1, 2, 3]` includes all talents (1, 2, 3). The minimum size is **3**.
- Starting at position 2: The subarray `[2, 3, 2, 1]` is the smallest subarray starting here that includes all talents. The minimum size is **4**.
- Starting at position 3: The subarray `[3, 2, 1]` includes all talents. The minimum size is **3**.
- Starting at positions 4 and 5: It's not possible to form a team with all 3 talents from these positions to the end of the array. Return `-1` for each.

#### Example 2

- **Input:** `talent = [1, 1, 2, 2, 3, 1, 3, 2]`, `talentsCount = 3`
- **Output:** `[5, 4, 4, 3, 4, 3, -1, -1]`

**Explanation:** The shortest subarrays for each position are:

| Starting Position | Subarray | Length |
|---|---|---|
| 1st | `[1, 1, 2, 2, 3]` | 5 |
| 2nd | `[1, 2, 2, 3]` | 4 |
| 3rd | `[2, 2, 3, 1]` | 4 |
| 4th | `[2, 3, 1]` | 3 |
| 5th | `[3, 1, 3, 2]` | 4 |
| 6th | `[1, 3, 2]` | 3 |
| 7th & 8th | - | -1 |

No further subarrays will have all 3 talents.

#### Example 3

- **Input:** `talent = [7, 5, 3, 4, 6, 1, 7, 2, 4]`, `talentsCount = 7`
- **Output:** `[8, 7, -1, -1, -1, -1, -1, -1, -1]`

**Explanation:** There have to be at least 7 elements in any subarray to have one from each talent. The shortest subarrays at each position are:

- Starting at position 1: `[7, 5, 3, 4, 6, 1, 7, 2]` (length **8**)
- Starting at position 2: `[5, 3, 4, 6, 1, 7, 2]` (length **7**)
- No further starting positions can form a team with all 7 talents.

---

### Constraints

- `1 <= n, talentsCount <= 10^5`, where `n` is the size of the talent array.
- `1 <= talent[i] <= talentsCount`

---

## Q2. Minimal Substrings with K Distinct Characters

### Problem Description

You're working on a new programming language with some interesting built-ins for strings. One of the features you'd like to implement involves splitting a string into substrings with a limited set of characters.

Given a string `inputStr` and an integer `k`, your task is to split `inputStr` into a minimal possible number of substrings so that there are no more than `k` different symbols in each of them. Return the minimal possible number of such substrings.

> **Hint:** Iterate over the string `inputStr` and try to use a `Set` structure to keep all letters used for the current substring. Every time when the set size becomes greater than `k`, it means that the last considered symbol should be the first one in a new substring.

---

### Function Signature

```cpp
int minimalSubstrings(std::string inputStr, int k) {
    // Your code goes here
    return 0;
}
```

**Parameters:**

- `inputStr` (`string`) - the input string to be split.
- `k` (`int`) - the maximum number of distinct characters allowed per substring.

**Returns:**

- `int` - the minimal number of substrings needed.

---

### Examples

#### Example 1

- **Input:** `inputStr = "aabeefegeeccrr"`, `k = 3`
- **Output:** `3`

**Explanation:** The string `"aabeefegeeccrr"` can be split into 3 substrings:

- `"aabee"` - unique characters: `'a'`, `'b'`, `'e'` (3 distinct characters)
- `"fegee"` - unique characters: `'f'`, `'e'`, `'g'` (3 distinct characters)
- `"ccrr"` - unique characters: `'c'`, `'r'` (2 distinct characters)

Each substring has at most 3 distinct characters. It's not possible to split it into fewer than 3 substrings.

---

### Constraints

- The string `inputStr` contains only lowercase English letters.

---

## Q3. Minimize Sum of Absolute Differences

### Problem Description

Given an array, remove a single continuous subarray of length `k` such that the sum of absolute differences between adjacent elements in the resulting array is minimized.

---

### Input & Output

#### Input Format

1. The first line contains two integers `n` and `k`.
2. The second line contains `n` space-separated integers (the array).

#### Output Format

A single integer: the minimum possible sum of absolute differences between adjacent elements after removing one continuous subarray of length `k`.

---

### Function Signature

```cpp
long long minimizeSumOfAbsoluteDifferences(int n, int k, vector<long long>& a) {
    // Your code here
    return 0;
}
```

**Parameters:**

- `n` (`int`) - the length of the input array.
- `k` (`int`) - the length of the continuous subarray to remove.
- `a` (`vector<long long>&`) - the input array.

**Returns:**

- `long long` - the minimum possible sum of absolute differences after the removal.

---

### Examples

#### Example 1

**Input:**

```
5 2
1 3 7 2 5
```

**Output:**

```
4
```

**Explanation:** Removing the length-2 subarray `[7, 2]` leaves `[1, 3, 5]`, whose adjacent absolute differences sum to `|1 - 3| + |3 - 5| = 4`, the minimum achievable.

---

### Constraints

- `1 <= n <= 10^5`
- `1 <= k <= 10^3`
- `1 <= k < n`

---

## Q4. Permutations of the String

### Problem Description

You are given a string `s` consisting of pairwise distinct lowercase English letters.

Your task is to generate all possible permutations of the characters in the string and output them in lexicographical order.

---

### Input & Output

#### Input Format

A single string `s` consisting of lowercase English letters. All characters in `s` are pairwise distinct.

#### Output Format

Print all permutations of the string `s` in lexicographical order, each on a new line.

---

### Function Signature

```cpp
void solve(string s) {
    // Your code here
}
```

**Parameters:**

- `s` (`string`) - the input string of pairwise distinct lowercase letters.

---

### Examples

#### Example 1

- **Input:** `abc`
- **Output:**
  ```
  abc
  acb
  bac
  bca
  cab
  cba
  ```

---

### Constraints

- `1 <= |s| <= 8`
- The string `s` consists only of lowercase English letters.
- All characters in `s` are pairwise distinct.

---

## Q5. Split Array into Two Unique Halves

### Problem Description

Given an array of integers `a` of even length, your task is to split it into two arrays of equal length such that all the numbers are unique in each of them.

There may be more than one possible answer, in which case you may return any of them. If there are no possible answers, return an empty array.

> **Hint:** Count the number of occurrences of each integer in `a`. If there are integers occurring more than twice, then there is no solution. Next, put the integers occurring twice into both answer arrays. Finally, put all other numbers into the answer arrays, following the condition that they should have equal sizes.

---

### Function Signature

```cpp
vector<vector<int>> solution(vector<int>& a) {
    // Core logic goes here
    return {};
}
```

**Parameters:**

- `a` (`vector<int>&`) - an array of integers of even length.

**Returns:**

- `vector<vector<int>>` - an array of two arrays, each of equal length and containing only unique elements, or an empty array if no solution exists.

---

### Examples

#### Example 1

- **Input:** `a = [1, 2, 3, 4]`
- **Output:** `[[1, 3], [2, 4]]`

**Explanation:** Answers like `[[1, 2], [3, 4]]` or `[[4, 2], [3, 1]]` would also be considered correct.

#### Example 2

- **Input:** `a = [1, 1, 2, 1]`
- **Output:** `[[1, 2], [1, 1]]`

**Explanation:** Again, there are other possible answers.

#### Example 3

- **Input:** `a = [2, 2, 3, 3, 2, 2]`
- **Output:** `[]`

**Explanation:** No matter how we try to split this array, there will be at least two `2`s in at least one of the resulting arrays. So the answer is `[]`.

---

### Constraints

- `a` has even length.
- `2 <= a.length <= 10^5`
- `1 <= a[i] <= 10^9`

---

## Q6. Subarrays with Sum Divisible by K

### Problem Description

A financial institution monitors daily transaction amounts for potential regulatory analysis. Given an array of integers where each element represents the transaction amount for a day, the institution wants to determine the number of continuous time periods (subarrays) for which the total amount is exactly divisible by a given integer `K`.

> **Note:** The solution must be designed using a **divide and conquer** approach.

---

### Function Signature

```cpp
long long solveProblem(int n, int k, const vector<int>& transactions) {
    // Logic goes here
    return 0;
}
```

**Parameters:**

- `N` (`int`) - the number of days (`1 <= N <= 10^5`).
- `transactions` (`int[]`) - an array of `N` integers, where each integer represents the transaction amount for that day.
- `K` (`int`) - a positive integer used to check for divisibility of the subarray sum.

**Returns:**

- `long long` - the total number of contiguous subarrays whose sum is divisible by `K`.

---

### Examples

#### Example 1

- **Input:** `N = 5`, `K = 3`, `transactions = [1, 2, 3, 4, 1]`
- **Output:** `4`

**Explanation:** The continuous subarrays with sums divisible by `3` are:

| Subarray | Sum |
|---|---|
| `[1, 2]` (index 0 to 1) | `3` |
| `[1, 2, 3]` (index 0 to 2) | `6` |
| `[2, 3, 4]` (index 1 to 3) | `9` |
| `[3]` (index 2 to 2) | `3` |

#### Example 2

- **Input:** `N = 4`, `K = 5`, `transactions = [5, 0, 5, 0]`
- **Output:** `10`

**Explanation:** All subarrays in this example yield sums that are divisible by `5`.

#### Example 3

- **Input:** `N = 3`, `K = 7`, `transactions = [1, 2, 3]`
- **Output:** `0`

---

### Constraints

- `1 <= N <= 10^5`
- Each transaction amount is an integer in the range `[-10^9, 10^9]`.
- `1 <= K <= 10^5`

> **Notes:**
> - A subarray refers to a contiguous segment of the array.
> - Every valid subarray must be considered, including subarrays of length 1.
> - The emphasis is on applying a **divide and conquer** approach.

---
