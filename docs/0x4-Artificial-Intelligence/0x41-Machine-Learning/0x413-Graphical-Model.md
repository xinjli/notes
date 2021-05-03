# 0x413 Graphical Model

## Introduction

The reason to use PGM:

*   without graphical structure, configurations over high dimension will be exponential, which makes it difficult to learn and inference
*   easy to integrate **domain knowledge**
*   easy to integrate **different models**

## Bayesian Network

Bayesian Network is the directed graphical model, it provides a skeleton for representing a joint distribution compactly in a factorized way as follows

$$P(x) = \prod_{v \in V} P(x_v | x_{\text{parent}_v})$$

#### Three types of problems in HMM (BN)

*   **evaluation** problem: Given observations $\mathbf{x}$ and model $\theta$, find its **marginal** probability $P(\mathbf{x}; \theta)$
*   **decoding** problem: Given observations $\mathbf{x}$ and model $\theta$, find the **conditional** probability of latent states $P(\mathbf{y} | \mathbf{x}; \theta)$
*   **learning** problem: Given the observations $\mathbf{x}$, find the model $argmax_\theta P(\theta | \mathbf{x})$

Local Structures and Independencies  

*   **common parent** (B->A, B->C): knowing B decouples A and C
*   **cascade** (A->B->C): knowing B decouples A and C
*   **v-structure** (A->C, B->C): knowing C couples A and B

#### I-map

A graph G is i-map of distribution P if I(G) is a subset of I(P)

#### D-separation

a procedure to check independence between nodes given some other nodes. If those nodes are connected after following steps, they are dependent. Otherwise they are independent at least in bayesian network.

*   build ancestral graph
*   moralize graph
*   remove direction
*   remove conditional nodes

### HMM

## Random Markov Field

undirected graphical model

## Reference

[1] CMU 10-708 ([lecture)](https://sailinglab.github.io/pgm-spring-2019/)