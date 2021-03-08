# 0x421 Supervised Learning

- [1. Simple Generative Model](#1-simple-generative-model)
    - [1.1. Simple Discrete Model](#11-simple-discrete-model)
        - [1.1.1. Beta-Binomial Model](#111-beta-binomial-model)
        - [1.1.2. Dirichlet-Multinomial Model](#112-dirichlet-multinomial-model)
        - [1.1.3. Multinoulli Naive Bayes Model](#113-multinoulli-naive-bayes-model)
    - [1.2. Simple Continuous Model](#12-simple-continuous-model)
        - [1.2.1. Gaussian Model](#121-gaussian-model)
        - [1.2.2. Gaussian Discriminant Analysis](#122-gaussian-discriminant-analysis)
            - [1.2.2.1. Quadratic Discriminant Analysis](#1221-quadratic-discriminant-analysis)
            - [1.2.2.2. Gaussian Naive Bayes](#1222-gaussian-naive-bayes)
            - [1.2.2.3. Linear Discriminative Analysis (LDA)](#1223-linear-discriminative-analysis-lda)
        - [1.2.3. GMM](#123-gmm)
- [2. Linear Regression Model](#2-linear-regression-model)
    - [2.1. Frequentist Linear Regression](#21-frequentist-linear-regression)
        - [2.1.1. MLE](#211-mle)
        - [2.1.2. Ridge Regression](#212-ridge-regression)
        - [2.1.3. Lasso](#213-lasso)
    - [2.2. Bayesian Linear Regression](#22-bayesian-linear-regression)
- [3. Linear Classification Model](#3-linear-classification-model)
    - [3.1. Discriminant Functions](#31-discriminant-functions)
        - [3.1.1. Fisher's Linear Discriminant](#311-fishers-linear-discriminant)
        - [3.1.2. The perceptron algorithm](#312-the-perceptron-algorithm)
    - [3.2. Generative Model](#32-generative-model)
        - [3.2.1. Naive Bayes](#321-naive-bayes)
        - [3.2.2. Linear Discrimative Analysis](#322-linear-discrimative-analysis)
    - [3.3. Discriminative Model](#33-discriminative-model)
        - [3.3.1. Max Entropy](#331-max-entropy)
- [4. Kernel Model](#4-kernel-model)
- [5. Tree Model](#5-tree-model)
    - [5.1. CART (Classification and Regression Tree)](#51-cart-classification-and-regression-tree)
        - [5.1.1. ID3](#511-id3)
        - [5.1.2. C4.5, C5](#512-c45-c5)
    - [5.2. Ensemble](#52-ensemble)
        - [5.2.1. Boosted](#521-boosted)
        - [5.2.2. Bootstrap Aggregation (Bagging)](#522-bootstrap-aggregation-bagging)
- [6. Sequential Model](#6-sequential-model)
    - [6.1. Markov Model](#61-markov-model)
- [7. Reference](#7-reference)

## 1. Simple Generative Model
Probably the most simple model for supervised learning is to just fit a single parametric distribution to the data, this is much simpler than linear models and nonlinear models.

For a single class, we simply model $p(x)$ with a simple parameteric distribution, for multiple class, we model it with

$$p(x, y; \theta) = p(y; \theta)p(x|y; \theta)$$

where $y$ is a class, and $x$ might be discrete or continuous.

These generative models can be used, for example, classification tasks by modeling generative distribution for each class.

### 1.1. Simple Discrete Model
Fit a parametric discrete model

#### 1.1.1. Beta-Binomial Model

#### 1.1.2. Dirichlet-Multinomial Model

#### 1.1.3. Multinoulli Naive Bayes Model
If there are multiple features, one simple model is the Naive Bayes model, assuming cfeatures are conditionally independent given the class label.

 This writes the class conditional density of one-dimensional density

$$p(x | y=c; \theta) = \prod_i p(x_i | y=c; \theta_{i})$$

The parameters of NB model is small $O(CD)$ where $C$ is the number of class, $D$ is the number of feature, so relatively immune to overfitting.


### 1.2. Simple Continuous Model
Fit a parametric continous model

#### 1.2.1. Gaussian Model

#### 1.2.2. Gaussian Discriminant Analysis
This looks to be a bad naming, it is actually a generative classifier.

It fits the Gaussian distribution for each class conditional distribution

$$p(x | y=c; \theta) = N(x | \mu_c, \Sigma_c)$$

##### 1.2.2.1. Quadratic Discriminant Analysis 
The most general form is to assume Gaussian distribution without any contraints on $\mu_c, \Sigma_c$

$$p(y=c | x; \theta) = \frac{\pi_i N(x|\mu_c, \Sigma_c)}{\sum_{c'} \pi_i N(x|\mu_{c'}, \Sigma_{c'})}$$

This will produce quadratic decision boundary (as its name indicates).

Gaussian Naive Bayes and Linear Discrimnative Analysis are two special forms of QDA.

##### 1.2.2.2. Gaussian Naive Bayes
Gaussian Naive Bayes assumes conditional independence, therefore the off-diagnoal entry of $\Sigma_c$ will be zero, therefore $\Sigma_c$ is contrained to be diagonal matrix.

Note that this still can produce quadratic decision boundary. It will produce linear boundary when variance are tied. 

##### 1.2.2.3. Linear Discriminative Analysis (LDA)
LDA are using the same covariance matrix.

$$\Sigma_c = \Sigma$$

This produces the linear decision boundary.

#### 1.2.3. GMM

## 2. Linear Regression Model
Linear regression is a probablistic discrminative model. Its conditiona probability is expressed by

$$p(y|x; \theta) = \mathcal{N}(w^Tx, \sigma^2)$$

### 2.1. Frequentist Linear Regression
#### 2.1.1. MLE
The target variable $t$ can be modeled as follows:

$$p(t|x, w, \beta) = \mathcal{N}(t|y(x, w), \beta^{-1})$$

The log likelihood function wrt $w$ can be written as

$$\mathcal{l}(w) = \sum_i \log \mathcal{N}(t_i | w^T x_i, \beta^{-1})$$

The MLE is to minimize the following formula

$$\frac{1}{2} \sum_i (t_i - w^T x_i)^2$$

In the matrix form, this is equivalent to the following convex function (this is convex because the twice derivative $w^Tw$ is positive semidefinite)

$$\frac{1}{2}(xw - t)^T (xw - t) = \frac{1}{2}w^T x^Tx w - w^Tx^Tt$$

To minimize this convex function, take the derivative to 0 gives the following solution

$$(x^Tx) w = x^T t$$

which is known as the normal equation.

#### 2.1.2. Ridge Regression

#### 2.1.3. Lasso

### 2.2. Bayesian Linear Regression
In a full Bayesian treatment, the parameter $w$ has a distribution, the conjugate prior of the likelihood can be given as follows (if variance is known)

$$p(w) = \mathcal{N}(m_0, S_0)$$

## 3. Linear Classification Model
The goal of classification is to take an input vector $\textbf{x}$ and assigned it to one of $K$ discrete classes $\mathcal{C_k}$

### 3.1. Discriminant Functions
In the case of two classes, we assign to $C_1$ if $y \geq 0$, otherwise $C_0$

$$y(\textbf{x}) = \textbf{w}^T x + w_0$$

the decision boundary is $y = 0$

In the case of multiclasses, we create a single $K$-class discriminant comprising $K$ linear functions of the form

$$y_k(\mathbf{x}) = \mathbf{w}_k^T \mathbf{x} + w_{k0}$$

where we assgin a point $\mathbf{x}$ to $\mathcal{C}_k$ if $(\forall j \neq k) y_k(\mathbf{x}) > y_j(\mathbf{x})$

The decision regions are connected and convex

The following are three solutions

Least squares for classification
has the closed-form but lack robustness to outliers

#### 3.1.1. Fisher's Linear Discriminant
#### 3.1.2. The perceptron algorithm
Proposed by Rosenblatt [1]. Minsky's work analyzes perceptron [2]. When linear sepratable, perceptron converges in finite steps, upper-bounded by $\frac{R^2}{\gamma^2}$ where $R$ is the upper-bound of norm of training set $x$, and $\gamma$ is the learning rate.  [proof](https://www.cse.iitb.ac.in/~shivaram/teaching/old/cs344+386-s2017/resources/classnote-1.pdf)


### 3.2. Generative Model
The general Gaussian Discriminative Analysis (GDA) is to model the class conditional densities with multivariate Gaussian distribution

$$p(x | \mathcal{C}_k) = \mathcal{N}(x|\mu_k, \Sigma_k)$$

If there is no assumption about the $\Sigma_k$, then it is known as quadratic discriminant analysis (QDA), which is literally a quadratic classifier (because of $\Sigma$)

GDA has two simplifications: Naive Bayes and Linear Discriminative Analysis.

#### 3.2.1. Naive Bayes
If the $\Sigma_k$ is diagonal, this is equivalent to the Naive Bayes classifier.

Naive bayes is based on the assumption that features $\mathbf{x}$ are mutually independent given the output $\mathcal{C}_k$. The joint probability distribution is modeled as follows

$$p(\mathcal{C}_k, x_1, x_2, ..., x_n) = \mathcal{C_k} \prod_i p(x_i|\mathcal{C}_k)$$

#### 3.2.2. Linear Discrimative Analysis
When $\Sigma_k$ in GDA are shared or tied across all classes (i.e.: $\Sigma_k = \Sigma$), then it is known as the linear discrimative analysis (LDA)
$$p(\mathcal{C}_k | x) \propto \exp (\mu_c^T \Sigma^{-1} x -\frac{1}{2} \mu_c^T \Sigma^{-1} \mu_c + \log \pi_c)$$

It is called linear because the exponent can be expressed in linear with respect to $x$

LDA can be solved analytically with MLE

$$pi_k = \frac{1}{N} \sum_i 1\{ y_i = k \}$$

$$\mu_k = \frac{1}{N} \sum_i 1\{ y_i=k \} x_i$$

$$\Sigma = \frac{1}{N} \sum_i (x_i - \mu_{y_i})(x_i - \mu_{y_i})^T$$

### 3.3. Discriminative Model
Advantage of discrminative models is that it has fewer adaptive parameters which may lead to improved predictive performance

#### 3.3.1. Max Entropy
maximize the entropy of joint distribution $H(X) = -\sum p(x,y)\log(p(x,y))$ with the feature constraint of $E_p f_j = E_{p^{~}} f_j$

[Tutorial](https://web.stanford.edu/class/cs124/lec/Maximum_Entropy_Classifiers.pdf)

## 4. Kernel Model

## 5. Tree Model
### 5.1. CART (Classification and Regression Tree)
The decision tree models are defined by recursively partitioning the input space, and defining a local model in each resulting region of input space. They are popular for several reasons.

Pros
- easy to interpret
- can handle discrete and continuous features
- insensitive to monotone transformation (scaling)

Cons
- accuracy is not as good as other models
- high variance

#### 5.1.1. ID3
ID3 is an algorithm by Ross Quilan in 1986. It recursively split the tree based on the Information gain.
The splitting process is by greedy search (the optimal split is NP-hard)

**Definition (information gain)** Information gain is defined as follows
$$IG(S,A) = H(S) - H(S|A) = H(S) - \sum_{t \in T} p(t)H(t)$$
where $S$ is the entropy of parent node, $A$ is the target splitting attribute, $T$ is the subsets splitted by $A$

#### 5.1.2. C4.5, C5
These have some improvements from ID3 including
- can handle discrete (categorical feature) as well
- can handle missing values

### 5.2. Ensemble
#### 5.2.1. Boosted
Adaboost

#### 5.2.2. Bootstrap Aggregation (Bagging)
As mentioned, the CART model is a high variance model. To reduce the vairance, we can apply the Bagging to ensemble $n$ trees
Typically, each tree receives a randomly chosen subset of the original data.

$$f(x) = \sum_{i=1}^N \frac{1}{N} f_i(x)$$

Unfortunately, simply rerun the same tree model will result in highly correlated predictors (which still results in high variance). Random forest can decorrelate it by randomly choosing the subset of input variables for each tree.

## 6. Sequential Model

### 6.1. Markov Model 

$$p_(\textbf{x}_1, ..., \textbf{x}_N) = \prod_{n=2}^{N} p(\textbf{x}_n | \textbf{x}_1, ..., \textbf{x}_{n-1})$$

## 7. Reference
[1] Bishop, Christopher M. Pattern recognition and machine learning. springer, 2006.

[2] Rosenblatt, Frank. Principles of neurodynamics. perceptrons and the theory of brain mechanisms. No. VG-1196-G-8. Cornell Aeronautical Lab Inc Buffalo NY, 1961.

[3] Minsky, Marvin, and Seymour A. Papert. Perceptrons: An introduction to computational geometry. MIT press, 2017.

[4] Sutton, Charles, and Andrew McCallum. "An introduction to conditional random fields." Foundations and Trends® in Machine Learning 4.4 (2012): 267-373.

[5] CS229 Lecture Note 

