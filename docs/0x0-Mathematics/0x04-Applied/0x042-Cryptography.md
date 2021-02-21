# 0x042 Cryptography

- [1. Classic Cipher](#1-classic-cipher)
    - [1.1. Substitution Ciphers](#11-substitution-ciphers)
    - [1.2. enigma](#12-enigma)
- [2. Symmetric-key Cipher](#2-symmetric-key-cipher)
    - [2.1. One Time Pad](#21-one-time-pad)
    - [2.2. Stream Cipher](#22-stream-cipher)
    - [2.3. DES (3DES)](#23-des-3des)
    - [2.4. AES](#24-aes)
- [3. Asymmetric-key Cipher](#3-asymmetric-key-cipher)
    - [3.1. RSA](#31-rsa)
    - [3.2. ECC (Elliptic Curve Crypto)](#32-ecc-elliptic-curve-crypto)
- [4. Digital Signature](#4-digital-signature)
    - [4.1. ElGamal](#41-elgamal)
    - [4.2. DSA](#42-dsa)
    - [4.3. ECDSA](#43-ecdsa)
- [5. Cryptographic Hash](#5-cryptographic-hash)
    - [5.1. MD5](#51-md5)
    - [5.2. SHA](#52-sha)
- [6. Message Authentication Code](#6-message-authentication-code)
- [7. Block Chain](#7-block-chain)
- [8. Data Structures](#8-data-structures)
- [9. Quantum Cipher](#9-quantum-cipher)
- [10. Reference](#10-reference)

## 1. Classic Cipher
Personally I think the code book by Simon Singh is a very good reference for old ciphers.

### 1.1. Substitution Ciphers
Substitution Ciphers can be easily attacked with frequency analysis (e.g: character e appears about 13% in a standard English text)

- scytale: a transposition cipher used in ancient Greece
- Caesar Cipher
- Vigenere Ciper
- ROT13: $(a+13)%26$

### 1.2. enigma
encryption
three roters
one plugboard
Alice message -> plugboard -> three roters -> plugboard -> encryption

**complexity**
- roter combination: (5x4x3)
- roter initialization: (26x26x26)
- plugboard combination: (factorial(26)/(factorial(6)xfactorial(10)xpower(2,10)))
total complexity: 10^21

**decryption**
Bob set up the roter and plugboard with correct combination and feed the encrypted message, and the output will be the original message

**how to break (bombe)**
basiclly, brute force with several tricks to reduce complexity
Tricks
use 'weather report' as a key word
same char would not be mapped to the same char

## 2. Symmetric-key Cipher
Alice and Bob use the same key: A cipher defined over $(\mathcal{K}, \mathcal{M}, \mathcal{C})$ is a pair of efficient algorithms $(E,D)$ where $C: \mathcal{K} \times \mathcal{M} \rightarrow \mathcal{C}$ and $D: \mathcal{K} \times \mathcal{C} \rightarrow \mathcal{M}$

Definitions

Consistency: $D(k, E(k, m))==m$
Perfect secrecy: A cipher $(E,D)$ over $(\mathcal{K}, \mathcal{M}, \mathcal{C})$ is said to have perfect secrecy if $P(E(k, m_0)==c) == P(E(k, m_1)==c) $ for all $m_0, m_1 \in \mathcal{M}, c \in \mathcal{C}$ where $k$ is uniformly random sampled over $\mathcal{K}$ (Rought idea is cipher text give no info about plain text). Hard to use in practice

### 2.1. One Time Pad
Vernam 1917. One Time Pad is defined by taking XOR between text and key of same length: $\mathcal{M}, \mathcal{E} \in \{0, 1\}^n, \mathcal{K} \in \in \{0, 1\}^n $.

### 2.2. Stream Cipher
Idea: Expand a short random seed (seed is key) into a long pseudorandom bit string, and then apply One Time Pad

### 2.3. DES (3DES)

### 2.4. AES

## 3. Asymmetric-key Cipher
Alice and Bob use different keys

### 3.1. RSA
### 3.2. ECC (Elliptic Curve Crypto)
Elliptic curve is a set of $(x,y)$ over Galois Field whose points are satisfying $y^2=x^3+ax+b$ along with inf points

**Definition**

- additive identity: inf 
- scalar multiplication: $Q = dP = P + P ... + P$. this operation will generate cyclic group
  
**ECC Discrete logarithm** Given a elliptic curve $<G>$ where G is the base pointer, and a pointer E, find a which satisfying $X=aG$

**Properties**
- No efficient solution for discrete logarithm (EC is hard to break)
- efficient solution for reverse exp operation (EC is hard to encode and decode)
  
**Curve**
- NIST curve: 192, 224, 256, 384, 521 bit (521 is selected for computation efficiency with a Mersenne prime)
- Brainpool curve: 160, 192, 224, 256, 320, 384, 512 bit (slow than NIST curve)
  

## 4. Digital Signature
### 4.1. ElGamal
### 4.2. DSA
### 4.3. ECDSA

## 5. Cryptographic Hash
Crypto hash takes any string as input, produces fixed size output, and should be efficiently computable. It should meet the following security properties.

**collision-free**: Nobody can find a pair $(x, y)$ such that $x!=y; H(x) == H(y)$
**hiding**: If $r$ is chosen from distribution with high min entropy. then given $H(r|x)$, it is infeasible to find $x$
**puzzle-friendly**: For every possible output $y$ and $k$ chosen from distribution with high-min entropy, it is infeasible to find $H(k|x)=y$. 
**avalanche effect**: a small change in input space would cause a drastic change in output space


### 5.1. MD5
### 5.2. SHA

## 6. Message Authentication Code
## 7. Block Chain
## 8. Data Structures
Hash Pointer: a pair of (pointer to an info, hash of the info). It can verify that the info has not been changed.

Merkle tree: binary tree using hash pointer, it can be used to prove membership in $log(n)$. Sorted merkle tree can prove non membership

## 9. Quantum Cipher

## 10. Reference
[1] Handbook of Applied Cryptography.
[2] The Code Book