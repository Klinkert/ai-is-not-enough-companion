# Problem 17 — Workload Placement Optimization: Mathematical Formulation

## Part 1 — Instantiated Formulation with Solution

### Data

**Servers:**
| Server | CPU Capacity | Memory Capacity |
|--------|-------------|----------------|
| S1 | 6 | 8 |
| S2 | 6 | 7 |

**Workloads:**
| Workload | Value | CPU | Memory |
|----------|-------|-----|--------|
| W1 | 10 | 4 | 6 |
| W2 | 8 | 3 | 4 |
| W3 | 7 | 2 | 3 |
| W4 | 6 | 3 | 2 |

### Decision Variables (instantiated)

$x_{ws} \in \{0,1\}$ for each workload-server pair:

$$x_{W1,S1},\ x_{W1,S2},\ x_{W2,S1},\ x_{W2,S2},\ x_{W3,S1},\ x_{W3,S2},\ x_{W4,S1},\ x_{W4,S2}$$

### Instantiated Objective

$$\text{Maximize} \quad Z = 10(x_{W1,S1}+x_{W1,S2}) + 8(x_{W2,S1}+x_{W2,S2}) + 7(x_{W3,S1}+x_{W3,S2}) + 6(x_{W4,S1}+x_{W4,S2})$$

### Instantiated Constraints

**CPU — Server 1:**
$$4x_{W1,S1} + 3x_{W2,S1} + 2x_{W3,S1} + 3x_{W4,S1} \leq 6$$

**CPU — Server 2:**
$$4x_{W1,S2} + 3x_{W2,S2} + 2x_{W3,S2} + 3x_{W4,S2} \leq 6$$

**Memory — Server 1:**
$$6x_{W1,S1} + 4x_{W2,S1} + 3x_{W3,S1} + 2x_{W4,S1} \leq 8$$

**Memory — Server 2:**
$$6x_{W1,S2} + 4x_{W2,S2} + 3x_{W3,S2} + 2x_{W4,S2} \leq 7$$

**Single assignment per workload:**
$$x_{W1,S1}+x_{W1,S2} \leq 1, \quad x_{W2,S1}+x_{W2,S2} \leq 1$$
$$x_{W3,S1}+x_{W3,S2} \leq 1, \quad x_{W4,S1}+x_{W4,S2} \leq 1$$

### Optimal Solution

$$x_{W1,S2}=1,\quad x_{W2,S1}=1,\quad x_{W3,S1}=1,\quad \text{all others} = 0$$

**Verification:**
- S1: CPU = $3+2 = 5 \leq 6$ ✓ | Memory = $4+3 = 7 \leq 8$ ✓
- S2: CPU = $4 \leq 6$ ✓ | Memory = $6 \leq 7$ ✓
- W4 is unassigned

$$Z^* = 10 + 8 + 7 = \mathbf{25}$$

---

## Part 2 — General Algebraic Formulation

### Sets and Indices

- $W = \{W1, W2, W3, W4\}$ — set of workloads
- $S = \{S1, S2\}$ — set of servers

### Parameters

| Symbol | Description |
|--------|-------------|
| $v_w$ | Business value of workload $w$ |
| $\text{cpu}_w$ | CPU demand of workload $w$ |
| $\text{mem}_w$ | Memory demand of workload $w$ |
| $\text{CPU}_s$ | CPU capacity of server $s$ |
| $\text{MEM}_s$ | Memory capacity of server $s$ |

### Decision Variables

$$x_{ws} \in \{0,1\} \quad \forall\ w \in W,\ s \in S$$

$x_{ws} = 1$ if workload $w$ is assigned to server $s$, 0 otherwise.

### Objective Function

$$\text{Maximize} \quad Z = \sum_{w \in W} v_w \sum_{s \in S} x_{ws}$$

### Constraints

**C1 — CPU Capacity per Server:**
$$\sum_{w \in W} \text{cpu}_w \cdot x_{ws} \leq \text{CPU}_s \quad \forall\ s \in S$$

**C2 — Memory Capacity per Server:**
$$\sum_{w \in W} \text{mem}_w \cdot x_{ws} \leq \text{MEM}_s \quad \forall\ s \in S$$

**C3 — Single Assignment per Workload:**
$$\sum_{s \in S} x_{ws} \leq 1 \quad \forall\ w \in W$$

**C4 — Binary:**
$$x_{ws} \in \{0,1\} \quad \forall\ w \in W,\ s \in S$$

