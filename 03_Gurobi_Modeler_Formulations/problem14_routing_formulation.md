# Problem 14 — Technician Routing (Traveling Salesman Problem)
## Mathematical Formulation

---

## Part 1: Instantiated Formulation with Solution

### Problem Data

Nodes: Depot (0), A (1), B (2), C (3), D (4)

Travel time matrix (rows = from, columns = to):

|        | Depot | A | B | C | D |
|--------|-------|---|---|---|---|
| Depot  | —     | 4 | 6 | 8 | 7 |
| A      | 4     | — | 2 | 5 | 6 |
| B      | 6     | 2 | — | 4 | 3 |
| C      | 8     | 5 | 4 | — | 2 |
| D      | 7     | 6 | 3 | 2 | — |

### Instantiated Objective

$$\text{Minimize} \quad Z = 4x_{0A} + 6x_{0B} + 8x_{0C} + 7x_{0D}$$
$$+ 4x_{A0} + 2x_{AB} + 5x_{AC} + 6x_{AD}$$
$$+ 6x_{B0} + 2x_{BA} + 4x_{BC} + 3x_{BD}$$
$$+ 8x_{C0} + 5x_{CA} + 4x_{CB} + 2x_{CD}$$
$$+ 7x_{D0} + 6x_{DA} + 3x_{DB} + 2x_{DC}$$

### Instantiated Constraints

**C1 — Depart each node exactly once:**

$$x_{0A} + x_{0B} + x_{0C} + x_{0D} = 1 \quad \text{(Depot)}$$
$$x_{A0} + x_{AB} + x_{AC} + x_{AD} = 1 \quad \text{(A)}$$
$$x_{B0} + x_{BA} + x_{BC} + x_{BD} = 1 \quad \text{(B)}$$
$$x_{C0} + x_{CA} + x_{CB} + x_{CD} = 1 \quad \text{(C)}$$
$$x_{D0} + x_{DA} + x_{DB} + x_{DC} = 1 \quad \text{(D)}$$

**C2 — Arrive at each node exactly once:**

$$x_{A0} + x_{BA} + x_{CA} + x_{DA} = 1 \quad \text{(Depot)}$$
$$x_{0A} + x_{BA} + x_{CA} + x_{DA} = 1 \quad \text{(A)}$$
$$x_{0B} + x_{AB} + x_{CB} + x_{DB} = 1 \quad \text{(B)}$$
$$x_{0C} + x_{AC} + x_{BC} + x_{DC} = 1 \quad \text{(C)}$$
$$x_{0D} + x_{AD} + x_{BD} + x_{CD} = 1 \quad \text{(D)}$$

**C3 — MTZ Subtour Elimination (for customer pairs):**

$$u_A - u_B + 4 x_{AB} \leq 3$$
$$u_A - u_C + 4 x_{AC} \leq 3$$
$$u_A - u_D + 4 x_{AD} \leq 3$$
$$u_B - u_A + 4 x_{BA} \leq 3$$
$$u_B - u_C + 4 x_{BC} \leq 3$$
$$u_B - u_D + 4 x_{BD} \leq 3$$
$$u_C - u_A + 4 x_{CA} \leq 3$$
$$u_C - u_B + 4 x_{CB} \leq 3$$
$$u_C - u_D + 4 x_{CD} \leq 3$$
$$u_D - u_A + 4 x_{DA} \leq 3$$
$$u_D - u_B + 4 x_{DB} \leq 3$$
$$u_D - u_C + 4 x_{DC} \leq 3$$

**C4 — Position bounds:**

$$1 \leq u_A,\ u_B,\ u_C,\ u_D \leq 4$$

### Optimal Solution

$$x_{0A}=1,\ x_{AB}=1,\ x_{BD}=1,\ x_{DC}=1,\ x_{C0}=1 \quad \text{(all others = 0)}$$

$$u_A=1,\ u_B=2,\ u_D=3,\ u_C=4$$

$$Z^* = t_{0A} + t_{AB} + t_{BD} + t_{DC} + t_{C0} = 4 + 2 + 3 + 2 + 8 = \mathbf{19}$$

Route: $\text{Depot} \rightarrow A \rightarrow B \rightarrow D \rightarrow C \rightarrow \text{Depot}$

---

## Part 2: General Algebraic Formulation

### Sets and Indices

- $N = \{0, 1, \ldots, n\}$ — all nodes, where $0$ is the depot
- $L = \{1, \ldots, n\}$ — customer locations only
- $(i,j) \in N \times N,\ i \neq j$ — all directed arcs

### Parameters

| Symbol | Description |
|--------|-------------|
| $t_{ij}$ | Travel time from node $i$ to node $j$ |
| $n$ | Number of customer locations $= \|L\|$ |

### Decision Variables

$$x_{ij} \in \{0,1\} \quad \forall\ i,j \in N,\ i \neq j$$

$x_{ij} = 1$ if the technician travels directly from node $i$ to node $j$.

$$u_i \geq 0 \quad \forall\ i \in L$$

$u_i$ is the visit position of customer $i$ in the tour (MTZ auxiliary variable).

### Objective Function

