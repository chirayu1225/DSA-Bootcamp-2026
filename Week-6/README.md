# Week 6 - DSA Bootcamp 2026

[Home](https://github.com/wncc/DSA-Bootcamp-2026/blob/main/README.md) > Week 6

---

## Learning Path

Week 6 has **4 topics** that build directly on what you learned in Week 5. You go deeper into trees — adding constraints and structure — and revisit stacks with a powerful new pattern. These topics are extremely common in interviews.

```
Binary Trees
    |
    |  General trees allowed any number of children. Binary trees restrict
    |  each node to at most two — left and right. This one constraint unlocks
    |  BSTs, heaps, and expression parsing. Learn this before BST.
    v
Binary Search Trees (BST)
    |
    |  Add one rule to a binary tree: left < node < right, always.
    |  Now you can search, insert, and delete in O(log n) on average —
    |  the same power as binary search, but on a dynamic structure.
    v
Heap
    |
    |  A complete binary tree with one extra property: parent is always
    |  greater (max-heap) or smaller (min-heap) than its children.
    |  The go-to structure for priority queues, scheduling, and top-K problems.
    v
Monotonic Stack
    |
    |  A regular stack with one extra rule: values inside stay sorted.
    |  Turns O(n²) "next greater/smaller element" problems into O(n).
    |  Once you see the pattern, a whole class of problems becomes trivial.
    v
Week 7

```

---

## Topics

| # | Topic | What You Will Learn | Est. Time |
|---|-------|---------------------|-----------|
| 1 | [Binary Trees](https://github.com/wncc/DSA-Bootcamp-2026/blob/main/Week-6/Binary_Trees.md) | Structure, node representation, left/right children, tree traversals, why binary trees power BSTs and heaps | 3–4 hrs |
| 2 | [Binary Search Trees](https://github.com/wncc/DSA-Bootcamp-2026/blob/main/Week-6/Binary_Search_Tree.md) | BST property, search/insert/delete in O(log n), inorder traversal gives sorted output, BST vs general binary tree | 3–4 hrs |
| 3 | [Heap](https://github.com/wncc/DSA-Bootcamp-2026/blob/main/Week-6/Heap.md) | Min-heap vs max-heap, heapify, heap operations, priority queue using STL, top-K problems, heap sort | 3–4 hrs |
| 4 | [Monotonic Stack](https://github.com/wncc/DSA-Bootcamp-2026/blob/main/Week-6/monotonic-stack.md) | Monotonic increasing/decreasing stacks, next greater element, next smaller element, stock span, largest rectangle | 3–4 hrs |

---

## Problem Set

Problem set for Week 6 will be added soon. In the meantime, practice these patterns on LeetCode:

- **Binary Trees:** LC 104, 226, 572, 543
- **BST:** LC 700, 701, 98, 230
- **Heap:** LC 215, 347, 703, 1046
- **Monotonic Stack:** LC 496, 739, 84, 85

---

## Suggested Daily Schedule

| Day | Topics | Focus |
|-----|--------|-------|
| 1 | Binary Trees | Structure, traversals, left/right child relationships |
| 2 | Binary Trees problems | Height, diameter, mirror, path sum |
| 3 | BST | Search, insert, delete, inorder = sorted |
| 4 | BST problems | Validate BST, LCA, kth smallest |
| 5 | Heap | Min/max heap, heapify, STL priority_queue |
| 6 | Heap problems | Top-K elements, merge K sorted lists |
| 7 | Monotonic Stack | Next greater/smaller, stock span, largest rectangle |

---

## Before You Move to Week 7

- Can you write inorder, preorder, and postorder traversal of a binary tree from memory?
- Do you know why inorder traversal of a BST gives a sorted sequence?
- Can you find the kth smallest element in a BST without extra space?
- Can you implement a min-heap from scratch using an array?
- Can you solve "Next Greater Element" using a monotonic stack in O(n)?
- Have you attempted the recommended problems for all 4 topics?

If yes, you are ready. [See you in Week 7.](https://github.com/wncc/DSA-Bootcamp-2026/blob/main/Week-7/README.md)

---

[Home](https://github.com/wncc/DSA-Bootcamp-2026/blob/main/README.md) | [Previous: Week 5](https://github.com/wncc/DSA-Bootcamp-2026/blob/main/Week-5/README.md) | [Next: Week 7](https://github.com/wncc/DSA-Bootcamp-2026/blob/main/Week-7/README.md)
