## Fractals

A fractal is a self-similar object. The definition of the geometrical fractal is the follwoing:

- it is a shape with self-similar geometry
- self-similarity is fulfilled over arbitrarily many iterations
- $N(l)$ is the number of volume units show non-trivial scaling as a function of $l$: $~ N(l) \propto l^{-D}$, where $D$ is non-integer

The ***embedding dimension*** of a fractal is given by the smallest Euclidean dimension in which the object can exist.

The ***box dimension*** of a fractal is defined the following way:

$$D_{B} = \lim_{l \rightarrow 0} \frac{lnN(l)}{ln(1/l)}$$

For growing fractals a simple rescaling should be executed for the system size $L$:

$$D_{B} = \lim_{L \rightarrow \infty}\frac{lnN(L)}{lnL}$$

The ***Hausdorff dimension*** of a fractal is defined as:

- covering a fractal with spheres with radii smaller than $\epsilon$
- for a given $D > 0$ we take the lower bound of $\sum_{i}r_{i}^{D}$ where $r_i$ is the radius of sphere $i$

$$M(D, \epsilon) := \inf_{covers} \Big\{ \sum_{i}r_{i}^{D}\Big\}$$

$$M(D) := \lim_{\epsilon \rightarrow 0}M(D, \epsilon) = \lim_{\epsilon \rightarrow 0} \Big( \inf_{covers} \Big\{ \sum_{i}r_{i}^{D} \Big\}\Big)$$

- the Hausdorff dimension is the upper bound of $D$ for which $M(D) > 0$:

$$D_{H} := \sup \Big\{ D \mid M(D) > 0 \Big\}$$

For simple, non-fractal object it is equivalent to the Euclidean dimension while for recursive geometrical fractals it is equivalent to the box dimension.

The dimension of set of rational numbers between $[0; 1]$:

- the box counting dimension goes with the length of the boxes and they occur in any non zero interval: $N(l) \propto l^{-1}$, therefore $D_{B} = 1$

- covering more and more rational numbers with small shperes of length $l = 2^{-k}$ in the $k^{th}$ iteration, therefore in the limit covering all rational numbers $M(k, D) = k\cdot 2^{-kD}$ if $D > 0$ then $M(D) = 0$, therefore $D_{H} = 0$.

### Properties of the fractal dimension

If a fractal dimension $D$, embedded in Euclidean dimension $d$ is projected to a subspace of diemsnion $d_{s}$:
- if $d_{s} > D$ then $D_{projection} = D$
- if $d_{s} < D$ then $D_{projection} = d_{s}$

If we take the intersection of a fractal of dimension $D$ embedded in $d$ with and Euclidean subspace of dimension $d - m$ then the dimension of the intersection is $D-m$.

The union of fractals $D_{A}$ and $D_{B}$ where $D_{A} > D_{B}$ then the dimension of the result is $D_{A \cup B} = D_{A}$.

The product of these fractals is $D_{AB} = D_A + D_B$.

The intersection of the above fractals is is based on densitiy, where in a linear size $L$ from fractal $A$ there are a 'particle density' of $\propto \frac{L^{D_A}}{L^{d}}$ and the same for fractal $B$. Since they are independent the density in the intersection is $\propto \frac{L^{D_A}L^{D_B}}{L^d} = L^{D_A + D_B -d}$. Therefore $D_{A\cap B} = D_A + D_B - d$. 

A fractal is ***deterministic*** if it is generated with self-similar recursion and the procedure is fully deterministic.

- $N \propto n^{k}$ and $l \propto 1/r^{k}$ then $D_{B} = \frac{ln ~n}{ln ~r}$

A ***non-uniform*** fractal is fully deterministic fractal where the scaling factors of the copies are varying.

- with varying scaling factors $\sum_{i = 1}^{q} r_{i}^{-D_{B}} = 1$ where $q$ is the number of scaling factors initially.

A fractal is ***stochastic*** if it is generated with self-similar recursion and some randomness is introduced into the generating procedure.

A fractal is ***random*** if it has no iteration rule. $\rightarrow$ most fractals occurring in nature

In practice fractal dimension is measured with the ***density*** correlation function:

