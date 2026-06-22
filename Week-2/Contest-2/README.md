# Week 2 - Contest 2

[Home](../../README.md) > [Week 2](../README.md) > Contest 2

This contest tested the core Week 2 topics - **prefix sums, two pointers, binary search, and strings** - through six problems of increasing difficulty. Below are the problem statements from the contest for your reference. If you didn't get a chance to attempt all of them during the contest, try solving them now - read each problem carefully, pay attention to edge cases, and think about which Week 2 pattern applies before writing code.

---

## Q1. String Compression

### Problem Description

You are given a string consisting of lowercase English letters. Your task is to compress the string into a new format where consecutive repeated characters are replaced with the character followed by the count of its repetitions.

> **Note:** If a character appears in a consecutive sequence of one, it should be followed by the number `1`.

---

### Input & Output

#### Input Format

A string `s` containing only lowercase English letters.

#### Output Format

A string representing the compressed version of the input.

---

### Examples

#### Example 1

- **Input:** `aaaabbbcca`
- **Output:** `a4b3c2a1`

#### Example 2

- **Input:** `abcccdd`
- **Output:** `a1b1c3d2`

#### Example 3

- **Input:** `bbbb`
- **Output:** `b4`

---

### Constraints

- `1 <= len(s) <= 100`

---

## Q2. Max Length Subarray Sum Difference

### Problem Description

To optimize storage allocation for a data processing system, you need to analyze the sizes of data segments to maintain efficient usage.

You are given an array of non-negative integers `dataSizes`, where each element represents the size of a data segment. Additionally, you are provided with a non-negative integer `threshold`.

Your task is to find the maximum length of a contiguous subarray such that the difference between the sum of the subarray and the sum of the elements before this subarray (note that this difference is **not** taken in absolute terms, meaning it can be positive or negative) is less than or equal to `threshold`.

In simpler terms, you need to identify the longest interval within `dataSizes` for which the condition:

> `sum(interval) - sum(prefix before interval) <= threshold`

is satisfied.

Return an integer representing the maximum length of such a subarray. If no such subarray exists, return `0`.

---

### Function Signature

```cpp
int solution(vector<int> dataSizes, int threshold) {
    // Function implementation goes here
}
```

---

### Examples

#### Example 1

- **Input:** `dataSizes = [1, 2, 3, 4]`, `threshold = 5`
- **Output:** `2`

**Explanation:**

| Subarray | Prefix Subarray | Difference | `<= 5`? |
|---|---|---|---|
| `[1]` | `[]` | `1 - 0 = 1` | ✅ |
| `[2]` | `[1]` | `2 - 1 = 1` | ✅ |
| `[3]` | `[1, 2]` | `3 - 3 = 0` | ✅ |
| `[4]` | `[1, 2, 3]` | `4 - 6 = -2` | ✅ |
| `[1, 2]` | `[]` | `3 - 0 = 3` | ✅ |
| `[2, 3]` | `[1]` | `5 - 1 = 4` | ✅ |
| `[3, 4]` | `[1, 2]` | `7 - 3 = 4` | ✅ |
| `[1, 2, 3]` | `[]` | `6 - 0 = 6` | ❌ |
| `[2, 3, 4]` | `[1]` | `9 - 1 = 8` | ❌ |
| `[1, 2, 3, 4]` | `[]` | `10 - 0 = 10` | ❌ |

The longest subarrays with acceptable differences are `[1, 2]`, `[2, 3]`, and `[3, 4]`, all of length 2. So the answer is **2**.

#### Example 2

- **Input:** `dataSizes = [8, 5, 6, 1, 4, 1, 9]`, `threshold = 5`
- **Output:** `4`

**Explanation:**

The contiguous subarray `[6, 1, 4, 1]` has a sum of `12` and the prefix subarray `[8, 5]` has a sum of `13`. The difference is `12 - 13 = -1`, which is within the threshold.

Another contiguous subarray of length 4, `[1, 4, 1, 9]`, also yields an acceptable difference. Its sum is `15`. The prefix subarray `[8, 5, 6]` has a sum of `19`. The difference is `15 - 19 = -4`.

Therefore, the answer is **4**.

---

### Constraints

- `1 <= len(dataSizes) <= 10^5`

---

## Q3. Count Binary Substrings

### Problem Description

Count the number of substrings in a binary string that contain an equal number of `0`s and `1`s, where all `0`s and `1`s are grouped together. Duplicate substrings are counted in the total.

A binary string consists only of `0`s and `1`s, and a substring is a contiguous group of characters within the string.

