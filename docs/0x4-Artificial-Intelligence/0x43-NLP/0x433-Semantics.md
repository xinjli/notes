# 0x433 Semantics

- [1. Theory](#1-theory)
    - [1.1. Semantic Roles](#11-semantic-roles)
- [2. Information Extraction](#2-information-extraction)
    - [2.1. Relation Extraction](#21-relation-extraction)
    - [2.2. Algorithms](#22-algorithms)
        - [2.2.1. Relation dataset](#221-relation-dataset)
- [3. Dependency Parsing](#3-dependency-parsing)
    - [3.1. Transition-based](#31-transition-based)
    - [3.2. Graph-based](#32-graph-based)

## 1. Theory
### 1.1. Semantic Roles

Semantic roles are roles of entities with respect to the action described by the governing verb

*   **Agent**: entity that performs the action
*   **Patient**: entity that receives the action / affected by the action (state changing)
*   **Theme**: entity described but without state changing

## 2. Information Extraction

### 2.1. Relation Extraction
**Task (Relation Extraction)** Relation Extraction is a task to find an classify semantic relations among the text entities such as: child-of, is-a, part-of and etc.

The text entities can be detected by, for example, name entity recognition.

### 2.2. Algorithms
**Algorithm (Hearst patterns)** The earlist and still common algorithm is using lexico-syntactic pattern matchings, proposed by Hearst in 1992.

The advantage is it has high-precision, but it has low-recall and takes lot of work.

For example, to recognize hyponym/hypernym, we can use the following patterns
$$NP_0 \text{ such as } NP_1$$

implies the following semantics

$$hyponym(NP_1, NP_0)$$

**Algorithm (supervised training)** use whatever classifier you like to. If it is a feature-based classification, the feature can be word feature (bag of words), named entity feature or syntactic feature.

**Algorithm (semi supervised)** Take some known relations and use these to filter more sentences from unlabeled data, then use those new sentences to train classifier and extract relations with high confidence score, and repeat...

#### 2.2.1. Relation dataset

Here is a list of some datasets for relation extraction tasks.
- Wikipedia
- Wordnet
- Freebase
- DBpedia
- TACRED
- SemEval


## 3. Dependency Parsing

### 3.1. Transition-based

### 3.2. Graph-based

# Reference
[1] Jurafsky, Dan. Speech & language processing. Pearson Education India, 2000.