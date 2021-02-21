# 0x110 Classical Mechanics

The following three formulation are equivalent.

## Newtonian Mechanics

### Newton's Law

The Newtonian formulation is useful for simple systems, in particular they apply to a *point mass* (or a *particle*), which is an abstract object with mass, but no size and has no internal degress of freedom.

**Law (Newton's First Law, the Law of Inertia)** In the absence of force, a particle moves with constant velocity.

Note the first law remains exactly true even in relativity.

**Law (Newton's Second Law)** For any particle of mass $m$, the net force $\bf F$ on the particle is alwayts equal to the mass $m$ times the particle's acceleration

$$\mathbf{F} = m\mathbf{a}$$

Or equivalently 

$$F = \mathbf{\dot{p}}$$

where $p$ is the momentum. Note that they are no longer equivalent in relativity where the first representation $F=ma$ is not valid anymore. 

Newtons' second law in different coordinate systems has difference representations. In Cartesian coordinate, we have
$$\begin{aligned}
F_x = m \ddot{x} \\
F_y = m \ddot y \\
F_z = m \ddot z\end{aligned}$$

In 2D Polar systems, we have
$$\begin{aligned}F_r = m (\ddot r - r \dot \phi^2) \\
F_\phi = m (r \ddot \phi + 2 \dot r \dot \phi)\end{aligned}$$

The final $\dot r \dot \phi$ is the Coriolis acceleration.

These two laws hold only in the special inertial reference frames, or the first law can be used to indentify these inertial frames: a reference frame is inertial if objects subject to no forces are seen to move with constant velosity 

**Law (Newton's Third Law)** If object 1 exerts a force $F_{21}$ on object 2, then object 2 always exerts a reaction force $F_{12}$ on object 1 given by

$$\bf{F}_{12} = -\mathbf{F}_{21}$$

Within the domain of classical physics, the third law is valid with such acuracy, but cannot hold as speeds approach the speed of light

Note the third law is equivalent to the principle of conservation of momentum.

### Momentum and Angular Momentum
As suggested by the Newton's third law, the rate of change of the system's total linear momentum $p=\sum_i p_i$ is determined by the external forces on the system:

$$\dot p = F$$

This leas to the conservation law
**Principle (Conservation of Momentum)** If the net external force $\mathbf{F}^{ext}$ on a N-particle system is 0, the system's total mechanical momentum is constant

$$p=\sum m_i v_i$$

The ordinary momentum is the "linear" momentum, the angular momentum is the "rotational" momentum.
**Definition (angular momentum)** The angular momentum $l$ of a single particle is defined as the vector

$$l = r \times p$$

Note that $l$ depends on the position vector $r$,  therefore depends on the origin $O$. The momentum, however, does not depend on the origin.

Taking derivatives on both sides, we get

$$\dot l = r \times F \equiv \Gamma $$

where $\Gamma$ is called torque, this the rotational analog of $\dot p = F$

Consider a single planet orbiting the sun, where the force is central, therefore the torque is 0 and angular momentum $r \times p$ is constant. This can be used to prove the Kepler's Second Law

**Law (Kepler's Second Law)** As each planet moves around the sun, a line drawn from the planet to the sun sweeps out equal areas in equal times.

The swept area $dA$ can be write as 

$$dA = \frac{1}{2}|r \times v dt|$$

This leads to 

$$\frac{dA}{dt} = \frac{l}{2m}$$

Because $l$ is constant, $dA/dt$ is also constant.

**Theorem (Conservation of Angular Momentum)** If the net exxternal torque on an N-particle system is zero, the system's total angular momentum is constant

$$L = \sum r_i \times p_i$$

### Energy

**Definition (kinetic energy)** The kinetic energy (KE), which for a single particle of mass $m$ traveling with speed $v$ is defined to be

$$T = \frac{1}{2}mv^2$$

Taking derivatives with respect to $t$, we have

$$\frac{dT}{dt} = m \dot v \cdot v = F \cdot v$$

This proved the Work-KE Theorem

**Theorem (Work-KE Theorem)** The work done by force $F$ can be written using line integral

$$\Delta T \equiv T_2 - T_1 = \int_1^2 F \cdot dr \equiv W(1 \to 2)$$


**Criterion (Conservative Force)** A force $F$ acting on a particle is convervative iff it satisfies two conditions

1. $F$ depends only on the particle's position $r$ (not on $v$, $t$...)

$$F = F(r)$$

2. For any two points 1, 2, the work $W(1 \to 2)$ done by $F$ is the same for all paths between 1 and 2

$$W (1 \to 2) = Const$$

If all forces on an object are conservative, we can define the potential enery, denoted $U(r)$, then the total mechanical energy

$$E = KE + PE = T + U(r)$$

$E$ is constant, therefore conserved.

**Definition (potential energy)** The potential enery at $r$ with respect to a reference point $r_0$ (where $U$ is defined to be 0)

$$U(r) = -W(r_0 \to r) \equiv - \int_{r_0}^r F(r') \cdot dr'$$

## Lagrangian Mechanics

### Formulation
Lagrangian formulation is better when involving constraints. Lagrangian is using configuration space for its formulation. The time evolution of a system is described in this space by a single path.

The main idea of Lagrangian formalism is that nature is lazy, which means the action $S$ defined as follows should be minimized

$$S = \int_{t_i}^{t_f} dt (T-V) $$

where the second term is called Lagrangian $L(q, \dot q)$

$$L = T - V$$

Intuitively, the principle of least action states that the lazy man do not want to move very actively, instead, they want to preserve their potential energy when integrating over time.

By solving the least action formula with variational calculus, we obtain the famous Euler-Lagrange equation

$$\frac{\partial  L}{\partial q} - \frac{d}{dt}\big(\frac{\partial L}{\partial \dot{q}}\big) = 0$$

This Eular Lagrange Equation can be connected with the Newtonian one

$$p = \frac{\partial L}{\partial \dot q}$$

$$F = \frac{\partial L}{\partial q} = -\frac{\partial V(q)}{\partial q}$$

where $p$ is the generalized momentum and $F$ is the generalized force

This leads to Newton second law (rate of change of the momentum equals the force)

$$\frac{d}{dt} p =F$$

### Constraint
One advantage of Lagrangian formulation is that constraints are easy to implement. In the Newtonian formulation, constraint need to be considered by introducing new forces. In Lagrangian formulation, the constraints can be implemented by either using Lagrange Multiplier or using the generalized coordinate.

#### Constraint with Lagrange Multiplier
In Lagrange Multipler, the constraints can be expressed using a level set

$$g(q_1, q_2, ..., q_n, t)=0$$

This can be used to create a new Lagrangian 
$$L_{full} = L_{free} + \lambda g(q,t)$$

Applying the Euler-Lagrange equation with respect to $\lambda$ can get the previous level set constraint.

$$\frac{\partial L}{\partial \lambda} = \frac{d}{dt} (\frac{\partial L}{\partial \dot \lambda})$$




## Hamiltonian Mechanics
Hamiltonian Mechanics and Lagrangian Mechanics are connected with the Legendre transform.

Hamiltonian $H(p,q)$ is an abstract concept of total energy in closed systems. It is a Legendre transform from Lagrangian.

$$H(p,q) = p\dot q - L(q,p)$$

The Hamilton's equations are

$$\frac{\partial{p}}{\partial t} = - \frac{\partial H}{\partial q}$$

$$\frac{\partial{q}}{\partial t} = \frac{\partial H}{\partial p}$$

Poisson bracket of two phase space functions $A(q,p), B(q,p)$, is defined as

$$\{ A, B \} = \frac{\partial A}{\partial q} \frac{\partial B}{\partial p} - \frac{\partial A}{\partial p} \frac{\partial B}{\partial q}$$

The Hamilton's equation of motion describes the time evolution of a general phase space function 

$$\frac{d}{dt} F = \{ F, H \}$$

Note that commutator is related to poisson bracket

$$[ \hat{f}, \hat{g} ] \sim i\hbar \{ f, g \}$$

A quick derivation can show that

$$\{ p_i, p_j \} = \{ q_i, q_j \} = \{ p_i, q_j \} = 0$$

A couple of properties related to Poisson brackets are 
* $\{ A, B \} = - \{ B, A \}$
* $\{ A + B, C \} = \{ A, C \} + \{ B, C \}$
* $\{ \lambda A, B \} = \lambda \{ A, B \}$
* $\{ AB, C \} = \{ A, C \} B + A \{ B, C \}$

## Reference
[1] Taylor, John R. Classical mechanics. University Science Books, 2005.