$$C(\vec{r}) = \frac{1}{V}\sum_{\vec{r}'}\rho(\vec{r} + \vec{r}')\rho(\vec{r}')$$

Where $\rho$ is $1$ if $\vec{r}$ is part of the fractal and otherwise it is $0$. For isotropic objects $C(\vec{r}) = C(r)$.

#### Scaling function

We call $F(x)$ scaling if $F(a\cdot x) = g(a) \cdot F(x)$.

For fractals the density correlation function is scaling.

$$C(r) \propto r^{-\alpha}$$

$$N(L) \propto \int_{0}^{L}C(r)d^{d}r \propto L^{d-\alpha}$$

Therefore $D = d - \alpha$.

#### Self-affine fractals

Direction-dependent transformations are called self-affine transformations. A fractal can be self-affine.

Self-affine functions are $F(bx) \propto b^{H}F(bx)$ where $H > 0$ and it's called the Hölder exponent.

It can be generalized to higher dimensions as well:

$$\vec{X} \rightarrow \vec{O} + \underline{\underline{s}}(\vec{O} - \vec{X})$$ 

Where $\vec{O}$ is the center of the transformation and $\underline{\underline{s}}$ is a direction dependent scaling factor.

For Brownian-motion the average variance of the function is self-affine: $\langle \mid F(t + dt) - F(t) \mid ^{2} \rangle \propto dt^{2H}$ where $H$ is called the roughness exponent. Its connection with the dimension is $H = 2 - D$.

### Multifractals

Meaning of the measure:

- let us consider the power set $P(\Omega)$ of the set $\Omega$. A $\sigma-algebra$ is defined on this since:
    - $\forall E \in P(\Omega) : E^{C} \in P(\Omega)$
    - $E_{1}, E_{2}, ..., E_{i} \in P(\Omega) : E_1 \cup E_2 \cup ... \cup E_i \in P(\Omega)$

- the function $\mu : P(\Omega) \rightarrow \real$ over the power set of $\Omega$ is a measure if $\forall E \in P(\Omega) : \mu(E) \geq 0$ and for disjoint sets $\mu(E + F) = \mu(E) + \mu(F)$

A ***multifractal*** is generated in a recursive fashion as the non-uniform fractal but in addition we assign a measure to its parts where they sum to 1.

Besides the number of covering boxes needed we can also measure the individual boxes since they were given a measure. 

$$p_{i}(\epsilon ) \propto \epsilon^{\alpha_{i}}$$

For multifractals there are infinitely many $\alpha$ values and they correspond to multiple different boxes at different locations of the fractal.

For a fixed $\epsilon$

$$N_{\alpha}(\epsilon) \propto \epsilon^{-f(\alpha)}$$

In the $\epsilon \rightarrow 0$ limit $\frac{lnN(p, \epsilon)}{ln\epsilon} \propto f(\alpha)$ is converging to $f(\alpha)$ which is called the spectrum of the multifractal.

$f(\alpha)$ corresponds to the fractal dimension of boxes for a given $\alpha$. Therefore the multifractal is the union of infinitely many fractals with varying fractal dimension.

The fractal dimension of the multifractal is:

$$D = \max_{\alpha}f(\alpha)$$

The Rényi-entropy of a probability distribution and of order $q$ is defined as:

$$S_{q} = \frac{1}{1-q}\cdot ln\sum_{i}p_{i}^{q}$$

When $q \rightarrow 1$, according to the L'Hospital rule:

$$\lim_{q \rightarrow 1}S_{q} = \lim_{q \rightarrow 1} \frac{\frac{d}{dq}ln\sum_{i}p_i^{q}}{\frac{d}{dq}(1-q)} = - \sum_i p_i lnp_i$$

Covering a multifractal with boxes of linear size $\epsilon$ we can define:

$$\chi_{q}(\epsilon) = \sum_i p_i(\epsilon)^q = e^{(1-q)S_{q}}$$

If $q = 0$ and $p_i > 0$ then $\chi_0(\epsilon) = N(\epsilon) \propto \epsilon^{-D}$.

For fractal and non-fractal objects:

- $\lim_{\epsilon \rightarrow 0}p_i(\epsilon) \propto \epsilon^d$

- $\lim_{\epsilon \rightarrow 0}N(\epsilon, p) \propto \epsilon^{-d}$

- $\lim_{\epsilon \rightarrow 0}\chi_q(\epsilon) \propto \epsilon^{(q-1)d}$

- $\chi_q(\epsilon) \approx N(\epsilon, p) \cdot p_i(\epsilon)^q$

A multifractal is only different in the sense that:

$$\lim_{\epsilon \rightarrow 0}\chi_q(\epsilon) \propto \epsilon^{(q-1)D_q}$$

Where $D_q$ shows a non-trivial dependence on $q$. It can be an alternative definition of multifractals that $D_q$ is not constant but a $q$ dependent function.

$\chi_q(\epsilon)$ can be evaluated as the sum of all sub-fractal corresponding to $\alpha$:

- $\epsilon \rightarrow 0$ then $p_i(\epsilon) \propto \epsilon^{\alpha}$
- the number of boxes $N(\epsilon, p_i) \propto \epsilon^{-f(\alpha)}$
- the contribution to $\chi$ is $N(\epsilon, p_i)\cdot p_i(\epsilon)^q \propto \epsilon^{-f(\alpha) + q\alpha}$

Alpha is either a discrete or a continouos variable:

$$\chi_q(\epsilon) = \sum_i p_i^{q} = \int \epsilon^{-f(\alpha) + q\alpha}d\alpha$$

In the $\epsilon \rightarrow 0$ limit this id dominated by a single sub-fractal so only the maximum of $\epsilon^{-f(\alpha) + q\alpha}$ is considered for $\alpha$:

$$\frac{df(\alpha)}{d\alpha} \Big|_{\alpha = \alpha_q} = q$$

We can now use that:
- $\chi_q \approx \epsilon^{-f(\alpha_q) + q\alpha_q}$
- $\chi_q \approx \epsilon^{(q-1)D_q}$

$\rightarrow$ therefore:

$$(q-1)D_q = q\alpha_q - f(\alpha_q)$$

Deriving by $q$:

$$\frac{d}{dq}\Big[ (q-1)D_q \Big] = \alpha_q + q\frac{d\alpha_q}{dq} - \frac{df(\alpha)}{d\alpha}\Big| _{\alpha = \alpha_q}\frac{d\alpha}{dq} = \alpha_q$$

For multifractals $\chi_{q}(\epsilon) = \sum_{i=1}^{n}\chi_{q, i}(\epsilon)$ which is the sum taken over the sub-fractals. From this:

$$\sum_{i=1}^{n}p_i^q r_i^{(1-q)D_q} = 1$$

#### 2d function - convergent $G_n$

$G_n$ is a sequence of graphs, if it converges, the frequency of any subgraph should converge.

Let $0 \leq W(x, y) \leq 1$ be a symmetric function on the unit square and let's drop $N$ nodes at random. The probability for drawing a link between $i, j$ is given by $W(x_i, y_j).$

$\rightarrow$ for any convergent series of graphs we can find a function $W(x, y)$ that generates the same limiting sub-graph densities. 

In a graph generated by $W(x, y)$:

- the average degree of the nodes: $\langle d \rangle = N \int \int W(x, y)dx dy$
    - therefore it becomes dense for large $N$
    - real networks are sparse

$\rightarrow$ let the linking probability be $p = \frac{W(x, y)}{N}$

#### Self-affine function

The nowhere differentiable, single valued $F(x)$ on the $[0; 1]$ interval is self-affine if:

$$F(x) = b^{-H}F(bx)$$

This means that $F(x)$ is invariant if the horizontal axis is rescaled by $1/b$ and the vertical is by $1/b^H$. Therefore if we have to scale some function by $b_x, b_y$ to make it self-similar then:

$$H = \frac{ln~b_y}{ln~b_x}$$

The simplest surface growth models is ***random deposition***:
- we drop a particle onto the surface at a randomly chosen location and it sticks to the surface at that position

Examining the roughness of the surface yields in an average height:

$$\langle h \rangle = \frac{1}{L}\sum_{i=1}^{L}h_i$$

A simple quantification of roughness is its averaged squared deviation:

$$w = \sqrt{\frac{1}{L}\sum_{i=1}^{L}\Big( h_i - \langle h \rangle \Big)^{2}}$$

In this case the average height is easilly obtained and the height distribtuion is binomial.

$$h = \langle h \rangle = \frac{N}{L}$$

$$p(h_i) = \binom{N}{h_i}p^{h_i}(1-p)^{N-h_i}$$

Here $p(h_i) = 1/L$ and the variance of the column height is:

$$\sigma^{2}(h_i) = w(L, h)^{2} = Np(1-p) = \frac{N}{L}\Big(1 - \frac{1}{L}\Big) = h\Big(1 - \frac{1}{L}\Big)$$

Therefore the roughness is:

$$w(L, h) = \sqrt{h\Big(1 - \frac{1}{L}\Big)}$$

This is not self-affine.

Another method is ***ballistic deposition***:

- particles are dropped vertically and stick to the surface
- however, they can stick from the side as well to other cells

Considerations about $w(L, h)$ in this case:

- if $h$ is large enough then $w(h, L)$ is only $L$ dependent and according to self-affinity $w(L, h) \propto L^{\alpha}$, where $\alpha = H$
- when $h$ is small it it only depends on $h$ $w(L, h) \propto h^{\beta}$

$\rightarrow$ this can be united in:

$$w(L, h) \propto L^{\alpha}f\Big( \frac{h}{L^{z}} \Big)$$

Here $f(x)$ is constant for large values and $\propto x^{\beta}$ for small values.

$z$ is the dynamic exponent, $\alpha$ is the roughness exponent.

The ***Eden-model*** is the following:
- a row of cells is filled at start
- at every iteration we choose an empty cell neighbouring a filled cell and fill it as well
    - version A: uniform random choice
    - version B: we choose uniformly between links between empty and filled cells
    - version C: filled cell at boundary, random choise of one of its neighbors

#### Dynamic scaling

The fundamental concept of dynamic scaling is that

$$w(L, t) = L^\alpha f\Big( \frac{t}{L^{z}} \Big)$$

The surface can be characterised with the help of a correlation function:

$$\hat{h}(\vec{r}, t) := h(\vec{r}, t) - \langle h(\vec{r}, t) \rangle_{\vec{r}}$$

$$C(\vec{r}, t) = \langle \mid \hat{h}(\vec{r}, t) - \hat{h}(\vec{r} + \vec{r'}, t + t') \mid \rangle _{\vec{r}', t'}$$

Let us assume that it depends only on the distance and that for $t >> 1$ the scaling is already stationary then $C \propto r^{\alpha}$ and for fixed $r$ and $t << 1$ we can assume that $C \propto t^\beta$.

$$C(r, t) \propto r^\alpha f\Big( \frac{t}{r^z} \Big)$$

$z$ is the previously discussed dynamic exponent.