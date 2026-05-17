# Chapter 18  Closed-Loop Decision Systems: From Optimization to Adaptive Control - AI Updates, DI Decides

> **Tip:** Copy/paste this prompt directly into ChatGPT, Claude, Gemini, or any AI assistant.

---

## Experiment Prompt — Two Steps

Send Step 1 first. Wait for a complete answer. Then send Step 2 as a follow-up in the same conversation.

---

### STEP 1

```
You are solving a workload placement problem for a data center.

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

Assign the workloads to maximize total value while respecting all constraints.

Provide:
- which workloads are assigned to Server 1
- which workloads are assigned to Server 2
- total value of assigned workloads
- verification that all CPU and memory constraints are satisfied
```

— Wait for a complete answer before sending Step 2 —

---

### STEP 2

*Send this as a follow-up in the same conversation — do not re-solve from scratch.*

```
One hour has passed. Conditions have changed:
- Server 2 memory capacity drops from 7 → 6
- The value of W3 increases from 7 → 11

Using your current assignment from Step 1, answer the following:

1. Is the current assignment still feasible under the new constraints?
2. Is the current assignment still optimal given the new values?
3. What is the best assignment under the new conditions?
4. What is the new total value?

Do not start over. Update your existing answer.
```

---

## Correct Answers

**Step 1:** Server 1 = {W1} | Server 2 = {W2, W3} | Total value = **25**

**Step 2:** The old assignment is infeasible (Server 2 memory: 4+3=7 > 6).
New optimal: Server 1 = {W2, W3} | Server 2 = {W1} | Total value = **29**

---
*From: AI Is Not Enough — Chapter 18  Closed-Loop Decision Systems: From Optimization to Adaptive Control - AI Updates, DI Decides*
*Repository: https://github.com/Klinkert/ai-is-not-enough-companion*