---

### Function Signature

```cpp
int getSubStringCount(string s);
```

**Parameters:**

- `s` - a binary string

**Returns:**

- `int` - the number of substrings that meet the criteria

---

### Examples

#### Example 1

- **Input:** `s = "011001"`
- **Output:** `4`

**Explanation:** The qualifying substrings are `"01"`, `"10"`, `"1100"`, and `"01"`, giving a total of 4. Note that `"0110"` has equal `0`s and `1`s but is not counted because the `0`s and `1`s are not grouped together.

#### Example 2

- **Input:** `s = "001100011"`
- **Output:** `6`

**Explanation:** The substrings `"01"`, `"0011"`, `"10"`, `"1100"`, `"01"`, and `"0011"` have an equal number of `0`s and `1`s with consecutive groupings.

#### Example 3

- **Input:** `s = "000110"`
- **Output:** `3`

**Explanation:** The substrings `"01"`, `"0011"`, and `"10"` satisfy the constraints.

---

### Constraints

- `1 <= length of s <= 10^5`
- The string `s` consists of `0`s and `1`s only.

---

## Q4. Satellite Signal Boosters

### Problem Description

A deep-space communications agency has placed `N` relay stations along a straight orbital path, each at a distinct integer coordinate. Signal quality degrades over distance - the greater the distance between two adjacent stations, the higher the chance of data loss. The agency defines the network's weakest link as the largest gap between any two consecutive stations.

To strengthen the network, the agency can deploy exactly `K` signal repeaters anywhere along the path at integer positions. Each repeater acts as a new relay station, effectively splitting the gap it is placed in. Your task is to place the `K` repeaters optimally to minimize the largest gap between any two consecutive stations (including the newly added repeaters).

---

### Function Signature

```cpp
long long signalBoosters(int N, int K, vector<int> pos);
```

**Parameters:**

- `N` (`int`) - Number of existing relay stations.
- `K` (`int`) - Number of repeaters to place.
- `pos` (`vector<int>`) - Sorted array of `N` distinct integers representing station positions.

**Returns:**

- `long long` - the minimized maximum gap after placing `K` repeaters optimally.

---

### Input & Output

#### Input Format

1. The first line contains a single integer `N`, the number of relay stations.
2. The second line contains a single integer `K`, the number of repeaters to deploy.
3. The third line contains `N` space-separated integers representing the positions of the stations in sorted order.

#### Output Format

Print a single integer - the minimized maximum gap between any two consecutive stations after placing all `K` repeaters.

---

### Examples

#### Example 1

**Input:**

```
5
3
1 5 12 17 28
```

**Output:**

```
5
```

**Explanation:**

Initial gaps: `4`, `7`, `5`, `11`.

To achieve an answer - try maximum gap = `5`:

- Gap `7`: needs 1 repeater (e.g., gaps `4` and `3`, both ≤ `5`).
- Gap `11`: needs 2 repeaters (e.g., sub-gaps `4`, `4`, `3`, all ≤ `5`).

---

### Constraints

- `2 <= N <= 10^5`
- `0 <= K <= 10^9`
- `1 <= pos[i] <= 10^9`

---

## Q5. Count Balancing Elements

### Problem Description

When an element is deleted from an array, higher-indexed elements shift down to fill the gap. A "balancing element" is one that, when deleted, results in the sum of even-indexed elements equaling the sum of odd-indexed elements in the resulting array. Your task is to determine how many balancing elements exist in a given array.

**Example:** `arr = [5, 5, 2, 5, 8]`

When the first `5` is deleted, the array becomes `[5, 2, 5, 8]`:

- Sum of even-indexed elements: `5 + 5 = 10`
- Sum of odd-indexed elements: `2 + 8 = 10`

Similarly, when the second `5` is deleted, the array becomes `[5, 2, 5, 8]` with the same balanced sums.

No other elements have this property, so there are **2** balancing elements: `arr[0]` and `arr[1]`.

---

### Function Signature

```cpp
int countBalancingElements(vector<int> arr);
```

**Parameters:**

- `arr` (`int[]`) - an array of integers

**Returns:**

- `int` - the number of balancing elements in the input array

---

### Examples

#### Example 1

- **Input:** `n = 4`, `arr = [2, 1, 6, 4]`
- **Output:** `1`

**Explanation:** When `arr[1] = 1` is deleted, the array becomes `[2, 6, 4]`. The sum of even-indexed elements is `2 + 4 = 6` and the sum of odd-indexed elements is `6`. No other elements of the original array have that property.

