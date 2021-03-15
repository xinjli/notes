# 0x310 Arithmetic
- [1. Bitwise](#1-bitwise)
- [2. Integer](#2-integer)
  - [2.1. Multiplication](#21-multiplication)
  - [2.2. Division](#22-division)
  - [2.3. Primality Test](#23-primality-test)
  - [2.4. Factorization](#24-factorization)
  - [2.5. Pseudorandom Number Generator (PRNG)](#25-pseudorandom-number-generator-prng)
- [3. Float](#3-float)
  - [3.1. Random Variable Generation](#31-random-variable-generation)
- [4. Reference](#4-reference)

## 1. Bitwise
Following are useful bitwise operations of set representations

- $\emptyset: 0$
- $\{ i \}: 1 << i$
- $\{0, 1, ..., n-1\}: (1<<n) -1$
- $i \in S: (S >>i) \& 1$
- $S \cup \{ i \} : S | 1 << i$
- $S \ \{ i \}: S \& ~(1<<i)$
- $S \cup T: S | T$
- $S \cap T: S \& T$

*The Go programming language* book has a good code sample to show this in Chapter 3.1

``` go
var x uint8 = 1<<1 | 1<<5
var y uint8 = 1<<1 | 1 <<2

fmt.Printf("%08b\n", x)    // "00100010", the set {1, 5}
fmt.Printf("%08b\n", y)    // "00000110", the set {1, 2}
fmt.Printf("%08b\n", x&y)  // "00000010", the intersection {1}
fmt.Printf("%08b\n", x|y)  // "00100110", the union {1, 2, 5}
fmt.Printf("%08b\n", x^y)  // "00100100", the symmetric difference {2, 5}
fmt.Printf("%08b\n", x&^y) // "00100000", the difference {5}

for i := uint(0); i < 8; i++ {
  if x&(1<<i) != 0 {           // membership test
    fmt.Println(i)           // "1", "5"
  }
}
```

## 2. Integer
### 2.1. Multiplication
**Algorithm (Russian Peasant Method)** multiply a, b by recursively doubling a and halve b, run in log complexity

``` lisp
(define (multi a b)
  (define (multi-iter a b s)
    (cond ((= b 1) (+ a s))
          ((even b) (multi-iter (double a) (halve b) s))
          (else (multi-iter a (- b 1) (+ s a)))))
  (multi-iter a b 0))
```

**Algorithm (Karatsuba)** efficient algorithm for big integer, reducing the standard complexity from $O(n^2)$ to $O(n^{\log_2 3})$ (around $O(n^{1.5})$)

Basic idea is to apply the following steps recursively:
Consider multiplication of $x=x_1 b + x_0$ and $y=y_1 b + y_0$, in the long multiplication's algorithm, we do 4 times of multiplications

$$z_2 = x_1 y_1, z_0 = x_0y_0, z_1 = x_1 y_0 + x_0 y_1$$

Instead, compute the $z_1$ with

$$z_1 = z_2 + z_0 - (x_1 - x_0)(y_1 - y_0)$$

**Algorithm (Schönhage–Strassen)** recursively apply FFT, complexity is $O(n \log(n) \log\log(n))$, used in Great Internet Mersenne Prime Search

### 2.2. Division
**Algorithm (Euclid)** The Euclid's algorithm is used to find the gcd of two integers, it is from the *Elements* (300 B.C) and one of the oldest algorithm in the world.

``` c
int gcd(int a, int b) {
  if (b==0) return a;
  return gcd(b, a%b);
}
```

The complexity of Euclid can be estimated with the Fibonacci number $F_k$ as follows
**Theorem (Lame's theorem)** For any integer $k \geq 1$, if $a > b \geq 1, b < F_{k+1}$, then the recursion call is less than $k$ recursive.

This gives us the complexity of $O(log_2(b))$

Euclid's algorithm can also be extended to solve the equation

$$ax + by = gcd(a,b)$$

or similarly

$$ax \equiv b \mod n$$

Consider we have solved the following equation and know $x', y'$
$$bx' + (a \% b)y' = gcd(a,b)$$

We can rearange this into

$$ay' + b(x' - (a/b)y') = gcd(a,b)$$

when $b=0$, the start point is

$$a \times 1 + b \times 0 = gcd(a,b)$$

``` c
int extgcd(int a, int b, int&x, int& y) {
  if d = a;
  if (b != 0){
    d = extgcd(b, a%b, y, x);
    y -= (a/b)*x;
  }
  else{
    x = 1; y=0;
  }
  return d;
}
```





### 2.3. Primality Test
**Problem (primality)** Check whether a give integer is prime or not
The most simple algorithm to check $n$'s primality is check all numbers up to $\sqrt{n}$.

**Algorithm (Sieve of Eratosthenes)** complexity is $O(n \log\log n)$, so nearly linear

**Algorithm (Fermat test)** probablistic $O(\log(n))$. To test primality of $n$, randomly select a number $a < n$, check whether $a^n$ is congruent to $a$ under base of $n$. This is based on the Fermat Little Theorem such that if $n$ is prime, then

$$\forall(a < n) a^n \equiv a \mod n$$

Note that Carmichael numbers are exceptions to Fermat test (e.g: 561, 1105, ....) 

**Algorithm (Miller-Rabin)** probablistic, check existence of square root
Given $n$, find $s$ such that $n-1 = 2^sq$ for some odd $q$, then do the following test
- pick a random number $a \in [1, n-1]$
- if $a^q=1$, then passes
- for $i=[0, s-1]$, check whether $a^{2^i q} = -1$, if so it passes
- otherwise $n$ is composite.

The prob to fail to detect composite with $k$ is around $(1/4)^k$

**Algorithm (AKS primality test)** deterministic (PRIMES is in P)

### 2.4. Factorization
Factorization problem is much more difficult than the primality test, which guarantees the safety of many cryptography schemes.

**Algorithm(Pollard's rho)** randomly generate $x,y$ based on cycle-detection algorithm, then check $gcd(x-y, n)$ until cycle detected.

- x ← 2, y ← 2; d ← 1
- While d = 1:
- x ← f(x)
- y ← f(f(y))
- d ← GCD(|x − y|, n)
- If d = n, return failure.
- Else, return d.


Its expected running time is proportional to the square root of the size of the smallest prime factor of the composite number being factorized

**Algorithm(Number Field Sieve)** I do not understand..

### 2.5. Pseudorandom Number Generator (PRNG)

**Algorithm (Linear Congruence Generator)** One of the oldest and best-known algorithm, many libraries (e.g: glibc) uses this to generate number.

$$X_{n+1} = (a X_{n} + c) \mod m$$

Note recently there is some improved version of this: Permuted congruential generator (PCG), this is used in numpy random.

**Algorithm (Mesenne Twister)**


## 3. Float

### 3.1. Random Variable Generation
**Algorithm (direct methods)** If $Y$ is a continuous random variable with cdf$F_Y$, then random variable $F^{-1}_Y(U)$ where $U \sim \text{uniform}(0,1)$  has distribution $F_Y$

$$F^{-1}_Y(u) = y$$

$$u = \int_{\infty}^{y} f_y(t) dt$$
Generate a random variable $u$, and solve it with respect to $y$.

**Algorithm (Box-Muller)** Given two independent $U_1, U_2 \sim \text{uniform}(0, 1)$, and set

$$R = \sqrt{-2 log{U_1}}, \theta = 2\pi U_2$$

then

$$X = R \cos\theta, Y = R\sin\theta$$

Are independent $n(0,1)$ random variables


## 4. Reference
[1] Cormen, Thomas H., et al. Introduction to algorithms. MIT press, 2009.
[2] Abelson, Harold, and Gerald Jay Sussman. Structure and interpretation of computer programs. The MIT Press, 1996.
[3] 秋葉拓哉, 岩田陽一, and 北川宜稔. "プログラミングコンテストチャレンジブック." (2010).
[4] Donovan, Alan AA, and Brian W. Kernighan. The Go programming language. Addison-Wesley Professional, 2015.
[5] [Miller-Rabin test note](https://crypto.stanford.edu/pbc/notes/numbertheory/millerrabin.html)
