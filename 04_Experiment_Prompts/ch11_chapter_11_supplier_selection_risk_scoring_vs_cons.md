# Chapter 11  Supplier Selection: Risk Scoring vs Constrained Sourcing

> **Tip:** Copy/paste this prompt directly into ChatGPT, Claude, Gemini, or any AI assistant.

---

## Experiment Prompt

```
You are participating in an experiment comparing AI-only reasoning versus explicit Decision Intelligence (DI) formulation for a constrained supplier selection problem.
A company must procure exactly 100 units of a critical component from three suppliers.
The suppliers have the following characteristics:
Supplier 1:
- Unit cost: $5 per unit
- Risk rate: 0.2 per unit
- Maximum capacity: 60 units
Supplier 2:
- Unit cost: $6 per unit
- Risk rate: 0.1 per unit
- Maximum capacity: 50 units
Supplier 3:
- Unit cost: $4 per unit
- Risk rate: 0.3 per unit
- Maximum capacity: 70 units
Constraints:
- Total procurement must equal exactly 100 units
- Total risk exposure (sum of risk rate × units for each supplier) must not exceed 25
- Each supplier cannot supply more than their stated capacity
The objective is to minimize total procurement cost while satisfying demand, capacity, and risk constraints.
Your task is to solve this problem in TWO ways.
----------------------------------------
PART 1 — AI-ONLY REASONING
----------------------------------------
Do not explicitly formulate the problem using mathematical optimization, linear programming, mixed-integer programming, or exhaustive enumeration.
Solve the problem naturally as a reasoning-oriented AI assistant.
Provide:
- recommended supplier allocations (units from each supplier)
- expected total procurement cost
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
- recommended supplier allocations
- expected total procurement cost
- whether the solution is guaranteed feasible
- explanation of the optimization result
----------------------------------------
PART 3 — COMPARISON TABLE
----------------------------------------
Provide a comparison table with the following columns:
| Approach | Supplier Strategy | Expected Cost | Feasible? | Confidence | Observations |
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
- scalability implications as the number of suppliers and constraints increases
- whether explicit constraints improved explainability and confidence
- whether larger or reasoning-oriented language models may still struggle as combinatorial complexity grows without formal optimization
```

---
*From: AI Is Not Enough — Chapter 11  Supplier Selection: Risk Scoring vs Constrained Sourcing*
*Repository: https://github.com/Klinkert/ai-is-not-enough-companion*
