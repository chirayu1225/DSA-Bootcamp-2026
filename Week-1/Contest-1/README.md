# Week 1 - Contest 1

[Home](../../README.md) > [Week 1](../README.md) > Contest 1

This contest tested the core Week 1 topics - **syntax & I/O, arrays, sorting, and STL basics** - through six problems of increasing difficulty. Below are the problem statements from the contest for your reference. If you didn't get a chance to attempt all of them during the contest, try solving them now - read each problem carefully, pay attention to edge cases, and think about which Week 1 pattern applies before writing code.

---

## Q1. Divisibility Label Mapping

### Problem Description

Consider a sequence of integers `values` with `n` entries.

For each item in `values`, determine a text label from its divisibility.

Use `fizzbuzz` when the value is divisible by both `3` and `5`.

Use `fizz` when the value is divisible by `3` but not by `5`.

Use `buzz` when the value is divisible by `5` but not by `3`.

Use `not fizzbuzz` when the value is divisible by neither `3` nor `5`.

Keep the output order the same as the order of `values`, with one label produced for each value.

---

### Input & Output

#### Input Format

- The first whitespace-separated value represents `n`, the number of integers in `values`.
- The next `n` whitespace-separated values represent the integers in the sequence `values`.

#### Output Format

- The output contains `n` lines when `n > 0`, and each line corresponds to the matching value from `values` in the same order.
- Each output line contains exactly one of these strings: `fizzbuzz`, `fizz`, `buzz`, or `not fizzbuzz`.
- If there are no values to process, the produced text is the empty string `""`, and that empty string is what is printed to standard output.

---

### Examples

#### Example 1

- **Input:** `5` `9 20 14 45 25`
- **Output:**

```
fizz
buzz
not fizzbuzz
fizzbuzz
buzz
```

**Explanation:**

- `9` is divisible by `3` only, so its label is `fizz`.
- `20` is divisible by `5` only, so its label is `buzz`.
- `14` is divisible by neither `3` nor `5`, so its label is `not fizzbuzz`.
- `45` is divisible by both `3` and `5`, so its label is `fizzbuzz`.
- `25` is divisible by `5` only, so its label is `buzz`.

#### Example 2

- **Input:** `6` `8 12 50 75 22 27`
- **Output:**

```
not fizzbuzz
fizz
buzz
fizzbuzz
not fizzbuzz
fizz
```

**Explanation:**

- `8` is divisible by neither `3` nor `5`, so its label is `not fizzbuzz`.
- `12` is divisible by `3` only, so its label is `fizz`.
- `50` is divisible by `5` only, so its label is `buzz`.
- `75` is divisible by both `3` and `5`, so its label is `fizzbuzz`.
- `22` is divisible by neither `3` nor `5`, so its label is `not fizzbuzz`.
- `27` is divisible by `3` only, so its label is `fizz`.

---

### Constraints

- `0 <= n <= 10^5`
- `-10^9 <= values[i] <= 10^9`

---

## Q2. Finding the Single Element in an Array

### Problem Description

You are given an array of integers `arr` of size `n`, where every element appears exactly twice except for one element, which appears only once.

Your task is to find the element that occurs only once in the array.

---

### Input & Output

#### Input Format

- The first line contains an integer `n`, denoting the size of the array.
- The second line contains `n` space-separated integers, representing the elements of the array `arr`.

#### Output Format

- A single integer denoting the element that appears only once in the array.

---

### Examples

#### Example 1

- **Input:** `n = 7`, `arr = [3, 5, 2, 1, 2, 5, 3]`
- **Output:** `1`

**Explanation:** In the given array, all elements occur twice except for `1`.

#### Example 2

- **Input:** `n = 5`, `arr = [2, 2, 3, 3, 1]`
- **Output:** `1`

**Explanation:** In the given array, all elements occur twice except for `1`.

---

### Constraints

- `2 <= n <= 10^5`

---

## Q3. Rating Peak Tracker

### Problem Description

You are provided with a sequence of integer adjustments `adjustments`.

Begin with a rating value of `1500`.

Apply the values in `adjustments` from left to right. After each update, keep track of the largest rating reached so far.

Determine two results: `peakValue`, which is the maximum rating seen at any point, and `finalValue`, which is the rating after all updates have been processed.

If `adjustments` is empty, both results remain `1500`.

---

### Input & Output

#### Input Format

- The first value is an integer `n`, representing how many adjustments are provided.
- The next `n` integers represent the elements of `adjustments` in order.
- These integers are read as whitespace-separated tokens, so they may appear on one line or across multiple lines.
- If `n` is `0`, no adjustment values follow.
- If the input is completely empty, `adjustments` is treated as an empty sequence.

#### Output Format

- A single line containing two space-separated integers: `peakValue` (the highest rating reached while processing the sequence from the initial value `1500`) and `finalValue` (the rating after all `n` adjustments have been applied).
- Two integers are always written, even when `n` is `0`.

---

### Examples

#### Example 1

- **Input:** `6` `80 120 -90 40 -30 10`
- **Output:** `1700 1630`

