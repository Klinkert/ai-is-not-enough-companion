# Problem 18 — Dynamic Workload Re-optimization
## Mathematical Formulation (Klinkert Package)

---

## Part 1 — Instantiated Formulation with Solution

### Phase 1: Initial State

Servers: S1 (CPU=6, Mem=8), S2 (CPU=6, Mem=7)
Workloads: W1(v=10,c=4,m=6), W2(v=8,c=3,m=4), W3(v=7,c=2,m=3), W4(v=6,c=3,m=2)

**Maximize:**
$$Z = 10(x_{W1,S1}+x_{W1,S2}) + 8(x_{W2,S1}+x_{W2,S2}) + 7(x_{W3,S1}+x_{W3,S2}) + 6(x_{W4,S1}+x_{W4,S2})$$

**Subject to (Phase 1):**
$$\text{S1 CPU: } 4x_{W1,S1}+3x_{W2,S1}+2x_{W3,S1}+3x_{W4,S1} \leq 6$$
$$\text{S1 Mem: } 6x_{W1,S1}+4x_{W2,S1}+3x_{W3,S1}+2x_{W4,S1} \leq 8$$
$$\text{S2 CPU: } 4x_{W1,S2}+3x_{W2,S2}+2x_{W3,S2}+3x_{W4,S2} \leq 6$$
$$\text{S2 Mem: } 6x_{W1,S2}+4x_{W2,S2}+3x_{W3,S2}+2x_{W4,S2} \leq \mathbf{7}$$

**Phase 1 Optimal Solution:**

| Workload | Assigned To | Value | CPU Used | Mem Used |
|----------|------------|-------|----------|----------|
| W1 | Server 1 | 10 | 4 | 6 |
| W2 | Server 2 | 8 | 3 | 4 |
| W3 | Server 2 | 7 | 2 | 3 |
| W4 | — | — | — | — |

$$Z_1^* = 10 + 8 + 7 = \mathbf{25}$$

Server 1: CPU 4/6, Mem 6/8 — Server 2: CPU 5/6, Mem 7/7

---

### Phase 2: Conditions Change

Two simultaneous updates:
- Server 2 memory: $7 \rightarrow \mathbf{6}$
- W3 value: $7 \rightarrow \mathbf{11}$

**Feasibility check of old assignment under new constraints:**
$$\text{S2 Mem (old): } 4(W2) + 3(W3) = 7 > 6 \quad \Rightarrow \quad \text{INFEASIBLE}$$

The old plan is no longer valid. Re-optimization finds a non-obvious solution:

**Phase 2 Updated Objective:**
$$Z = 10(x_{W1,S1}+x_{W1,S2}) + 8(x_{W2,S1}+x_{W2,S2}) + \mathbf{11}(x_{W3,S1}+x_{W3,S2}) + 6(x_{W4,S1}+x_{W4,S2})$$

**Updated S2 Memory Constraint:**
$$6x_{W1,S2}+4x_{W2,S2}+3x_{W3,S2}+2x_{W4,S2} \leq \mathbf{6}$$

**Phase 2 Optimal Solution:**

| Workload | Assigned To | Value | CPU Used | Mem Used |
|----------|------------|-------|----------|----------|
| W2 | Server 1 | 8 | 3 | 4 |
| W3 | Server 1 | 11 | 2 | 3 |
| W1 | Server 2 | 10 | 4 | 6 |
| W4 | — | — | — | — |

$$Z_2^* = 8 + 11 + 10 = \mathbf{29}$$

Server 1: CPU 5/6, Mem 7/8 — Server 2: CPU 4/6, Mem 6/6

**Why 29, not 27?**
The intuitive guess (W1→S1, W3+W4→S2 = 27) misses the better move:
W3's increased value (11) makes it optimal to consolidate W2+W3 on S1 (CPU=5, Mem=7 — both fit),
freeing S2 to host W1 alone (Mem=6, exactly at the new limit).
This is why re-optimization is necessary — the optimal move is counterintuitive.

---

## Part 2 — General Algebraic Formulation

### Sets and Indices

- $W$ — set of workloads, indexed by $w$
- $S$ — set of servers, indexed by $s$

### Parameters

| Symbol | Description |
|--------|-------------|
| $v_w^{(t)}$ | Business value of workload $w$ at time $t$ |
| $c_w$ | CPU demand of workload $w$ |
| $m_w$ | Memory demand of workload $w$ |
| $\text{CPU}_s$ | CPU capacity of server $s$ |
| $\text{MEM}_s^{(t)}$ | Memory capacity of server $s$ at time $t$ (may change) |

### Decision Variables

$$x_{ws} \in \{0,1\} \quad \forall\ w \in W,\ s \in S$$

$x_{ws} = 1$ if workload $w$ is assigned to server $s$, 0 otherwise.

### Objective Function

