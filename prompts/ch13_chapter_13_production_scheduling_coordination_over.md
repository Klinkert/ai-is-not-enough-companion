# Chapter 13  Production Scheduling: Coordination Over Time and Resources

> **Tip:** Scan the QR code in the Appendix to copy and paste this prompt directly into ChatGPT, Claude, Gemini, or any AI assistant.

---

## Experiment Prompt

```
You are participating in an experiment comparing AI-only reasoning versus explicit Decision Intelligence (DI) formulation for a constrained production scheduling problem.
A factory must schedule three production jobs on a single machine.
The jobs are:
Job A:
- Processing time: 3 hours
Job B:
- Processing time: 2 hours
Job C:
- Processing time: 4 hours
The objective is to determine the production sequence that minimizes total completion time.
Your task is to solve this problem in TWO ways.
----------------------------------------
PART 1 — AI-ONLY REASONING
----------------------------------------
Do not explicitly formulate the problem using mathematical optimization, scheduling algorithms, combinatorial optimization methods, or exhaustive enumeration.
Solve the problem naturally as a reasoning-oriented AI assistant.
Provide:
- recommended production sequence
- expected total completion time
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
- recommended production sequence
- expected total completion time
- whether the solution is guaranteed feasible
- explanation of the optimization result
----------------------------------------
PART 3 — COMPARISON TABLE
----------------------------------------
Provide a comparison table with the following columns:
| Approach | Production Strategy | Expected Completion Time | Feasible? | Confidence | Observations |
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
- scalability implications as additional jobs, machines, and sequencing constraints are added
- whether explicit constraints improved explainability and confidence
- whether larger or reasoning-oriented language models may still struggle as combinatorial complexity grows without formal optimization.
This example is intentionally simple. In small scheduling problems, AI reasoning and optimization methods may sometimes produce similar answers. As the number of jobs, machines, time dependencies, sequencing constraints, and operational objectives increases, informal reasoning becomes increasingly unreliable. Decision Intelligence methods provide the structure required for scalable and operationally feasible production scheduling decisions.
```

---
*From: AI Is Not Enough — Chapter 13  Production Scheduling: Coordination Over Time and Resources*
*Repository: https://github.com/Klinkert/ai-is-not-enough-companion*
