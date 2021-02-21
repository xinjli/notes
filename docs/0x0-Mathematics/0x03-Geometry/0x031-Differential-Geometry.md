# 0x030 Differential Geometry
## Curve

**Definition (parametrized curve)** A parameterized curve in $\R^n$ is a smooth function $\gamma: I \to \R^n$, where $I \subset \R$ is an interval

Note smooth function means $C^\infty$ function. If the interval contains at least one boundary point, then it means it can be extended to a smooth function on an open set containing $I$.S

**Definition (derivative)** If $\gamma: I \to \R^n$ is a curve with components $\gamma(t) = (x_1(t), ..., x_n(t))$, then its derivative $\gamma': I \to \R^n$ is the curve defined as $\gamma'(t)=(x'_1(t), ..., x'_n(t))$

$$\gamma'(t) = \lim_{h \to 0} \frac{\gamma(t+h) - \gamma(t)}{h}$$

**Definition (speed, arc length)** The speed at time $t \in I$ of a curve $\gamma: I \to \R^n$ is $|\gamma'(t)|$. The arc length between time $t_1, t_2$ is $\int_{t_1}^{t_2} |\gamma'(t)| dt$

A curve is called **regular** if its speed is always nonzero. and it is called **unit-speed** or parametrized by arc length if speed is always equal to 1.

