# 0x412 Unsupervised Learning

- [1. Density Estimation](#1-density-estimation)
    - [1.1. Parametric Density Estimation](#11-parametric-density-estimation)
        - [1.1.1. Beta-Binomial Model](#111-beta-binomial-model)
        - [1.1.2. Dirichlet-Multinomial Model](#112-dirichlet-multinomial-model)
        - [1.1.3. Gaussian Model](#113-gaussian-model)
    - [1.2. Nonparametric Density Estimation](#12-nonparametric-density-estimation)
- [2. Clustering](#2-clustering)

In supervised learning, we are only give input data $X$, without any output. The goal is to discover interesting strucutre in the data.

## 1. Density Estimation
Density estimation is to model the probablisitic distribution $p(x)$ of a random variable $x$, given a finite set $x_1, ..., x_N$ of observations.

In unsupervised learning, we care about the unconditional density estimation $p(x_i; \theta)$, in supervised learning we care about conditional density estimation $p(y_i | x_i; \theta)$

### 1.1. Parametric Density Estimation

#### 1.1.1. Beta-Binomial Model
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


#### 1.1.2. Dirichlet-Multinomial Model

#### 1.1.3. Gaussian Model

### 1.2. Nonparametric Density Estimation

## 2. Clustering