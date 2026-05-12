# Chapter 16  Resource Assignment: Matching Supply to Demand.

> **Tip:** Scan the QR code in the Appendix to copy and paste this prompt directly into ChatGPT, Claude, Gemini, or any AI assistant.

---

## Experiment Prompt

```
You are participating in an experiment comparing AI-only reasoning versus explicit Decision Intelligence (DI) formulation for a constrained resource assignment problem.
A company must assign employees to projects.
The employees have the following available work capacity:
Employee A:
- Available capacity: 40 hours
Employee B:
- Available capacity: 30 hours
Employee C:
- Available capacity: 50 hours
The projects require the following work effort:
Project 1:
- Required effort: 35 hours
Project 2:
- Required effort: 45 hours
Project 3:
- Required effort: 40 hours
Estimated assignment value scores are:
Employee A:
- Project 1: 9
- Project 2: 6
- Project 3: 5
Employee B:
- Project 1: 7
- Project 2: 8
- Project 3: 6
Employee C:
- Project 1: 5
- Project 2: 7
- Project 3: 9
The objective is to maximize total assignment value while satisfying employee capacity and project effort requirements.
Your task is to solve this problem in TWO ways.
----------------------------------------
PART 1 — AI-ONLY REASONING
----------------------------------------
Do not explicitly formulate the problem using mathematical optimization, assignment algorithms, linear programming, or exhaustive enumeration.
Solve the problem naturally as a reasoning-oriented AI assistant.
Provide:
- recommended employee assignments
- expected total assignment value
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
- recommended employee assignments
- expected total assignment value
- whether the solution is guaranteed feasible
- explanation of the optimization result
----------------------------------------
PART 3 — COMPARISON TABLE
----------------------------------------
Provide a comparison table with the following columns:
| Approach | Assignment Strategy | Expected Assignment Value | Feasible? | Confidence | Observations |
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
- scalability implications as additional employees, projects, and constraints are added
- whether explicit constraints improved explainability and confidence
- whether larger or reasoning-oriented language models may still struggle as combinatorial complexity grows without formal optimization
This example is intentionally simple. In small assignment problems, AI reasoning and optimization methods may sometimes produce similar answers. As the number of employees, projects, skills, dependencies, and operational constraints increases, informal reasoning becomes increasingly unreliable. Decision Intelligence methods provide the structure required for scalable and operationally feasible assignment decisions.
```

---
*From: AI Is Not Enough — Chapter 16  Resource Assignment: Matching Supply to Demand.*
*Repository: https://github.com/Klinkert/ai-is-not-enough-companion*
