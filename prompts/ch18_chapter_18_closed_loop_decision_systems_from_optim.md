# Chapter 18  Closed-Loop Decision Systems: From Optimization to Adaptive Control - AI Updates, DI Decides

> **Tip:** Scan the QR code in the Appendix to copy and paste this prompt directly into ChatGPT, Claude, Gemini, or any AI assistant.

---

## Experiment Prompt

```
You are participating in an experiment comparing AI-only reasoning versus explicit Decision Intelligence (DI) formulation for a constrained closed-loop AI infrastructure optimization problem.
An AI infrastructure platform continuously receives changing workload demand throughout the day.
At the current optimization cycle, the workloads are:
Training Job A:
- GPU requirement: 8 GPUs
- Expected business value: 15
Inference Service B:
- GPU requirement: 5 GPUs
- Expected business value: 11
Analytics Job C:
- GPU requirement: 4 GPUs
- Expected business value: 8
Realtime Service D:
- GPU requirement: 6 GPUs
- Expected business value: 13
The infrastructure currently has 16 GPUs available.
The optimization process repeats every 5 minutes as workload demand changes.
The objective is to maximize total business value while staying within available GPU capacity during each optimization cycle.
Your task is to solve this problem in TWO ways.
----------------------------------------
PART 1 — AI-ONLY REASONING
----------------------------------------
Do not explicitly formulate the problem using mathematical optimization, adaptive control methods, integer programming, or exhaustive enumeration.
Solve the problem naturally as a reasoning-oriented AI assistant.
Provide:
- recommended workload allocation
- expected total business value
- total GPU utilization
- explanation of reasoning
- confidence in the solution
- how the allocation might change during future workload cycles
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
- recommended workload allocation
- expected total business value
- total GPU utilization
- whether the solution is guaranteed feasible
- explanation of the optimization result
- how the optimization process could repeat continuously as workload conditions change
----------------------------------------
PART 3 — COMPARISON TABLE
----------------------------------------
Provide a comparison table with the following columns:
| Approach | Allocation Strategy | Total Business Value | GPU Utilization | Feasible? | Confidence | Observations |
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
- scalability implications as workload volatility and infrastructure constraints increase
- whether explicit constraints improved explainability and confidence
- whether larger or reasoning-oriented language models may still struggle as dynamic combinatorial complexity grows without formal optimization
- why repeated re-optimization becomes important in closed-loop operational systems
This example is intentionally simple. In small dynamic allocation problems, AI reasoning and optimization methods may sometimes produce similar answers. As workloads fluctuate continuously and infrastructure environments become larger and more dynamic, informal reasoning becomes increasingly unreliable. Decision Intelligence methods provide the structure required for scalable, adaptive, and operationally feasible closed-loop decision systems.
```

---
*From: AI Is Not Enough — Chapter 18  Closed-Loop Decision Systems: From Optimization to Adaptive Control - AI Updates, DI Decides*
*Repository: https://github.com/Klinkert/ai-is-not-enough-companion*
