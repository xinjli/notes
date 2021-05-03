# 0x030 Foundation

## Foundation
The vector differential operator del, written in $\nabla$, is defined as follows:

$$\nabla = \frac{\partial}{\partial x} \mathbf{i} + \frac{\partial}{\partial y} \mathbf{j} + \frac{\partial}{\partial z} \mathbf{k}$$

**Definition (gradient)** Gradient acting on a scalar field to produce vector field.

$$\nabla T = \frac{\partial{T}}{\partial x}\mathbf{x} + \frac{\partial{T}}{\partial y}\mathbf{y} + \frac{\partial{T}}{\partial z}\mathbf{z}$$

The gradient $\nabla T$ points in the direction of maximum increase of the function $T$, its slop along this direction is given by $|\nabla T|$

**Definition (divergence)** Divergence acting on a vector field to produce scalar field.

$$\nabla \cdot \mathbf{v} = \frac{\partial{v_x}}{\partial x} + \frac{\partial{v_y}}{\partial y} + \frac{\partial{v_z}}{\partial z}$$

Divergence is a measure of how much the vector $v$ spreads out from each point (therefore a scalar field). In fluid dynamics, if there is no loss of fluid anywhere, then $\nabla \cdot \mathbf{b} = 0$. This is called the **continuity equation** for an **incompressible fluid**. It is said to have no sources or sinks. A vector field whose divergence is zero is sometimes called **solenoidal**.

**Lemma (properties of divergence)**  Divergence is a linear operator

$$\nabla \cdot (a\mathbf{f} + b\mathbf{g}) = a(\nabla \cdot \mathbf{f}) + b(\nabla \cdot \mathbf{g})$$

Product rule

$$\nabla \cdot (\phi \mathbf{A}) = (\nabla \phi) \cdot \mathbf{A} + \phi (\nabla \cdot \mathbf{A})$$

**Definion (curl)** curl acting on a vector field to produce another vector field.

$$\nabla \times \mathbf{v} = (\frac{\partial v_z}{\partial y} - \frac{\partial v_y}{\partial z}) \mathbf{x} + (\frac{\partial v_x}{\partial z} - \frac{\partial v_z}{\partial x}) \mathbf{y} + (\frac{\partial v_y}{\partial x} - \frac{\partial v_x}{\partial y}) \mathbf{z}$$

curl is a measure of how much the vector $v$ swirls around the point in question. A vector field wihtout rotation (i.e.: $\nabla \times \mathbf{v}=0$) is called **irrotational**, a field that is not irrotational is sometimes called a **vortex field**.

Furthermore, if the vector field is irrotational $\nabla \times \mathbf{v} = 0$, then it is a conservative vector field, which means there exists a scalar field $\phi$ such that

$$\mathbf{v} = \nabla \phi$$

In conservative vector field, the line integral is path independent.

**Lemma (properties of curl)**

- $\nabla \times (\phi \mathbf{A}) = (\nabla \phi) \times \mathbf{A} + \phi (\nabla \times \mathbf{A})$
- $\nabla \cdot (\mathbf{A} \times \mathbf{B}) = \mathbf{B} \cdot (\nabla \times \mathbf{A}) - \mathbf{A} \cdot (\nabla \times \mathbf{B})$
- $\nabla \times (A \times B) = (B \cdot \nabla) A - B(\nabla \cdot A) - (A \cdot \nabla)B + A(\nabla \cdot B)$
- $\nabla(A \cdot B) = (B \cdot \nabla) A + (A \cdot \nabla) B + B \times (\nabla \times A) + A \times (\nabla \times B)$



## Curve
**Definition (osculating plane)** The plane which contains the tangent and principal normal

**Definition (normal plane)** The plane contains principal normal and binormal, it is the plane perpendicular to the tangent vector

**Definition (rectifying plane)** The plane contains the tangent and binormal, perp to the principal normal.


**Theorem (Frenet-Serret)** 
$$\frac{d}{ds}\left(\begin{array}{c} \mathbf{T} \\ \mathbf{N} \\ \mathbf{B} \end{array}\right) =
		\left( \begin{array}{ccc}
		0 & \kappa & 0 \\
		-\kappa & 0 & \tau \\
		0 & -\tau & 0
		\end{array} \right)
		\left(\begin{array}{c} \mathbf{T} \\ \mathbf{N} \\ \mathbf{B} \end{array}\right)$$

