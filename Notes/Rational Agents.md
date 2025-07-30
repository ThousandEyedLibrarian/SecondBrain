An 'agent' generally has sensors to perceive an environment, and actuators to act upon that environment.

A *rational* agent, **selects actions that maximises it's expected utility in the environment**, naturally this involves the agent having a set of preferences over the set of possible choices it can make.

These preference relations are called *rational* if they exhibit both [[Completeness]] and [[Transitivity]].

## Agent Environments

Environments can be fully or partially observable, i.e. does the agent have all the information in the environment available to it or just a subset.

They can also be dynamic or static, self-explanatory, does it change or not.

Actions taken can be discrete or continuous, do X or not, vs. turn a wheel by any angle between 0 and 180.

Environments can also be deterministic or stochastic, i.e. have an element of randomness (stochastic) or not (deterministic).

Your problem may be episodic or sequential, i.e. the problem sequence doesn't matter vs. sequential where the sequence of things does.

Environments can also be known or unknown, does the agent know what elements in the environment result in (red mushroom in Mario) vs. does it not (changing the mushroom to purple).

Environments can be polynomial if the number of states grows polynomially with the input size, same for exponential.

## Agent Planning vs. Execution

Planning is where the agent simulates the effects of different actions to construct an idealised plan for goal achievement, execution is the agent trying to follow that step-by-step in the environment, validating as it goes against any environmental changes.


See also:
- [[Machine Learning]]
- [[Agents]]
- [[Artificial Intelligence (AI)]]
- [[Tree Search]]
- [[Graph Search]]