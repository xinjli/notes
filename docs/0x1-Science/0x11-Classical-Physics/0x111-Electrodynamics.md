# 0x111 Electrodynamics

## Electrostatics
Electrostatics applies to the case when the source charges are stationary (though the test charge maybe moving).

### Electric Field

**Law (Coulomb's law)** The force on a test Charge $Q$ due to a single charge $q$ is given by
$$\mathbf{F} = \frac{1}{4 \pi \epsilon_0} \frac{qQ}{r^2} \mathbf{\hat{r}}$$

where the constant $\epsilon_0$ is called the **permittivity of free space**. 

$$\epsilon_0 =8.85 \times 10^{-12} \frac{C^2}{N \cdot m^2}$$

**Defintion (Electric Field)** If there are several point charges $q_1, q_2, ..., q_n$ at $r_1, ..., r_n$, the total force on $Q$ is
$$F=QE$$

and $E$ is the elctric field of the source charge.
$$E(r) = \frac{1}{4\pi \epsilon_0} \sum_{i=1}^{n} \frac{q_i}{r_i^2} \mathbf{\hat{r_i}}$$

When the charge are distributed continuously, it can be written in the integral form by

$$E(r) = \frac{1}{4\pi \epsilon_0} \int \frac{\rho(\mathbf{\hat{r}})}{r^2} \mathbf{\hat{r_i}} dq$$

**Law (Gauss's law)** The flux through a enclosing surface is proportional to the charge inside.
$$\oint \mathbf{E} \cdot d \mathbf{a} = \frac{Q}{\epsilon_0}$$

This is equivalent to
$$\nabla \cdot \mathbf{E} = \frac{1}{\epsilon_0}\rho$$

## Reference
- [1] David J. Griffiths Introduction to Electrodnyamics

