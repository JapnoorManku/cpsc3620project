# CPSC_3620_Project_Report
# Efficient Algorithms for Text Segmentation Variants

## 1. Introduction
Text segmentation is a fundamental problem in **Natural Language Processing (NLP)**. Given a sequence of characters, the goal is to partition it into valid words using a predefined dictionary.  

This repository provides **Dynamic Programming (DP)** solutions for three variants of the text segmentation problem.  

We assume access to a function `IsWord(s)`, which checks whether a given substring `s` is a valid word.

---

## 2. Problem Statements and Solutions

### (a) Counting the Number of Ways to Partition a String into Words
#### Problem Description
Given an array `A[1..n]` of characters, determine the number of ways to segment `A` into valid words.  
For example, given `"ARTISTOIL"`, the valid segmentations are:
1. `"ARTIST · OIL"`
2. `"ART · IS · TOIL"`

Thus, the algorithm should return `2`.

#### Approach
We use **Dynamic Programming (DP)** to efficiently count the number of partitions:
- Define `dp[i]` as the number of ways to segment `A[0..i]` into valid words.
- Iterate over possible ending positions and check whether the substring `A[j:i]` is a valid word.
- Use the recurrence relation:  
  ```math
  dp[i] = ∑ dp[j]  if A[j:i] is a valid word
---
## 3. Complexity analysis
### (a) count_partitions(A)
This function calculates the number of ways to partition a string A into words from a dictionary.
#### Time Complexity:
1. Let n = len(A), the function iterates over i from 1 to n.
2. For each i, it iterates over j from 0 to i-1, checking if A[j:i] is a word using IsWord(A[j:i]), which takes O(1) time in an ideal hash-based dictionary lookup.
3. The worst-case scenario for the nested loop results in: O(n) + (O(n-1) + O(n-2) +...+ O(1) = O(n²)
Thus, the total time complexity is O(n²).
#### Space Complexity:
1. The dp array has a size of O(n).
2. No additional space is used except for function call stack and variables.
Thus, the space complexity is O(n).

### (b) can_partition_same_indices(A, B)
This function determines if two strings can be partitioned at the same indices into valid words.
#### Time Complexity:
1. Similar to count_partitions, the function has two nested loops iterating up to n, leading to a worst-case complexity of O(n²).
2. The IsWord function is called inside the inner loop and runs in O(1) time.
3. The overall complexity remains O(n²).
#### Space Complexity:
1. The dp array takes O(n) space.
Thus, the space complexity is O(n).

### (c) count_partition_same_indices(A, B)
This function counts the number of ways to partition A and B at the same indices.
#### Time Complexity:
1. We have two nested loops iterating up to n, leading to a worst-case O(n²) complexity.
2. IsWord(A[j:i]) and IsWord(B[j:i]) are called inside the inner loop in O(1) time.
3. The overall time complexity is O(n²).
#### Space Complexity:
1. The dp array requires O(n) space.
Thus, the space complexity is O(n).

### Summary of Complexity Analysis
| Function | Time Complexity | Space Complexity |
|----------|---------------|----------------|
| `count_partitions(A)` | **O(n²)** | **O(n)** |
| `can_partition_same_indices(A, B)` | **O(n²)** | **O(n)** |
| `count_partition_same_indices(A, B)` | **O(n²)** | **O(n)** |

## 4. Proof of Correction by using Induction
### **1️⃣ Proof for `count_partitions(A)`**

**Claim:** The function correctly computes the number of ways to partition `A` into valid words.

#### **Proof by Induction on `n` (Length of `A`)**
- **Base Case (`n = 0`)**:  
  - The empty string has **one valid partition** (doing nothing).  
  - `dp[0] = 1`, which is correct.

- **Inductive Step:**  
  - Suppose the function correctly counts partitions for all strings up to length `n-1`.  
  - For a string of length `n`, the algorithm checks all possible prefixes `A[j-1:i]` (where `j ≤ i`) and sums valid partitions.
  - If `A[j-1:i]` is a valid word, we add `dp[j-1]` to `dp[i]`, ensuring that `dp[i]` correctly accumulates all valid segmentations.

- **Conclusion:**  
  By induction, `dp[n]` correctly computes the number of ways to partition `A`.

---

### **2️⃣ Proof for `can_partition_same(A, B)`**

**Claim:** The function correctly determines whether `A` and `B` can be partitioned at the same indices.

#### **Correctness Argument**
- **Base Case (`n = 0`)**:  
  - The empty strings trivially have a matching partition.
  - `dp[0] = True`, which is correct.

- **General Case:**  
  - The function iterates through `A` and `B`, checking if both can be partitioned into valid words at the same indices.
  - If `A[j-1:i]` and `B[j-1:i]` are both words, we propagate `dp[j-1] → dp[i] = True`.
  - This ensures `dp[i] = True` if and only if `A[0:i]` and `B[0:i]` share a valid segmentation.

- **Conclusion:**  
  - If a valid common partition exists, `dp[n] = True`.  
  - Otherwise, `dp[n] = False`, which is correct.

---

### **3️⃣ Proof for `count_common_partitions(A, B)`**

**Claim:** The function correctly computes the number of ways `A` and `B` can be partitioned at the same indices.

#### **Proof Using Dynamic Programming and Induction**
- **Base Case (`n = 0`)**:  
  - There is **one valid partition** for empty strings.  
  - `dp[0] = 1`, which is correct.

- **Inductive Hypothesis:**  
  - Assume for all strings up to length `n-1`, the function correctly counts the number of common partitions.

- **Inductive Step:**  
  - The function iterates through `A` and `B`, checking all substrings `A[j-1:i]` and `B[j-1:i]`.  
  - If both substrings are valid words, we sum `dp[j-1] → dp[i]`, ensuring that `dp[i]` correctly accumulates valid common segmentations.

- **Conclusion:**  
  By induction, `dp[n]` correctly computes the number of ways `A` and `B` can be partitioned at the same indices.

---

### **Final Conclusion**
Each algorithm follows **dynamic programming principles**, ensuring correctness through:
- **Optimal substructure** (Each problem depends on subproblems).
- **Overlapping subproblems** (Previously computed values are reused).
- **Inductive reasoning** (Base case is correct, and correctness extends to larger cases).

Thus, all algorithms are **provably correct**.

