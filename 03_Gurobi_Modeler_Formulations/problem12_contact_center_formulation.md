# Problem 12: Contact Center Workforce Scheduling - Mathematical Formulation

---

## 1. Sets and Indices

$$S = \{S1, S2, S3\} \quad \text{set of shifts, indexed by } s$$

$$P = \{P1, P2, P3, P4\} \quad \text{set of time periods, indexed by } p$$

$$\text{cov}(s) \subseteq P \quad \text{subset of periods covered by shift } s$$

$$\text{cov}(S1) = \{P1, P2\}, \quad \text{cov}(S2) = \{P2, P3\}, \quad \text{cov}(S3) = \{P3, P4\}$$

---

## 2. Parameters

$$c \in \mathbb{R}_{+} \quad \text{cost per agent assigned to any shift (e.g., } c = 8 \text{)}$$

$$\pi \in \mathbb{R}_{+} \quad \text{penalty per understaffed agent per period (e.g., } \pi = 100 \text{)}$$

$$d_p \in \mathbb{Z}_{+} \quad \text{required number of agents in period } p$$

$$d_{P1} = 3, \quad d_{P2} = 5, \quad d_{P3} = 4, \quad d_{P4} = 2$$

---

## 3. Decision Variables

$$x_s \in \mathbb{Z}_{+} \quad \text{number of agents assigned to shift } s \in S$$

$$u_p \in \mathbb{Z}_{+} \quad \text{number of understaffed agents in period } p \in P$$

The understaffing variable $u_p$ captures the shortfall: the number of agents by which the actual staffing falls below the requirement $d_p$ in period $p$.

---

## 4. Objective Function

Minimize total operational cost, defined as the sum of agent assignment cost and understaffing penalty cost:

$$\min \quad c \sum_{s \in S} x_s \; + \; \pi \sum_{p \in P} u_p$$

---

## 5. Constraints

### C1: Staffing Coverage Balance

For each period $p \in P$, the total agents from all shifts covering that period, plus any understaffing slack, must be at least the required staffing level:

$$\sum_{s \in S \,:\, p \in \text{cov}(s)} x_s \; + \; u_p \;\geq\; d_p \qquad \forall \; p \in P$$

This constraint is directional ($\geq$) to allow overstaffing at no cost. The optimizer naturally drives $u_p$ to zero whenever hiring is cheaper than the penalty, and accepts positive $u_p$ only when the penalty is cheaper than hiring.

Expanded for each period:

$$x_{S1} + u_{P1} \geq 3$$

$$x_{S1} + x_{S2} + u_{P2} \geq 5$$

$$x_{S2} + x_{S3} + u_{P3} \geq 4$$

$$x_{S3} + u_{P4} \geq 2$$

### C2: Non-negativity

$$x_s \geq 0 \qquad \forall \; s \in S$$

$$u_p \geq 0 \qquad \forall \; p \in P$$

### C3: Integrality

$$x_s \in \mathbb{Z} \qquad \forall \; s \in S$$

$$u_p \in \mathbb{Z} \qquad \forall \; p \in P$$

---

## 6. Complete Model Formulation

$$\min \quad c \sum_{s \in S} x_s + \pi \sum_{p \in P} u_p$$

subject to:

$$\sum_{s \in S \,:\, p \in \text{cov}(s)} x_s + u_p \geq d_p \qquad \forall \; p \in P$$

$$x_s \in \mathbb{Z}_{+} \qquad \forall \; s \in S$$

$$u_p \in \mathbb{Z}_{+} \qquad \forall \; p \in P$$

---

## 7. Additional Notes

### Model Size (Standard Case)
- Variables: $|S| + |P| = 3 + 4 = 7$ integer variables
- Constraints: $|P| = 4$ staffing constraints

### Optimal Solution (Standard Case: $c = 8$, $\pi = 100$)

Since $\pi \gg c$ (100 vs 8), it is always cheaper to hire one more agent than to accept one unit of understaffing. Therefore the optimizer fully staffs all periods:

$$x_{S1} = 3, \quad x_{S2} = 2, \quad x_{S3} = 2, \quad u_p = 0 \; \forall \; p$$

$$\text{Total cost} = 8 \times (3 + 2 + 2) + 100 \times 0 = 56$$

### Break-even Analysis

The model switches from full staffing to accepting understaffing when:

$$c > \pi \quad \Rightarrow \quad \text{it becomes cheaper to pay the penalty than to hire}$$

At $c = 200 > \pi = 100$, the optimizer assigns zero agents and pays all penalties instead.

### Overstaffing
Note that Period P2 requires 5 agents but is covered by both $S1$ and $S2$. Assigning $x_{S1} = 3$ and $x_{S2} = 2$ provides exactly 5 agents for P2 with zero overstaffing, which is a coincidence of the specific demand values in this instance.

### Model Extensions
- To add a maximum staffing cap per period, add: $\sum_{s: p \in \text{cov}(s)} x_s \leq M_p \; \forall \; p$
- To add period-specific penalties, replace $\pi$ with $\pi_p$ indexed by period
- To model shift availability, add binary variables $y_s \in \{0,1\}$ and big-M constraints $x_s \leq M \cdot y_s$