### Complete Algebraic Model

$$\begin{aligned} \text{Maximize} \quad & \sum_{w \in W} v_w \sum_{s \in S} x_{ws} \\ \text{subject to} \quad & \sum_{w \in W} \text{cpu}_w \cdot x_{ws} \leq \text{CPU}_s \quad \forall\ s \in S \\ & \sum_{w \in W} \text{mem}_w \cdot x_{ws} \leq \text{MEM}_s \quad \forall\ s \in S \\ & \sum_{s \in S} x_{ws} \leq 1 \quad \forall\ w \in W \\ & x_{ws} \in \{0,1\} \end{aligned}$$

---

## Part 3 — Matrix Form

**Convention note (corrected 2026-07-29):** vector and row ordering below
has been aligned to the published book convention (workload-major
variable stacking; constraint rows ordered single-assignment → CPU →
memory), so this matrix is directly comparable to the printed appendix
and to Problem 18's Phase-1 matrix, which shares the same $A$.

Let $\mathbf{x} \in \{0,1\}^{|W| \times |S|}$ be vectorized **workload-major**
(each workload's server variables kept adjacent):
$\mathbf{x} = [x_{W1,S1},\ x_{W1,S2},\ x_{W2,S1},\ x_{W2,S2},\ x_{W3,S1},\ x_{W3,S2},\ x_{W4,S1},\ x_{W4,S2}]^T$

**Objective:**
$$\text{Maximize} \quad \mathbf{c}^T \mathbf{x}$$

where $\mathbf{c} = [10, 10, 8, 8, 7, 7, 6, 6]^T$

**Constraints:** $A\mathbf{x} \leq \mathbf{b}$, rows ordered single-assignment → CPU → memory:

$$A = \begin{bmatrix} 1 & 1 & 0 & 0 & 0 & 0 & 0 & 0 \\ 0 & 0 & 1 & 1 & 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 & 1 & 1 & 0 & 0 \\ 0 & 0 & 0 & 0 & 0 & 0 & 1 & 1 \\ 4 & 0 & 3 & 0 & 2 & 0 & 3 & 0 \\ 0 & 4 & 0 & 3 & 0 & 2 & 0 & 3 \\ 6 & 0 & 4 & 0 & 3 & 0 & 2 & 0 \\ 0 & 6 & 0 & 4 & 0 & 3 & 0 & 2 \end{bmatrix}, \quad \mathbf{b} = \begin{bmatrix} 1 \\ 1 \\ 1 \\ 1 \\ 6 \\ 6 \\ 8 \\ 7 \end{bmatrix}$$

Row structure:
- Rows 1–4: Single assignment (one per workload)
- Rows 5–6: CPU capacity (one per server)
- Rows 7–8: Memory capacity (one per server)

$$\mathbf{x} \in \{0,1\}^8$$

**Optimal solution vector:**
$$\mathbf{x}^* = [0,\,1,\,1,\,0,\,1,\,0,\,0,\,0]^T \qquad A\mathbf{x}^* \leq \mathbf{b}\;\checkmark \qquad \mathbf{c}^T\mathbf{x}^* = 25$$

($x_{W1,S2}=1,\ x_{W2,S1}=1,\ x_{W3,S1}=1$, matching Part 1's solution.)

---

## Part 4 — Code

See `problem17_workload_placement_optimizer.py` for the full Python/gurobipy implementation.

### Problem Classification

This problem is a **Multi-Dimensional Multiple-Knapsack Problem (MDMKP)**:

| Problem | Type | Variables | Key Feature |
|---|---|---|---|
| 8 — Sales Leads | IP | Binary $x_i$ | Single knapsack, 1D |
| 9 — Marketing Budget | LP | Continuous $x_i$ | Single bin, continuous |
| 10 — Supply Chain | Transportation LP | Continuous $x_{ij}$ | Flow balance |
| 13 — Job Sequencing | MIP | Binary + Continuous | Time ordering |
| 14 — Routing | MIP (TSP) | Binary $x_{ij}$ + $u_i$ | Space + time |
| 15 — Network Flow | LP | Continuous $x_{ij}$ | Flow + capacity |
| 16 — Assignment | IP | Binary $x_{ij}$ | 1-to-1 matching |
| 17 — Workload Placement | IP (MDMKP) | Binary $x_{ws}$ | Multi-bin, multi-resource |
