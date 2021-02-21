# 0x313 Sort & Search

- [1. Sort](#1-sort)
    - [1.1. TimSort](#11-timsort)
- [2. Hash](#2-hash)
    - [2.1. Hash Function](#21-hash-function)
    - [2.2. Open Addressing Hash Scheme](#22-open-addressing-hash-scheme)
    - [2.3. Dynamic Rehashing](#23-dynamic-rehashing)

## 1. Sort

### 1.1. TimSort
First implemented in 2002 by Tim Peters for use in Python
- insertion sort for every fixed length block
- merge blocks by merge sort

## 2. Hash
This section will only cover non-crypto hash

### 2.1. Hash Function
- MurmurHash
- Google CityHash
- Google FarmHash
- CLHash
- FNV hash: 34bit to 1024bit, simple and fast, one round of FNA-1 consists of only prime multiplication and xor


### 2.2. Open Addressing Hash Scheme
- Linear Probe Hashing: resolve collisions by linearly searching for the next free slot
- Robin Hood Hashing: variant of linear probe hashing. Allow poor keys to steal position from rich keys. try to reduce the std of probing.
- Cuckoo Hashing: prepare two hash tables

### 2.3. Dynamic Rehashing
Extendible Hashing: use trie to identify the hash table. Split the trie node if its hash table is full, in this case only rehash of this node table rather than all entire tables is required.
- Linear Hashing: split bucket iteratively whenever an overflow detected
