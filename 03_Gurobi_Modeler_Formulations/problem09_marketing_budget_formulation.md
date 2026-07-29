# Problem 9: Marketing Budget Allocation — Mathematical Formulation

---

## Part 1 — Instantiated Formulation with Solution

### Data

| Channel | Return Rate | Min Spend | Max Spend |
|---|---|---|---|
| Digital Ads | 12% | $10,000 | none |
| Email Campaigns | 10% | $0 | $60,000 |
| Events | 18% | $0 | $40,000 |

Total Budget: $100,000

### Instantiated Model

$$\text{Maximize} \quad Z = 0.12\, x_D + 0.10\, x_E + 0.18\, x_V$$

$$\text{subject to:}$$

$$x_D + x_E + x_V = 100{,}000 \qquad \text{(full budget)}$$
$$x_D \geq 10{,}000 \qquad \text{(digital minimum)}$$
$$x_E \leq 60{,}000 \qquad \text{(email cap)}$$
$$x_V \leq 40{,}000 \qquad \text{(events cap)}$$
$$x_D,\ x_E,\ x_V \geq 0$$

### Solution

Rank channels by return rate: Events (18%) > Digital (12%) > Email (10%).

- Allocate Events to its cap: $x_V = 40{,}000$
- Remaining: $100{,}000 - 40{,}000 = 60{,}000$
- Digital beats Email, no upper cap: $x_D = 60{,}000$
- Email receives nothing: $x_E = 0$

| Channel | Allocation | Return Rate | Expected Return |
|---|---|---|---|
| Digital Ads | $60,000 | 12% | $7,200 |
| Email Campaigns | $0 | 10% | $0 |
| Events | $40,000 | 18% | $7,200 |
| **Total** | **$100,000** | | **$14,400** |

$$Z^* = 0.12 \times 60{,}000 + 0.10 \times 0 + 0.18 \times 40{,}000 = 7{,}200 + 0 + 7{,}200 = \mathbf{\$14{,}400}$$

---

## Part 2 — General Algebraic Formulation

### Sets and Indices

$$C = \{1, 2, \ldots, n\} \quad \text{set of marketing channels, indexed by } i$$

### Parameters

| Symbol | Description |
|---|---|
| $r_i$ | Expected return rate for channel $i$ (decimal) |
| $l_i$ | Minimum spend required for channel $i$ ($l_i \geq 0$) |
| $u_i$ | Maximum spend allowed for channel $i$ ($u_i \leq +\infty$) |
| $B$ | Total available marketing budget |

### Decision Variables

$$x_i \geq 0 \quad \forall\ i \in C$$

$x_i$ is the dollar amount allocated to channel $i$.

### Objective Function

$$\text{Maximize} \quad Z = \sum_{i \in C} r_i\, x_i$$

### Constraints

$$\sum_{i \in C} x_i = B \qquad \text{(C1: full budget equality)}$$

$$x_i \geq l_i \qquad \forall\ i \in C \qquad \text{(C2: minimum spend)}$$

$$x_i \leq u_i \qquad \forall\ i \in C,\ u_i < +\infty \qquad \text{(C3: maximum spend)}$$

$$x_i \geq 0 \qquad \forall\ i \in C \qquad \text{(C4: non-negativity)}$$

### Complete Model

$$\begin{aligned}
\text{Maximize} \quad & Z = \sum_{i \in C} r_i\, x_i \\
\text{subject to} \quad
& \sum_{i \in C} x_i = B & \text{(C1)} \\
& l_i \leq x_i \leq u_i & \forall\ i \in C \quad \text{(C2, C3, C4)}
\end{aligned}$$

---

## Part 3 — Matrix Form

Let $n = |C|$ be the number of channels. Stack variables into:

$$\mathbf{x} = [x_1,\ x_2,\ \ldots,\ x_n]^T \in \mathbb{R}^n$$

**Objective (maximize):**

$$\mathbf{r}^T \mathbf{x}, \quad \mathbf{r} = [r_1,\ r_2,\ \ldots,\ r_n]^T$$

**Budget equality:**

$$\mathbf{1}^T \mathbf{x} = B, \quad \mathbf{1} = [1,\ 1,\ \ldots,\ 1]^T$$

**Bounds:**

$$\mathbf{l} \leq \mathbf{x} \leq \mathbf{u}$$

**Full matrix form:**

$$\begin{bmatrix} 1 & 1 & 1 \end{bmatrix} \begin{bmatrix} x_D \\ x_E \\ x_V \end{bmatrix} = \begin{bmatrix} 100{,}000 \end{bmatrix}$$

$$\begin{bmatrix} 10{,}000 \\ 0 \\ 0 \end{bmatrix} \leq \begin{bmatrix} x_D \\ x_E \\ x_V \end{bmatrix} \leq \begin{bmatrix} +\infty \\ 60{,}000 \\ 40{,}000 \end{bmatrix}$$

**Key structural note:** This is a pure **LP** (no integer variables). The constraint matrix $A = \mathbf{1}^T$ has a single row — the budget equality. All complexity is encoded in the variable bounds. The LP is solved in a single simplex pivot.

---

## Part 4 — Code Reference

See: `problem09_marketing_budget_optimizer.py`

The model uses:
- `model.addVar(lb=min_spend, ub=max_spend)` — bounds encode C2/C3/C4 directly
- `model.addConstr(gp.quicksum(...) == total_budget)` — budget equality C1
- `model.setObjective(gp.quicksum(...), GRB.MAXIMIZE)` — maximize total return

---

## Additional Notes

- This is the **simplest LP in the series** — one equality constraint plus variable bounds
- The optimal solution follows the **greedy rule**: fill highest-return channel to its cap, then next, etc.
- Contrast with Problem 8 (binary knapsack): here $x_i$ is continuous, so fractional allocations are valid
- Contrast with Problem 10 (transportation): here there is one supply node (budget) and multiple demand nodes (channels), but no flow conservation — just a single equality
