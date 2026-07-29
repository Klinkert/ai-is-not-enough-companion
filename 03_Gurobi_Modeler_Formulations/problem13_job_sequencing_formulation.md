# Problem 13 — Job Sequencing: Mathematical Formulation

## 1. Sets and Indices

- $J = \{A,\ B,\ C\}$ — set of jobs to be processed
- $P = \{1,\ 2,\ \ldots,\ |J|\}$ — set of positions in the processing sequence
- $i,\ i' \in J$ — job indices
- $k,\ k' \in P$ — position indices

---

## 2. Parameters

| Symbol | Description | Values |
|--------|-------------|--------|
| $p_i$ | Processing time of job $i$ | $p_A = 3,\ p_B = 2,\ p_C = 4$ |
| $n$ | Total number of jobs | $n = 3$ |

---

## 3. Decision Variables

### Primary Assignment Variables

$$y_{ik} \in \{0, 1\} \quad \forall\ i \in J,\ k \in P$$

where $y_{ik} = 1$ means job $i$ is assigned to position $k$ in the sequence, and $0$ otherwise.

### Completion Time Variables

$$C_i \geq 0 \quad \forall\ i \in J$$

where $C_i$ is the time at which job $i$ finishes processing on the machine.

---

## 4. Objective Function

Minimize the total sum of completion times across all jobs:

$$\text{Minimize} \quad Z = \sum_{i \in J} C_i = C_A + C_B + C_C$$

Minimizing this sum reduces the total waiting burden across all jobs in the system.

---

## 5. Constraints

### C1 — Each Job Assigned to Exactly One Position

$$\sum_{k \in P} y_{ik} = 1 \quad \forall\ i \in J$$

Each job must occupy exactly one position in the sequence.

### C2 — Each Position Holds Exactly One Job

$$\sum_{i \in J} y_{ik} = 1 \quad \forall\ k \in P$$

No two jobs can share the same position. Together with C1, constraints C1 and C2 define a valid **permutation** (assignment problem structure).

### C3 — Completion Time Calculation

The completion time of job $i$ equals the sum of processing times of all jobs scheduled at or before its position. Since the machine starts at time 0 and is never idle, if job $i$ is placed in position $k$, then:

