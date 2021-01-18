---
layout: post
title:  "Dueling Network Architectures for Deep Reinforcement Learning"
---


Large number of actions in an MDP, combined with function approximation could easily lead to sub-optimal policies. Even inaccurate q-values for one of the actions in a state will result in a possibly sub-optimal action being chosen. Intuitively, this problem gets worse with the action space cardinality.

A $$Q$$-value has the structure of $$Q(s,a) = V_\pi(s) + A_\pi(s,a)$$, where $$A_\pi(s,a)$$ is the advantage function.

Very loosely speaking, an accurate $$V_\pi(s)$$ gets us halfway there to a correct $$Q_\pi(s,a)$$

Although there are multiple actions in a state, they clearly share the same $$V(s)$$

The paper proposes to learn $$V(s)$$ and $$A_\pi(s,a)$$ seperately to accelerate $$Q(s,a)$$ learning in large action-space MDPs.

Just seperate neural network branches for predicting the 2 doesn't impose sufficient structure. The reason is that we could add a constant value to one branch, and subtract this constant from the other, and it would result in the same Q value (the sum remains same). We need to impose a structure such that the 2 branches actually represent $$V(s)$$ and $$Q(s,a)$$.

To address this issue of identifiability, the authors propose to force the advantage function estimator to have zero advantage at the greedy action. This makes sense, since we are trying to learn the value of the optimal policy, which is greedy w.r.t to the Q-value function. Clearly, the advantage of the greedy action is zero.

$$ Q(s,a;\theta) =  V(s) + (A(s,a) - \max_{a' \in |A}A(s, a' ;\theta))$$


For the greedy action, the second term is zero, and $$Q_\pi(s,a) = V_\pi(s)$$ as expected, as $$\pi$$ is the greedy policy.


The second term is the output of the advantage stream, and the first term is the output of the value stream. 

How does this fix the add/subtract issue we pointed out earlier? Suppose we add an arbitrary value to the value stream. Note now, that the maximum value of the advantage stream is always zero. (because of the max subtraction). We can no longer arbitrarly adjust the output of the stream. Both the stream have the right semantics of the value and the advantage function. 

In practice the authors use a average operation rather than the max operation.




