# Finite Time Horizon:
- Initial state `s`
- Finite time Horizon *T*
	- Objective: Find a sequential decision policy $\pi$ maximizing the expected reward up to time *T*
	$$
	R(s_1 , a^\pi_1 ,  s^\pi_1 ,...,  s^\pi_T, a^\pi_T )
	$$
	Maximize over $\pi$: $E[R(s_1 , a^\pi_1 ,  s^\pi_1 ,...,  s^\pi_T, a^\pi_T )]$
	where E is the expected value.
	
So the reward is dependent on the policy as we can since the state and action in state is also dependet on the policy $\pi$. We show this affet of the policy by using the $\pi$ superscript.

### Finite Horizon MDP:
- Objective: find a Policy $\pi$ that is Markov deterministic:

$$
E[\sum^T_{t=1} r_t(s^\pi_t, a^\pi_t)]
$$

#### The value function
- The value function is the maximal expected reward depending on the time horizon `T` and the initial state `s`:
$$
V^*_T(s) = sup_{\pi \in md } V^\pi_T(s)
$$
The star means its the best possible value function. Sup means it gives the largest expected value of the policy $\pi$.

Where $V^*_T(s)$ is the average reward achieved under policy $\pi$ with initial state `s`, i.e ;
$$
V^*_T(s) = E [\sum^T_{t+1}r_t(s^\pi_t, a^\pi_t) | s^\pi_1=s]
$$

we usually omit the last part $s^\pi_1=s$ and just write
$$
V^*_T(s) = E_s [\sum^T_{t+1}r_t(s^\pi_t, a^\pi_t)]
$$

### Policy Evaluation
Note here that we will be calculating the expected reward of a policy we are given.
So say that we wish to compute
$$

$$

---
Status:
tags: [[Markov Decision Processes]] - [[Reinforcment learning]]
date:2021-03-29