**Explanation:** Starting from `1500`, the running values become `1580`, `1700`, `1610`, `1650`, `1620`, and `1630`. So `peakValue` is `1700` and `finalValue` is `1630`.

#### Example 2

- **Input:** `4` `-70 -80 20 -10`
- **Output:** `1500 1360`

**Explanation:** The rating changes to `1430`, `1350`, `1370`, and `1360`. It never goes above the starting value, so `peakValue` stays `1500`, while `finalValue` is `1360`.

---

### Constraints

- `0 <= n <= 10^5`
- `-10^4 <= adjustments[i] <= 10^4`
- After every processed prefix of `adjustments`, the running rating is at least `0`.

---

## Q4. Exclusive Sum Root

### Problem Description

You are provided with two integer sequences `valuesA` and `valuesB`.

Form an `exclusiveTotal` by checking both sequences. Add each entry from `valuesA` if that value does not occur anywhere in `valuesB`, and add each entry from `valuesB` if that value does not occur anywhere in `valuesA`.

If a qualifying value appears multiple times in the same sequence, each occurrence contributes to `exclusiveTotal`.

Repeatedly replace `exclusiveTotal` with the total of its digits until only one digit remains.

Determine that final digit.

---

### Input & Output

#### Input Format

- The first integer represents `n`, the number of values in `valuesA`.
- The next `n` space-separated integers represent `valuesA`.
- The next integer represents `m`, the number of values in `valuesB`.
- The next `m` space-separated integers represent `valuesB`.

#### Output Format

- A single integer representing the final single digit obtained after repeatedly adding the digits of `exclusiveTotal`.

---

### Examples

#### Example 1

- **Input:** `n = 5`, `valuesA = [14, 3, 88, 6, 21]`, `m = 4`, `valuesB = [6, 14, 9, 10]`
- **Output:** `5`

**Explanation:** In `valuesA`, the exclusive values are `3`, `88`, and `21`. In `valuesB`, the exclusive values are `9` and `10`. Their combined total is `131`, and `1 + 3 + 1 = 5`.

#### Example 2

- **Input:** `n = 7`, `valuesA = [4, 4, 12, 30, 17, 1, 8]`, `m = 5`, `valuesB = [30, 2, 4, 19, 19]`
- **Output:** `6`

**Explanation:** From `valuesA`, the exclusive values are `12`, `17`, `1`, and `8`. From `valuesB`, the exclusive values are `2`, `19`, and `19`. The combined total is `78`, then `7 + 8 = 15`, and finally `1 + 5 = 6`.

---

### Constraints

- `1 <= n <= 10`
- `1 <= m <= 10`
- `1 <= valuesA[i] <= 10^9`
- `1 <= valuesB[i] <= 10^9`
- At least one occurrence belongs to exactly one of the two sequences.

---

## Q5. Union of Two Sorted Arrays

### Problem Description

You are given two sorted arrays `a` and `b` of integers of length `m` and `n` respectively. Your task is to find the union of the arrays.

> **Note:** The union of two arrays is defined as the set containing all distinct elements from both arrays.

---

### Input & Output

#### Input Format

- The first line of input contains two integers `m` and `n`.
- The second line of input contains `m` space-separated integers.
- The third line of input contains `n` space-separated integers.

#### Output Format

- The set of distinct elements from the union of both input arrays, printed in sorted order.

---

### Examples

#### Example 1

- **Input:** `m = 5, n = 4`, `a = [3, 5, 5, 6, 6]`, `b = [1, 2, 3, 5]`
- **Output:** `1 2 3 5 6`

**Explanation:** `1, 2, 3, 5` and `6` are the elements included in the union set of both arrays.

#### Example 2

- **Input:** `m = 6, n = 6`, `a = [1, 3, 3, 7, 9, 11]`, `b = [2, 4, 6, 6, 10, 12]`
- **Output:** `1 2 3 4 6 7 9 10 11 12`

**Explanation:** `1, 2, 3, 4, 6, 7, 9, 10, 11` and `12` are the elements included in the union set of both arrays.

---

### Constraints

- `1 <= m, n <= 10^5`
- `0 <= a[i], b[i] <= 10^5`

---

## Q6. Missing and Repeating Elements

### Problem Description

You are given an unsorted array `arr` of size `n` containing integers from the range `1` to `n`, with exactly one number missing and one number repeating.

Your objective is to identify the repeating number and the missing number, and return them in the format `[repeating, missing]`.

---

### Input & Output

#### Input Format

- The first line contains an integer `n` representing the number of elements in the array `arr`.
- The second line contains `n` space-separated integers representing the elements of the array `arr`.

#### Output Format

- A single line containing two integers: the repeating number followed by the missing number.

---

### Examples

#### Example 1

- **Input:** `arr = [1, 2, 2]`
- **Output:** `2 3`

**Explanation:** The number `2` appears twice. The number `3` is missing.

#### Example 2

- **Input:** `arr = [3, 1, 3]`
- **Output:** `3 2`

**Explanation:** The number `3` appears twice. The number `2` is missing.

---

### Constraints

- `2 <= n <= 10^5`
- `1 <= arr[i] <= n`