# 0x453 Speech Recognition

Speech recognition is a task modeling relation between speech input $X$ and linguistic (text output) $Y$

## GMM-HMM
GMM-HMM is one of the traditional generative models.

An alternative generative model with HMM is the DBN-HMM

## DNN-HMM
DNN is a discriminative model, so it can not be directly connected with the HMM model, In the DNN-HMM hybrid model, DNN first estimates the posterior $P(p|X)$ where $p$ is usually a CD state, then converting this output to likelihood with prior by using

$$P(X|p) \propto \frac{P(p|X)}{P(p)}$$

Then the $P(X|p)$ can be plugged into the generative HMM framework.

## CTC
CTC is a discriminative model

## RNN Transducer
RNN-T extends the CTC model by removing the conditional independence assumption

## E2E

## Reference
[1] Lecture Note on Hybrid HMM/DNN
