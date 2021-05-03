# 0x410 Foundation

- [1. Decision Theory](#1-decision-theory)
    - [1.1. Frequentist Decision Theory](#11-frequentist-decision-theory)
        - [1.1.1. Bayes Risk](#111-bayes-risk)
        - [1.1.2. Minimax Risk](#112-minimax-risk)
    - [1.2. Bayesian Decision Theory](#12-bayesian-decision-theory)
- [2. Learning Theory](#2-learning-theory)
    - [2.1. PAC](#21-pac)
    - [Rademacher Complexity](#rademacher-complexity)
- [4. Reference](#4-reference)


Machine Learning is to find a function

$$f: X \to Y$$

The task of machine learning can be roughly classified into following groups
- When $Y$ is a float scalar, it is called a regression task
- When $Y$ is an integer scalar, it is called the classification task
- When it is a more complex structure, it is called the structured learning.

## 1. Decision Theory

Mean square error loss is a special case of loss function, the study of the performance of estimators using loss function is a branch of decision theory

### 1.1. Frequentist Decision Theory

**Definition (risk function)** The quality of an estimator is quantified in its risk function wrt estimator $\delta(X)$

$$R(\theta, \delta) = E_{\theta} L(\theta, \delta(X))$$

!!! example "MSE is the risk with square error loss"
    For square error loss, 

    $$L(\theta, a) = (a - \theta)^2$$
    
    the risk function is mean square error (MSE) where 

    $$R(\theta, \delta) = E_{\theta}(\delta - \theta)^2 = \mathrm{Var}_\theta \delta(X) + (\mathrm{Bias} \delta(X))^2$$

For a fixed $\theta$, the risk function is the average loss that will be incurred if the estimator $\delta(x)$ is used. However, since the true $\theta$ is unknown, we would like to use an estimator that has a samll value $R(\theta, \delta)$ for all values of $\theta$

As the optimality will change based on different $\theta$, we have variosu solutions here

#### 1.1.1. Bayes Risk
**Definition (Bayes risk)** In Bayesian analysis wewould use the prior distribution $\pi(\theta)$ to compute an average risk, known as the *Bayes risk*

$$R_{B} (\delta) = \int_{\Theta} R(\theta, \delta) \pi(\theta) d\theta$$

The Bayes estimator or Bayes decision rule is one which minimizes the expected risk:

$$\delta_{B} = \text{argmin}_{\delta} (R_B(\delta))$$

#### 1.1.2. Minimax Risk
An alternative approach is to use minimax risk

**Definition (minimax risk)** The maximum risk of an estimator is

$$R_{max}(\delta) = \max_{\theta} R(\theta, \delta)$$

A minimax rule is one which minimizes the maximum risk

$$\delta_{MM} = \text{argmin}_{\delta} R_{max}(\delta)$$

### 1.2. Bayesian Decision Theory


## 2. Learning Theory

**Definition (input, output space)** We denote by $\mathcal{X}$ the set of all possible examples or instances, which is referred to as the input space. The set of all possible labels or target values is denoted by $\mathcal{Y}$.

**Definition (concept)** A concept is a mapping $c: \mathcal{X} \to \mathcal{Y}$, or equivalently we can identify $c$ with the subset of $\mathcal{X}$ over which it takes the value 1. A concept class is a set of concepts we may wish to learn and denoted by $C$

**Definition (true error, risk)** Given a hypothesis $h \in H$, a target concept $c \in C$ and an underlying distribution $D$, the generalization error or risk of $h$ is defined by

$$R(h) = P_{x \sim D}(h(x) \neq c(x)) E_{x \sim D}[1_{h(x) \neq c(x)}]$$

This error is not directly accessible to the learner scince both the distribution $D$ and target concept $c$ are unknown. However, the learner can measure the empirical error of a hypothesis on the labeled sample $S$

**Definition (empirical error, risk)** Given a hypothesis $h \in H$, a target concept $c \in C$ and a sample $S=(x_1, ..., x_m)$, the empirical error or empirical risk of $h$ is defined by

$$\hat{R}(h) = \frac{1}{m} \sum_{i=1}^m 1_{h(x_i) \neq c(x_9)}$$

There are several relations between the empirical error and the true error, for example

**Definition (PAC learnable)** A concept class $C$ is said to be PAC-learnable if there exists an algorithm $\mathcal{A}$ and a polynomial function $poly$ such that $\forall{\epsilon > 0}, \forall{\delta > 0}$, forall distributions on $\mathcal{X}$ and any target concept $c \in C$, the following holds for any sample size $m \geq poly(1/\epsilon, 1/\sigma, n, size(c))$

$$P_{S \sim D^m}[R(h_S) \leq \epsilon] \geq 1 - \delta$$



### 2.1. PAC
PAC framework helps define the class of learnable concepts in terms of the number of sample points needed to achieve an approximate solution (sample complexity)

In the case of zero training errors, we can bound the true error as follows:

**Theorem (PAC, Haussler)** Suppose a model class has size $H$, dataset has $m$ iid samples, $0 < \epsilon < 1$, for any learned classifier that get 0 training error, the true error is bounded by

$$P(error_{true} > \epsilon) \leq |H| e^{-m\epsilon}$$

PAC bound holds for all $h$ with 0 training error, but does not guarantee the algorithm find the best $h$

By flipping the formula, we know the following relations:

Given $\epsilon, \delta$, yields sample complexity

$$m \geq \frac{\log{|H|} + \log{(1/\delta)}}{\epsilon}$$

Given $m, \delta$ yields error bound

$$\epsilon \geq \frac{\log{|H|} + \log{(1/\delta)}}{m}$$


In the case of non-zero training errors, we can use training error $\hat{\theta}$ to estimate the true error $\theta$. For example, we can use the Hoeffding's bound.

$$P(|\theta - \frac{1}{m}\sum_i x_i| \geq \epsilon) \leq 2e^{-2m\epsilon^2}$$

For a single classifier $h$

$$P(|error_{true}(h) - error_{train}(h)| \geq \epsilon) = \leq 2e^{-2m\epsilon^2}$$

**Theorem (PAC)** For any learned classifier $h \in H$:

$$P(|error_{true}(h) - error_{train}(h)| \geq \epsilon) \leq 2|H|e^{-2m\epsilon^2} \leq \delta$$

With probability $1-\delta$,

$$|error_{true}(h) - error_{train}(h)| \leq \epsilon = \sqrt{\frac{\log{|H|} + \log{2/\delta} }{2m}}$$

### Rademacher Complexity

The Rademacher complexity captures the richness of a family of functions by measuring the degree to which a hypothesis set can fit random noise

**Definition (empirical Rademacher complexity)** Let $G$ be a family of functions mapping from $Z$ to $[a,b]$, $S = (z_1, ..., z_m)$ a fixed sample of size $m$ with elements in $Z$. Then the empirical Rademacher complexity of $G$ with respect to the sample $S$ is defined as

$$\hat{R}_S(G) = E_{\sigma} [\sup_{g \in G} \frac{1}{m} \sum_i \sigma_i g(z_i)]$$

where $\sigma=(\sigma_1, ..., \sigma_m)$ are independent uniform random variable taking values in $\{ -1, +1 \}$. Intuitively, it measures the on average how well the function class $G$ can correlate with random noise on $S$.

**Definition (Rademacher complexity)** Let $D$ denote the distribution according to which samples are drawn. For any integer $m \geq 1$, the Rademacher complexity of $G$ is

$$R_m(G) = E_{S \sim D^m}[\hat{R}_{S}(G)]$$

**Theorem (Rademacher complexity bound)** Let $G$ be a family of functions mapping from $Z$ to $[0,1]$, then for any $\delta > 0$ , with probability at least $1 - \delta$, each of the following holds for all $g \in G$

$$E[g(z)] \leq \frac{1}{m}\sum_i g(z_i) + 2R_m(G) + \sqrt{\frac{\log{1/\delta}}{2m}}$$

and

$$E[g(z)] \leq \frac{1}{m}\sum_i g(z_i) + 2\hat{R}_S(G) + 3 \sqrt{\frac{\log{2/\delta}}{2m}}$$


## 4. Reference
[1] Murphy, Kevin P. Machine learning: a probabilistic perspective. MIT press, 2012.