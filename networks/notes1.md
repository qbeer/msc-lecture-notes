# Networks

***Complex system*** : composed of interconnected parts that as a whole exhibit one or more properties not obvious from the properties of the individul parts

## Graphs and networks
-----------------------------------------------------------

*Graph* : vertices, edges, directed or not, weighted or not

*Network* : nodes, links, flows, epidemics, growth, rewiring, etc.

The next step from graphs to networks is complex systems which we model with networks!

#### Graph types
- simple graph: only single connections, no self loops
- multi graph: multiple connections, no self loops
- pseudo graph: self loops allowed
- directed graph: directed links
- undirected graph: undirected links
- weighted graph: weighted links
- unweighted graph: binary links
- bi-partite graph: two types of nodes, different are linked

Sotring it on computer can be done in an adjecency matrix (not memory efficient) or in an adjecency list (linked list).

$$A_{ij} = \Big( 1 ~ if ~ i ~ \rightarrow j ~, ~ 0 ~ otherwise \Big)$$

For undirected graphs **A** is symmetric. Multiplying a position vector with **A** gives the neighbors of that point.

#### Sparseness
A network is sparse in the $N \rightarrow \infty$ limit if the number of links $M \propto N$.

A networks is dense in the $N \rightarrow \infty$ limit if the number of links $M \propto N^{2}$.

In the dense case the average connections per node goes to infinity. ($< k > = \frac{2M}{N}$).

*Most real networks are sparse.* Therefore the probability of two nodes being linked is negligible, goes to 0 in the $N \rightarrow \infty$ limit.

### Basics of networks

- number of connections per node: $k_{i}$, if directed $k_{i}^{in}$, $k_{i}^{out}$
- weighted networks have node strenght: $s_{i}$, a node's strenght is the biggest weight of the edges connecting it to other nodes
- avarage degree: $< k > = \frac{1}{N}\sum_{i = 1}^{N}k_{i} = \frac{2M}{N}$, for directed networks $< k_{in} > = < k_{out} > = \frac{M}{N}$
- clustering coefficient: $C_{i} = \frac{2e_{i}}{k_{i}(k_{i} - 1)}$ where $e_{i}$ is the number of links between its neighbors, in the directed case $C_{i}/2 \rightarrow C_{i}$, one can also the the average clustering coeff. of a networks as well

    - $< k >$ is the measure of global densitiy of the network, therefore $< C >$ is a local density measure

#### Pathology
- Cycle: path with same start and end node
- Eulerian path: a path traversing each link exactly onces
- Hamiltonian path: a path visiting eaxh node exactly once
- ***distance*** : $l_{ij}$ minimum number of steps it takes to reach j from i, in undirected networks this matrix is symmetric and if j cannot be reached from i then $l_{ij} = \infty$

- avarage shortest path lenght: $< l > = \frac{2}{N(N-1)}\sum_{i < j}l_{ij}$ and for a given node $< l_{i} > = \frac{1}{N - 1}\sum_{j}l_{ij}$

    - for sparse networks where N is large and $< k >$ is small a good estimate is $< l > = \frac{ln N}{ln < k >}$ 
    - ***small world property*** : $< l > \propto lnN$ this always results in a small average shortest path lenght for big system sizes

- diameter: $D = max_{ij} \{ l_{ij} \}$
- ***centrality*** : $C_{c}(i) = \frac{1}{<l_{i}>}$ where unreachable nodes are not considered in the sum $\rightarrow$ intuitively a node closer to the rest of the network is more central

- ***betweenness*** : of a node or link is equal to the number of shortest path passing through a given node or link, if multiple shortest paths are possible between a given pair of nodes then they are given equal weidghts and adding up to one:
 
 $$b_{i} = \sum_{v \neq i, s \neq i} \frac{\sigma_{sv}(i)}{\sigma_{sv}}$$

#### Algorithms
- breadth first search
- depth first search
- Dijkstra's algorithm

#### PageRank

The importance of a node is affected by the number of in-neighbors and the importance of the in-neighbors.

