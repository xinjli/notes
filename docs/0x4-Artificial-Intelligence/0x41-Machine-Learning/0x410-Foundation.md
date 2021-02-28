# 0x410 Foundation

- [1. Decision Theory](#1-decision-theory)
- [2. Information Theory](#2-information-theory)
- [3. Models](#3-models)
    - [3.1. Generative Model](#31-generative-model)
    - [3.2. Discriminative Model](#32-discriminative-model)
- [4. Reference](#4-reference)


Machine Learning is to find a function

$$f: X \to Y$$

The task of machine learning can be roughly classified into following groups
- When $Y$ is a float scalar, it is called a regression task
- When $Y$ is an integer scalar, it is called the classification task
- When it is a more complex structure, it is called the structured learning.

## 1. Decision Theory

## 2. Information Theory
Information Theory is concerned with representing daata in a compact fashion, the most important concepts are summarized here

**Definition (entropy)** The entropy of a random variable $X$ with distribution $p$ is

$$H(X) = \sum_{k=1}^K p(X=k) \log_2 p(X=k)$$

**Definition (relative entropy, KL divergence)** One way to measure the dissimilarity of two probability distribution $p, q$ is the Kullback-Leibler divergence (KL divergence) or relative entropy

$$KL(p||q) = \sum_k p_k \log\frac{p_k}{q_k} = -H(p) + H(p, q)$$

**Definition (cross entropy)** $H(p,q)$ is called cross entropy, it is to measure the average number of bits to encode data of distribution $p$ using codebook of distribution $q$, it is defined as

$$H(p, q) = -\sum_k p_k \log q_k$$


**Definition (conditional entropy)** The conditional entropy $H(Y|X)$ is defined as

$$H(Y|X) = \sum_x p(x) H(Y|X=x)$$

**Definition (mutual information)** Mutual information or MI is an approach to estimate how similar the joint distribution $p(X,Y)$ can be factored into $p(X)p(Y)$

$$I(X;Y) = KL(p(X,Y)||p(X)p(Y)) = \sum_x \sum_y p(x,y)\log \frac{p(x,y)}{p(x)p(y)}$$

Obviously, MI is zero iff two random variables are independent.

MI can be expressed using entropy as follows

$$I(X;Y) = H(X) - H(X|Y) = H(Y) - H(Y|X)$$

**Definition (pointwise mutual information)** A related concept is pointwise mutual information or PMI, this is about two events $x,y$

$$PMI(x,y) = \log \frac{p(x,y)}{p(x)p(y)}$$

## 3. Models
The ML probabilistic model can be largely grouped into the following two groups.



### 3.1. Generative Model
Generative Model is to model the joint distribution $P(\textbf{x}, \textbf{y})$. This typically can be broken into modelling of conditional distribution and probability distribution:

- models a class conditional densities $P( \textbf{x} | \mathcal{C}_k)$
- models a prior $P(\mathcal{C}_k)$

With the joint distribution, the prediction task is easily solve with posterior distribution.
- compute posterior $P(\mathcal{C}_k | \textbf{x})$ with Bayes' theorem
  
Generative model tends to be better when training data are limited, but the bound of the asymptotic error is reached more quickly by a  generative model than a discriminative model.

### 3.2. Discriminative Model
The approach of a discriminative model is to model posterior distribution directly $P(\textbf{y} | \textbf{x})$ directly. For example, in the classification task, it is to model  $P(\mathcal{C}_k | \textbf{x})$ directly 

Parameters are typically estimated with MLE. for example, by iterative reweighted least squares (IRLS)

Discriminative model tends to achieve better results with asymptotic classification error (when training data are large enough)

Models that do not have probabilistic interpretation but can learn decision boundary are called discriminant function, these can also be classified as the (nonprobabilistic model) discriminative model. For example, SVM.


## 4. Reference
[1] Murphy, Kevin P. Machine learning: a probabilistic perspective. MIT press, 2012.