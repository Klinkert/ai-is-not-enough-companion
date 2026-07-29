# Problem 15: Minimum Cost Network Flow — Klinkert Package

---

## Part 1: Instantiated Formulation with Solution

### Network Data

Nodes and their supply/demand:
- Plant: supply = +100
- Hub: supply = 0 (transshipment)
- Region 1: demand = −40
- Region 2: demand = −60

Arcs with cost and capacity:

| Arc | Cost/unit | Capacity |
|-----|-----------|----------|
| Plant → Hub | 2 | 100 |
| Plant → Region 1 | 5 | 40 |
| Hub → Region 1 | 1 | 60 |
| Hub → Region 2 | 3 | 80 |

### Decision Variables (Instantiated)

Let:
- $x_1$ = units shipped Plant → Hub
- $x_2$ = units shipped Plant → Region 1
- $x_3$ = units shipped Hub → Region 1
- $x_4$ = units shipped Hub → Region 2

### Objective (Instantiated)

$$\text{Minimize} \quad Z = 2x_1 + 5x_2 + 1x_3 + 3x_4$$

### Constraints (Instantiated)

**Plant supply (C1):**
$$x_1 + x_2 = 100$$

**Hub balance (C2):**
$$x_1 = x_3 + x_4$$

**Region 1 demand (C3):**
$$x_2 + x_3 = 40$$

**Region 2 demand (C4):**
$$x_4 = 60$$

**Arc capacities (C5):**
$$x_1 \leq 100, \quad x_2 \leq 40, \quad x_3 \leq 60, \quad x_4 \leq 80$$

**Non-negativity (C6):**
$$x_1, x_2, x_3, x_4 \geq 0$$

### Solution Derivation

From C4: $x_4 = 60$

From C2: $x_1 = x_3 + 60$

From C3: $x_2 = 40 - x_3$

Substitute into objective:

$$Z = 2(x_3 + 60) + 5(40 - x_3) + x_3 + 3(60) = -2x_3 + 500$$

Minimize $Z$ by **maximizing** $x_3$. With $x_2 = 40 - x_3 \geq 0$, the maximum is $x_3 = 40$.

### Optimal Solution

| Variable | Value | Arc |
|----------|-------|-----|
| $x_1$ | 100 | Plant → Hub |
| $x_2$ | 0 | Plant → Region 1 |
| $x_3$ | 40 | Hub → Region 1 |
| $x_4$ | 60 | Hub → Region 2 |

$$Z^* = 2(100) + 5(0) + 1(40) + 3(60) = 200 + 0 + 40 + 180 = \mathbf{420}$$

All supply, demand, and capacity constraints are satisfied. It is cheaper to route everything through the Hub (cost 2+1=3 to Region 1) than to ship directly from Plant to Region 1 (cost 5).

---

## Part 2: General Algebraic Formulation

### Sets and Indices

- $V$ — set of nodes (vertices) in the network
- $E \subseteq V \times V$ — set of directed arcs (edges)
- $(i,j) \in E$ — an arc from node $i$ to node $j$

### Parameters

| Symbol | Description |
|--------|-------------|
| $b_i$ | Net supply at node $i$ ($b_i > 0$: supply, $b_i < 0$: demand, $b_i = 0$: transshipment) |
| $c_{ij}$ | Transportation cost per unit on arc $(i,j)$ |
| $u_{ij}$ | Capacity (maximum flow) on arc $(i,j)$ |

### Decision Variables

$$x_{ij} \geq 0 \quad \forall\ (i,j) \in E$$

$x_{ij}$ is the number of units shipped on arc $(i,j)$.

### Objective Function

$$\text{Minimize} \quad Z = \sum_{(i,j) \in E} c_{ij} \cdot x_{ij}$$

### Constraints

**C1–C4: Flow Balance at each node:**
$$\sum_{j:(i,j)\in E} x_{ij} - \sum_{j:(j,i)\in E} x_{ji} = b_i \quad \forall\ i \in V$$

**C5: Arc Capacity:**
$$x_{ij} \leq u_{ij} \quad \forall\ (i,j) \in E$$

