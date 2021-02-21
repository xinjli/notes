# 0x434 Translation

- [1. Foundation](#1-foundation)
- [2. Word Model](#2-word-model)
    - [2.1. IBM Model 1](#21-ibm-model-1)
- [3. Phrase Model](#3-phrase-model)
- [4. Neural Model](#4-neural-model)

## 1. Foundation

To get translate a Foreign sentence $f$ into English sentence $\mathbf{e}$. Two fundamental approaches exist.

*   **direct model** $argmax_{\mathbf{e}} P(\mathbf{e} | \mathbf{f})$
*   **noisy channel model** $argmax_{\mathbf{e}} P(\mathbf{f} | \mathbf{e}) P(\mathbf{e})$

## 2. Word Model

Suppose $\mathbf{a}, \mathbf{f}, \mathbf{e}$ denote alignment, Foreign sentence, English sentence respectivelly. Word based model optimize the model $\theta$ with the alignment model (if noisy channel model) as follows

$$P(\mathbf{f} | \mathbf{e}; \theta) = \sum_{\mathbf{a}} P(\mathbf{f}, \mathbf{a} | \mathbf{e}; \theta)$$

### 2.1. IBM Model 1

IBM model 1 is the simplest word model with the assumption that $P(a_j=i | \mathbf{e})$ is constant. It models the joint probability of $\mathbf{a}, \mathbf{f}$ as follows:

$$P(\mathbf{f}, \mathbf{a} | \mathbf{e}; \theta) = \prod_{1 \leq j \leq |\mathbf{f}| } P(f_j | e_{a_j}; \theta) P(a_j | f_j, \mathbf{e}; \theta)$$

The first term on the right side is the emission probability, the second term is the alignment probability. The alignment probability $P(a_j | f_j, \mathbf{e}; \theta)$ can be further decomposed as follows. The alignment is estimated in the expectation step.

$$P(a_j=i | f_j, \mathbf{e}; \theta) = \frac{P(a_j; \theta) P(f_j| a_j=i, \mathbf{e}; \theta)}{\sum_k P(a_j=k; \theta) P(f_j| a_j=k, \mathbf{e}; \theta)}$$

$$P(a_j=i | f_j, \mathbf{e}; \theta) = \frac{P(f_j | e_i; \theta)}{\sum_k P(f_j| e_k; \theta)}$$

The translation model is optimized in the maximization step

$$P(f_j | e_i; \theta) = \frac{P(a_j=i | \mathbf{e}, \mathbf{f})}{\sum_k P(a_k=i | \mathbf{e}, \mathbf{f})}$$

## 3. Phrase Model

## 4. Neural Model