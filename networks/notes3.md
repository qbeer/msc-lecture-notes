### The configuration model

The goal is to generate N nodes with a given $p(k)$ degree distribution.We are drawing $N$ nodes from the $p(k)$ distribution and then we set up the links between them.

The hard part is the node connecting procedure becasue it has to be randomized as well.

### The hidden variable model

Real networks are not completely random, thus we are interested in by how much they are described by their parameters.

Let's assumae that $\rho(h)$ is the hidden parameter distribution and $r(h, h')$ are the linking probabilities. For each of $N$ nodes we draw its hidden variable from $\rho$ and then the connecting probability of nodes $i, j$:

$$P(i~-~j) ~=~ r(h_i, h_j)$$

Given that a degree has a hidden variable $h$ what's the probability of it having $k$ degreess $P(k | h)$:

$$p(k) = \sum_{h}P(k | h)\rho(h)$$

So $\langle k \rangle$ can be calculated:

$$\langle k \rangle = \sum_{k}kp(k) = \sum_{k}k\sum_{h}P(k|h)\rho(h) = \sum_{h}\rho(h)\langle k(h) \rangle$$

Let $P^{(h)}(k_i, h_i)$ denote the probability that a node with hidden variable $h$ is connected to a node with hidden variable $h_i$ and degree $k_i$. Therefore $P(k, h)$ can be expressed as the product of its neighbors:

$$P(h, k) = \sum_{k_1, ..., k_c}P^{(h)}(k_1, h_1)\cdot ... \cdot P^{(h)}(k_c, h_c)\delta_{k_1 + k_2 + ... + k_c, k}$$

Since links are established with probability $r(h_i, h_j)$ therefore:

$$P^{(h)}(k_i, h_i) = \binom{N_i}{k_i}r(h_i, h)^{k_i} (1 - r(h_i, h))^{N_i - k_i}$$

Where $N_i = \rho(h_i)N$ are the number of nodes with hidden variable $h$. The generating function of this distribution is:

$$G^{(h)}_{i}(z) ~=~ \sum_{k_{i}}z^{k_i} \binom{N_i}{k_i}r(h_i, h)^{k_i} (1 - r(h_i, h))^{N_i - k_i}$$

And using the binomial theorem this results in:

$$G^{(h)}_{i}(z) ~=~ \Big[1 - (1 - z)r(h_i, h)\Big]^{N_i}$$

Since $k = \sum_{k_i}k_i$ and $P(k | h)$ is the conolution of $P^{(h)}(k_i, h_i)$ distributions:

$$G(z) = \prod_{i}G_{i}^{(h)}(z) = \prod_{i}\Big[1 - (1 - z)r(h_i, h)\Big]^{N_i}$$

Taking the logarithm of this and using that $N_{i} = \rho(h)N$:

