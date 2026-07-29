# Chapter 8 — Lead Prioritization: Mathematical Formulation

## Part 1 — Instantiated Formulation with Solution

### Problem Data

| Lead | Value ($v_i$) | Time ($t_i$) |
|------|--------------|-------------|
| A    | 10           | 2           |
| B    | 7            | 3           |
| C    | 15           | 5           |
| D    | 6            | 4           |
| E    | 18           | 6           |

Total available hours: $T = 10$

### Instantiated Objective

$$\text{Maximize} \quad Z = 10x_A + 7x_B + 15x_C + 6x_D + 18x_E$$

### Instantiated Constraints

**Time budget:**
$$2x_A + 3x_B + 5x_C + 4x_D + 6x_E \leq 10$$

**Binary decisions:**
$$x_A,\ x_B,\ x_C,\ x_D,\ x_E \in \{0,1\}$$

### Solution by Enumeration (key candidates)

| Selection | Time | Value |
|-----------|------|-------|
| E only | 6 | 18 |
| E + A | 8 | 28 |
| E + B | 9 | 25 |
| E + D | 10 | 24 |
| A + B + C | 10 | **32** ← optimal |
| A + C | 7 | 25 |
| B + C + D | 12 | infeasible |

$$\boxed{Z^* = 10(1) + 7(1) + 15(1) + 6(0) + 18(0) = \mathbf{32}}$$

**Optimal plan:**

| Lead | Selected | Value | Time |
|------|----------|-------|------|
| Lead A | Yes | 10 | 2 |
| Lead B | Yes | 7  | 3 |
| Lead C | Yes | 15 | 5 |
| Lead D | No  | —  | — |
| Lead E | No  | —  | — |
| **Total** | | **32** | **10 hrs** |

**Why not Lead E?** Lead E has the highest individual value (18) but requires 6 hours, leaving
only 4 hours — not enough to add any combination that beats 32. Lead A+B+C uses all 10 hours
and produces 32 > 18+any-single-remaining.

---

## Part 2 — General Algebraic Formulation

### Sets and Indices

- $L$ — set of candidate leads, indexed by $i$

### Parameters

| Symbol | Description |
|--------|-------------|
| $v_i$ | Business value of lead $i$ |
| $t_i$ | Outreach hours required for lead $i$ |
| $T$   | Total available outreach hours |

### Decision Variables

$$x_i \in \{0,1\} \quad \forall\ i \in L$$

$x_i = 1$ if lead $i$ is selected, $0$ otherwise.

### Objective Function

$$\text{Maximize} \quad Z = \sum_{i \in L} v_i \cdot x_i$$

### Constraints

**C1 — Time Budget:**
$$\sum_{i \in L} t_i \cdot x_i \leq T$$

**C2 — Binary Selection:**
$$x_i \in \{0,1\} \quad \forall\ i \in L$$

### Complete Algebraic Model

$$\begin{aligned}
\text{Maximize}   \quad & \sum_{i \in L} v_i \cdot x_i \\
\text{subject to} \quad & \sum_{i \in L} t_i \cdot x_i \leq T \\
                        & x_i \in \{0,1\} \quad \forall\ i \in L
\end{aligned}$$

---

## Part 3 — Matrix Form

Let $n = |L|$ be the number of leads.

### Vector definitions

$$\mathbf{v} = \begin{bmatrix} 10 \\ 7 \\ 15 \\ 6 \\ 18 \end{bmatrix}, \quad
\mathbf{t} = \begin{bmatrix} 2 \\ 3 \\ 5 \\ 4 \\ 6 \end{bmatrix}, \quad
\mathbf{x} = \begin{bmatrix} x_A \\ x_B \\ x_C \\ x_D \\ x_E \end{bmatrix}$$

### Matrix form

$$\begin{aligned}
\text{Maximize}   \quad & \mathbf{v}^T \mathbf{x} \\
\text{subject to} \quad & \mathbf{t}^T \mathbf{x} \leq T \\
                        & \mathbf{x} \in \{0,1\}^n
\end{aligned}$$

Expanded:

$$\begin{aligned}
\text{Maximize}   \quad & \begin{bmatrix} 10 & 7 & 15 & 6 & 18 \end{bmatrix} \mathbf{x} \\
\text{subject to} \quad & \begin{bmatrix} 2 & 3 & 5 & 4 & 6 \end{bmatrix} \mathbf{x} \leq 10 \\
                        & \mathbf{x} \in \{0,1\}^5
\end{aligned}$$

**Structural note:** This is the classical **0-1 Knapsack Problem** — a single inequality
constraint over binary variables. The constraint matrix $A = \mathbf{t}^T$ is a single row,
meaning the LP relaxation bound is tight unless item weights have fractional structure. Gurobi
solves this via branch-and-bound with LP relaxation at each node.

---

## Part 4 — Code Reference

See `problem08_lead_prioritization_optimizer.py` for the full gurobipy implementation.

Key implementation notes:
- Binary variables created with `vtype=GRB.BINARY`
- Single `addConstr` for the time budget using `gp.quicksum`
- Objective set with `GRB.MAXIMIZE` and `gp.quicksum`
- Solution extracted by checking `x.X > 0.5` for each binary variable

## Additional Notes

**Problem class:** 0-1 Knapsack — NP-hard in general, but small instances solve instantly.

**Comparison with adjacent problems:**

| Problem | Model Class | Variables | Constraint type |
|---------|-------------|-----------|-----------------|
| 8 — Lead Prioritization | Binary IP | $x_i \in \{0,1\}$ | Single knapsack |
| 9 — Marketing Budget | LP | $x_i \geq 0$ continuous | Budget equality |
| 10 — Supply Chain | Transportation LP | $x_{wj} \geq 0$ | Supply + demand |
| 17 — Workload Placement | Multi-dim Knapsack MIP | $x_{ws} \in \{0,1\}$ | Multiple bins, 2 resources |
