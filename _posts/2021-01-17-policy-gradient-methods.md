---
layout: post
title:  "Policy Gradient Methods with Function Approximation"
---

Personal notes on the Generalized Advantage Estimation Paper

Instead of using Monte-carlo return as done in REINFORCE, we can learn a q-value estimator and use it for performance estimation for gradients. The key idea is that if the function approximator for the Q-value function is 'compatible' with the policy (sufficiently powerful, loosely speaking), and the q-value function estimator is at a local minima for the value predictIon error over the trahectory distribution of the current policy - the policy gradient remains unbiased if we use the q-value estimator instead of the Monte carlo estimate. 
