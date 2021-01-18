---
layout: post
title:  "Generalized Advantage Estimation"
---

Personal notes on the Generalized Advantage Estimation Paper

The paper is concerned with how to estimate the advantage function for use in the policy gradient theorem. If we use the one step advantage estimator, $$ r + \gamma v(s') - v(s)$$, it has low variance, but high bias if the value function approximator $$V$$ is inaccurate. However, a n-step advantage estimator, which does $$ r + \gamma r_1 + \gamma^2 r_2.... \gamma^n V(s_n) - V(s)$$, has very low bias even if V is approximate, as the weightage given to $$\gamma^n V(s_n)$$ is nearly zero, since $$\gamma$$ is less than 1. 

However, this estimator has high variance since it involves a summation of multiple reward terms which are stochastic. Hence one-step estimator is high bias, low variance, n-step estimator is low bias, high variance. The paper proposes a weighted combination of one step, 2 step, ..n step advantage estimator, similar to TD($$\lambda$$), but for advantage functions, called the generalized advantage estimate (GAE). 
