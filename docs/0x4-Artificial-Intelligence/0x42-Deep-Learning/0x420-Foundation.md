# 0x420 Foundation

## Approximation

Neural network with relu activation can approximate a random continous function. The approximation is achieved by connecting many piecewise linear functions. Intuitively, 1 neuron can provide at least 1 linear piecewise, which might be increased significantly in the deep layer.

In the case of 1 layer shallow network to approxmiate a random L-Lipshitz function, we can break the domain into $O(L/\epsilon)$ piecewise linear function where $\epsilon$ is the maximum tolerance.

In the case of deep neural network, we can build following blocks to approximate any random function
- $y=x^2$ can be efficiently approximated by deep networks
- $y=x_1 x_2$ can be built from previous block
- $y=x^n$ can be built from the second block
- A random polynomial can be built from the 3rd block
- Any random continous function can be approximated by the Weierstrass approximation theorem

## Reference
- [Hung-yi Lee Deep Learning Theory Video](https://www.youtube.com/watch?v=FN8jclCrqY0)