where $\mathbf{T}$ is the unit tangent vector, $\mathbf{N}$ is the **principal normal vector** and $\mathbf{B}$ is the **binormal vector**, $\kappa$ is the **curvature** and $\tau$ is the **torsion**, torsion measures how sharply it is twisting out of the plane of curvature. (curve up?)

![Frenet frame](https://upload.wikimedia.org/wikipedia/commons/1/11/Frenet.svg)

### Line Integral

**Definition (arc length)** Let $\mathbf{x} \in C^1: [a,b] \to R^3$ where $\mathbf{x}(t) = (x(t), y(t), z(t))$with $\mathbf{x}'(t) \neq 0$. The $\mathbf{x}$ is called a smooth parametrization of $C$. The length of the curve is

$$\int_C ds = \int_a^b ||\mathbf{x}'(t)|| dt$$

**Definition (line integral of a scalar field)** Let $f$ be a continuous function on a smooth curve $C$ parameterized by $\mathbf{x}(t)$, the integral of $f$ over $C$ with respect to arc length is

$$\int_C f ds = \int_a^b f(\mathbf{x}(t))||\mathbf{x}'(t)|| dt$$

The illustration on Wikipedia is pretty good

![gif](https://en.wikipedia.org/wiki/Line_integral#/media/File:Line_integral_of_scalar_field.gif)


**Definition (line integral of a vector field)** For a vector field $\mathbf{F}: R^n \to R^n$, the line integral along a piecewise smooth curve $C$, in the direction of $r$, is defined as

$$\int_C \mathbf{F}(r) \cdot d\mathbf{r} = \int_a^b \mathbf{F}(\mathbf{r}(t)) \cdot \mathbf{r}'(t) dt$$

**Theorem (fundamental theorem of calculus for line integrals, gradient theorem)** Let $\varphi: U \subseteq R^n \to R^n$ be a continuously differentiable function and $\gamma$ any curve in $U$ which starts at $\mathbf{p}$ and ends at $\mathbf{q}$. then

$$\int_\gamma \nabla \varphi(\mathbf{r}) \cdot d\mathbf{r} = \varphi(\mathbf{q}) - \varphi(\mathbf{p})$$

It implies the line integrals through a gradient field are **path independent**. In Physics, $\varphi$ is a potential and $\nabla \varphi$ is a conservative field: Work done by the conservative forces does not depend on the path, but only on the end points.




## Surface

**Definition (smooth surface)** Let $\mathbf{x}$ be a smoothly bounded set $D: \mathbb{R}^2 \to \mathbb{R}^3$, denoted $\mathbf{x}(u, v) = (x(u,v), y(u,v), z(u,v))$, Suppose $\mathbf{x}$ satisfies the following conditions on the interior of $D$

- $\mathbf{X}$ is 1-to-1
- the partial deriavtives are bounded
- partial derivatives are linearly independent, $\mathbf{x}_u(u,v) \times \mathbf{x}_v(u,v) \neq 0$.

Then the range of $\mathbf{x}$ is called a smooth surface, parametrized by $\mathbf{x}$

**Definition (surface integral)** If a surface $S$ is parametrized by the continuously differentiable function $x(u,v)$ over the domain $D$ in the uv-plane, then the scalar surface integral of the function $f(x)$ over $S$ is

$$\int_S f(x) dS = \int_D f(x(u,v)) || x_u \times x_v || du dv$$

## Integration

**Theorem (divergence, Gauss)** Let $F$ be a $C^1$ vector field on regular set $D$ and let $N$ be the unit normals to $\partial D$ that point out of $D$, then

$$\int_{\partial D} (F \cdot N) d\sigma = \int_D (\nabla \cdot F) dV$$

**Theorem (curl, Stokes)** Let $G$ be a vector field that is $C^1$ on a piece-wise smooth oriented surface $S$ whose boundary $\partial S$ is a piecewise smooth curve

$$\int_{\partial S} (G \cdot T) ds = \int_{S} (\nabla \times G) dS $$


## Reference
[1] Lax, Peter D., and Maria Shea Terrell. Multivariable Calculus with Applications. Springer, 2017.