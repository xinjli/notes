# 0x380 Design Pattern

- [1. Foundations](#1-foundations)
    - [1.1. Basic Concepts](#11-basic-concepts)
- [2. Catalogs](#2-catalogs)
        - [2.0.1. Facade](#201-facade)
        - [2.0.2. Iterator](#202-iterator)
- [3. Reference](#3-reference)

## 1. Foundations

### 1.1. Basic Concepts

**SOLID**

*   S: Single-responsiblity principle.
*   O: Open-closed principle.
*   L: Liskov substitution principle.
*   I: Interface segregation principle.
*   D: Dependency Inversion Principle

Composition vs Aggregation

Both are Association

*   Composition: A "owns" B
*   Aggregation: A "uses" B

## 2. Catalogs

#### 2.0.1. Facade

*   hide complex logic by providing an clean interface (just a wrapper?)

#### 2.0.2. Iterator

*   Iterator provides a way to access an aggregate object without exposing internal representations
*   Each Iterator is responsible to maintain the current element
*   Each iterator is associated with its aggregate, so aggregate object should implement Aggregate (Iterable) interface which supports the createIterator

## 3. Reference

[1] Gamma, Erich. _Design patterns: elements of reusable object-oriented software_. Pearson Education India, 1995.