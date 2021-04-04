# 0x315 Sequence

- [1. Sequence](#1-sequence)
    - [1.1. Strategies](#11-strategies)
    - [1.2. Subsequence Problems](#12-subsequence-problems)
- [2. String Problems](#2-string-problems)
    - [2.1. Data Structure](#21-data-structure)
        - [2.1.1. Rope](#211-rope)
        - [2.1.2. Suffix Array](#212-suffix-array)
    - [2.2. Matching Problems](#22-matching-problems)
    - [2.3. Sequence Query Problems](#23-sequence-query-problems)
- [3. Compression](#3-compression)
    - [3.1. Huffman Code](#31-huffman-code)

This page deals with sequence algorithms and string algorithms

## 1. Sequence
This section handles algorithms and data structures related to sequences. I also merged string algorithm in this section, because string is a specific instance of sequence.

### 1.1. Strategies
Two pointer: maintain a subsequence by recording its left pointer and right pointer Both pointers will iteratively get updated while keeping the subsequence to be invariant to a specific property.
Look up your sequence! : sometimes it is helpful to check whether your sequence is a well-known sequence

### 1.2. Subsequence Problems
- Longest Increasing Subsequence (LIS) [c++]: $ O(n^2) $ solution or $ O(nlog(n)) $ solution
- Longest Common Subsequence (LCS) [wiki]: DP solution
- Maximum Subarray Problem: find subarray whose sum is the maximum (kadane)


## 2. String Problems
Find matching patterns in a string. Introduction to algorithm has a chapter of good introduction regarding this topic.

### 2.1. Data Structure

#### 2.1.1. Rope
Normal array might not be efficient in some cases. For example, concatenation takes $O(n)$. Rope represents a string in a balanced tree where each leaf is a immutable string, and each node stores the total length of the left subtree.

It has better performance for some operations such as concatenation $O(log(n))$, but worse performance for indexing $O(log(n))$.

This is usually used to store strings, for example, in editor.

#### 2.1.2. Suffix Array

### 2.2. Matching Problems
**Definition (string matching problem)** Given an string *text* $T[n]$ and another string *pattern* $P[m]$, where $m \leq n$, find all matching shifts with which a given pattern $P$ occurs in a given text.


- Levenshetin distance: edit distance. In the bioinformatics, there is an equivalent algorithm called  Needleman–Wunsch algorithm which maximizes the similarity instead of minimizing distance.

- Rabin-Karp: hash the pattern into an integer (rolling hash), and find whether the hash appears in the string. pay attention to the spurious hits.

- Finite Automata: transforming the pattern into an automata

- KMP: build a transition table. When failing match ith char, transit to match table[i-1]

- Aho-Corasick: the multi-pattern version of KMP: transition table becomes a transition graph on top of Trie. (used in fgrep)

- Boyer-Moore: match pattern from right to left, shift the pattern when mismatched using (1) bad character rule (2) good suffix rule

- Suffix Array

- Manber & Myers: sort suffix array by increasing subsequence by the factor of 2. $O(nlog^2 n)$

### 2.3. Sequence Query Problems
RMQ (Range Minimum Query)
statement: query the minimum element within a given range on a sequence

- segment tree
- dynamic programming
- sparse table
- LCA


## 3. Compression
### 3.1. Huffman Code
prefix code of loss less compression
variable length code
algorithm: recursively merge top two lowest frequent nodes to build the binary tree
LZ77/LZ78


