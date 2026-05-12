# Chapter 17  Data Center: Matching workloads for AI Infrastructure with finite GPU Capacity

> **Tip:** Scan the QR code in the Appendix to copy and paste this prompt directly into ChatGPT, Claude, Gemini, or any AI assistant.

---

## Experiment Prompt

```
You are participating in an experiment comparing AI-only reasoning versus explicit Decision Intelligence (DI) formulation for a constrained AI infrastructure resource allocation problem.
An AI data center must allocate GPU resources across competing workloads.
The workloads are:
Training Job A:
- GPU requirement: 8 GPUs
- Expected business value: 15
Training Job B:
- GPU requirement: 6 GPUs
- Expected business value: 11
Inference Service C:
- GPU requirement: 4 GPUs
- Expected business value: 9
Analytics Workload D:
- GPU requirement: 5 GPUs
- Expected business value: 10
The data center has a total of 16 GPUs available.
The objective is to maximize total business value while staying within available GPU capacity.
Your task is to solve this problem in TWO ways.
----------------------------------------
PART 1 — AI-ONLY REASONING
----------------------------------------
Do not explicitly formulate the problem using mathematical optimization, resource allocation methods, integer programming, or exhaustive enumeration.
Solve the problem naturally as a reasoning-oriented AI assistant.
Provide:
- recommended workload allocation
- expected total business value
- total GPU utilization
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
- recommended workload allocation
- expected total business value
- total GPU utilization
- whether the solution is guaranteed feasible
- explanation of the optimization result
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
- scalability implications as additional workloads, GPU pools, and infrastructure constraints are added
- whether explicit constraints improved explainability and confidence
- whether larger or reasoning-oriented language models may still struggle as combinatorial complexity grows without formal optimization
This example is intentionally simple. In small infrastructure allocation problems, AI reasoning and optimization methods may sometimes produce similar answers. As the number of workloads, GPU pools, scheduling windows, latency constraints, energy limits, and operational objectives increases, informal reasoning becomes increasingly unreliable. Decision Intelligence methods provide the structure required for scalable and operationally feasible AI infrastructure allocation decisions.
```

---
*From: AI Is Not Enough — Chapter 17  Data Center: Matching workloads for AI Infrastructure with finite GPU Capacity*
*Repository: https://github.com/Klinkert/ai-is-not-enough-companion*
