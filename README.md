### High-Level Overview:
[**This**](https://arxiv.org/abs/1910.12164) paper explores Quantum Neighborhood Preserving Embedding (qNPE) which is a quantum algorithm designed for dimensionality reduction. It stores the local manifold structure of data. While PCA or LDA loses information between neighbourhood relationships, qNPE maintains it properly between data points. The algorithm consists of _four_ major steps: finding K-nearest neighbors, computing the weight matrix, solving the generalized eigenvalue problem, and extracting the lower-dimensional manifold representation.

### Technical Overview:

#### Finding K-Nearest Neighbors:
At first, a neighborhood graph $G$ should be constructed where each data point $x_i$ is connected to its $K$-nearest neighbors using a quantum search algorithm with swap tests.

#### Computing the Weight Matrix $W$:
Solving the convex optimization problem:

$$
\min \sum_{i=0}^{M-1} \left\| x_i - \sum_{j=0}^{K-1} \omega_{ij} x_j \right\|^2, \quad \text{subject to} \quad \sum_{j=0}^{K-1} \omega_{ij} = 1
$$

We compute each point as a linear combination of its neighbors.

#### Solving the Generalized Eigenvalue Problem:

Computing the projection matrix \( A \) by solving

$$
X Q X^\dagger a = \lambda X X^\dagger a
$$

where 

$$
X = (x_0, x_1, \dots, x_{M-1})
$$ 

and 

$$
Q = (I - W)^\dagger (I - W).
$$ 

This step is performed using the Variational Quantum Generalized Eigenvalue Solver.

#### Extracting the Lower-Dimensional Representation:

We obtain the final embedding via

$$
|y_i\rangle = A^\dagger |x_i\rangle
$$

where Quantum Singular Value Decomposition (QSVD) or swap tests are used to extract the embeddings.

