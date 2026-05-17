# Chapter 16  Resource Assignment: Matching Supply to Demand

> **Tip:** Copy/paste this prompt directly into ChatGPT, Claude, Gemini, or any AI assistant.

---

## Experiment Prompt

```
You are participating in an experiment comparing AI-only reasoning versus explicit Decision Intelligence (DI) formulation for a constrained resource assignment problem.
Three technicians must each be assigned to exactly one of three jobs. Each job must be assigned exactly one technician. The objective is to find the one-to-one assignment that minimizes total cost.
Cost of assigning each technician to each job:
Tech A: Job 1 = 9, Job 2 = 2, Job 3 = 7
Tech B: Job 1 = 6, Job 2 = 4, Job 3 = 3
Tech C: Job 1 = 5, Job 2 = 8, Job 3 = 1
Constraints:
- Each technician must be assigned to exactly one job
- Each job must be assigned to exactly one technician
- Assignments must be one-to-one (no sharing)
The objective is to minimize total assignment cost.
Your task is to solve this problem in TWO ways.
----------------------------------------
PART 1 — AI-ONLY REASONING
----------------------------------------
Do not explicitly formulate the problem using mathematical optimization, assignment algorithms, linear programming, or exhaustive enumeration.
Solve the problem naturally as a reasoning-oriented AI assistant.
Provide:
- recommended technician-to-job assignments
- expected total cost
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
- recommended technician-to-job assignments
- expected total cost
- whether the solution is guaranteed feasible
- explanation of the optimization result
----------------------------------------
PART 3 — COMPARISON TABLE
----------------------------------------
Provide a comparison table with the following columns:
| Approach | Assignment Strategy | Total Cost | Feasible? | Confidence | Observations |
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
- scalability implications as additional technicians, jobs, and constraints are added
- whether explicit constraints improved explainability and confidence
- whether larger or reasoning-oriented language models may still struggle as combinatorial complexity grows without formal optimization
```

---
*From: AI Is Not Enough — Chapter 16  Resource Assignment: Matching Supply to Demand*
*Repository: https://github.com/Klinkert/ai-is-not-enough-companion*
