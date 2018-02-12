# rl-foundation

## Topics in RL:
Deep RL,
Bayesian RL,
RL in POMDP,
Hierarchical RL,
Inverse RL,
Safe RL, 
Transfer learning in RL,
Curriculum learning,
Multiagent RL,
Evolutionary RL,
...

## Major taxonomy
model-based _vs_ model-free,
value-based _vs_ policy-based,
episodic _vs_ continuing tasks,
average _vs_ cumulative discounted rewards,
on-policy _vs_ off-policy,
gradient-based _vs_ gradient-free,
...

## People
Goto [thesis](https://github.com/tttor/rl-foundation/tree/master/thesis).

## Quotes
Richard S. Sutton: <br />
Reinforcement Learning: Past, Present and Future?:
"Just as reinforcement learning present took a step away from the ultimate goal of reward to
focus on value functions, so reinforcement learning future may take a further step
away to focus on the structures that enable value function estimation [...] In psy-
chology, the idea of a developing mind actively creating its representations of the
world is called constructivism. My prediction is that for the next tens of years rein-
forcement learning will be focused on constructivism."

Marco Wiering, Martijn van Otterlo: <br/>
Two dominant books:
(1) From an artificial intelligence perspective: Introduction to reinforcement learning by Rich Sutton and Andy Barto from 1998, and
(2) From the standpoint of operations research: Neuro-dynamic programming by Dimitri Bertsekas and John Tsitsiklis in 1996.

## Misc, anonymous, untracked, unknown sources
RL is formalized as MDP, but in which agents only knows about the sets of possible states and actions.
The dynamics, $P(s'|s,a)$, and the reward function, $R(s,a,s')$ are initially unknown; otherwise we have planning problems.

RL is difficult because:
* the blame attribution problem:
  the responsible action may have occurred a long time before the reward was received
* even if the dynamics of the world does not change,
  the effect of an action of the agent depends on what the agent will do in the future.
* the explore-exploit dilemma

RL: learning through interaction with the environment with limited prior knowledge and guidance
