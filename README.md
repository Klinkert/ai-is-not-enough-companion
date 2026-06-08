# AI Is Not Enough — Companion Code

**Solver-verified optimization models for Chapters 8–19**  
*By Dr. A.J. Klinkert*

---

## Two Notebooks — One for Every Reader

| Notebook | Solver | Requirement |
|----------|--------|-------------|
| `AI_Is_Not_Enough_Companion_Code.ipynb` | Google OR-Tools (CPU) | Python 3.8+, any OS, no GPU needed |
| `AI_Is_Not_Enough_cuOPT_Edition2.2.ipynb` | NVIDIA cuOPT (GPU) | NVIDIA GPU, Linux or WSL2 |

**Both notebooks produce identical solutions.** The solver is the execution layer. The model structure is invariant. This is the book's central thesis demonstrated in code.

---

## Edition 1 — OR-Tools (CPU, any machine)

No GPU required. Runs on Windows, Mac, or Linux.

### Run in your browser (no install)

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Klinkert/ai-is-not-enough-companion/blob/main/AI_Is_Not_Enough_Companion_Code.ipynb)

### Run locally

```bash
pip install ortools
jupyter notebook AI_Is_Not_Enough_Companion_Code.ipynb
```

---

## Edition 2 — NVIDIA cuOPT (GPU-accelerated)

Requires an NVIDIA GPU (Compute Capability ≥ 7.0) and Linux or WSL2.  
Features a dual-backend design: set `BACKEND = 'cuopt'` for GPU or `BACKEND = 'scipy'` for CPU fallback — same interface either way.

### Hardware requirements

| Component | Minimum |
|-----------|---------|
| GPU | NVIDIA Compute Capability ≥ 7.0 (any RTX 20/30/40 series) |
| Driver | ≥ 527.41. Check with: `nvidia-smi` |
| Python | 3.10 – 3.12 (not 3.13) |
| OS | Linux or WSL2. Native Windows will fail. |

### Need help setting up your environment?

Paste the following prompt into [claude.ai](https://claude.ai) and Claude will walk you through setup step by step for your specific machine — WSL2, native Linux, or Google Colab:

> *"I want to run the GPU companion notebook for 'AI Is Not Enough' by Dr. A.J. Klinkert. It uses NVIDIA cuOPT and requires Python 3.10–3.12 on Linux or WSL2. My machine is: [describe your OS and GPU, e.g. Windows 11, RTX 4070]. Please walk me through setup step by step."*

### Install cuOPT (inside WSL2 Ubuntu or Linux terminal)

```bash
conda create -n cuopt python=3.12 -y
conda activate cuopt
pip install --extra-index-url https://pypi.nvidia.com/ cuopt-cu12 scipy numpy jupyter
```

### Launch

```bash
jupyter notebook AI_Is_Not_Enough_cuOPT_Edition2.2.ipynb
```

---

## Chapter Index

| Chapter | Problem | Type |
|---------|---------|------|
| 8  | Lead Prioritization | Binary Knapsack |
| 9  | Marketing Budget Allocation | Linear Programming |
| 10 | Inventory Allocation | Transportation LP |
| 11 | Supplier Selection | LP with Cost + Risk |
| 12 | Contact Center Staffing | Integer Programming |
| 13 | Production Scheduling | Single Machine MIP |
| 14 | Field Service Routing | Vehicle Routing (VRP) |
| 15 | Distribution Logistics | Network Flow LP |
| 16 | Resource Assignment | Assignment Problem |
| 17 | Data Center Resource Allocation | Multi-Dimensional Knapsack |
| 18 | Dynamic Re-Optimization | Closed-Loop AI + DI |
| 19 | cuOPT Reference — All Problems | GPU-Accelerated Templates |

---

## Requirements Summary

**Edition 1:** Python 3.8+, `pip install ortools`

**Edition 2:** Python 3.10–3.12, Linux or WSL2, NVIDIA GPU CC ≥ 7.0,  
`pip install --extra-index-url https://pypi.nvidia.com/ cuopt-cu12`

---

## License

Code is provided for educational use by readers of *AI Is Not Enough*.  
© Dr. A.J. Klinkert. All rights reserved.
