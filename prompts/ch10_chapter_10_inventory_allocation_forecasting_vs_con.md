# Chapter 10  Inventory Allocation: Forecasting vs Constrained Distribution

> **Tip:** Scan the QR code in the Appendix to copy and paste this prompt directly into ChatGPT, Claude, Gemini, or any AI assistant.

---

## Experiment Prompt

```
You are participating in an experiment comparing AI-only reasoning versus explicit Decision Intelligence (DI) formulation for a constrained inventory allocation problem.

A supply chain team must distribute inventory from two warehouses to two retail stores.

Supply available:
- Warehouse 1: 50 units
- Warehouse 2: 40 units

Demand at each store:
- Store 1: up to 60 units
- Store 2: up to 50 units

Value generated per unit shipped:
- Warehouse 1 → Store 1: 8
- Warehouse 1 → Store 2: 6
- Warehouse 2 → Store 1: 7
- Warehouse 2 → Store 2: 9

The objective is to maximize total shipment value while respecting warehouse supply limits and store demand limits.

Your task is to solve this problem in TWO ways.

----------------------------------------
PART 1 — AI-ONLY REASONING
----------------------------------------
Do not explicitly formulate the problem using mathematical optimization, linear programming, or transportation models.

Solve the problem naturally as a reasoning-oriented AI assistant.

Provide:
- units shipped on each route
- total value
- explanation of reasoning
- confidence in the solution

----------------------------------------
PART 2 — DECISION INTELLIGENCE (DI) APPROACH
----------------------------------------
Now solve the same problem using formal Decision Intelligence formulation.

Define:
- decision variables
- objective function
- constraints

Then solve the problem using optimization.

Provide:
- the formulation
- units shipped on each route
- total value
- whether all supply and demand constraints are satisfied
- explanation of the optimization result

----------------------------------------
PART 3 — COMPARISON TABLE
----------------------------------------
Provide a comparison table with the following columns:
| Approach | Route Allocations | Total Value | All Constraints Met? | Confidence | Observations |

Include rows for:
- AI-only reasoning
- DI optimization approach

----------------------------------------
PART 4 — OBSERVATIONS
----------------------------------------
Discuss:
- whether AI-only reasoning correctly coordinated supply across both warehouses simultaneously
- whether the DI approach produced a globally optimal allocation
- whether greedy or heuristic reasoning led to suboptimal routes
- scalability implications as warehouses, stores, and routes increase
- whether explicit supply and demand constraints improved solution quality
```

---

*From: AI Is Not Enough — Chapter 10 Inventory Allocation*
*Repository: https://github.com/Klinkert/ai-is-not-enough-companion*
