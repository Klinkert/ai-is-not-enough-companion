# Chapter 12  Contact Center Staffing  A Constrained Staffing Problem

> **Tip:** Scan the QR code in the Appendix to copy and paste this prompt directly into ChatGPT, Claude, Gemini, or any AI assistant.

---

## Experiment Prompt

```
You are participating in an experiment comparing AI-only reasoning versus explicit Decision Intelligence (DI) formulation for a constrained contact center staffing problem.
A contact center must schedule agents across four time periods.
Forecasted staffing demand is:
Period 1:
- Required agents: 3
Period 2:
- Required agents: 5
Period 3:
- Required agents: 4
Period 4:
- Required agents: 2
Available shift types are:
Shift S1:
- Covers Periods 1 and 2
- Cost: 4
Shift S2:
- Covers Periods 2 and 3
- Cost: 5
Shift S3:
- Covers Periods 3 and 4
- Cost: 3
Additional understaffing penalty:
- Penalty cost of 10 per uncovered staffing requirement
The objective is to minimize total staffing and understaffing cost while satisfying staffing demand as effectively as possible.
Your task is to solve this problem in TWO ways.
----------------------------------------
PART 1 — AI-ONLY REASONING
----------------------------------------
Do not explicitly formulate the problem using mathematical optimization, workforce scheduling methods, linear programming, or exhaustive enumeration.
Solve the problem naturally as a reasoning-oriented AI assistant.
Provide:
- recommended staffing assignments
- expected staffing shortages, if any
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
- recommended staffing assignments
- expected staffing shortages
- whether the solution is guaranteed feasible
- explanation of the optimization result
----------------------------------------
PART 3 — COMPARISON TABLE
----------------------------------------
Provide a comparison table with the following columns:
| Approach | Staffing Strategy | Staffing Shortages | Feasible? | Confidence | Observations |
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
- scalability implications as additional shifts, labor rules, and staffing constraints are added
- whether explicit constraints improved explainability and confidence
- whether larger or reasoning-oriented language models may still struggle as combinatorial complexity grows without formal optimization
```

---
*From: AI Is Not Enough — Chapter 12  Contact Center Staffing  A Constrained Staffing Problem*
*Repository: https://github.com/Klinkert/ai-is-not-enough-companion*
