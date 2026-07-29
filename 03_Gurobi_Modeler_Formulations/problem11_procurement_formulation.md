# Mathematical Formulation: Procurement Optimization (Problem 11)

## 1. Sets and Indices

| Symbol | Description |
|--------|-------------|
| $S$ | Set of available suppliers, indexed by $s$ |

**Example**: $S = \{\text{Supplier1},\, \text{Supplier2},\, \text{Supplier3}\}$

---

## 2. Parameters

| Symbol | Type | Description |
|--------|------|-------------|
| $c_s$ | float | Unit procurement cost for supplier $s$ |
| $r_s$ | float | Risk score per unit ordered from supplier $s$ |
| $u_s$ | float | Maximum order capacity of supplier $s$ |
| $D$ | float | Total demand that must be fulfilled (exact) |
| $R^{\max}$ | float | Maximum allowable total risk exposure |

**Example values**:

| Supplier | $c_s$ | $r_s$ | $u_s$ |
|----------|-------|-------|-------|
| Supplier1 | 5.0 | 0.20 | 60 |
| Supplier2 | 6.0 | 0.10 | 50 |
| Supplier3 | 4.0 | 0.30 | 70 |

$D = 100$, $R^{\max} = 25$

---

## 3. Decision Variables

$$x_s \geq 0 \qquad \forall\; s \in S$$

where $x_s$ is the quantity of units ordered from supplier $s$.

Each variable is bounded above by the supplier's capacity:

$$0 \leq x_s \leq u_s \qquad \forall\; s \in S$$

This is a **continuous linear program** (LP) - no integrality constraints are required.

---

## 4. Objective Function

Minimize total procurement cost:

$$\min \quad \sum_{s \in S} c_s \cdot x_s$$

---

## 5. Constraints

### C1: Exact Demand Fulfillment

The total quantity ordered across all suppliers must exactly equal demand:

$$\sum_{s \in S} x_s = D$$

### C2: Supplier Capacity Limits

No supplier can be assigned more than its available capacity (encoded as variable upper bounds):

$$x_s \leq u_s \qquad \forall\; s \in S$$

### C3: Risk Exposure Policy

The weighted risk exposure across all orders must not exceed the corporate policy limit:

$$\sum_{s \in S} r_s \cdot x_s \leq R^{\max}$$

### C4: Non-negativity

$$x_s \geq 0 \qquad \forall\; s \in S$$

---

## 6. Complete Model Formulation

$$\min \quad \sum_{s \in S} c_s \cdot x_s$$

subject to:

$$\sum_{s \in S} x_s = D \qquad \text{(C1: demand fulfillment)}$$

$$\sum_{s \in S} r_s \cdot x_s \leq R^{\max} \qquad \text{(C3: risk policy)}$$

$$0 \leq x_s \leq u_s \qquad \forall\; s \in S \qquad \text{(C2, C4: capacity and non-negativity)}$$

---

## 6a. Matrix Form (Added 2026-07-29)

*Not present in the original Gurobi Modeler output — added to match the
book's existing Part 5. Note the representation choice: the book writes
supplier capacity as explicit rows of $A$ rather than as variable upper
bounds. Both are mathematically equivalent (Gurobi's own model above
uses bounds, `addVar(ub=u_s)`), but the explicit-row form is used here so
this matrix is directly comparable, row for row, to the printed book
appendix.*

$$\text{Minimize} \quad \mathbf{c}^T\mathbf{x} \quad \text{subject to} \quad A\mathbf{x} \leq \mathbf{b}, \quad \mathbf{x} \geq 0$$

$$\mathbf{c} = \begin{bmatrix}5\\6\\4\end{bmatrix}, \quad
\mathbf{x} = \begin{bmatrix}x_1\\x_2\\x_3\end{bmatrix}$$

$$A = \begin{bmatrix}
1 & 1 & 1\\
1 & 0 & 0\\
0 & 1 & 0\\
0 & 0 & 1\\
0.2 & 0.1 & 0.3
\end{bmatrix}, \quad
\mathbf{b} = \begin{bmatrix}100\\60\\50\\70\\25\end{bmatrix}$$

Row structure: Row 1 is the demand equality (modeled here as $\le$ and
binding at 100); Rows 2–4 are supplier capacity upper bounds; Row 5 is
the risk policy constraint.

**Optimal solution vector:**
$$\mathbf{x}^* = [10,\,20,\,70]^T \qquad A\mathbf{x}^* \leq \mathbf{b}\;\checkmark \qquad \mathbf{c}^T\mathbf{x}^* = 450$$

---

## 7. Additional Notes

### Model Size
For $|S|$ suppliers, the model contains:
- $|S|$ continuous decision variables
- $1$ equality constraint (demand)
- $1$ inequality constraint (risk)
- $|S|$ implicit upper-bound constraints (capacity)

For the standard 3-supplier example: **3 variables, 2 explicit constraints**.

### Optimal Solution (Standard Case)
For the T1 example ($D=100$, $R^{\max}=25$):

| Supplier | $x_s^*$ | Cost contribution |
|----------|---------|-------------------|
| Supplier1 | 10 | $50.00 |
| Supplier2 | 20 | $120.00 |
| Supplier3 | 70 | $280.00 |
| **Total** | **100** | **$450.00** |

Total risk: $10 \times 0.2 + 20 \times 0.1 + 70 \times 0.3 = 2 + 2 + 21 = 25 \leq 25$ (binding)

### Key Insight: Risk-Cost Trade-off
The risk constraint acts as a penalty on cheap-but-risky suppliers. Without C3, the optimizer would order as much as possible from Supplier3 (cheapest at \$4/unit) and fill the remainder with Supplier1. The risk limit forces a blend toward Supplier2 (safest at $r=0.1$), increasing cost but improving supply reliability.

### Sensitivity Analysis
The shadow price of the risk constraint (C3) measures how much the objective improves per unit relaxation of $R^{\max}$. A tighter risk limit (e.g., $R^{\max}=15$) forces greater reliance on Supplier2, increasing total cost - confirming the binding nature of the risk constraint.

### LP Structure
This is a pure **Linear Program (LP)**. Gurobi solves it via the simplex or barrier method, typically reaching optimality in 0 iterations after presolve due to the small problem size.
