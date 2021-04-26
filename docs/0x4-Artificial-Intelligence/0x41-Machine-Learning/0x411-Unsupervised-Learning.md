# 0x412 Unsupervised Learning

- [1. Parametric Density Estimation](#1-parametric-density-estimation)
    - [1.1. Beta-Binomial Model](#11-beta-binomial-model)
    - [1.2. Dirichlet-Multinomial Model](#12-dirichlet-multinomial-model)
    - [1.3. Gaussian Model](#13-gaussian-model)
        - [1.3.1. MLE Point Estimate](#131-mle-point-estimate)
        - [1.3.2. Bayes Estimate](#132-bayes-estimate)
- [2. Nonparametric Density Estimation](#2-nonparametric-density-estimation)
- [3. Clustering](#3-clustering)
    - [3.1. Partitional Clustering](#31-partitional-clustering)
        - [3.1.1. Spectral Clustering](#311-spectral-clustering)
    - [3.2. Hierarchical Clustering](#32-hierarchical-clustering)
- [4. Reference](#4-reference)

In supervised learning, we are only give input data $X$, without any output. The goal is to discover interesting strucutre in the data.

## 1. Parametric Density Estimation
Density estimation is to model the probablisitic distribution $p(x)$ of a random variable $x$, given a finite set $x_1, ..., x_N$ of observations.

In unsupervised learning, we care about the unconditional density estimation $p(x_i; \theta)$, in supervised learning we care about conditional density estimation $p(y_i | x_i; \theta)$

### 1.1. Beta-Binomial Model
Suppose we want to model a binary random variable $X \in \{ 0, 1 \}$ with Bernoulli distribution

Given the sample $\mathcal{D}=\{X_1, ..., X_n \}$, we know the likelihood can be written as

$$p(\mathcal{D}|\mu) = \prod_n \mu^{X_n}(1-\mu)^{1-X_n}$$

The ML estimator is 

$$\hat{\mu}_{ML} = \frac{m}{N}$$

where $m = \sum_n X_i$ is the sufficient statistics.

The conjugate of Bernoulli/Binomial distribution is the Beta distribution, recall its pdf form is

$$B(\mu | a,b) = \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} \mu^{a-1}(1-\mu)^{b-1}$$

It has the same shape of $\mu^X (1-\mu)^{1-X}$, therefore can serve as the prior and posterior.

The posterior has the form

$$\mu(\mu | m, l, a, b) \propto \mu^{m+a-1}(1-\mu)^{l+b-1}$$

Using the properties of beta distributions, we know the MAP estimator is

$$\hat{\mu}_{MAP} = \frac{m+a-1}{N+a+b-2}$$

however, be careful that posterior mean is different

$$\bar{\mu} = \frac{m+a}{N+a+b}$$

If our goal is to predict the outcome of the next trial, we can

$$p(x=1 | \mathcal{D}) = \int_0^1 p(x=1|\mu)p(\mu|\mathcal{D}) d\mu = E[\mu | \mathcal{D}] = \bar{\mu}$$


### 1.2. Dirichlet-Multinomial Model

### 1.3. Gaussian Model

#### 1.3.1. MLE Point Estimate
Maximum Likelihood Estimation on a dataset $(x_1, ..., x_n)$ is 

$$\hat{\mu}_{ML} = \frac{1}{n} \sum_{i=1}^n x_n$$

$$\hat{\Sigma}_{ML} = \frac{1}{n} \sum_{i=1}^n (x_n - \hat{\mu}_{ML})(x_n - \hat{\mu}_{ML})^T$$

To prove the second line, we can apply the following derivative rules to the precision matrix
$$\frac{\partial}{\partial A} \log |A| = A^-T$$
$$tr(ABC)=tr(CAB)=tr(BCA)$$

This MLE can be applied to, for example, Gaussian discriminant analysis where each class has a generative Gaussian distribution.


#### 1.3.2. Bayes Estimate
Conjugate distribution of $\mu$ is normal distribution. Suppose the prior distribution of $\mu$ is $\mathcal{N}(\mu_0, \sigma^2_0)$, then the posterior distribution is

$$p(\mu | x) = \mathcal{N}(\mu_N, \sigma^2_N)$$

where

$$\mu_N = \frac{\sigma^2}{N\sigma^2_0 + \sigma^2} \mu_0 + \frac{N \sigma^2_0}{N\sigma^2_0 + \sigma^2} \mu_{ML}$$

$$\frac{1}{\sigma^2_N} = \frac{1}{\sigma^2_0} + \frac{N}{\sigma^2}$$

Conjugate distribution of precision $\lambda$ is Gamma distribution. Suppose the prior distribution is Gamma distribution with $(a,b)$ hyperparameter, then posterior Gamma distribution is 

$$a_N = a_0 + \frac{N}{2}$$

$$b_N = b_0 + \frac{N}{2}\sigma^2_{ML}$$

The multivariate version is the Wishart distribution

Conjugate distribution of $\sigma$ is inverse-Gamma distribution

Conjugate distribution of both mean and precision is called normal gamma distribution

## 2. Nonparametric Density Estimation

## 3. Clustering
Clustering is the process of grouping similar objects together. 

There are two kinds of inputs we might use

- **similarity based clustering**: the input to the algorithm is an $N \times N$ distance matrix or dissimilarity matrix matrix $D$
- **feature-based clustering**: the input is an $N \times D$ feature matrix or design matrix $X$.

There are also two kinds of outputs we might expect:

- **flat clustering (partitional clustering)**: we partition the objects into disjoint sets
- **hierarchical clustering**: we create a nested tree of partitions


### 3.1. Partitional Clustering

#### 3.1.1. Spectral Clustering
Spectral clustering make uses of spectrum of the similarity matrix to perform dimension reduction before clustering in fewer dimension. In application to image segmentation, spectral clustering is known as segmentation-based object categorization.


This [tutorial](https://people.csail.mit.edu/dsontag/courses/ml14/notes/Luxburg07_tutorial_spectral_clustering.pdf) has the full treatment of this topic.

The basic idea of spectral clustering is to use **graph cuts**: find $K$ disjoint nodes whose interconnections have small weights. If we want to find a partition into $K$ clusterings

$$cut(A_1, ..., A_k) = \frac{1}{2} \sum_k W(A_k, V \setminus A_k)$$

where $W(A,B) = \sum_{i \in A, j \in B} w_{ij}$

Unfortunately, this often partitions off a single data point from the rest. To ensure the sets are reasonably large, we use the *normalized cut* as the objective

$$Ncut(A_1, ..., A_k) = \frac{1}{2} \sum_k \frac{W(A_k, V \setminus A_k)}{vol(A_k)}$$

where $vol(A) = \sum_{i \in A} d_i$

To find the optimal assignment binary vector $c = [c_1, ..., c_K]$, however, is NP-hard. We can relax the binary to be real-value and solves it as an eigenvector problem.

We first create a sparse matrix $W$ from the similarity matrix $S$ by

- only keeping edge whose distance is less than $\epsilon$
- for each vertex, only keeping the $K$ nearest neighbor connections

Then we create the Graph Laplacian $L$

$$L = D - W$$

There are a couple of important properties of Graph Laplacian, most importantly

**Proposition (Number of connected components and the spectrum of L)** Let $G$ be an undirected graph with non-negative weights. Then the multiplicity $k$ of the eigenvalue 0 of $L$ equals the
number of connected components $A_1,...,A_k$ in the graph. The eigenspace of eigenvalue 0 is spanned
by the indicator vectors $\mathbf{1}_{A_1} ,..., \mathbf{1}_{A_k}$ of those components

This suggests the following algorithm

```text
Input: Similarity matrix S \in R^{n x n}, number of k cluster
- Construct the weighted adjacency matrix W from S
- compute the Graph Laplacian L
- compute the k eigenvectors (corresponding to the k smallest eigenvalues) u_1, ..., u_k
- Let U = [u_1, ..., u_k] be a new feature matrix where each row y_i \in R^k is the feature for point i
- run k-means on the new feature matrix and fine the k clusters
```

There are two normalized version of Graph Laplacian

The symmetric matrix

$$L_{sym} = D^{-1/2}LD^{-1/2} = I - D^{-1/2}WD^{-1/2}$$

The random matrix

$$L_{rw} = D^{-1}L = I - D^{-1}W$$

Both are highly related to the original problem and can be solved using similar approaches.


### 3.2. Hierarchical Clustering

## 4. Reference