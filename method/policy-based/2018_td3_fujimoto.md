# Addressing Function Approximation Error in Actor-Critic Methods
* Scott Fujimoto, Herke van Hoof, David Meger
* icml2018
* http://proceedings.mlr.press/v80/fujimoto18a.html
* https://arxiv.org/abs/1802.09477
* https://github.com/sfujim/TD3 # pytorch
* https://www.youtube.com/watch?v=x33Vw-6vzso&feature=youtu.be

## problem
* in an actor-critic setting,
  * function approximation errors lead to overestimated value estimates and
  * the accumulation of error in temporal difference methods and suboptimal policies

## observation
* While in the discrete action setting overestimation bias is
  an obvious artifact from the analytical maximization,
  * the presence and effects of overestimation bias is less clear
    in an actor-critic setting.

## idea
* core
  * takes the **minimum** value between a pair of critics to restrict overestimation and
  * **delays policy updates** to reduce per-update error
* a clipped Double Q-learning variant (a pair of critics along with a single actor) which
  * favors underestimations by
    bounding situations where Double Q-learning does poorly.
    * preferable as underestimations do not tend to be propagated during learning,
      as states with a low value estimate are avoided by the policy
* address variance reduction by
  * show that target networks, a common approach in deep Q-learning methods, are
    critical for variance reduction.
  * propose delaying policy updates until each target has converged,
    in order to address the coupling of value and policy
  * introduce a novel regularization strategy, where
    a SARSA-style update bootstraps similar action estimates to further reduce variance.

## setup
* critic:
  * a clipped Double Q-learning variant
* nets
  * arch: fully-connected
  * optim: Adam
  * activ-fn: relu, relu, tanh
* openai gym mujoco task
  * max average return over 10 trials of 1 millions timesteps
*  both networks receive the state and action as input to the first layer

## result
* TD3 > (DDPG, ACKTR, PPO from OpenAI baselines) in gym mujoco
* suggest delaying policy updates to reduce per-update error and further improve performance.
* TD3 greatly reduces overestimation by the critic
  * graph the average value estimate over 10000 states and
    compare it to an estimate of the true value.
    * the true value is estimated using the average discounted return over 1000
      evaluations following the current policy, starting from states sampled from the buffer replay

## background
* In temporal difference learning (Sutton, 1988)
  an estimate of the value function is updated using the estimate of a sub- sequent state.
  * If this subsequent estimate is far from the true value, then the update might be poor.
  * Furthermore, each update leaves some residual error which is then
    repeatedly propagated throughout the state space by the nature of the temporal difference update.
  * This accumulated error can cause arbitrarily bad states to be estimated as high value,
    resulting in sub-optimal policy updates and divergent behavior
* With a discrete action space, a greedy policy that selects the highest valued action is often used.
  * However, in a continuous action space, the value-maximizing action **cannot usually** be found analytically.
  * Instead, actor-critic meth- ods can be used, where the policy, known as the actor, is
    trained to maximize the estimated expected return defined by the value estimate, known as the critic.
  * The policy can be updated through the deterministic policy gradient theorem (Silver et al., 2014)

## comment
* fn approx err is indeed present
* td3= ddpg + doubleQlearning
  * well, doubling the Q-network (for Double Q-learning) may be costly
* one of contribs:
> suggest delaying policy updates to reduce per-update error and further improve performance
* (-) no atari xprmt
* (-) use -v1 of OpenAI Mujoco
* (?) max average return?
