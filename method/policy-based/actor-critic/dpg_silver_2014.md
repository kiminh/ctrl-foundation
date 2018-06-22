# Deterministic Policy Gradient Algorithms
* David Silver et al
* icml2014
* http://proceedings.mlr.press/v32/silver14.pdf
* http://techtalks.tv/talks/deterministic-policy-gradient-algorithms/61098/

## problem
* computing the stochastic policy gradient may **require more samples**,
  especially if the action space has **many** dimensions.
* the stochastic policy gradient harder to estimate,
  * because the policy gradient $\nabla_{\theta} \pi_{\theta}(a|s)$ changes more rapidly near the mean
    * the variance of the stochastic policy gradient for a Gaussian policy $N(\mu,\sigma^2)$ is
      proportional to $1/σ^2$ (Zhao et al., 2012),
      which grows to infinity as the policy becomes deterministic
  * because the policy becomes more deterministic as the algorithm homes in on a good strategy
  * This problem is compounded in high dimensions, as illustrated by the continuous bandit task

## idea: deterministic policy gradients (theorem 1)
* vs stochastic case
  * In the stochastic case: the policy gradient integrates over both state and action spaces,
  * in the deterministic case:  the policy gradient **only** integrates over the state space.
* to choose actions according to a stochastic behaviour policy (to ensure adequate exploration), but
  to **learn about a deterministic target policy** (exploiting the efficiency of the deterministic policy gradient)
  * use the deterministic policy gradient to derive an off-policy actor-critic algorithm that
    estimates the action-value function using a differentiable function approximator, and
  * then updates the policy parameters in the direction of the approximate action-value gradient.
* to explore: learn off-policy using stochastic behaviour policy  
* Deterministic Actor-Critic Algorithms
  * On-Policy Deterministic Actor-Critic
    * using a simple Sarsa critic
  * Off-Policy Deterministic Actor-Critic (OPDAC)
    * using a simple Q-learning critic
    * learn a deterministic target policy from trajectories generated by an arbitrary stochastic behaviour policy
    * updates the policy in the direction of the off-policy deterministic policy gradient.
* Compatible Function Approximation (Theorem 3)
  * such that the true gradient is preserved.
  * For any deterministic policy µθ(s), there always exists a compatible function approximator of the form ...
  * yields Compatible OPDAC (COPDAC)

## setup
* task
  * bandit with 50 continuous action dimensions
  * a high-dimensional task for controlling an octopus arm
  * continuous-action variants: mountain car, pendulum and 2D puddle world.
* experiment focuses on a direct comparison between
  * the stochastic policy gradient: stochastic actor-critic in the bandit task (SAC-B)
  * the deterministic policy gradient: based on COPDAC

## result
* the deterministic policy gradient
  * has a simple model-free form that simply follows the gradient of the action-value function
  * can be **estimated much more efficiently** than the usual stochastic policy gradient,
    especially in high dim cont action spaces
  * update policy in the direction that most improves $Q$
* our algorithms require no more computation than prior methods:
  the computational cost of each update is linear in the action dimensionality and the number of policy parameters
* the deterministic policy gradient theorem is in fact a limiting case of the stochastic policy gradient theorem;
  theorem 2
* COPDAC-B still outperforms SAC-B by a very wide margin that grows larger with increasing dimension
* COPDAC-Q 
  * slightly outper- formed both SAC and OffPAC in all three domains.
  * the octopus arm converged to a good solution in all cases.
* the deterministic policy gradient can be com- puted immediately in closed form
* may view our deterministic actor-critic as analogous, in a policy gradient context, to Q-learning
  * Q-learning learns a deterministic greedy policy, off-policy, while executing a noisy version of the greedy policy
  * analogous to asking whether Q-learning or Sarsa is more efficient
* Our actor-critic algorithms are based on
  model-free, incremental, stochastic gradient updates;
  * suitable when the model is unknown, data is plentiful and computation is the bottleneck

## background
* Policy gradient algorithms typically proceed by sampling this stochastic policy and
  adjusting the policy parameters in the direction of greater cumulative reward.
* Stochastic Policy Gradient Theorem:
  * reduces the computation of the performance gradient to a simple expectation;
    eg: by forming a sample-based estimate of this expectation.
  * One issue: how to estimate the action-value function $Q_{\pi}(s, a)$.
    * simplest approach is to use a sample return,
      which leads to a variant of the REINFORCE algorithm
* It is often useful **to estimate** the policy gradient **off-policy** from trajectories sampled from
  a **distinct behaviour policy**, $\beta(a|s) \neq \pi_{\theta}(a|s)$.
  * In an off-policy setting, the performance objective is typically modified to be
    the **value function of the target policy**, averaged over the **state distribution of the behaviour policy**
  * leads to
    * off-policy policy gradients,
    * Off-Policy Actor-Critic (OffPAC) algorithm:
      * uses a behaviour policy $\beta(a|s)$ to generate trajectories
      * A critic estimates a state-value function, V v(s) ≈ V π(s), **off-policy** from these trajectories,
        by gradient temporal-difference learning (Sutton et al., 2009).
      * An actor updates the policy parameters $\theta$, also **off-policy** from these trajectories,
        by stochastic gradient ascent of Equation 5.
      * Both the actor and the critic use an **importance sampling ratio** to
        adjust for the fact that actions were selected according to $\pi$ rather than $\beta$
* In continuous action spaces, greedy policy improvement becomes problematic, requiring a global maximisation at every step
  * Instead, alternative is to move the policy in the direction of the gradient of Q, rather than globally maximising Q
* the notion of **compatible function approximation** for deterministic policy gradients,
  to ensure that the approximation does not bias the policy gradient.
* In general, behaving according to a deterministic policy will **not ensure** adequate exploration and
  may lead to sub- optimal solutions.
  
## comment
* (?) is deterministic policy more suitable in robotics?
* (?) compatible fn approx using neural nets?