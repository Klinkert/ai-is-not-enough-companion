# Chapter 15  Distribution Logistics: From Demand Clusters to Network Flow

> **Tip:** Scan the QR code in the Appendix to copy and paste this prompt directly into ChatGPT, Claude, Gemini, or any AI assistant.

---

## Experiment Prompt

```
You are participating in an experiment comparing AI-only reasoning versus explicit Decision Intelligence (DI) formulation for a constrained distribution logistics problem.
A company must distribute products from distribution centers to customer regions.
The distribution centers have the following supply capacities:
Distribution Center A:
- Available supply: 70 units
Distribution Center B:
- Available supply: 50 units
The customer regions have the following demand requirements:
Region 1:
- Required demand: 40 units
Region 2:
- Required demand: 30 units
Region 3:
- Required demand: 50 units
Estimated transportation costs per unit are:
Distribution Center A → Region 1:
- Cost per unit: 4
Distribution Center A → Region 2:
- Cost per unit: 6
Distribution Center A → Region 3:
- Cost per unit: 8
Distribution Center B → Region 1:
- Cost per unit: 5
Distribution Center B → Region 2:
- Cost per unit: 3
Distribution Center B → Region 3:
- Cost per unit: 4
The objective is to minimize total transportation cost while satisfying all regional demand requirements.
Your task is to solve this problem in TWO ways.
----------------------------------------
PART 1 — AI-ONLY REASONING
----------------------------------------
Do not explicitly formulate the problem using mathematical optimization, transportation models, network flow methods, or exhaustive enumeration.
Solve the problem naturally as a reasoning-oriented AI assistant.
Provide:
- recommended shipment allocations
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
- constraints
Then solve the problem using optimization.
Provide:
- the formulation
- recommended shipment allocations
- expected total transportation cost
- whether the solution is guaranteed feasible
- explanation of the optimization result
----------------------------------------
PART 3 — COMPARISON TABLE
----------------------------------------
Provide a comparison table with the following columns:
| Approach | Distribution Strategy | Expected Transportation Cost | Feasible? | Confidence | Observations |
Include rows for:
- AI-only reasoning
- DI optimization approach
----------------------------------------
PART 4 — OBSERVATIONS
----------------------------------------
Discuss:
- differences between the two approaches
- whether AI-only reasoning appeared heuristic
- whether the DI approach appeared more structured
- scalability implications as additional regions, distribution centers, and transportation constraints are added
- whether explicit constraints improved explainability and confidence
- whether larger or reasoning-oriented language models may still struggle as combinatorial complexity grows without formal optimization
This example is intentionally simple. In small logistics problems, AI reasoning and optimization methods may sometimes produce similar answers. As the number of regions, distribution centers, transportation links, operational constraints, and time dependencies increases, informal reasoning becomes increasingly unreliable. Decision Intelligence methods provide the structure required for scalable and operationally feasible logistics decisions.
```

---
*From: AI Is Not Enough — Chapter 15  Distribution Logistics: From Demand Clusters to Network Flow*
*Repository: https://github.com/Klinkert/ai-is-not-enough-companion*