$$\text{Minimize} \quad Z = \sum_{i \in N}\ \sum_{\substack{j \in N \\ j \neq i}} t_{ij} \cdot x_{ij}$$

### Constraints

$$\sum_{\substack{j \in N \\ j \neq i}} x_{ij} = 1 \quad \forall\ i \in N \tag{C1: depart once}$$

$$\sum_{\substack{i \in N \\ i \neq j}} x_{ij} = 1 \quad \forall\ j \in N \tag{C2: arrive once}$$

$$u_i - u_j + n \cdot x_{ij} \leq n - 1 \quad \forall\ i,j \in L,\ i \neq j \tag{C3: subtour elimination}$$

$$1 \leq u_i \leq n \quad \forall\ i \in L \tag{C4: position bounds}$$

$$x_{ij} \in \{0,1\},\quad u_i \geq 0 \tag{C5: integrality}$$

### Complete Model

$$\begin{aligned}
\text{Minimize} \quad & \sum_{i \in N} \sum_{j \neq i} t_{ij} \cdot x_{ij} \\
\text{subject to} \quad
& \sum_{j \neq i} x_{ij} = 1 & \forall\ i \in N \\
& \sum_{i \neq j} x_{ij} = 1 & \forall\ j \in N \\
& u_i - u_j + n \cdot x_{ij} \leq n-1 & \forall\ i,j \in L,\ i \neq j \\
& 1 \leq u_i \leq n & \forall\ i \in L \\
& x_{ij} \in \{0,1\},\quad u_i \geq 0
\end{aligned}$$

---

## Part 3: Matrix Form

### Variable Vector

Order the arc variables lexicographically and stack position variables:

$$\mathbf{x} = [x_{01},\ x_{02},\ \ldots,\ x_{n,n-1}]^\top \in \{0,1\}^{n(n+1)} \qquad \mathbf{u} = [u_1,\ u_2,\ \ldots,\ u_n]^\top \in \mathbb{R}^n$$

Combined variable vector: $\mathbf{z} = \begin{bmatrix} \mathbf{x} \\ \mathbf{u} \end{bmatrix}$

### Objective (vector form)

$$\text{Minimize} \quad \mathbf{c}^\top \mathbf{z}$$

where $\mathbf{c} = [t_{01},\ t_{02},\ \ldots,\ t_{n,n-1},\ 0,\ \ldots,\ 0]^\top$ (travel times for arc variables; zeros for position variables).

### Degree Constraints (C1 and C2)

The degree constraints can be written as:

$$A_{\text{deg}}\ \mathbf{x} = \mathbf{1}_{2(n+1)}$$

where $A_{\text{deg}}$ is the node-arc incidence matrix with two blocks:

- **Row block 1** (out-degree): $[A_{\text{out}}]_{ik} = 1$ if arc $k$ departs from node $i$
- **Row block 2** (in-degree): $[A_{\text{in}}]_{jk} = 1$ if arc $k$ arrives at node $j$

For the 5-node instance ($n+1=5$ nodes, 20 arcs), $A_{\text{deg}}$ is a $10 \times 20$ binary matrix.

### MTZ Constraints (C3)

For each ordered pair $(i,j) \in L \times L,\ i \neq j$, the constraint is:

$$u_i - u_j + n \cdot x_{ij} \leq n-1$$

In matrix form over all such pairs:

$$B_{\text{MTZ}}\ \mathbf{u} + n \cdot C_{\text{MTZ}}\ \mathbf{x} \leq (n-1)\ \mathbf{1}_{n(n-1)}$$

where:
- $B_{\text{MTZ}}$ is an $n(n-1) \times n$ matrix with $+1$ in column $i$ and $-1$ in column $j$ for each pair $(i,j)$
- $C_{\text{MTZ}}$ is an $n(n-1) \times n(n+1)$ binary selector matrix with $1$ in the column of $x_{ij}$

### Position Bounds (C4)

$$\mathbf{1} \leq \mathbf{u} \leq n \cdot \mathbf{1}$$

### Complete Matrix Form

$$\begin{aligned}
\text{Minimize} \quad & \mathbf{c}^\top \mathbf{z} \\
\text{subject to} \quad
& A_{\text{deg}}\ \mathbf{x} = \mathbf{1} \\
& B_{\text{MTZ}}\ \mathbf{u} + n \cdot C_{\text{MTZ}}\ \mathbf{x} \leq (n-1)\,\mathbf{1} \\
& \mathbf{1} \leq \mathbf{u} \leq n\,\mathbf{1} \\
& \mathbf{x} \in \{0,1\}^{n(n+1)},\quad \mathbf{u} \in \mathbb{R}^n_+
\end{aligned}$$

For the 5-node instance:
- $\mathbf{x} \in \{0,1\}^{20}$ (20 directed arcs)
- $\mathbf{u} \in \mathbb{R}^4$ (4 customer position variables)
- $A_{\text{deg}}$: $10 \times 20$
- $B_{\text{MTZ}}$: $12 \times 4$, $C_{\text{MTZ}}$: $12 \times 20$

---

## Part 4: Code Reference

See `problem14_routing_optimizer.py` for the full Python/gurobipy implementation.
See `test_problem14_routing.py` for the full pytest test suite.
