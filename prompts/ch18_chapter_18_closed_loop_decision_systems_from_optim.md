# Chapter 18  Closed-Loop Decision Systems: From Optimization to Adaptive Control - AI Updates, DI Decides

> **Tip:** Scan the QR code in the Appendix to copy and paste this prompt directly into ChatGPT, Claude, Gemini, or any AI assistant.

---

## Experiment Prompt

```
You are participating in an experiment comparing AI-only reasoning versus explicit Decision Intelligence (DI) formulation for a closed-loop re-optimization problem.

A data center allocates workloads across two servers. Each server has CPU and Memory capacity constraints.

INITIAL STATE
-------------
Server capacities:
- Server 1: CPU 6, Memory 8
- Server 2: CPU 6, Memory 7

Workloads:
- W1: value 10, CPU 4, Memory 6
- W2: value 8,  CPU 3, Memory 4
- W3: value 7,  CPU 2, Memory 3
- W4: value 6,  CPU 3, Memory 2

PART 1 — INITIAL OPTIMIZATION
Solve the initial workload assignment to maximize total value within server capacity constraints.
Provide:
- assigned workloads per server
- total value
- whether all capacity constraints are satisfied

ONE HOUR LATER — CONDITIONS CHANGE
------------------------------------
- Server 2 memory drops from 7 → 6
- Value of W3 increases from 7 → 11

PART 2 — RE-OPTIMIZATION
Without starting from scratch, determine:
- Is the current assignment still feasible?
- Is it still optimal?
- What is the new optimal assignment?
- What changed and why?

PART 3 — COMPARISON TABLE
| Approach | Detected Infeasibility? | Re-optimized Correctly? | New Total Value | Confidence |
Include rows for:
- AI-only reasoning
- DI optimization approach

PART 4 — OBSERVATIONS
Discuss:
- whether AI-only reasoning detected that re-optimization was needed
- whether AI reasoning produced a correct updated assignment
- whether the DI approach re-solved systematically
- implications for real-time systems where conditions change continuously
- whether AI alone is sufficient for closed-loop decision systems
```

---
*From: AI Is Not Enough — Chapter 18  Closed-Loop Decision Systems: From Optimization to Adaptive Control - AI Updates, DI Decides*
*Repository: https://github.com/Klinkert/ai-is-not-enough-companion*
