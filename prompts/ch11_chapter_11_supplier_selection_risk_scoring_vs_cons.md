# Chapter 11  Supplier Selection: Risk Scoring vs Constrained Sourcing

> **Tip:** Scan the QR code in the Appendix to copy and paste this prompt directly into ChatGPT, Claude, Gemini, or any AI assistant.

---

## Experiment Prompt

```
You are participating in an experiment comparing AI-only reasoning versus explicit Decision Intelligence (DI) formulation for a constrained supplier selection problem.
A company must procure at least 100 units of material from suppliers.
The suppliers have the following characteristics:
Supplier A:
- Unit cost: $5
- Risk score: 1
- Maximum capacity: 40 units
Supplier B:
- Unit cost: $4
- Risk score: 2
- Maximum capacity: 50 units
Supplier C:
- Unit cost: $3
- Risk score: 4
- Maximum capacity: 80 units
Constraints:
- Total procurement must be at least 100 units
- Total supplier risk score must not exceed 25
The objective is to minimize total procurement cost while satisfying demand and risk constraints.
Your task is to solve this problem in TWO ways.
----------------------------------------
PART 1 — AI-ONLY REASONING
----------------------------------------
Do not explicitly formulate the problem using mathematical optimization, linear programming, mixed-integer programming, or exhaustive enumeration.
Solve the problem naturally as a reasoning-oriented AI assistant.
Provide:
- recommended supplier allocations
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
- whether larger or reasoning-oriented language models may still struggle as combinatorial complexity grows without formal optimization.
```

---
*From: AI Is Not Enough — Chapter 11  Supplier Selection: Risk Scoring vs Constrained Sourcing*
*Repository: https://github.com/Klinkert/ai-is-not-enough-companion*
