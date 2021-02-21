# 0x101 Quantum Mechanics

## Foundation

### Experiments

**The Stern-Gerlach experiment**
SG experiment measures the z-component of the magnetic momentum $\mu$ of random oriented silver atoms, which are expected to distribute continuously between $[ -|\mu|, |\mu| ]$, but are actually realized in the two quantized spots. 

Furthermore, concating multiple SG apparatus show that determining x,z component simutaneously is impossible. Measuring one will destroy info of the other.

### Schrödinger Equation
The **wave function** $\Psi{(x,y)}$ encodes all information about the state of a particle.
Wave function can be added, multiplied by a complex number and taken inner product, therefore they are in the Hilbert space

The wave function can be obtained by solving the **Schrödinger's equation**

$$i \hbar \frac{\partial \Psi}{\partial t} = - \frac{\hbar^2}{2m} \frac{\partial^2 \Psi}{\partial x^2} + V \Psi$$

The wave function should satisfy the normalization constraint, which states

$$\int_{-\infty}^{\infty} |\Psi(x,t)|^2 dx = 1$$

### Observable
Location $x$ to find a particle has the PDF distribution. It is a valid distribution because of the normalization contraint.

$$f_t(x) = |\Psi(x,t)|^2$$


# Reference
[1] Sakurai, Jun John, and Eugene D. Commins. "Modern quantum mechanics, revised edition." (1995): 93-95.
[2] David J.Griffiths and Darrell F. Schroeter Introduction to Quantum Mechanics

