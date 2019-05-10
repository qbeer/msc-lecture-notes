# Network models

## The Erdős-Rényi model

The Erdős-Rényi model is based on generating a network with N nodes and distributing M links between them evenly or formalised othewrwise, linking the nodes with probability $p$.

It was already discussed here that a two nodes are linked with probability $p$ and not linked with probability $1-p$ therefore resulting in a Binomial degree distribution and in the $N \rightarrow \infty$ limit in a Poisson degree distribution where $<k> = Np$.

The variance can be calculated as well. It can be tiresome to go through $\sum_{k = 0}^{N}k^{2} \cdot Binom(k, N)$

$$
    <k^{2}> ~ = ~ \sum_{k=0}^{N} k^{2}\frac{N!}{(N-k)!k!}p^{k}(1-p)^{N-k}
$$

For this first see:

$$
    <k> ~ = ~ \sum_{k=0}^{N} k\frac{N!}{(N-k)!k!}p^{k}(1-p)^{N-k} = Np
$$

Reparametrizing the equation for $<k^{2}>$ :

$$
    <k^{2}> ~ = Np(N-1)p + Np
$$

Thus the variance is:

$$
    Var(k) ~ = ~ <k^{2}> - <k>^{2} = Np(1-p) 
$$

In the $N \rightarrow \infty$ limit $p \rightarrow 0$ while the $<k>$ is constant so therefore the variance becomes negligeble. A large Erdős-Rényi graph is extremely homogenous with no outliers.

Also, all the nodes have approximately the same clustering coefficient so $C_{i} \approx <C>$. It can be interpreted as probability of neighbors $i$ being connected which corresponds to $p = <C>$.

Giant component in the Erdős-Rényi model:
- Given that the giant component $S_{1}$ has a relative size $S = \frac{S_{1}}{N}$ the fraction of the nodes that are not in the giant component is $u = 1 - S$.
- Taking one node not in the giant component $i$ we can say about its connection to $j$ the following:
    - not connected to $i$ directly with probability $(1-p)$
    - not in the giant component with prob. $u\cdot p$
- Therefore we found that if $i$ is not connected to any other point or connected but not in the giant component for $N-1$ points with probability:
    - $(1-p + pu)^{N-1}$ which should correspond to not being in the giant component $u$

From this equation we can approximate in the large $N$ limit that $<k> = 1$ is the critical avarage node degree above which a giant component forms.

### Generating function

We have the degree distribution $p(k)$ and we assume no degree correlation (we are in a random network), we approach the problem from the state where the network can be assumed sparse and local tree-like.

The generating function:

$$
    G_{X}(z) = \sum_{k=0}^{\infty}z^{k}p_{X}(k)
$$

Where:

$$
    p_{X}(k) = \frac{1}{k!}\frac{dG_{X}(z)}{dz^{k}} \Big| _{z=0}
$$

And the m$th$ moment is:

$$
    <X^{m}> ~ = ~ <k^{m}> ~ = ~ \Big[ z\frac{d}{dz} \Big]^{m} G_{X}(z) \Big| _{z = 1}
$$

For $n$ intependent variables $Z = \sum_{i = 1}^{n}X_{i}$:

$$
    G_{Z}(x) = \prod_{i=1}^{n}G_{X_{i}}(x)
$$

$p(k)$ is the degree distribution function, $I(k)$ is the distribution function of a randomly chosen node being in component of size $k$, while $H(k)$ is the distribution function of a link being connected to a component of size $k$ on one end.

$H_{m}(k)$ should denote the probability distribution of randomly chosing $m$ links which on one end sum up to $k$ in component size.

***The idea behind creating these PDFs a component can be separated in such a way.***

1. Choosing a node with $m$ links the probability of the links to sum up to size $k-1$. The node and its neighbors therefore sum up to $k$ in size and that distribution is $I(k)$:

$$
    I(k) = \sum_{m=0}^{\infty}p(m)H_{m}(k-1)
$$

Taking the generating function of both sides:

$$
    G_{I}(x) ~ = ~ \sum_{k=0}^{\infty}\sum_{m=0}^{\infty}p(m)H_{m}(k-1)x^{k}
$$ 

Where:

$$
    H_{m}(k-1) = \frac{1}{(k-1)!}\frac{d^{k-1}}{dx^{k-1}}G_{H, m}(x) |  _{x=0} ~ x^{k}