**C6: Non-negativity:**
$$x_{ij} \geq 0 \quad \forall\ (i,j) \in E$$

### Complete General Model

$$\begin{aligned} \text{Minimize} \quad & \sum_{(i,j) \in E} c_{ij} \cdot x_{ij} \\ \text{subject to} \quad & \sum_{j:(i,j)\in E} x_{ij} - \sum_{j:(j,i)\in E} x_{ji} = b_i \quad \forall\ i \in V \\ & 0 \leq x_{ij} \leq u_{ij} \quad \forall\ (i,j) \in E \end{aligned}$$

---

## Part 3: Matrix Form

### Variable Vector

$$\mathbf{x} = \begin{bmatrix} x_1 \\ x_2 \\ x_3 \\ x_4 \end{bmatrix} = \begin{bmatrix} x_{\text{Plant,Hub}} \\ x_{\text{Plant,R1}} \\ x_{\text{Hub,R1}} \\ x_{\text{Hub,R2}} \end{bmatrix}$$

### Objective (Cost Vector)

$$\mathbf{c}^T = \begin{bmatrix} 2 & 5 & 1 & 3 \end{bmatrix}$$

$$\text{Minimize} \quad Z = \mathbf{c}^T \mathbf{x}$$

### Flow Balance Constraints — Node-Arc Incidence Matrix

The matrix $A$ is the **node-arc incidence matrix** where $A_{ij} = +1$ if arc $j$ leaves node $i$, $A_{ij} = -1$ if arc $j$ enters node $i$, and $0$ otherwise.

$$A = \begin{array}{c|cccc} & x_1 & x_2 & x_3 & x_4 \\ \hline \text{Plant} & +1 & +1 & 0 & 0 \\ \text{Hub} & -1 & 0 & +1 & +1 \\ \text{Region 1} & 0 & -1 & -1 & 0 \\ \text{Region 2} & 0 & 0 & 0 & -1 \end{array}$$

### Supply/Demand Vector

$$\mathbf{b} = \begin{bmatrix} 100 \\ 0 \\ -40 \\ -60 \end{bmatrix}$$

### Capacity Bounds

$$\mathbf{u} = \begin{bmatrix} 100 \\ 40 \\ 60 \\ 80 \end{bmatrix}$$

### Complete Matrix Form

$$\begin{aligned} \text{Minimize} \quad & \mathbf{c}^T \mathbf{x} \\ \text{subject to} \quad & A\mathbf{x} = \mathbf{b} \\ & \mathbf{0} \leq \mathbf{x} \leq \mathbf{u} \end{aligned}$$

Expanded:

$$\begin{bmatrix} 1 & 1 & 0 & 0 \\ -1 & 0 & 1 & 1 \\ 0 & -1 & -1 & 0 \\ 0 & 0 & 0 & -1 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ x_3 \\ x_4 \end{bmatrix} = \begin{bmatrix} 100 \\ 0 \\ -40 \\ -60 \end{bmatrix}, \quad \mathbf{0} \leq \mathbf{x} \leq \begin{bmatrix} 100 \\ 40 \\ 60 \\ 80 \end{bmatrix}$$

---

## Part 4: Code

See `problem15_network_flow_optimizer.py` for the full gurobipy implementation.

---

## Problem Type Classification

This is a **Minimum Cost Flow (MCF)** problem — a Linear Program (LP) with a special network structure. The LP relaxation always yields integer solutions when supplies, demands, and capacities are integer-valued (total unimodularity property).

## Comparison Across Problems

| Problem | Type | Variables | Key Feature |
|---|---|---|---|
| 8 — Sales Leads | IP | Binary $x_i$ | 0-1 Knapsack |
| 9 — Marketing Budget | LP | Continuous $x_i$ | Budget equality |
| 10 — Supply Chain | Transportation LP | Continuous $x_{wj}$ | 2-layer flow |
| 13 — Job Sequencing | MIP | Binary + Continuous | Ordering in time |
| 14 — Technician Routing | MIP (TSP) | Binary $x_{ij}$ + $u_i$ | Route through space |
| 15 — Network Flow | Min-Cost Flow LP | Continuous $x_{ij}$ | Multi-hop network flow |
