# Chapter 17  Data Center: Matching Workloads for AI Infrastructure with Finite GPU Capacity

> **Tip:** Copy/paste this prompt directly into ChatGPT, Claude, Gemini, or any AI assistant.

---

## Experiment Prompt

```
You are participating in an experiment comparing AI-only reasoning versus explicit Decision Intelligence (DI) formulation for a constrained multi-resource infrastructure allocation problem.

A data center has two servers available for workload placement.

Server capacities:
- Server 1: CPU capacity = 6, Memory capacity = 8
- Server 2: CPU capacity = 6, Memory capacity = 7

Workloads to be assigned:

Workload | Value | CPU Demand | Memory Demand
---------|-------|------------|---------------
W1       |  10   |     4      |       6
W2       |   8   |     3      |       4
W3       |   7   |     2      |       3
W4       |   6   |     3      |       2

Constraints:
- Each workload may be assigned to at most one server
- Each server must not exceed its CPU capacity
- Each server must not exceed its Memory capacity
- Workloads not assigned to any server are simply not run

The objective is to maximize total value of assigned workloads while respecting both CPU and memory limits on each server.

Your task is to solve this problem in TWO ways.

----------------------------------------
PART 1 — AI-ONLY REASONING
----------------------------------------
Do not explicitly formulate the problem using mathematical optimization, integer programming, or exhaustive enumeration.

Solve the problem naturally as a reasoning-oriented AI assistant.

Provide:
- which workloads are assigned to Server 1
- which workloads are assigned to Server 2
- total value of assigned workloads
- explanation of reasoning
- confidence that no better assignment exists

----------------------------------------
PART 2 — DECISION INTELLIGENCE (DI) APPROACH
----------------------------------------
Now solve the same problem using formal Decision Intelligence formulation.

Define:
- decision variables (binary assignment variables per workload per server)
- objective function
- constraints (CPU capacity per server, Memory capacity per server, each workload assigned to at most one server)

Then solve the problem using optimization.

Provide:
- the formulation
- which workloads are assigned to Server 1
- which workloads are assigned to Server 2
- total value
- whether all CPU and memory constraints are satisfied
- explanation of the optimization result

----------------------------------------
PART 3 — COMPARISON TABLE
----------------------------------------
Provide a comparison table with the following columns:
| Approach | Server 1 Workloads | Server 2 Workloads | Total Value | All Constraints Met? | Confidence | Observations |

Include rows for:
- AI-only reasoning
- DI optimization approach

----------------------------------------
PART 4 — OBSERVATIONS
----------------------------------------
Discuss:
- whether AI-only reasoning correctly coordinated across both resource dimensions (CPU and Memory) simultaneously
- whether greedy or priority-based reasoning led to constraint violations or suboptimal placement
- whether the DI approach produced a globally optimal assignment
- how complexity grows as servers, workloads, and resource dimensions increase
- whether AI alone is sufficient for real infrastructure placement decisions at scale
```

---
*From: AI Is Not Enough — Chapter 17  Data Center Resource Allocation*
*Repository: https://github.com/Klinkert/ai-is-not-enough-companion*