Assume an iteraive process, each node distributes its PageRank evenly at each timestep between its neighbors.

$$r_{i}(t + 1) = \sum_{j ~ \in ~ Negihbors(i)} \frac{r_{j}(t)}{k_{j}}$$

Total PageRank of the system is therefore conserved since it is only being redistributed at each timestep. For simplicity one should scale it to 1.

If we intruduce **dampening** with probability $p_{d}$:

$$r_{i}(t + 1) = \frac{p_{d}}{N} + (1 - p_{d})\sum_{j ~ \in ~ Negihbors(i)} \frac{r_{j}(t)}{k_{j}}$$

#### Components

A component is an undirected network that corresponds to a maximal set of nodes in which a path exists between any pair of nodes.

***Most networks contain a giant component.***

A giant component in a network is a subsystem which relative size remains finite in the $N \rightarrow \infty$ limit.

$$lim_{N \rightarrow \infty} \frac{S_{1}}{N} > 0$$

Can be generalized to the directed case:
- *strongly connected component*: is a maximal set of nodes in which a directed path exists between any pair of nodes
- *weakly connected component*:  is a maximal set of nodes in which an undirected path exist between any pair of nodes

### Advacned network characteristics

- degree distribution $p(k)$
    - for a finite netork with N nodes: $p(k) = \frac{N_{k}}{N}$ where $N_{k}$ is the number of nodes with degree k
        - for an Erdős-Rényi graph where links are established with probability $p$ and not established with probablity $1-p$ for small network size N the degree dstribution is approximately *binomial* but in the $N \rightarrow \infty$ limit it is a *Poisson-distribution* with $<k> = Np$
        
        $$p(j) \approx \frac{<k>^{j}}{j!}e^{-<k>}$$

### Scale-free networks

A network is ***scale-free*** if the tail of its degree distribution decays as a power-law, where $\gamma$ is the node degree decay exponent:

$$p(k) \propto k^{-\gamma}$$

It is called scale free because scaling functions are defined as:

$$F(a\cdot x) = g(a)\cdot F(x)$$

and power laws are scaling.

Wealth densitiy is a scaling probability density ( $\rho(x) \propto x^{-\alpha}$ ), this is called the Pareto-distribution.

Also there is no typical degree in scale-free networks as a result of being scaling.

Normalizing the scale-free degree distribution:

$$
    \int_{k_{min}}^{\infty} p(k)dk = \int_{k_{min}}^{\infty} Ck^{-\gamma}dk = 1
$$

Therefore $C$ is: 

$$
     C = \frac{\gamma - 1}{k_{min}^{1 - \gamma}}
$$

As a result:

$$
 p(k) = (\gamma - 1)\frac{k^{-\gamma}}{k_{min}^{1 - \gamma}}
$$

Scale-freeness implies large ***hubs*** in the network.

In physics being scale-free usually occurs at phase transitions at critical points and often suggests divergence. The moments of p(k) are divergent for a scale-free system when $m > \gamma - 1$.

***Most real world networks are scale-free*** and their node degree decay factor ($\gamma$) is below 3 thus $<k^{2}>$ is divergent in the $N \rightarrow \infty$ limit, therefore the **standard deviation is divergent** as well!

