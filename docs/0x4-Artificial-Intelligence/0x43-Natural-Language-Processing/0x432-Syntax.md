# 0x432 Syntax

- [1. Theory](#1-theory)
    - [1.1. X-bar theory](#11-x-bar-theory)
        - [1.1.1. Grammatical Category](#111-grammatical-category)
- [2. Generative Grammar](#2-generative-grammar)
- [3. Dependency Grammar](#3-dependency-grammar)
- [4. Categorical Grammar](#4-categorical-grammar)
- [5. Constituent Tree Parsing](#5-constituent-tree-parsing)
    - [5.1. CFG](#51-cfg)
    - [5.2. PCFG](#52-pcfg)
        - [5.2.1. Estimation](#521-estimation)
- [6. Parsing](#6-parsing)
    - [6.1. CKY](#61-cky)
        - [6.1.1. Horizontal Expansion](#611-horizontal-expansion)
        - [6.1.2. Vertical Expansion](#612-vertical-expansion)
- [7. Discriminative Rerankings](#7-discriminative-rerankings)

## 1. Theory

word changes forms depending on other words to which it is related.

### 1.1. X-bar theory

#### 1.1.1. Grammatical Category

*   tense: present, past
*   number: singular, plural
*   gender: masculine, feminine, neuter
*   voice: passive, applicative
*   valency: number of argument controlled by a verb
*   aspect: progressive, perfect
*   case: nominative, accusative, genitive, dative, ergative, instrumental, absolutive

## 2. Generative Grammar

## 3. Dependency Grammar

## 4. Categorical Grammar

## 5. Constituent Tree Parsing

### 5.1. CFG
Ambiguities
coordination ambiguity: CFG cannot enforce agreement in the context. (e.g: koalas eat leaves and (barks))
prepositional phrase attachment ambiguity (e.g: I saw a girl (with a telescope))
Solution is to use PCFG to score all the derivations to encode how plausible they are

### 5.2. PCFG
#### 5.2.1. Estimation
ML Estimation

$$P(X \to \alpha) = \frac{C(X \to \alpha)}{C(X)}$$

smoothing is helpful

## 6. Parsing
### 6.1. CKY

complexity is $O(n^3 |R|)$ where $n$ is the number of words and $|R|$ is the number of rules in the grammar

#### 6.1.1. Horizontal Expansion

#### 6.1.2. Vertical Expansion

## 7. Discriminative Rerankings
generate top-k candidates from the previous parser and rerank them with discriminative reranking might be helpful

Features
Classifiers

