# Chapter 15  Distribution Logistics: From Demand Clusters to Network Flow

> **Tip:** Copy/paste this prompt directly into ChatGPT, Claude, Gemini, or any AI assistant.

---

## Experiment Prompt

```
You are participating in an experiment comparing AI-only reasoning versus explicit Decision Intelligence (DI) formulation for a constrained distribution logistics problem.
A company operates a logistics network with four nodes: a Plant, a Hub, Region 1, and Region 2.
Network supply and demand:
- Plant: supplies 100 units
- Hub: transshipment node (no net supply or demand)
- Region 1: requires 40 units
- Region 2: requires 60 units
Available shipping arcs, unit costs, and capacities:
- Plant → Hub: cost = 2, capacity = 100
- Plant → Region 1: cost = 5, capacity = 40
- Hub → Region 1: cost = 1, capacity = 60
- Hub → Region 2: cost = 3, capacity = 80
The objective is to determine how much product to send on each arc to satisfy all demand at minimum total transportation cost.
Your task is to solve this problem in TWO ways.
----------------------------------------
PART 1 — AI-ONLY REASONING
----------------------------------------
Do not explicitly formulate the problem using mathematical optimization, transportation models, network flow methods, or exhaustive enumeration.
Solve the problem naturally as a reasoning-oriented AI assistant.
Provide:
- recommended flow on each arc
- expected total transportation cost
- explanation of reasoning
- confidence in the solution
----------------------------------------
PART 2 — DECISION INTELLIGENCE (DI) APPROACH
----------------------------------------
Now solve the same problem using formal Decision Intelligence formulation.
Define:
- decision variables
- objective function
- constraints (flow balance, capacity bounds)
Then solve the problem using optimization.
Provide:
- the formulation
- recommended flow on each arc
- expected total transportation cost
- whether all flow balance and capacity constraints are satisfied
- explanation of the optimization result
----------------------------------------
PART 3 — COMPARISON TABLE
----------------------------------------
Provide a comparison table with the following columns:
| Approach | Flow Strategy | Total Cost | All Constraints Met? | Confidence | Observations |
Include rows for:
- AI-only reasoning
- DI optimization approach
----------------------------------------
PART 4 — OBSERVATIONS
----------------------------------------
Discuss:
- whether AI-only reasoning correctly coordinated flow across the full network
- whether the DI approach produced a globally optimal flow pattern
- whether local cheapest-link reasoning led to suboptimal decisions
- scalability implications as the network grows in nodes and arcs
- whether explicit flow balance and capacity constraints improved solution quality
```

---
*From: AI Is Not Enough — Chapter 15  Distribution Logistics: From Demand Clusters to Network Flow*
*Repository: https://github.com/Klinkert/ai-is-not-enough-companion*
