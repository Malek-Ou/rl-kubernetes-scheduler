# Reinforcement Learning for Adaptive Scheduling in Kubernetes

## Overview

This project explores the use of **Reinforcement Learning (RL)** to design an **adaptive pod scheduler for Kubernetes**.  
Instead of relying on static heuristics used by the default Kubernetes scheduler, the proposed approach trains an RL agent to dynamically optimize pod placement based on cluster state and workload characteristics.

The solution is implemented as a **simulated OpenAI Gym environment** and trained using **Proximal Policy Optimization (PPO)**.  
Performance is evaluated against the **default Kubernetes scheduler** and a **random scheduling policy**.

This work was developed as an **academic mini-project in Telecommunications Engineering** at **ENET’COM – University of Sfax (2025–2026)**.

---
## Technologies Used

- Python 3  
- OpenAI Gym  
- Stable-Baselines3  
- NumPy  
- Matplotlib  
- TensorBoard  
- Jupyter Notebook  
---
## Project Objectives

- Model a Kubernetes-like cluster as a Reinforcement Learning environment  
- Train an RL agent to optimize pod placement decisions  
- Compare RL-based scheduling with:
  - Kubernetes heuristic-based scheduler  
  - Random baseline policy  
- Study the impact of realistic constraints, such as pod waiting time  

---
## Environments Description

### Environment 1 – Simplified (Non-Realistic)

- No waiting-time constraint for pods  
- Used primarily for training and initial validation  
- Demonstrates the effectiveness of PPO compared to baseline schedulers  

**Key characteristics**
- 10 nodes  
- 20 pods  
- Immediate scheduling decisions  

**Results**
- PPO achieves ~83% successful pod placement  
- Outperforms both heuristic and random schedulers  

---

### Environment 2 – Realistic (With Waiting-Time Constraint)

- Introduces a maximum waiting time for pods  
- More representative of real Kubernetes scheduling challenges  
- Highlights limitations of reward design and state representation  

**Key characteristics**
- 10 nodes  
- 50 pods  
- Maximum wait time = 3  

**Results**
- PPO performance degrades  
- Reveals the importance of:
  - Reward shaping  
  - State completeness  
  - Sufficient exploration during training  

---

## Reinforcement Learning Approach

- **Algorithm:** Proximal Policy Optimization (PPO)  
- **Framework:** Stable-Baselines3  
- **Environment API:** OpenAI Gym  

### State Space
- CPU and memory utilization of each node  
- Resource requirements of the incoming pod  

### Action Space
- Select one of the available nodes  
- Or skip scheduling (in constrained scenarios)  

### Reward Function (Simplified)
- Positive reward for successful placement  
- Bonus for balanced resource usage  
- Penalty for delays and inefficient decisions  

---
## How to Run the Project
```bash
git clone https://github.com/Malek-Ou/rl-kubernetes-scheduler.git
cd rl-kubernetes-scheduler


