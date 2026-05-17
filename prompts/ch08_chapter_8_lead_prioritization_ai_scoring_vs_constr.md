# Chapter 8  Lead Prioritization: AI Scoring vs Constrained Selection

> **Tip:** Copy/paste this prompt directly into ChatGPT, Claude, Gemini, or any AI assistant.

---

## Experiment Prompt

```
You are participating in an experiment comparing AI-only reasoning versus explicit Decision Intelligence (DI) formulation for a constrained lead prioritization problem.
A sales team has 10 hours available tomorrow to contact leads.
Each lead has:
- a predicted value score
- an estimated outreach duration
The leads are:
Lead A: Value 10, Time 2
Lead B: Value 7, Time 3
Lead C: Value 15, Time 5
Lead D: Value 6, Time 4
Lead E: Value 18, Time 6
Your task is to solve this problem in TWO ways.
----------------------------------------
PART 1 — AI-ONLY REASONING
----------------------------------------
Do not explicitly formulate the problem using mathematical optimization, integer programming, dynamic programming, knapsack methods, or exhaustive enumeration.
Solve the problem naturally as a reasoning-oriented AI assistant.
Provide:
- selected leads
- total value
- total outreach time
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
- selected leads
- total value
- total outreach time
- whether the solution is guaranteed feasible
- explanation of the optimization result
----------------------------------------
PART 3 — COMPARISON TABLE
----------------------------------------
Provide a comparison table with the following columns:
| Approach | Selected Leads | Total Value | Total Time | Feasible? | Confidence | Observations |
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
- scalability implications as the number of leads increases
- whether explicit constraints improved explainability and confidence
- whether larger or reasoning-oriented language models may still struggle as combinatorial complexity grows without formal optimization
This experiment is intentionally small. In tiny problems such as this one, AI reasoning, heuristics, human intuition, and optimization methods may sometimes converge on similar answers. The distinction becomes far more important as scale, constraints, dependencies, uncertainty, and time relationships increase. That is where formal Decision Intelligence methods become increasingly necessary.
```

---
*From: AI Is Not Enough — Chapter 8  Lead Prioritization: AI Scoring vs Constrained Selection*
*Repository: https://github.com/Klinkert/ai-is-not-enough-companion*
