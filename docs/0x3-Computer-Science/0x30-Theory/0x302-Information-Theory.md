# 0x302 Information Theory

## Foundation
Information Theory is concerned with representing data in a compact fashion, the most important concepts are summarized here

**Definition (entropy)** The entropy of a discrete random variable $X$ with distribution $p$ is

$$H(X) = -\sum_{k=1}^K p(X=k) \log_2 p(X=k)$$

For a K-ary random variable, the maximum entropy is $H(X) = \log K$ when $p(X=k) = 1/K$


**Definition (differential entropy)** The continuous version is the differential entropy.

$$H(X) = - \int_{\mathcal{X}} f(x)\log f(x) dx$$

Note this differential entropy is not the exact generalization of the discrete version, the actual generalization is called LDDP

**Definition (relative entropy, KL divergence)** One way to measure the dissimilarity of two probability distribution $p, q$ is the Kullback-Leibler divergence (KL divergence) or relative entropy

$$KL(p||q) = \sum_k p_k \log\frac{p_k}{q_k} = -H(p) + H(p, q)$$

KL divergence is the average number of extra bits needed to encode the data $p$ with distribution $q$.

**Definition (cross entropy)** $H(p,q)$ is called cross entropy, it is to measure the average number of bits to encode data of distribution $p$ using codebook of distribution $q$, it is defined as

$$H(p, q) = -\sum_k p_k \log q_k$$


**Definition (conditional entropy)** The conditional entropy $H(Y|X)$ is defined as

$$H(Y|X) = \sum_x p(x) H(Y|X=x)$$

**Definition (mutual information)** Mutual information or MI is an approach to estimate how similar the joint distribution $p(X,Y)$ can be factored into $p(X)p(Y)$

$$I(X;Y) = KL(p(X,Y)||p(X)p(Y)) = \sum_x \sum_y p(x,y)\log \frac{p(x,y)}{p(x)p(y)}$$

Obviously, MI is zero iff two random variables are independent.

MI can be expressed using entropy as follows

$$I(X;Y) = H(X) - H(X|Y) = H(Y) - H(Y|X)$$

Therefore, MI can be interpreted as the reduction in uncertainty about $Y$ after observing $X$

Statistics based on MI might capture nonlinear relation between variables that can not be discovered by correlation coefficients.

**Definition (pointwise mutual information)** A related concept is pointwise mutual information or PMI, this is about two events $x,y$

$$PMI(x,y) = \log \frac{p(x,y)}{p(x)p(y)}$$

## Reference
[1] Cover, Thomas M., and Joy A. Thomas. Elements of information theory. John Wiley & Sons, 2012.

