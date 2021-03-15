# 0x300 Computation

- [1. Regular Languages (Type 3)](#1-regular-languages-type-3)
    - [1.1. Finite Automaton](#11-finite-automaton)
    - [1.2. Deterministic Finite Automaton](#12-deterministic-finite-automaton)
    - [1.3. Nondeterministic Finite Automaton](#13-nondeterministic-finite-automaton)
    - [1.4. Finite State Transducer](#14-finite-state-transducer)
    - [1.5. Regular Expression](#15-regular-expression)
- [2. Context Free Languages (Type 2)](#2-context-free-languages-type-2)
    - [2.1. Context Free Grammar](#21-context-free-grammar)
    - [2.2. Chomsky Normal Form (CNF)](#22-chomsky-normal-form-cnf)
    - [2.3. Pushdown Automaton](#23-pushdown-automaton)
- [3. Context-Sensitive Languages (Type 1)](#3-context-sensitive-languages-type-1)
- [4. Recursive Languages (Type 0)](#4-recursive-languages-type-0)
    - [4.1. Turing Machine](#41-turing-machine)
    - [4.2. Recursive Function](#42-recursive-function)
    - [4.3. Lambda Calculus](#43-lambda-calculus)
- [5. Computability](#5-computability)
- [6. Reference](#6-reference)

This note is arranged based on the Chomsky hierarchy from Type 3 to Type 0.

Note that all models here have access to some memory (limited or not), these are all models of sequential logic. An even model low-level model is the combinational logic, which is the pure function of the input and it has no access to any memory

**Definition (alphabet)** Alphabet are defined as a finite set of symbols. e.g: $\Sigma = \{ 0, 1 \}, \Sigma = \{ A,B, ..., Z \}$

**Definition (string)** A string is a finite sequence of symbols from some alphabet. e.g: $0101010$ from $\Sigma = \{ 0, 1 \}$

**Definition (language)** A language is a set of string chosen from some $\Sigma^*$

**Definition (grammar)** A grammar is a set of rules defining the syntax of a specific language

**Definition (recognition)** We say that a model $M$ recognizes language $A$ if

$$A = \{ w | M \text{ accepts } w \}$$

**Definition (model of computation)** a model of computation is a model which describes how a set of outputs are computed given a set of inputs 

In my personal understanding, it is just the f part of a general $y=f(x)$

Personally, I think model of computation (or formal language) is IDL of abstract machines.

There are mainly three models of computation: regular languages, CFG and Turing Machine.

The difference of three models can be characterized by their memory usage

- regular language: limited memory
- CFG: unlimited stack-like memory (restricted)
- Turing Machine: unlimited random access memory (unrestricted)

![Computation](../../img/computation.png)

## 1. Regular Languages (Type 3)

**Definition (regular language)** A language is called a regular language is some FA recognizes it

**Lemma (closed operations)** The regular languages are closed under following operations
- (union) If $A_1, A_2$ are regular languages, then $A_1 \cup A_2$ is regular
- (intersection) If $A_1, A_2$ are regular languages, then $A_1 \cap A_2$ is regular
- (concatenation) If $A_1, A_2$ are regular languages, then $A_1 \circ A_2$ is regular

The proof is easy by using NFA formulation.

Regular languages can be expressed by three different formulation: finite automaton, nondeterministic finite automaton and regular expression. They are all equivalent.

### 1.1. Finite Automaton
The automaton computes a function that maps string into the set ${0,1}$ (i.e. acceptance or not)

### 1.2. Deterministic Finite Automaton
**Definition (finite automaton)** A finite automaton is a 5-tuple $(Q, \Sigma, \delta, q_0, F) $

- $Q$ is a finite set called the states
- $\Sigma$ is a finite set called alphabet
- $\delta: Q \times \Sigma \rightarrow Q$ is the transition function
- $q_0 \in Q$ is the start state
- $F \subseteq Q $ is the set of accept states
  
Interface:
- input: a string of alphabet
- output: Accept or Reject  (I prefer to understanding the output as a 1/0 bit)
  
If $A$ is the set of all strings that FA $M$ accepts, then $A$ is the language of machine $M$, which means $L(M)=A$


### 1.3. Nondeterministic Finite Automaton
**Definition (nondeterministic finite automaton)** A nondeterministic finite automaton (NFA) is a 5-tuple $(Q, \Sigma, \delta, q_0, F)$

- $Q$ is a finite set of states
- $\Sigma$ is a finite alphabet
- $\delta: Q \times \Sigma_{\epsilon} \to \mathcal{P}(Q)$ is the transition function
- $q_0 \in Q$ is the start start
- $F \subseteq Q$ is the set of accept states

**Theorem (equivalence between DFA and NFA)** The two machines are equivalent (they are recognizing the same language)

Proof outline: Every DFA is a special case of NFA, so DFA -> NFA is obvious. To prove the other direction (NFA -> DFA), we can construct a NFA from DFA by consider the power set of states and assign deterministic transition based on NFA transitions.

Thus NFA gives an alternative way of characterizing the regular language.

**Corollary (NFA and regular language)** A language is regular iff some NFA recognizes it.



### 1.4. Finite State Transducer
FST accept pairs of strings

**Definition (finite state transducer)** A finite state transducer is a tuple of

- $Q$ is a finite set of states
- $\Sigma$ is a finite set of input alphabet
- $\Gamma$ is a finite set of output alphabet
- $I \subset Q$ is the set of initial states
- $F \subset Q$ is the final states
- $\epsilon \subseteq Q \times (\Sigma \cup \{ \lambda \}) \times (\Gamma \cup \{ \lambda \} ) \times Q$ is the transition relation
  
**Definition (regular relations)** A generalization (tuple) of regular languages.

- the empty set and all $(x, y)$ where $x \in \Sigma, y \in \Gamma$
- $R_1 \circ R_2$ where $R_1, R_2$ are regular relation
- $R_1 \cup R_2$ where $R_1, R_2$ are regular relation
- $R^* = \cup_{i=0}^{\infty} R_i$
  

### 1.5. Regular Expression
We can use the regular operations to build up expressions describing languages, which are called regular expressions. e.g.: $(0 \cup 1)0^*$

We can define regular expression inductively as follows:
**Definition (regular expression)** $R$ is said to be a regular expression if $R$ is

- $a$ for some $a$ in the alphabet $\Sigma$
- $\epsilon$
- $\emptyset$
- $(R_1 \cap R_2)$
- $(R_1 \circ R_2)$
- $(R_1^*)$

Note that the value of a regular expression is a language.

Regular expression is useful, for example, to implement lexical analysis rule in compiler.

## 2. Context Free Languages (Type 2)
Context Free languages is a more expressive language collection than regular languages. It can be used for natural language parsing and compiler.

Note that the name of context-free is because subtree node is not affected by its surrounding context (On the other hand, context-sensitive languages are affected by contexts $\alpha, \beta$ as in the following section)

The models of CFL is a computation model with un-limited memory but with limited manner of using memory.

### 2.1. Context Free Grammar
**Definition (context-free grammar)** A context free grammar is a 4-tuple $(V, \Sigma, R, S)$ where

$V$ is a finite set of variables
$\Sigma$ is a finite set, disjoint from $V$, called the terminals
$R$ is a finite set of rules, with each rule being a variable and a string of variables and terminals
$S \in V$ is the start variable

### 2.2. Chomsky Normal Form (CNF)
Any context free grammar can be converted to an equivalent CNF

Unary rule $C \to x$
Binary rule $ C \to C_1 C_2$
How to transform: binarization

### 2.3. Pushdown Automaton

## 3. Context-Sensitive Languages (Type 1)
Grammar
$$\alpha A \beta \to \alpha \gamma \beta$$

## 4. Recursive Languages (Type 0)
The recursive languages have three different formulations: Turing machine, recursive function and lambda calculus, which is proved by the Church-Turing thesis.

### 4.1. Turing Machine
**Definition (recognizable)** A language is called recognizable (or Recursive Enumerable) if some Turing machine recognizes it.

Any string in the language will be accepted by the TM
Any other string will not be accepted (halting OR rejected)
**Definition (decidable)** A language is called decidable (or Recursive) if some Turing machine decides it

- Any string in the language will be accepted by the TM
- Any other string will not be rejected
  
**Definition (Universal Turing Machine)** Universal turing machine is a machine that can simulate any other Turing Machine.

### 4.2. Recursive Function

### 4.3. Lambda Calculus

## 5. Computability
The cardinality of all possible languages is continuum, and the cardinality of language recognizable by Turing Machine is countable. Therefore, there are languages that are not recognizable by TM.

**Decision problem**: whether TM can decide a language by answering yes or no without looping. The following are some famous undecidable problems.

**Entscheidungsproblem**: the decision problem in first-order logic. Proven undecidable by Church-Turing Thesis.
**Hilbert's 10th problem**: the decision problem of Diophantine equations which have integer roots. Proven undecidable.

**Halting problem**: the decision problem of deciding whether a TM will halt. Proven undecidable by Turing. (proof: by easy contradiction)


## 6. Reference
[1] Sipser, Michael. "Introduction to the Theory of Computation." ACM Sigact News 27.1 (1996): 27-29.

