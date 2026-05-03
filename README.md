# ai-is-not-enough-companion
Companion code for "AI Is Not Enough" — solver-verified optimization models for Chapters 8–18. Requires OR-Tools.
# AI Is Not Enough — Companion Code

**Solver-verified optimization models for Chapters 8–18**  
*By Dr. A.J. Klinkert*

---

## About This Repository

This is the companion code repository for the book **"AI Is Not Enough."**

Each chapter in the Appendix (Chapters 8–18) presents a real-world decision problem where AI prediction alone is insufficient. This notebook contains the complete Python implementation of every optimization model — solver-verified using Google OR-Tools.

## What You Will Find

| Chapter | Problem | Type |
|---------|---------|------|
| 8  | Lead Prioritization | Binary Knapsack |
| 9  | Marketing Budget Allocation | Linear Programming |
| 10 | Inventory Allocation | Transportation Problem |
| 11 | Supplier Selection | LP with Cost + Risk |
| 12 | Contact Center Staffing | Integer Programming |
| 13 | Production Scheduling | Single Machine Scheduling |
| 14 | Field Service Routing | Vehicle Routing (VRP) |
| 15 | Distribution Logistics | Network Flow |
| 16 | Resource Assignment | Assignment Problem |
| 17 | Data Center Resource Allocation | Multi-Dimensional Knapsack |
| 18 | Dynamic Re-Optimization | Closed-Loop AI + DI |

## How to Use

### Option 1 — Run in your browser (no install)
Click the badge below to open in Google Colab:

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Klinkert/ai-is-not-enough-companion/blob/main/AI_Is_Not_Enough_Companion_Code.ipynb)

### Option 2 — Run locally
```bash
pip install ortools
jupyter notebook AI_Is_Not_Enough_Companion_Code.ipynb
```

## Requirements

- Python 3.8+
- `ortools` (install with `pip install ortools`)

## License

Code is provided for educational use by readers of *AI Is Not Enough*.  
© Dr. A.J. Klinkert. All rights reserved.