#### Example 2

- **Input:** `n = 3`, `arr = [2, 2, 2]`
- **Output:** `3`

**Explanation:** The input array is `[2, 2, 2]`. All three elements of this array are balancing elements. After deleting any of them, the array becomes `[2, 2]`. The sum of even-indexed elements is `2` and the sum of odd-indexed elements is `2`.

---

### Constraints

- `1 <= n <= 2 * 10^5`
- `1 <= arr[i] <= 10^9`

---

## Q6. Amazon Order Delays

### Problem Description

In an Amazon warehouse, there are `n` orders to be processed, each with a priority represented by an array `priorities`, where `priorities[i]` denotes the priority of the `i`-th order. Orders are processed in reverse, starting from the last order (index `n - 1`) and moving to the first order (index `0`).

An order experiences "delay" if an order with lower priority is processed before it. The delay period for an order starts when the first lower-priority order begins processing and ends when the order itself is finally being processed.

Given that each order takes 1 unit of time to process, calculate the delay time for each order.

**Example:** `n = 4`, `priorities = [8, 2, 5, 3]`

The orders are processed in reverse, starting from the last order and moving to the first:

- **Order 3** (priority `3`): No prior orders processed, so delay = `0`.
- **Order 2** (priority `5`): First lower-priority order processed before it is Order 3 (priority `3`), so the delay is the difference in their positions: `3 - 2 = 1`.
- **Order 1** (priority `2`): No lower-priority orders processed before it, so delay = `0`.
- **Order 0** (priority `8`): First lower-priority order processed before it is Order 3 (priority `3`), so delay = `3 - 0 = 3`.

Thus, the delay time for each order is: `[3, 0, 1, 0]`.

---

### Function Signature

```cpp
vector<int> CalculateOrderDelays(vector<int> priorities);
```

**Parameters:**

- `priorities` (`int[]`) - the priorities of the orders to be processed

**Returns:**

- `int[]` - an integer array representing the delay time for each order

---

### Examples

#### Example 1

**Input:**

```
STDIN      FUNCTION
-----      --------
4       -> priorities[] size n = 4
6       -> priorities = [6, 10, 9, 7]
10
9
7
```

**Output:**

```
0
2
1
0
```

**Explanation:**

- **Order 3** (priority `7`): Since no orders were processed before it, there is no delay, so delay = `0`.
- **Order 2** (priority `9`): The first order with a lower priority processed before it is Order 3 (priority `7`). So, the delay is the difference in their positions: `3 - 2 = 1`.
- **Order 1** (priority `10`): Two orders with lower priorities (`7` and `9`) were processed before it. The earliest among them is Order 3 (priority `7`) at position `3`. So, the delay is: `3 - 1 = 2`.
- **Order 0** (priority `6`): No orders with a lower priority were processed before it, so delay = `0`.

Thus, the delay time for each order is: `[0, 2, 1, 0]`.

#### Example 2

**Input:**

```
STDIN      FUNCTION
-----      --------
7       -> priorities[] size n = 7
8       -> priorities = [8, 2, 11, 4, 9, 4, 7]
2
11
4
9
4
7
```

**Output:**

```
6
0
4
0
2
0
0
```

**Explanation:**

- **Order 6** (priority `7`): Since no orders were processed before it, there is no delay, so delay = `0`.
- **Order 5** (priority `4`): No orders with a lower priority were processed before it, so delay = `0`.
- **Order 4** (priority `9`): Two orders with lower priorities (`4` and `7`) were processed before it. The earliest among them is Order 6 (priority `7`) at position `6`, so delay = `6 - 4 = 2`.
- **Order 3** (priority `4`): No orders with a lower priority were processed before it, so delay = `0`.
- **Order 2** (priority `11`): Four orders with lower priorities (`4`, `4`, `7`, and `9`) were processed before it. The earliest among them is Order 6 (priority `7`) at position `6`, so delay = `6 - 2 = 4`.
- **Order 1** (priority `2`): No orders with a lower priority were processed before it, so delay = `0`.
- **Order 0** (priority `8`): Four orders with lower priorities (`2`, `4`, `4`, and `7`) were processed before it. The earliest among them is Order 6 (priority `7`) at position `6`, so delay = `6 - 0 = 6`.

Thus, the delay time for each order is: `[6, 0, 4, 0, 2, 0, 0]`.

---

### Constraints

- `1 <= n <= 3 * 10^5`
- `1 <= priorities[i] <= 10^9`