# Infinite Time Horizon with Discount

- T = infinity
- Stationary transitions and rewards: $p(s'|s,a)$ and $r(s,a)$
- Objective: Maximize the discounted expected reward $\lambda$ $\in$ $[0,1)$
$$
lim_{T \rightarrow \infty} E[ \sum^T_{t=1} \lambda^{t-1} r(s^\pi_t, a^\pi_t)]
$$
For this objective we have a [[geometric decrease]] of the reward. This means that we value the first steps of the system more. 

---
Status:
tags:
date:2021-03-29
