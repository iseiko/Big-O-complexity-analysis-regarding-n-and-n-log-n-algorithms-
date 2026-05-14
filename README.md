## Abstract
This document compares **QuickSort** and **Selection Sort** in terms of **how they work**, **time/space complexity**, and **practical performance** when implemented in **Java**. It also proposes an experimental setup to measure execution time across different input sizes and data distributions.

---

## 1. Background: What does it mean to “sort”?
Sorting arranges elements into a chosen order (typically ascending). In practice, the choice of sorting algorithm depends on:
- input size,
- input distribution (already sorted, random, reversed, many duplicates),
- memory constraints,
- stability requirements,
- and constant-factor performance on real machines.

---

## 2. QuickSort

### 2.1 Overview
QuickSort is a **divide-and-conquer** sorting algorithm. It repeatedly:
1. selects a **pivot** element,
2. partitions the array so that values lower than the **pivot** are placed before it and values higher than the **pivot** after it,
3. recursively sorts the left and right partitions.

If partitioning is balanced, the recursion depth stays small and the algorithm is very fast in practice.

---

### 2.2 Pivot selection strategies
Pivot selection has a large impact on performance:

- **First/last element**: simple, but can perform poorly on already-sorted or reverse-sorted inputs.
- **Random pivot**: reduces the chance of consistently bad partitions.
- **Median-of-three** (first, middle, last): often improves practical performance without heavy overhead.

**Java note:** for benchmarking, it’s common to implement either *random pivot* or *median-of-three* to reduce worst-case behavior in typical datasets.

---

### 2.3 Partitioning approaches
Partitioning is the core of QuickSort. Common schemes:

- **Lomuto partition**
  - easy to implement,
  - usually more swaps,
  - can be slower in practice.

- **Hoare partition**
  - fewer swaps on average,
  - typically faster,
  - but requires careful index handling.

---

### 2.4 Complexity
Let `n` be the array size.

- **Best case:** `O(n log n)` (partitions are balanced)
- **Average case:** `O(n log n)` (typical random input)
- **Worst case:** `O(n²)` (highly unbalanced partitions repeatedly)

**Space (in-place array)**
- Partitioning can be in-place, so extra memory is small.
- However, recursion uses call stack:
  - average: `O(log n)` stack depth
  - worst: `O(n)` stack depth

---

### 2.5 Advantages
- Very good performance on large arrays in typical scenarios.
- In-place partitioning: low additional memory usage.
- Often cache-friendly due to sequential scans during partitioning.

---

### 2.6 Disadvantages
- Worst-case time `O(n²)` if pivot choices produce bad partitions.
- Not stable in its common in-place forms (equal elements may change order).
- Recursive implementation can risk deep recursion on adversarial input (unless mitigated).

---

## 3. Selection Sort

### 3.1 Overview
Selection Sort is a simple comparison sort. For each position `i` from left to right:
1. find the smallest element in the unsorted part (`i..n-1`),
2. swap it into position `i`.

---

### 3.2 Complexity
- **Best / Average / Worst:** always `O(n²)` comparisons.
- **Swaps:** at most `n - 1` swaps (one per outer-loop step).

**Space:** `O(1)` extra space (in-place).

---

### 3.3 Advantages
- Very easy to implement and explain.
- Predictable behavior: always the same asymptotic time.
- Low number of writes/swaps, which can matter if writes are expensive.

---

### 3.4 Disadvantages
- Slow for medium/large inputs due to `O(n²)`.
- Not stable in the standard implementation.
- Generally not used in production for large datasets.

---

## 4. Side-by-side comparison

| Aspect          | QuickSort                     | Selection Sort              |
| --------------- | ----------------------------- | --------------------------- |
| Strategy        | Divide-and-conquer            | Repeated selection          |
| Typical time    | `O(n log n)`                  | `O(n²)`                     |
| Worst-case time | `O(n²)`                       | `O(n²)`                     |
| Extra memory    | small, recursion stack        | `O(1)`                      |
| Stable?         | usually no                    | usually no                  |
| Best use case   | large inputs, general-purpose | very small inputs, teaching |

---

## 5. Experimental plan to implement on section 6 of this research

### 5.1 Goal
Measure and compare execution time of both algorithms under different conditions, and visualize results.

### 5.2 Dataset sizes
Example sizes chosen to be used on this example:
- 10k, 20k, 30k, 40k and 50k (Selection Sort may be too slow beyond this depending on machine)

### 5.3 Input distributions
Test each size under:
- random values
- already sorted
- reverse sorted
- many duplicates (e.g., values in small range like 0..100)

---

## 6. Graphics and value-based comparison

### 6.1 Random values

### 6.2 Already sorted values

### 6.3 Reverse sorted values

### 6.4 Many duplicates on dataset

---

## 7. Conclusion (draft)
QuickSort is generally more suitable for large datasets due to its `O(n log n)` average behavior and strong real-world performance. Selection Sort remains valuable for learning and for small inputs where simplicity matters, but its `O(n²)` growth makes it impractical as input size increases.

---

## References
- Tests made by myself using different datasets sizes.
- geeksforgeeks.org
- stackoverflow.com
- analysis 
