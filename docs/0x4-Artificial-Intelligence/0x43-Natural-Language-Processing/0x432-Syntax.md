# 0x432 Syntax

- [1. Generative Grammar](#1-generative-grammar)
    - [1.1. Transformational Grammar](#11-transformational-grammar)
        - [1.1.1. Standard Theory (1956 - 1965)](#111-standard-theory-1956---1965)
        - [1.1.2. Extended Standard Theory, X-bar theory (1965 - 1973)](#112-extended-standard-theory-x-bar-theory-1965---1973)
        - [1.1.3. Minimalist Program (1990 - )](#113-minimalist-program-1990---)
- [2. Dependency Grammar](#2-dependency-grammar)
- [3. Categorical Grammar](#3-categorical-grammar)
- [4. Constituent Tree Parsing](#4-constituent-tree-parsing)
    - [4.1. CFG](#41-cfg)
    - [4.2. PCFG](#42-pcfg)
        - [4.2.1. Estimation](#421-estimation)
- [5. Parsing](#5-parsing)
    - [5.1. CKY](#51-cky)
        - [5.1.1. Horizontal Expansion](#511-horizontal-expansion)
        - [5.1.2. Vertical Expansion](#512-vertical-expansion)
- [6. Discriminative Rerankings](#6-discriminative-rerankings)


## 1. Generative Grammar
Generative grammar is a small and finite set of rules that can produce a large and potentially infinite number of well-formed structures.

It looks that there are two schools of linguistics:
- Transformational grammar
- Monostratal (non-transformational) grammar

There are some interesting papers about how infants know about syntax, for example, *What infants know about syntax but couldn’t have learned: experimental evidence for syntactic structure at 18 months*

### 1.1. Transformational Grammar

**Definition (deep structure vs surface structure)** Surface structure is the syntactic forms of the outward form, deep structure is the abstract underlying syntactic form.

**Definition (structural ambiguity)** If there are two distinct underlying interpretations that have to be represented differently in deep structure, then it has *structural ambiguity*


#### 1.1.1. Standard Theory (1956 - 1965)
The original model proposed by Chomsky in 1965

#### 1.1.2. Extended Standard Theory, X-bar theory (1965 - 1973)

Grammatical Category

*   tense: present, past
*   number: singular, plural
*   gender: masculine, feminine, neuter
*   voice: passive, applicative
*   valency: number of argument controlled by a verb
*   aspect: progressive, perfect
*   case: nominative, accusative, genitive, dative, ergative, instrumental, absolutive


#### 1.1.3. Minimalist Program (1990 - )

## 2. Dependency Grammar

## 3. Categorical Grammar

## 4. Constituent Tree Parsing

### 4.1. CFG
Ambiguities
coordination ambiguity: CFG cannot enforce agreement in the context. (e.g: koalas eat leaves and (barks))
prepositional phrase attachment ambiguity (e.g: I saw a girl (with a telescope))
Solution is to use PCFG to score all the derivations to encode how plausible they are

### 4.2. PCFG
#### 4.2.1. Estimation
ML Estimation

$$P(X \to \alpha) = \frac{C(X \to \alpha)}{C(X)}$$

smoothing is helpful

## 5. Parsing
### 5.1. CKY

complexity is $O(n^3 |R|)$ where $n$ is the number of words and $|R|$ is the number of rules in the grammar

#### 5.1.1. Horizontal Expansion

#### 5.1.2. Vertical Expansion

## 6. Discriminative Rerankings
generate top-k candidates from the previous parser and rerank them with discriminative reranking might be helpful

Features
Classifiers

