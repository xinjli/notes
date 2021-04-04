# 0x301 Complexity

- [Asymptotic Analysis](#asymptotic-analysis)
- [1. Time Complexity](#1-time-complexity)
- [2. Space Complexity](#2-space-complexity)
- [3. Quantum Complexity](#3-quantum-complexity)

Complexity zoo has a good explanation for each of the complexity classes.

![complexity](../../img/complexity.svg)

## Asymptotic Analysis

**Definition ($\Theta$-notation)** For a given function $g(n)$, we denote by $\Theta(g(n))$ the set of functions

$$\Theta(g(n)) = \{ f(n) | (\exists{c_1, c_2, n_0 > 0 })(\forall{n \geq n_0}) 0 \leq c_1 g(n) \leq f(n) \leq c_2g(n) \}$$

We say that $g(n)$ is an asymptotically tight bound for $f(n)$, it bounds the function from above and below

**Definition (O-notation)** For a given function $g(n)$, we denote by $O(g(n))$ the set of functions

$$O(g(n)) = \{ f(n) | (\exists{c, n_0 > 0})(\forall{n \geq n_0}) 0 \leq f(n) \leq cg(n) \}$$

This is an asymptotic upper bound.

**Definition ($\Omega$-notation)** For a given function $g(n)$, we denote by $\Omega(g(n))$ the set of functions

$$\Omega(g(n)) = \{ (\exists{c, n_0 > 0})(\forall{n \geq n_0}) 0 \leq cg(n) \leq f(n) \}$$

This is an asymptotic lower bound.

**Theorem (notation relations)** For any two functions $f(n), g(n)$, we have

$$f(n) = \Theta(g(n)) \text{ iff } f(n) = O(g(n)), f(n) = \Omega(g(n))$$

## 1. Time Complexity

**Definition (time complexity)** Let $M$ be a deterministic Turing machine that halts on all inputs. The time complexity of $M$ is the function $f: \mathcal{N} \to \mathcal{N}$ where $f(n)$ is the max number of steps that $M$ uses on any input of length $n$

*   **P**: decidable in polynomial times
*   **NP**: verifiable in polynomial times
*   **co-NP**: complement is NP
*   **NP-complete**: A NP problem is NP-complete if any NP can be reduced to this problem in polynomial times
*   **NP-hard**: A problem <g class="gr_ gr_175 gr-alert gr_spell gr_inline_cards gr_disable_anim_appear ContextualSpelling ins-del" id="175" data-gr-id="175">if</g> NP-hard if any NP can be reduced to this problem in polynomial times
*   **EXPTIME**: decidable in exponential time

Theorems:

*   **Cook-Levin**: Any NP problems can be reduced in polynomial times to Boolean satisfiability problem (Boolean satisfiability is NP-complete)

## 2. Space Complexity

Definitions

*   **PSPACE**: decidable using polynomial space
*   **NPSPACE**: verifiable in polynomial space

Theorems:

*   **Savitch**: NPSPACE can be reduced to PSPACE (with square space complexity bound)

## 3. Quantum Complexity

Definitions

*   **BQP**: decidable by quantum computer in polynomial time within 1/3 error probability.