$$\text{Maximize} \quad Z^{(t)} = \sum_{w \in W} v_w^{(t)} \sum_{s \in S} x_{ws}$$

### Constraints

**C1 — CPU Capacity:**
$$\sum_{w \in W} c_w \cdot x_{ws} \leq \text{CPU}_s \quad \forall\ s \in S$$

**C2 — Memory Capacity:**
$$\sum_{w \in W} m_w \cdot x_{ws} \leq \text{MEM}_s^{(t)} \quad \forall\ s \in S$$

**C3 — Single Assignment:**
$$\sum_{s \in S} x_{ws} \leq 1 \quad \forall\ w \in W$$

**C4 — Binary:**
$$x_{ws} \in \{0,1\} \quad \forall\ w \in W,\ s \in S$$

---

## Part 3 — Matrix Form

**Convention note (corrected 2026-07-29):** row ordering below has been
aligned to the published book convention (single-assignment → CPU →
memory) and to Problem 17's corrected matrix. The variable stacking here
was already workload-major and required no change — only the constraint
row order was inconsistent with Problem 17's own file. With this fix,
$A$ is now identical in both problems (as the model text already
claimed), and only $\mathbf{b}$ and $\mathbf{c}$ change between phases.

Let $\mathbf{x} \in \{0,1\}^{|W| \times |S|}$ be the vectorized assignment matrix
(workload-major: $[x_{W1,S1},\ x_{W1,S2},\ x_{W2,S1},\ x_{W2,S2},\ \ldots]$).

$$A\mathbf{x} \leq \mathbf{b}^{(t)}, \quad \mathbf{x} \in \{0,1\}^{|W|\cdot|S|}$$

For Phase 2 ($|W|=4$, $|S|=2$, vectorized as $[x_{W1S1},x_{W1S2},x_{W2S1},x_{W2S2},x_{W3S1},x_{W3S2},x_{W4S1},x_{W4S2}]$),
rows ordered single-assignment → CPU → memory:

**Constraint matrix $A$ (8 rows x 8 columns) — identical to Problem 17:**

$$A = \begin{bmatrix}
1&1&0&0&0&0&0&0 \\
0&0&1&1&0&0&0&0 \\
0&0&0&0&1&1&0&0 \\
0&0&0&0&0&0&1&1 \\
4&0&3&0&2&0&3&0 \\
0&4&0&3&0&2&0&3 \\
6&0&4&0&3&0&2&0 \\
0&6&0&4&0&3&0&2
\end{bmatrix}, \quad
\mathbf{b}^{(2)} = \begin{bmatrix}1\\1\\1\\1\\6\\6\\8\\\mathbf{6}\end{bmatrix}$$

Row structure: Rows 1–4 single assignment, Rows 5–6 CPU, Rows 7–8 memory
(Row 8 = Server 2 memory, the row that changes between phases).

**Objective vector $\mathbf{c}^{(2)}$ (maximize):**

$$\mathbf{c}^{(2)} = [10,10,8,8,\mathbf{11},\mathbf{11},6,6]$$

The dynamic changes manifest as:
- $b_8$ changes from $7 \rightarrow 6$ (Server 2 memory degradation)
- $c_5, c_6$ change from $7 \rightarrow 11$ (W3 value increase)

**Optimal solution vector (Phase 2):**
$$\mathbf{x}^* = [0,\,1,\,1,\,0,\,1,\,0,\,0,\,0]^T \qquad \mathbf{c}^{(2)T}\mathbf{x}^* = 29$$

($x_{W1,S2}=1,\ x_{W2,S1}=1,\ x_{W3,S1}=1$ — matches Part 1.)

---

## Part 4 — Code

See `problem18_reoptimization_optimizer.py` for the full gurobipy implementation.

The implementation uses `update_memory_capacity()` and `update_workload_value()` methods
to modify only the affected constraint RHS and objective coefficients — no full model rebuild.
This demonstrates Gurobi's ability to efficiently re-optimize after incremental model changes.

---

## Key Insight: Re-optimization vs. Static Planning

| | Phase 1 | Phase 2 |
|--|---------|---------|
| S2 Memory | 7 | **6** |
| W3 Value | 7 | **11** |
| Optimal Assignment | W1→S1, W2+W3→S2 | W2+W3→S1, W1→S2 |
| W4 Status | Unassigned | Unassigned |
| Total Value | 25 | **29** |

Two key non-obvious insights emerge:
1. The new optimal routes W3 (now value 11) to S1 — counterintuitively away from the degraded server.
2. W1 migrates to S2 precisely because its large memory footprint (6) exactly fills the degraded S2 capacity.
3. Total value actually **increases** from 25 to 29 because W3's value gain outweighs any penalty from rebalancing.
This result is impossible to derive from heuristics or intuition alone — it requires re-solving the optimization model.
