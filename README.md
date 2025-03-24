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
