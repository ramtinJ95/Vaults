# Markov Chains
A sequence of random variables (r.v's) with values in *S* is a Markov chain iff for all `n >= 1` and all j,i,...,i<sub>n</sub> ∈ *S*

$$P(X_{n+1} = j | X_1 = i_i ,..., X_n = i_n  ) = P(X_{n+1} | X_n = i_n) $$

This essentially means that the state is dependent on the previous state. So there is no memory in the system.

The transition matrix for homogeneous Markov chains:
$$
P_{ij} = P(X_{n+1} = j | X_n = i), \forall i,j \in S
$$

#### Reflected Random Walk
Say we have a system as below with some set of states *S*. Also assume that this system of states has transition probablities such that *P*<sub>0,1</sub> = *P*<sub>n, n-1</sub> = 1
And for all other states that are not 0,1 or N (in this case N is 4) the probability is *1/2*.


![[Screenshot 2021-03-29 at 23.36.44.png]]

Reflected means that once we reach limiting states such as s = N = 4 or s = 0 there is a 100% probability (since we can see above that the probability is 1 for these states) we go the other direction at next time step.

---
Status: #🌱 
tags: [[Reinforcment learning]] - [[050 Machine Learning]]
date:2021-03-29
