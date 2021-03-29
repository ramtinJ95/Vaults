# Markov Decision Processes
For these examples with Markov decision process's which are [[finite time horizon MDP's]] or [[discounted infinite time horizon MDP's]] we are simply solving for the value function or learning the optimal policy, in other words there is no learning going on here since we are given all the system dynamics.

### MDP's
- Fully observable state and reward
- Known reward distribution and transition probabilities

#### Markovian Dynamics
$$
P[s_{t+1} | h_t , a_t] = P_t (s_{t+1}|s_t, a_t ) 
$$

This equation says that the probability distribution of ending up in some state *s* at time *t+1* is dependent on the previous state only and the action performed in that state at time *t*

#### Finite Time Horizon
- 


---
Status:
tags: [[Reinforcment learning]] - [[050 Machine Learning]] - [[Markov Chains]]
date:2021-03-29
