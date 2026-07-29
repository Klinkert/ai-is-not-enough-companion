# Problem 10 — Supply Chain Inventory Allocation: Mathematical Formulation

## 1. Sets and Indices

| Symbol | Description | Values |
|--------|-------------|--------|
| $W$ | Set of warehouses | $W = \{\text{WH1},\ \text{WH2}\}$ |
| $S$ | Set of retail stores | $S = \{\text{S1},\ \text{S2}\}$ |
| $R \subseteq W \times S$ | Set of valid shipping routes | All warehouse-store pairs |

---

## 2. Parameters

| Symbol | Description | Values |
|--------|-------------|--------|
| $s_w$ | Available supply at warehouse $w$ | WH1 = 50, WH2 = 40 |
| $d_j$ | Maximum demand at store $j$ | S1 = 60, S2 = 50 |
| $v_{wj}$ | Value per unit shipped from warehouse $w$ to store $j$ | See table below |

### Value Matrix $v_{wj}$

|  | S1 | S2 |
|--|----|----|
| **WH1** | 8 | 6 |
| **WH2** | 7 | 9 |

---

## 3. Decision Variables

$$x_{wj} \geq 0 \quad \forall\ (w, j) \in R$$

where $x_{wj}$ is the **number of units shipped** from warehouse $w$ to store $j$.

This is a **continuous linear program (LP)** — fractional shipment quantities are permitted.

---

## 4. Objective Function

Maximize total value generated across all shipment routes:

$$\text{Maximize} \quad Z = \sum_{(w,j) \in R} v_{wj} \cdot x_{wj}$$

Expanded:

$$Z = 8\,x_{\text{WH1,S1}} + 6\,x_{\text{WH1,S2}} + 7\,x_{\text{WH2,S1}} + 9\,x_{\text{WH2,S2}}$$

---

## 5. Constraints

### C1 — Warehouse Supply Limit
Total units shipped from each warehouse cannot exceed its available inventory:

$$\sum_{j \in S} x_{wj} \leq s_w \quad \forall\ w \in W$$

Expanded:

$$x_{\text{WH1,S1}} + x_{\text{WH1,S2}} \leq 50$$
$$x_{\text{WH2,S1}} + x_{\text{WH2,S2}} \leq 40$$

### C2 — Store Demand Cap
Total units received by each store cannot exceed its stated demand:

$$\sum_{w \in W} x_{wj} \leq d_j \quad \forall\ j \in S$$

Expanded:

$$x_{\text{WH1,S1}} + x_{\text{WH2,S1}} \leq 60$$
$$x_{\text{WH1,S2}} + x_{\text{WH2,S2}} \leq 50$$

### C3 — Non-negativity

$$x_{wj} \geq 0 \quad \forall\ (w, j) \in R$$

---

## 6. Complete Model Formulation

$$\begin{aligned}
\text{Maximize} \quad & 8\,x_{\text{WH1,S1}} + 6\,x_{\text{WH1,S2}} + 7\,x_{\text{WH2,S1}} + 9\,x_{\text{WH2,S2}} \\[6pt]
\text{subject to} \quad 
& x_{\text{WH1,S1}} + x_{\text{WH1,S2}} \leq 50 & \text{(WH1 supply)} \\
& x_{\text{WH2,S1}} + x_{\text{WH2,S2}} \leq 40 & \text{(WH2 supply)} \\
& x_{\text{WH1,S1}} + x_{\text{WH2,S1}} \leq 60 & \text{(S1 demand)} \\
& x_{\text{WH1,S2}} + x_{\text{WH2,S2}} \leq 50 & \text{(S2 demand)} \\
& x_{\text{WH1,S1}},\ x_{\text{WH1,S2}},\ x_{\text{WH2,S1}},\ x_{\text{WH2,S2}} \geq 0
\end{aligned}$$

---

## 6a. Matrix Form (Added 2026-07-29)

*Not present in the original Gurobi Modeler output — added to match the
book's existing Part 5 (Generalized and Instantiated Matrix Form), which
already carries this exact matrix.*

Stack variables warehouse-major: $\mathbf{x} = [x_{11},\ x_{12},\ x_{21},\ x_{22}]^T$
(i.e. $x_{\text{WH1,S1}}, x_{\text{WH1,S2}}, x_{\text{WH2,S1}}, x_{\text{WH2,S2}}$).

$$\text{Maximize} \quad \mathbf{c}^T\mathbf{x} \quad \text{subject to} \quad A\mathbf{x} \leq \mathbf{b}, \quad \mathbf{x} \geq 0$$

$$\mathbf{c} = \begin{bmatrix}8\\6\\7\\9\end{bmatrix}, \quad
A = \begin{bmatrix}
1 & 1 & 0 & 0\\
0 & 0 & 1 & 1\\
1 & 0 & 1 & 0\\
0 & 1 & 0 & 1
\end{bmatrix}, \quad
\mathbf{b} = \begin{bmatrix}50\\40\\60\\50\end{bmatrix}$$

Row structure: Rows 1–2 warehouse supply (WH1, WH2); Rows 3–4 store demand (S1, S2).

**Optimal solution vector:**
$$\mathbf{x}^* = [50,\,0,\,0,\,40]^T \qquad A\mathbf{x}^* \leq \mathbf{b}\;\checkmark \qquad \mathbf{c}^T\mathbf{x}^* = 760$$

---

## 7. Optimal Solution

### Strategy
- WH2 → S2 has the highest value (9): maximize this route first
- WH1 → S1 has the next highest value (8): maximize this route second
- Remaining capacity fills lower-value routes

### Allocation Table

| Route | Units Shipped | Value/Unit | Total Value |
|-------|---------------|------------|-------------|
| WH1 → S1 | 50 | 8 | 400 |
| WH1 → S2 | 0  | 6 | 0   |
| WH2 → S1 | 0  | 7 | 0   |
| WH2 → S2 | 40 | 9 | 360 |
| **Total** | **90** | | **760** |

$$Z^* = 8(50) + 6(0) + 7(0) + 9(40) = 400 + 360 = \mathbf{760}$$

### Summary Table

|  | S1 | S2 | Total Shipped |
|--|----|----|---------------|
| **WH1** | 50 | 0 | 50 / 50 |
| **WH2** | 0 | 40 | 40 / 40 |
| **Total Received** | 50 / 60 | 40 / 50 | 90 |

---

## 8. Additional Notes

### Problem Type Comparison

| Problem | Type | Variables | Key Constraint |
|---------|------|-----------|----------------|
| Problem 8 — Sales Leads | Integer Program (IP) | Binary $x_i \in \{0,1\}$ | Knapsack (time budget) |
| Problem 9 — Marketing Budget | Linear Program (LP) | Continuous $x_i \geq 0$ | Budget equality |
| Problem 10 — Supply Chain | Linear Program (LP) | Continuous $x_{wj} \geq 0$ | Supply + Demand |

### Transportation Problem Structure
Problem 10 is a classic **Transportation Problem** — a special case of LP where:
- Supply nodes (warehouses) have capacity limits
- Demand nodes (stores) have upper bounds on receipt
- Each arc (route) carries a value/cost coefficient
- Total supply (90 units) exceeds total demand capacity (110 units), so not all supply need be shipped

Because total supply $\leq$ total demand ($90 \leq 110$), **all available inventory can be shipped**, and the binding constraints are the warehouse supply limits.