$$

Since $H_{m}(k)$ was chosen that $m$ links to sum to $k$ in compoennt size, therefore $G_{H, m}(x) = [G_{H}(x)]^{m}$, substituting this into $G_{I}(x)$:

$$
    G_{I}(x) = \sum_{m=0}^{\infty}p(m)[G_{H}(x)]^{m}x = xG(G_{H}(x))
$$

Where $G$ is the degree distribution's generating function. From this we can get the mean component size in a random graph:

$$
    <S> = G'_{I}(1) = [xG(G_{H}(x))]'|_{x=1} =  G(G_{I}(1)) + G'(1)G'_{H}(1)
$$

Where $G'(1) ~ = ~ <k>$ but and for calculating $G'_{H}(1)$ we should see:

$$
    H(k) = \sum_{m=0}^{\infty}q(m)H_{m}(k-1)
$$

Where $q(k)$ is the probability distribtuion of a randomly choosen link to be able to proceed to $k$ direction at one end.

Taking the generating function on both sides and making the same assumptions as before:

$$
    G_{H}(x) = xG_{q}(G_{H}(x))
$$

And therefore the derivative can be translated into:

$$
    G'_{H}(1) = \frac{1}{1 - G'_{q}(x)}
$$

So we find that the critical point should be at $G'_{q}(1) = 1$ since:

$$
    <S> ~ =  ~ 1 + <k>G'_{H}(1) ~ = ~ 1 + \frac{1}{1 - G'_{q}(1)} 
$$

We can actually calculate $q(k)$ by simply saying that:

