# Problem 16 – Technician-Job Assignment: Mathematical Formulation

---

## Part 1 — Instantiated Formulation with Solution

### Data

Cost matrix (plugged in with actual numbers):

|          | Job 1 | Job 2 | Job 3 |
|----------|-------|-------|-------|
| Tech A   |   9   |   2   |   7   |
| Tech B   |   6   |   4   |   3   |
| Tech C   |   5   |   8   |   1   |

### Decision Variables (instantiated)

$x_{A,1}, x_{A,2}, x_{A,3}, x_{B,1}, x_{B,2}, x_{B,3}, x_{C,1}, x_{C,2}, x_{C,3} \in \{0,1\}$

### Objective (instantiated)

$$\text{Minimize} \quad Z = 9x_{A,1} + 2x_{A,2} + 7x_{A,3} + 6x_{B,1} + 4x_{B,2} + 3x_{B,3} + 5x_{C,1} + 8x_{C,2} + 1x_{C,3}$$

### Constraints (instantiated)

**Each technician assigned to exactly one job:**

$$x_{A,1} + x_{A,2} + x_{A,3} = 1$$

$$x_{B,1} + x_{B,2} + x_{B,3} = 1$$

$$x_{C,1} + x_{C,2} + x_{C,3} = 1$$

**Each job assigned to exactly one technician:**

$$x_{A,1} + x_{B,1} + x_{C,1} = 1$$

$$x_{A,2} + x_{B,2} + x_{C,2} = 1$$

$$x_{A,3} + x_{B,3} + x_{C,3} = 1$$

### Optimal Solution

By inspection / enumeration (only 3! = 6 permutations):

| Assignment | Cost |
|---|---|
| A→J1, B→J2, C→J3 | 9+4+1 = **14** |
| A→J1, B→J3, C→J2 | 9+3+8 = 20 |
| A→J2, B→J1, C→J3 | 2+6+1 = **9** ← optimal |
| A→J2, B→J3, C→J1 | 2+3+5 = 10 |
| A→J3, B→J1, C→J2 | 7+6+8 = 21 |
| A→J3, B→J2, C→J1 | 7+4+5 = 16 |

$$\boxed{Z^* = 2 + 6 + 1 = 9}$$

**Optimal assignment: Tech A → Job 2, Tech B → Job 1, Tech C → Job 3**

---

## Part 2 — General Algebraic Formulation

### Sets and Indices

- $I$ — set of technicians, $|I| = n$
- $J$ — set of jobs, $|J| = n$
- $(i, j) \in I \times J$ — all technician-job pairs

### Parameters

| Symbol | Description |
|---|---|
| $c_{ij}$ | Cost of assigning technician $i$ to job $j$ |
| $n$ | Number of technicians (= number of jobs) |

### Decision Variables

$$x_{ij} \in \{0, 1\} \quad \forall\ i \in I,\ j \in J$$

where $x_{ij} = 1$ if technician $i$ is assigned to job $j$, and $0$ otherwise.

### Objective Function

$$\text{Minimize} \quad Z = \sum_{i \in I} \sum_{j \in J} c_{ij}\, x_{ij}$$

### Constraints

**C1 — One job per technician:**

$$\sum_{j \in J} x_{ij} = 1 \quad \forall\ i \in I$$

**C2 — One technician per job:**

$$\sum_{i \in I} x_{ij} = 1 \quad \forall\ j \in J$$

**C3 — Binary assignment:**

$$x_{ij} \in \{0, 1\} \quad \forall\ i \in I,\ j \in J$$

### Complete Model

$$\begin{aligned} \text{Minimize} \quad & \sum_{i \in I} \sum_{j \in J} c_{ij}\, x_{ij} \\ \text{subject to} \quad & \sum_{j \in J} x_{ij} = 1 \quad \forall\ i \in I \\ & \sum_{i \in I} x_{ij} = 1 \quad \forall\ j \in J \\ & x_{ij} \in \{0, 1\} \quad \forall\ i \in I,\ j \in J \end{aligned}$$

---

## Part 3 — Matrix Form

Vectorize the $n \times n$ matrix $X$ by stacking rows: $\mathbf{x} = \text{vec}(X) \in \{0,1\}^{n^2}$

For $n = 3$, $\mathbf{x} = [x_{A,1},\ x_{A,2},\ x_{A,3},\ x_{B,1},\ x_{B,2},\ x_{B,3},\ x_{C,1},\ x_{C,2},\ x_{C,3}]^T$

**Objective:**

$$\text{Minimize} \quad \mathbf{c}^T \mathbf{x}$$

where $\mathbf{c} = [9,\ 2,\ 7,\ 6,\ 4,\ 3,\ 5,\ 8,\ 1]^T$

**Row constraints** (one job per technician), $A_r \mathbf{x} = \mathbf{1}$:

$$A_r = \begin{bmatrix} 1 & 1 & 1 & 0 & 0 & 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 1 & 1 & 1 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 & 0 & 0 & 1 & 1 & 1 \end{bmatrix}$$

**Column constraints** (one technician per job), $A_c \mathbf{x} = \mathbf{1}$:

$$A_c = \begin{bmatrix} 1 & 0 & 0 & 1 & 0 & 0 & 1 & 0 & 0 \\ 0 & 1 & 0 & 0 & 1 & 0 & 0 & 1 & 0 \\ 0 & 0 & 1 & 0 & 0 & 1 & 0 & 0 & 1 \end{bmatrix}$$

**Combined system:**

$$\begin{bmatrix} A_r \\ A_c \end{bmatrix} \mathbf{x} = \begin{bmatrix} \mathbf{1}_n \\ \mathbf{1}_n \end{bmatrix}, \quad \mathbf{x} \in \{0,1\}^{n^2}$$

**Note:** The constraint matrix $[A_r;\ A_c]$ is **totally unimodular** — meaning the LP relaxation ($x_{ij} \geq 0$) always yields an integer optimal solution. The assignment problem can be solved as a pure LP.

---

## Part 4 — Code

See `problem16_assignment_optimizer.py` for the full Python/gurobipy implementation.

Key implementation notes:
- Binary variables `x[i,j]` via `model.addVars(technicians, jobs, vtype=GRB.BINARY)`
- Row constraints via `model.addConstrs(quicksum(x[i,j] for j in jobs) == 1 for i in technicians)`
- Column constraints via `model.addConstrs(quicksum(x[i,j] for i in technicians) == 1 for j in jobs)`
- Objective: `model.setObjective(quicksum(cost[i,j] * x[i,j] ...), GRB.MINIMIZE)`

---

## Comparison Across Problems 8–16

| Problem | Type | Variables | Key Feature |
|---|---|---|---|
| 8 — Sales Leads | IP (Knapsack) | Binary $x_i$ | Select subset under budget |
| 9 — Marketing Budget | LP | Continuous $x_i$ | Allocate across channels |
| 10 — Supply Chain | Transportation LP | Continuous $x_{wj}$ | Flow across network |
| 13 — Job Sequencing | MIP | Binary + Continuous | Order in time |
| 14 — Technician Routing | MIP (TSP) | Binary $x_{ij}$ + MTZ $u_i$ | Route through space |
| 15 — Network Flow | Min-Cost Flow LP | Continuous $x_{ij}$ | Flow balance at nodes |
| 16 — Assignment | BIP (totally unimodular) | Binary $x_{ij}$ | One-to-one matching |
