# Chapter 14  Field Service Routing: From Priorities to Feasible Paths

> **Tip:** Scan the QR code in the Appendix to copy and paste this prompt directly into ChatGPT, Claude, Gemini, or any AI assistant.

---

## Experiment Prompt

```
You are participating in an experiment comparing AI-only reasoning versus explicit Decision Intelligence (DI) formulation for a constrained field service routing problem.

A technician must visit four customer locations and return to the depot. The objective is to find the route that minimizes total travel time.

Travel times between locations (in hours):

From / To   | Depot | A | B | C | D
------------|-------|---|---|---|---
Depot       |   -   | 4 | 6 | 8 | 7
A           |   4   | - | 2 | 5 | 6
B           |   6   | 2 | - | 4 | 3
C           |   8   | 5 | 4 | - | 2
D           |   7   | 6 | 3 | 2 | -

Constraints:
- The technician must start at the depot
- Each location must be visited exactly once
- The technician must return to the depot at the end
- The route must form a single continuous tour

The objective is to minimize total travel time across the complete route.

Your task is to solve this problem in TWO ways.

----------------------------------------
PART 1 — AI-ONLY REASONING
----------------------------------------
Do not use mathematical optimization, TSP solvers, or exhaustive enumeration.

Solve the problem naturally as a reasoning-oriented AI assistant — for example using nearest-neighbor, greedy selection, or intuitive sequencing.

Provide:
- the route sequence (Depot → ... → Depot)
- total travel time
- explanation of how you chose the sequence
- confidence that this is the optimal route

----------------------------------------
PART 2 — DECISION INTELLIGENCE (DI) APPROACH
----------------------------------------
Now solve the same problem using formal Decision Intelligence formulation.

Define:
- decision variables
- objective function
- constraints (including subtour elimination)

Then solve the problem using optimization.

Provide:
- the formulation
- the optimal route sequence
- total travel time
- whether all routing constraints are satisfied
- explanation of the optimization result

----------------------------------------
PART 3 — COMPARISON TABLE
----------------------------------------
Provide a comparison table with the following columns:
| Approach | Route Sequence | Total Travel Time | Optimal? | Confidence | Observations |

Include rows for:
- AI-only reasoning
- DI optimization approach

----------------------------------------
PART 4 — OBSERVATIONS
----------------------------------------
Discuss:
- whether AI-only reasoning produced the globally optimal route or a local approximation
- whether greedy or nearest-neighbor heuristics led to suboptimal sequencing
- whether the DI approach guaranteed a feasible, optimal tour
- how routing complexity grows as locations increase (combinatorial explosion)
- whether AI alone is sufficient for real-world routing decisions at scale
```

---

*From: AI Is Not Enough — Chapter 14 Field Service Routing*
*Repository: https://github.com/Klinkert/ai-is-not-enough-companion*

