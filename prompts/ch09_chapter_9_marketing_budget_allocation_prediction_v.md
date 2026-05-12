# Chapter 9  Marketing Budget Allocation: Prediction vs Constrained Optimization

> **Tip:** Scan the QR code in the Appendix to copy and paste this prompt directly into ChatGPT, Claude, Gemini, or any AI assistant.

---

## Experiment Prompt

```
You are participating in an experiment comparing AI-only reasoning versus explicit Decision Intelligence (DI) formulation for a constrained marketing budget allocation problem.
A company has a $100,000 marketing budget to allocate across three channels.
Estimated campaign returns are:
Digital Advertising:
- Expected return rate: 12%
Email Campaigns:
- Expected return rate: 10%
Industry Events:
- Expected return rate: 18%
Constraints:
- At least $20,000 must be allocated to Digital Advertising
- No more than $40,000 may be allocated to Industry Events
- The total marketing budget cannot exceed $100,000
Your task is to solve this problem in TWO ways.
----------------------------------------
PART 1 — AI-ONLY REASONING
----------------------------------------
Do not explicitly formulate the problem using mathematical optimization, linear programming, resource allocation methods, or exhaustive enumeration.
Solve the problem naturally as a reasoning-oriented AI assistant.
Provide:
- recommended budget allocation
- expected total return
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
- recommended budget allocation
- expected total return
- whether the solution is guaranteed feasible
- explanation of the optimization result
----------------------------------------
PART 3 — COMPARISON TABLE
----------------------------------------
Provide a comparison table with the following columns:
| Approach | Allocation Strategy | Expected Return | Feasible? | Confidence | Observations |
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
- scalability implications as the number of channels and constraints increases
- whether explicit constraints improved explainability and confidence
- whether larger or reasoning-oriented language models may still struggle as combinatorial complexity grows without formal optimization
```

---
*From: AI Is Not Enough — Chapter 9  Marketing Budget Allocation: Prediction vs Constrained Optimization*
*Repository: https://github.com/Klinkert/ai-is-not-enough-companion*