If $\gamma$ is in the range $]2; 3[$ the system behaves ultra-small world and the scale-free property is relevant.

- assortative network: small degree nodes tend to link to small degree nodes and hubs tend to link to each other
- diasortative network: hubs do not link, they connect to small degree nodes
- neutral network: random

Let $P(k' | k)$ denote the conditional probability of finding a node with degree $k'$ from a node with degree $k$.
From the definition of conditional probability:

$$
    P(k' | k ) = \frac{P(k, k')}{P(k)} 
$$

Where it is easier to count all the nodes denoted with $E_{k, k'}$ and then dividing by the nodes that all have $k$ degrees $\sum_{k'}E_{k, k'}$.

$$
    P(k' | k) = \frac{E_{k, k'}}{\sum_{k'}E_{k, k'}}
$$

If we divide $E_{k, k'}$ (the matrix of number of links between degree $k$, $k'$ node pairs) with the total number of links in the networks beging $2M$ we can get $P(k, k')$ which obviously sums to one for both degrees:

$$
    \sum_{k, k'} P(k, k') = 1
$$

$$
    \sum_{k'} P(k, k') = q_{k} \quad \sum_{k} P(k, k') = q_{k'}
$$

The meaning of $q_{k}$ is the probability of finding a node on the end of a link with degree $k$. This is obviously proportional to the number of links from nodes with degree $k$:

$$
    q_{k} \propto kN_{k} \quad \rightarrow \quad q_{k} = \frac{kN_{k}}{\sum_{k'}k'N_{k'}} = \frac{kp(k)N}{\sum_{k'}k'p(k')N} = \frac{kp(k)}{<k>}
$$

For a neutral network we expect $P(k, k') = P(k) P(k')$ which after the normalization of $q_{k}$ and $q_{k'}$ translates to $P(k, k') = q_{k}q_{k'}$ therefore any significant deviance from this value indicates degree correlations in a networks.

In practice preparing $P(k, k')$ is difficult and computationally expensive so ***average nearest neighbor degree*** is calculated instead:

$$
    k_{i}^{ANND} = <k_{j}>_{j ~ linked ~ to ~ i} = \frac{1}{k_{i}}\sum_{j ~ linked ~ to ~ i} k_{j}
$$

In terms of $P(k' | k)$, $k^{ANND}(k) = \sum_{k'}P(k' | k)k' = \frac{\sum_{k'}k'P(k', k)}{q_{k}}$.

In case of a neutral network $P(k, k') = P(k)P(k')$ and therefore:

$$
    k^{ANND}(k) = \frac{\sum_{k'}k'P(k', k)}{q_{k}} = \frac{\sum_{k'}k'P(k')P(k)}{P(k)}
$$

We should remeber that $P(k')$ is the normalized $q_{k'}$ which is $\frac{k'p(k')}{<k>}$ therefore:

$$
    k^{ANND}(k) = \frac{<k^{2}>}{<k>}
$$

Calculating this parameter is takes $k$ variables in memory and less steps than calculating $P(k, k')$. We can now calculate the covariance of $k, k'$:

$$
    Cov_{~ P(k, k') ~ }(k, k') ~ = ~ <kk'>_{~ P(k, k') ~ } - <k'>_{~ P(k, k') ~ }<k>_{~ P(k, k') ~ }
$$

Substituting the joint probability in the above equation:

$$
    Cov_{~ P(k, k') ~ }(k, k') ~ = ~ \sum_{k, k'}k'kP(k, k') - \Big(\sum_{k, k'}kP(k, k')\Big)\Big(\sum_{k, k'}k'P(k, k')\Big)
$$

After simplification:

$$
    Cov_{~ P(k, k') ~ }(k, k') ~ = ~ \sum_{k, k'}kk'\Big(P(k, k') - P(k)P(k')\Big)
$$

We can simply check this formula by remembering that in a neutral network the probabilities in the parantheses cancel out and there is no co-variance between degrees.

The Pearson-correlation is defined as the co-variance of the parameters diveded by their variances. The variance of $k$ and $k'$ is:

$$
    \sigma^{2}_{~ P(k, k') ~}(k) = <k^{2}>_{~ P(k, k') ~} - <k>^{2}_{~ P(k, k') ~} = \sum_{k} k^{2}q_{k} - \Big(\sum_{k}q_{k}\Big)^{2}
$$

The Pearson-correlation is therefore:

$$
    r = \frac{Cov_{~ P(k, k') ~}(k, k')}{\sigma_{~ P(k, k') ~}(k')\sigma_{~ P(k, k') ~}(k)} = \frac{\sum_{k, k'}kk'\Big(P(k, k') - P(k)P(k')\Big)}{\sigma_{~ P(k, k') ~}^{2}(k)}
$$

If $r = 0$ the network is neutral, if $r < 0$ it is disassortative otherwise assortative.