$$C_i = \sum_{k \in P} y_{ik} \cdot \left(\sum_{k'=1}^{k} \sum_{i' \in J} p_{i'} \cdot y_{i'k'}\right) \quad \forall\ i \in J$$

This can be equivalently expressed in a **linear** form by introducing precedence variables. Define:

$$\delta_{i'i} \in \{0, 1\} \quad \forall\ i',\ i \in J,\ i' \neq i$$

where $\delta_{i'i} = 1$ means job $i'$ is processed **before** job $i$. The completion time becomes:

$$C_i = p_i + \sum_{i' \in J,\ i' \neq i} p_{i'} \cdot \delta_{i'i} \quad \forall\ i \in J$$

### C4 — Precedence Consistency (Anti-symmetry)

$$\delta_{i'i} + \delta_{ii'} = 1 \quad \forall\ i,\ i' \in J,\ i \neq i'$$

For every pair of jobs, exactly one precedes the other.

### C5 — Transitivity (No Cyclic Sequences)

$$\delta_{i'i} + \delta_{ij} + \delta_{ji'} \leq 2 \quad \forall\ i,\ i',\ j \in J,\ \text{all distinct}$$

If job $i'$ precedes job $i$, and job $i$ precedes job $j$, then job $i'$ must precede job $j$. This eliminates circular orderings.

### C6 — Non-negativity and Binary Requirements

$$y_{ik} \in \{0, 1\} \quad \forall\ i \in J,\ k \in P$$

$$\delta_{i'i} \in \{0, 1\} \quad \forall\ i',\ i \in J,\ i' \neq i$$

$$C_i \geq 0 \quad \forall\ i \in J$$

---

## 6. Complete Model Formulation

$$\begin{aligned}
\text{Minimize} \quad & \sum_{i \in J} C_i \\[6pt]
\text{subject to} \quad
& \sum_{k \in P} y_{ik} = 1 & \forall\ i \in J & \quad \text{(C1: one position per job)} \\
& \sum_{i \in J} y_{ik} = 1 & \forall\ k \in P & \quad \text{(C2: one job per position)} \\
& C_i = p_i + \sum_{i' \neq i} p_{i'} \cdot \delta_{i'i} & \forall\ i \in J & \quad \text{(C3: completion time)} \\
& \delta_{i'i} + \delta_{ii'} = 1 & \forall\ i \neq i' \in J & \quad \text{(C4: anti-symmetry)} \\
& \delta_{i'i} + \delta_{ij} + \delta_{ji'} \leq 2 & \forall\ i,i',j \in J \text{ distinct} & \quad \text{(C5: transitivity)} \\
& y_{ik} \in \{0, 1\} & \forall\ i \in J,\ k \in P & \quad \text{(C6: binary assignment)} \\
& \delta_{i'i} \in \{0, 1\} & \forall\ i',i \in J,\ i' \neq i & \quad \text{(C6: binary precedence)} \\
& C_i \geq 0 & \forall\ i \in J & \quad \text{(C6: non-negativity)}
\end{aligned}$$

---

## 7. Optimal Solution

For the standard dataset $(p_A = 3,\ p_B = 2,\ p_C = 4)$, the optimal sequence follows the **Shortest Processing Time (SPT)** rule:

$$\sigma^* = B \rightarrow A \rightarrow C$$

| Job | Position | Start Time | Completion Time |
|-----|----------|------------|-----------------|
| B | 1 | 0 | 2 |
| A | 2 | 2 | 5 |
| C | 3 | 5 | 9 |

$$Z^* = C_B + C_A + C_C = 2 + 5 + 9 = \mathbf{16}$$

---

## 8. Additional Notes

### Problem Classification

This is a **Mixed Integer Program (MIP)** — specifically a **single-machine scheduling problem** denoted in scheduling notation as $1\ |\ r_j = 0\ |\ \sum C_j$, meaning:

| Symbol | Meaning |
|--------|---------|
| $1$ | Single machine |
| $r_j = 0$ | All jobs available at time 0 |
| $\sum C_j$ | Minimize total completion time |

### Why SPT is Optimal

The SPT rule (sequence jobs in non-decreasing order of $p_i$) provably minimizes $\sum C_i$ for this problem class. The intuition: shorter jobs scheduled first reduce the waiting time for all subsequent jobs, much like minimizing the total wait time in a queue by serving the fastest customers first.

### Comparison Across Problems 8, 9, 10, and 13

| Problem | Type | Variables | Key Structural Feature |
|---------|------|-----------|------------------------|
| 8 — Sales Leads | **IP** (Integer Program) | Binary $x_i \in \{0,1\}$ | 0-1 Knapsack |
| 9 — Marketing Budget | **LP** (Linear Program) | Continuous $x_i \geq 0$ | Budget equality |
| 10 — Supply Chain | **Transportation LP** | Continuous $x_{wj} \geq 0$ | Supply/demand balance |
| 13 — Job Sequencing | **MIP** (Mixed Integer) | Binary $y_{ik},\ \delta_{i'i}$; Continuous $C_i$ | Permutation + precedence |

Problem 13 introduces a new element: the **ordering** of decisions matters, not just selection or allocation. This makes it a combinatorial scheduling problem, with $n!$ possible sequences to evaluate (here $3! = 6$).

---

## Editorial Note (Added 2026-07-29)

The published book uses a different, simpler formulation for this
problem: a **big-M disjunctive** model with 3 completion-time variables
$C_i$ and 6 precedence variables $y_{ij}$ (one per ordered pair), using
$C_j \geq C_i + p_j - M(1-y_{ij})$ in place of the position-assignment
$y_{ik}$ + separate precedence $\delta_{i'i}$ + transitivity-constraint
approach above. Both are valid MIP formulations of single-machine total
completion time scheduling and both certify the same optimum
($Z^*=16$, sequence B→A→C). The book's big-M version was kept as
canonical for the reprint: fewer variables (9 vs. 18), no separate
transitivity constraint required, and it is the more commonly taught
textbook formulation for $1\,\|\,\sum C_j$. This file's formulation is
retained here for reference and is not being reconciled to match.