$$
    P(~node~with~degree~~\underline{k}~~link~at~one~end) ~ = ~\frac{kN_{k}}{\sum_{k'}k'N_{k'}} ~ = ~ \frac{kp(k)}{<k>} 
$$

There are $N_{k}$ nodes with $k$ degrees therefore there are $N_{k}\cdot k$ links with a $k$ degree node at one end. $q(k)$ denotes the probability of a link to have a node at one end with $k$ other connections so basically the probability of having a node with a $k+1$ degree node at one end:

$$
    q(k) ~ = ~ \frac{k+1}{<k>}p(k+1)
$$

And the generating function of this is simple:

$$
    G_{q}(x) ~ = ~ \sum_{k=0}^{\infty}x^{k}q(k) ~ = ~ \sum_{k=0}^{\infty}x^{k}\frac{k+1}{<k>}p(k+1) ~ = ~ \frac{1}{<k>}\sum_{l=1}^{\infty}lp(l)x^{l-1} ~ = ~ \frac{G'(x)}{<k>}
$$

We are not done yet, introducing $q_{m}(k)$ as the probability of choosing $m$ random links that at one end sum to $k$ other connections. Therefore the number of second neighbors can be calculated:

$$
    n_{second}(k) ~ = ~ \sum_{m=0}^{\infty}p(m)q_{m}(x)
$$

Taking the generating function of both sides:

$$
    G_{second}(x) ~ = ~ \sum_{k=0}^{\infty}\sum_{m=0}^{\infty}p(m)q_{m}(x)x^{k} ~ = ~ ... ~ = ~ G(G_{q}(x))
$$

Finally:

$$
    <n_{second}> ~ = ~ G'_{second}(1) ~ = ~ <k>G'_{q}(1) ~ \rightarrow ~ G'_{q}(1) ~ = ~ \frac{<n_{second}>}{<k>}  
$$

After all we arrive at the concluding formula regarding the giant component size:

$$
    <S> ~ =  ~ 1 + \frac{<k>}{1 - \frac{<n_{second}>}{<k>}} ~ = ~ 1 + \frac{<n_{second}>^{2}}{<k> - <n_{second}>}
$$

Therefore if $<k> ~~ < ~~ <n_{second}>$ a giant component form, otherwise the system is critical or smaller clusters form only.

It was shown that:

$$
    <n_{second}> ~ = ~ <k>G'_{q}(1) ~ = ~ <k>\sum_{k=0}^{\infty}kq(k) ~ = ~ ... ~ = ~ <k^{2}> - <k>
$$

***For scale-free networks $<k^{2}>$ is always divergent therefore they always contain a giant component!***

The Erdős-Rényi model does not compare well to real networks, it does not show scale-free behaviour ( *no power law degree distibution* ), doesn't have a large clustering coefficient ( $<C> ~ \rightarrow ~ 0$ )and only shows the small-world effect ( small $<l>$ ). **It is and important reference system but not more.**

## The Watts-Strogatz model

It tries to make small-world and local clustering co-exist in a simple random graph by some slight modifications.

### The model

Start from a regular ring of nodes in which the first $q$ neighbors are linked and then rewire each link randomly with probability $\beta$.

When $\beta ~ = ~ 0$ for large $N$:

$$
    <l> ~=~ \frac{N}{4q}
$$

And:

$$
    <C> ~=~ C = \frac{q(q-1)\frac{1}{3}}{q(2q-1)} ~=~ \frac{3q-3}{4q-2}
$$

Also when $\beta ~=~ 0$ we get back the totally random Erdős-Rényi model:

$$
    <l> ~\propto~ logN ~~and~~ <C> ~=~ \frac{2q}{N-1}
$$

There are a range of $\beta$ values when $<l>$ is relatively low while $C$ is still very high, meaning ***high clustering and small wolrd properties***.

    Takeaway:
    It takes a lot of randomness to ruin the clustering, but a very small amount to overcome locality.

Number of random links in the system: $\beta q N$. What happens when $\beta q N << 1$?
Basically there will be not many random links that can change the graph thus $<l> ~\propto~ N$. In the case when $\beta q N >> 1$ then the system becomes random and $<l> ~\propto~ lnN$. Approximating the transition at $\beta_{critical} q N = 1$!

It can be shown that a scaling function where:

$$
    l = N \cdot f(N/N_{critical}) \\
    f(x) = \Big( const. ~ x << 1, ~~~ ln(x)/x ~ x >> 1 \Big)
$$

From numerical studies $N_{critical} ~\propto~ \beta^{-\tau}$, therefore:

$$
    l = N\cdot f(\beta^{\tau}N)
$$

## The Barabási-Albert model

The problem was still open until the Barabási-Albert model of how to generate scale-free random graphs in a simple way.

Motivated by real networks the network size is *not static*, ***the system grows at each time step***.

A new node can be connected random or can be connected to high degree nodes with a larger probability. $~\rightarrow~$ very logical based on real networks, it is called ***preferential attachement***.

    Generating procedure:

    Adding one node with m links at a time-step (the initial core should be at least containing m nodes) and choosing node i with probability that is proportional to its degree.

For a large $t$ timestep:
- $N ~\propto~ t$ and $M ~\propto~ mt$
- the probability of coohsing node $i$ is:

$$
    P_{i} = \frac{k_{i}}{\sum_{j}k_{j}}
$$

- with this probability $m$ new links could be added to node $i$ therefore the change in its degree can be approximated by:

$$
    \Delta k_{i} ~\approx~ mP_{i}\Delta t
$$

From which the differential equation:

$$
    \frac{\partial k_{i}}{\partial t} ~=~ m\frac{k_{i}}{\sum_{j}k_{j}}
$$

For large $t$ the sum of the degrees is twice the number of links $\sum_{j}k_{j} ~=~ 2M ~=~= 2mt$ therefore the differential equation is very simle and can be analitically solved:

$$
    \frac{\partial k_{i}}{\partial t} ~=~ \frac{k_{i}}{2t} ~~~~~ \rightarrow k_{i}(t) ~=~ C\sqrt{t}
$$

Given that at timestep $t_{i}$ the degree of node $i$ is $m$ the constant can be eliminated as $C = m\cdot t_{i}^{-\frac{1}{2}}$.

We want to calculate the degree distibution function and expect it to be scale-free. The probabilit of finding a node with degree at least $k$ is:

$$
    P(k) = P(k_{i} < k) = P(m t_{i}^{-\frac{1}{2}}\sqrt{t} < k) = P\Big(\frac{t}{t_{i}} < \Big(\frac{k}{m}\Big)^{2}\Big)
$$ 

Where:

$$
    P(k) = P\Big(\frac{t_{i}}{t} > \Big(\frac{m}{k}\Big)^{2}\Big)
$$

So the relative length of the time steps $t_{i}/t$ tells that:

$$
    P(k) ~=~ 1 - \Big(\frac{m}{k}\Big)^{2}
$$

From the cumulative distibution function we can get the degree-distribution by simply derivating by $k$ not considering that the problem is discrete. Therefore:

$$
    p(k) ~=~ 2m^{2}k^{-3}
$$ 

Which is a scale-free distibution with $\gamma ~=~ 3$.

If links are connected with uniform porbability instead of preferential attachement $P_{i} = 1/N ~\approx~ 1/t$:

$$
    \frac{\partial k_{i}}{\partial t} ~=~ mP_{i} = \frac{m}{t} ~~~ \rightarrow ~~ k_{i}(t) = m\cdot ln(t/t_{i}) + m
$$

Making the same chain of calculations this result in a degree distibution that is not scale free $p_{k} = (e^{1-k/m})/m$, therefore preferential attachement is truly necessary.

To calculate the clustering coefficient in the Barabási-Albert model we should ask the quation of what the probability is that node $i$ intorduced at $t_{i}$ is connected to node $j$ introduced at $t_{j}$.

$$
    P(i - j) = mP_{i} = m\frac{k_{i}}{2mt} = \frac{k_{i}}{2t} = m\Big(\frac{t_{j}}{t_{i}}\Big)^{1/2}\frac{1}{2t_{j}} = \frac{m}{2}(t_{i}t_{j})^{-1/2}
$$

What is the expected number of links between a nodes links at the end of the generating process which was introduced at timestep $t_{l}$?

$$
    n_{l} ~=~ \frac{1}{2}\sum_{t_i = 1}^{N}\sum_{t_j = 1}^{N}P(l-i)P(l-j)P(i-j) = ... = \frac{m^{3}}{16t_l}(lnN)^{2}
$$

With words: if $l$ is linked to $j$ and it is linked to $i$ the probability of $i$ being linked to $j$ is $P(i-j)$ and it is true for all the links of $l$ and therefore the summation, taking the continous limit and actually integrating in the $...$ process one can acquire the result above.

The number of links between the neighbors of $l$ is $\approx ~ \frac{k^{2}_l}{2} = \frac{m^{2}N}{2t_{l}}$ in $t = N$. The clustering coefficient is the number of links between the neighbors of $l$ in the paths where $l$ is present divided by all the edges.

$$
    C = \frac{m^{3}}{16t_l}(lnN)^{2}\frac{2t_l}{m^{2}N} = \frac{m(lnN)^{2}}{8N}
$$

We can see that it is not $l$ dependent at all. This is decaying slower with $N$ than the Erdős-Rényi model, however, in real networks there is no decay at all.

Preferential attachement can be measured by simply observing the system for $\Delta t$ amount of time.

$$
    \frac{\Delta k_i}{\Delta t} ~\propto~ P(k_{i})
$$

Taking the integral of $P(k)$ for all degrees in order to reduce noise in real networks.

$$
    \kappa (k) = \int P(k)dk
$$

If $\kappa$ is proportional to $k$ then there is no preferential attachement if it is proportional to $k^{2}$ then there is.

The problem with the Barabási-Albert model so far is that in real networks $\gamma$ is $\in ]2;3[$ while here it is $3$. This results in oldest nodes having the most connections which is not true for real networks either.

We can introduce a finesse $a$, a parameter that makes $\gamma$ tunable by modifying preferential attachement's $P_{i} \propto k_{i} - a$ probability.

Going to the same process and taking the large $N$ limit:

$$
    P_{i} ~=~ \frac{k_{i} - a}{\sum_{j}(k_{j} - a)} = \frac{k_{i} - a}{2M - Na}
$$

After all the differential equation results in:

$$
    k_{i}(t) = m\cdot\Big(\frac{t}{t_{i}}\Big)^{\frac{1}{2 - a/m}} ~~\rightarrow ~~ p(k) = 2m^{2}k^{-3 + a/m}
$$

This can also be done with not an additive but a multiplicative finesse parameter $\eta_{i}$ which is drawn from a $\rho(\eta)$ distribution.

- *scale-free* : if $\rho(\eta) = \delta(\eta - \eta_{0})$ results in the original Barabási-Albert model
- *fit-gets-rich* : nodes have different $\eta$, $\beta$ gets larger with $\eta$ and it is scale-free and in the long run the largest hubs are the fittest
- *Bose-Einsteinn condensation* : winner takes all
