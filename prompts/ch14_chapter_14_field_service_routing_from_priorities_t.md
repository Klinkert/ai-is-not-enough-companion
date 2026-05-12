# Chapter 14  Field Service Routing: From Priorities to Feasible Paths

> **Tip:** Scan the QR code in the Appendix to copy and paste this prompt directly into ChatGPT, Claude, Gemini, or any AI assistant.

---

## Experiment Prompt

```
You are participating in an experiment comparing AI-only reasoning versus explicit Decision Intelligence (DI) formulation for a constrained field service routing problem.
A field service technician must visit customer locations during a single workday.
The locations are:
Customer A:
- Priority score: 8
- Travel time required: 2 hours
Customer B:
- Priority score: 6
- Travel time required: 3 hours
Customer C:
- Priority score: 10
- Travel time required: 5 hours
Customer D:
- Priority score: 5
- Travel time required: 2 hours
The technician has a maximum of 8 available work hours.
The objective is to maximize total customer priority served while staying within the available work time.
Your task is to solve this problem in TWO ways.
----------------------------------------
PART 1 — AI-ONLY REASONING
----------------------------------------
Do not explicitly formulate the problem using mathematical optimization, routing algorithms, vehicle routing methods, or exhaustive enumeration.
Solve the problem naturally as a reasoning-oriented AI assistant.
Provide:
- recommended customer visit plan
- expected total priority served
- total work time used
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
- recommended customer visit plan
- expected total priority served
- total work time used
- whether the solution is guaranteed feasible
- explanation of the optimization result
----------------------------------------
PART 3 — COMPARISON TABLE
----------------------------------------
Provide a comparison table with the following columns:
| Approach | Routing Strategy | Total Priority Served | Total Time | Feasible? | Confidence | Observations |
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
- scalability implications as additional locations, technicians, and routing constraints are added
- whether explicit constraints improved explainability and confidence
- whether larger or reasoning-oriented language models may still struggle as combinatorial complexity grows without formal optimization
This example is intentionally simple. In small routing problems, AI reasoning and optimization methods may sometimes produce similar answers. As the number of locations, technicians, travel constraints, schedules, and operational dependencies increases, informal reasoning becomes increasingly unreliable. Decision Intelligence methods provide the structure required for scalable and operationally feasible routing decisions.
```

---
*From: AI Is Not Enough — Chapter 14  Field Service Routing: From Priorities to Feasible Paths*
*Repository: https://github.com/Klinkert/ai-is-not-enough-companion*
