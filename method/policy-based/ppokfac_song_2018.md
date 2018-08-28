# An Empirical Analysis of Proximal Policy Optimization with Kronecker-factored Natural Gradients
* https://arxiv.org/abs/1801.05566

## problem
* Both PPO and ACKTR are state-of-the-art in their respective regimes
  * PPO obtains the advantage through the clipping objective function that can be easily optimized, while 
  * ACKTR achieves higher performance through (an approximation of) natural gradient updates. 
  * How would an algorithm perform if we combine the advantages of both fronts?

## setup
* For the critic, we consider the Gauss-Newton matrix, which is
equivalent to the Fisher for a Gaussian observation model

## result
* PPOKFAC > PPO
  * in terms of sample complexity and speed in a range of MuJoCo environments, 
    while being scalable in terms of batch size. 
* PPOKFAC < ACKTR.    
* adding more epochs is not necessarily helpful for sample efficiency
* combining the advantages of both sides does not seem to improve sample complexity as expected; 
  * the objective and optimization procedure that works for SGD does not necessarily work for K-FAC
  * the PPO objective implicitly defines a trust region through ratio clipping, and 
    this overlaps with the learning rate selection criteria of ACKTR.
  * ACKTR takes much larger step-sizes than PPO and 
    taking more iterations with such a step size might hurt performance (for example, in value function estimation).

## background
* Policy gradient methods: current state-of-the-art
  (take different approaches to better sample efficiency)
  * Proximal Policy Optimization ( Schulman et al. [2017]) 
    * considers a particular “clipping” objective that mimics a trust-region,
    * penalizes the new policy to be far from the old policy without explicitly enforcing the trust region constraint.
    * optimized through stochastic gradients descent (PPO-SGD)
  * ACKTR [Wu et al., 2017].
    * considers approximated natural gradients that balances speed and optimization.
    
