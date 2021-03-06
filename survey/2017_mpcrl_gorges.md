# Relations between Model Predictive Controland Reinforcement Learning
* Daniel Görges
* https://www.sciencedirect.com/science/article/pii/S2405896317311941

* Model predictive control (aka receding horizon control)
  * is model-based, not adaptive,and has a high online complexity, 
  * but also has a mature stability, feasibility and robustness theory as well as an in-herent constraint handling

* Reinforcement learning 
  * is model-free, is adaptive, and has a low online complexity, 
  * but also has an immature stability,feasibility and robustness theory as well as a diﬃcult con-straint handling. 

* the notion of stability is **diﬀerent** 
  (a uniﬁed stability and robustness theory isnot available yet)
  * control systems:
    * concentrates on stability of the closed-loop system
  * computational intelligence:
    * focuses on stability, or more precisely convergence,of the learning algorithm.
    * Stability of the closed-loop system is essentially addressed with certainty equivalence
    
## related
> Sutton, R.S., Barto, A.G., and Williams, R.J. (1992). Reinforcement learning is direct adaptive optimal control.
IEEE Control Systems Magazine, 12(2), 19–22.

## comment
* ? is MPC value- or policy-based?
* here, RL refers to model-free RL