$$lnG(z) = N\sum_{h'}\rho(h')ln\Big[1 - (1 - z)r(h, h')\Big]$$

For $z = 1$ G is $1$ since that $(1-z)$ multiplicative factor. Therefore $[lnG(z)]' |_{z=1} = G'(z)|_{z = 1}$. we need this because the avarage degree distribution of a node with hidden variable $h$ was previous denoted as $\langle k(h) \rangle$ corresponds to this derivatie.

$$\langle k(h) \rangle ~=~ G'(z)|_{z=1} = [lnG(z)]'|_{z=1} ~=~ N\sum_{h'}\rho(h')\frac{r(h, h')}{1 - (1-z)r(h, h')}\Big|_{z = 1}$$

At $z=1$ this is simply takes the form:

$$\langle k(h) \rangle ~=~ N\sum_{h'}\rho(h')r(h, h')$$

***If we want to generate sparse networks then $\langle k(h) \rangle$ should be indenpendent of $N$!*** Thus we should define $r(h, h') = C(h,h')/N$.

$$lnG(z) = N\sum_{h'}\rho(h')ln\Big[1 - (1 - z)r(h, h')\Big] \approx \sum_{h'}\rho(h')(z - 1)C(h, h')$$

Where $\sum_{h'}\rho(h')C(h, h')$ is the avarage degree with hidden variable $h$ and therefore the generating function is very simple:

$$G(z) = e^{(z-1)\langle k(h)\rangle}$$

From previous studies it is know that an exponential generating function corresponds to a Poissin point mass function.

$$P(k | h) = \frac{\langle k(h) \rangle^{k}}{k!}e^{-\langle k(h) \rangle}$$

We can move on with this but I don't see the point of defining more joint and porbablities to prove nothing with it at the end.

### Robustness and percolation

A system is called robust if many of its nodes are removed but can still function properly.

We described previously percolation in the Erdős-Rényi model, where at $\langle k \rangle \geq 1$ a giant component forms in the network. We are now removing nodes, so approaching the problem from the other end and checking when the system goes to the 'phase transition'.

We already calculated the expected component size in the generating function formalism which is model independent.

$$\langle S \rangle = 1 + \frac{\langle k \rangle}{1 - G'_{q}(1)}$$.

Where $G_{q}(x)$ can be expressed based on degree distribution where $q(k)$ was the distribution to be able to procedd at one end of a link on $k$ other links from the end node. We normalized it already:

$$q(k) = \frac{(k + 1)\cdot p(k+1)}{\langle k \rangle}$$

And we defined $G_{q}(x)$ with this as well:

$$G_{q}(x) = \frac{1}{\langle k \rangle}\sum_{l=1}^{\infty}lp(l)x^{l-1}$$

Deriving this we can acquire:

$$G'_{q}(1) = \frac{\langle k^{2} \rangle - \langle k \rangle}{\langle k \rangle}$$

At the critical point this results in $\langle k^{2}\rangle /\langle k\rangle = 2$. A general equation for the existence of the giant component is:

$$\frac{\langle k^{2} \rangle}{\langle k \rangle} \geq 2$$

For the Erdős-Rényi model we derived this, in scale-free networks $\langle k^2 \rangle$ is diverging thus it has a giant component independently from the degree distribution.

#### How to used this to define network damage?

Removing $f$ fraction of nodes modifies $\langle k \rangle, \langle k^2 \rangle$ to $\langle k' \rangle, \langle k'^{~2} \rangle$ but if $f \ll 1$ then it is easilly:

$$\langle k \rangle\cdot (1 - f) = \langle k' \rangle$$

A node with $k$ degrees will loose on average $q$ neighbors.

$$P_{k} = \binom{k}{q}f^{q}(1-f)^{k-q}$$

Therefore the new degree should be $k' = k - q$:

$$P(k \rightarrow k') = \binom{k}{k'}f^{k-k'}(1- f)^{k'}$$

Therefore the new degree distribution is:

$$p'(k') = \sum_{k=k'}^{\infty}p(k')P(k \rightarrow k')$$

The new average degree can be calculated as $\langle k' \rangle = \sum_{k'}k'p'(k')$ which will correspond to $(1-f)\cdot \langle k \rangle$. The modified $\langle k'^{~2} \rangle$ will correspond to $(1-f)^{2}\langle k(k-1) \rangle$. The calculations are tricky and the summations are replaced on a trianle instead of calculating both of them to infinity.

Substituting this to the giant component formation inequality one can acaquire after some easy simplifications that the critical fraction of removed nodes is:

$$f_c = 1 - \frac{1}{\frac{\langle k^{2}\rangle}{\langle k \rangle} - 1}$$

In the Erdős-Rényi model we know that we have to remove a fraction of nodes until $\langle k' \rangle$ becomes 1 and then the giant component disappears therefore the system collapses. In scale-free networks $f_{c} \rightarrow 1$ therefore they are extremely robust agains node removal. Real world networks almost behave like this, thus making them not so vulnerable to random node removal but very much so to ***targeted attacks***. Killing the hubs results in failure.

### Spreading on networks - epidemics models

**S**usceptible - **I**nfected - **R**emoved

Some diseases like the flu are modeled as SIS, some like SIR (plague).

The model assumptions for epidemics are the following:
- homogenous network, everyone has more or less $\langle k \rangle$ connections
- every node can be linked to an infected node with the same probability
- spreading time $\lambda$, probability of recovery $\mu$, at $t = 0$ there are $\rho_{0}$ fraction of infected nodes

A differential equation for $\rho(t)$ can be formulated:

$$\frac{\partial \rho}{\partial t} = \lambda \langle k \rangle \rho (1 - \rho) - \mu \rho$$

The number of links to the infected nodes at each timestep is $\rho \langle k \rangle$ while the disease can spread to a $(1-\rho)$ fraction of healty nodes with probability $\lambda$ and with probability $\mu$ some of the infected can heal.

Solving the equation results in:

$$\rho(t) = \Big(1 - \frac{\mu}{\lambda \langle k \rangle}\Big)\cdot \frac{ce^{-(\lambda \langle k \rangle - \mu)t}}{1 + ce^{-(\lambda \langle k \rangle - \mu)t}}$$

If $\lambda \langle k \rangle > \mu$, at $t = 0$ it is $\rho_{0}$ therefore $c$ can be acquired and at $t \rightarrow \infty$ the fraction of infected nodes is $1 - \frac{\mu}{\lambda \langle k \rangle}$ $\rightarrow$ exponential outbreak. Otherwise their is exponential decay.

The threshold is at $\lambda = \mu / \langle k \rangle$. Assuming that $\mu = 1$ this becomes very intuitive since a node can infect its neighbors with uniform probability at each timestep.

Assuming that the probability of a link pointing to an infected node is $\Gamma$ given that $\rho_{k}$ denotes the infected fraction of nodes with $k$ connections. Basically the same differential equation can be deduced as before for this fraction:

$$\frac{\partial \rho_{k}}{\partial t} = \lambda k \Gamma [1 - \rho_{k}] - \mu \rho_{k}$$

Given that we reach a stationary phase the equation simplifies and we get:

$$\rho_{k} = \frac{\lambda k \Gamma}{\mu + \lambda k \Gamma}$$

We know that the probability of a randomly chosen link having $k$ nodes at one end is:

$$P_{k} = \frac{k p(k)}{\langle k \rangle}$$

Substituting this back to the equation for $\Gamma = \sum_{k}\rho_{k}P_{k}$ results in a self-consistent equation for $\Gamma$.

This can be solved graphically and from the condition of having a non-trivial solution (derivative according to $\Gamma$) we get:

$$\frac{\lambda}{\mu} \geq \frac{\langle k \rangle}{\langle k^{2} \rangle}$$

For scale-free networks with $\gamma < 3$ this results in zero epidemic threshold since $\langle k^2 \rangle \rightarrow \infty$.

The result of $\lambda_{c} = 0$ is that no matter how weak the infection is it will prevail.

### Network motifs and communities

A motif is small, connected subgraph in which the configuration of the links is predefined. They have a key role in information processing and controlling.

$$z(m_i) ~=~ \frac{\langle m_i \rangle _{real} - \langle m_{i} \rangle _{random}}{\sigma_{rand}}$$

Communites, groups, clusters and modules are more interconnected parts with no widely accepted definitions.

There are several community finding methods:

- ***hierarchical clustering*** : *dendogram*, finds groups/clusters/communities based on similarity - it is important *where to make the cut* based on similarity

- ***Girvan-Newman method*** : 1) calculating the betweeness of the links 2) delete the ones with the biggest $b$ and if disconnected parts emerge update the dendogram $\rightarrow$ re-iterate

#### How to measure the quality of the communities?

Comparing them to random partitions seems to be a good idea.
- high quality: more links than expected
- low quality: less than expected

We should compare it to the configurational model. This way the degree distribution can be kept.