# CIA 2
To create a Markov Decision Process (MDP)-based Reinforcement Learning (RL) agent for a 100x100 grid with obstacles, we will outline the environment setup, MDP formulation, and the implementation of both Dynamic Programming (DP) methods and Q-learning. We will also see why SARSA tends to be slower compared to Q-learning.

## Environment Setup
The environment consists of a **100x100 grid** where:
- The agent starts at the bottom-left corner (0,0) and aims to reach the top-right corner (99,99).
- Obstacles are placed in a line between two randomly selected points on the grid, which restrict movement.
- Each cell represents a possible state for the agent.

## MDP Formulation
### States
Each cell $$(x, y)$$ in the grid corresponds to a state, resulting in a total of **10,000 states**.

### Actions
The agent can perform one of four actions:
- **Up**
- **Down**
- **Left**
- **Right**

### Transition Probabilities
The transitions are deterministic:
- When an action is taken, the agent moves to the adjacent cell in the chosen direction unless blocked by an obstacle or boundary, in which case it remains in its current state.

### Rewards
The reward structure is as follows:
- **+100** for reaching the goal state.
- **-1** for each step taken to encourage finding the shortest path.
- No additional penalty for hitting obstacles, as the time wasted serves as a natural penalty.

### Discount Factor ($$\gamma$$)
A discount factor close to 1 (e.g., **0.99**) is used to balance immediate and future rewards, promoting exploration towards the goal.

## Dynamic Programming Methods
### Value Iteration
This method computes the optimal value function for each state by iteratively evaluating possible actions and their expected future rewards. It results in an optimal policy that maps states to actions.

### Policy Iteration
Policy iteration alternates between:
1. **Policy Evaluation**: Calculating the value function for a given policy.
2. **Policy Improvement**: Updating the policy based on the current value function until convergence to an optimal policy.

## Q-Learning
Q-learning is a model-free RL algorithm that learns the optimal action-value function (Q-function) through exploration and exploitation:
- The agent explores its environment and updates its Q-values based on received rewards.
- The learning process continues until convergence or until early stopping criteria are met based on average rewards over episodes.
  
## Visualization
The implementation includes visualizing:
- The grid environment with obstacles.
- Learned policies from DP methods.
- The learning curve of Q-learning showing rewards over episodes.

## Why SARSA is Slower than Q-Learning
SARSA (State-Action-Reward-State-Action) is typically slower than Q-learning due to its inherent nature of updating Q-values based on the action actually taken by the agent rather than the optimal action. Here are key reasons for this difference:

1. **On-policy Learning**: SARSA is an on-policy algorithm that updates its Q-values based on the current policy being followed. This means it can be less efficient because it may not always take advantage of exploring more optimal actions during learning.

2. **Exploration vs. Exploitation**: In SARSA, if an agent chooses a suboptimal action due to exploration, it updates its Q-value based on this less favorable outcome. In contrast, Q-learning updates its values using the maximum possible future reward (greedy approach), leading to faster convergence towards optimal policies.

3. **Learning Rate Sensitivity**: SARSA's performance can be more sensitive to its learning rate and exploration strategy compared to Q-learning, which can adaptively learn from all experiences more effectively.

In summary, while both algorithms aim to find optimal policies in an MDP framework, Q-learning generally converges faster due to its off-policy nature and use of maximum future rewards for updates.

Citations:

[1] https://motion.cs.illinois.edu/RoboticSystems/PlanningWithDynamicsAndUncertainty.html

[2] https://repository.gatech.edu/server/api/core/bitstreams/90cbab29-afab-4772-8080-76e8157bbea5/content

[3] https://apps.dtic.mil/sti/tr/pdf/ADA367893.pdf

[4] https://www.cse.iitm.ac.in/~ravi/courses/Reinforcement%20Learning_files/Solution3.pdf

[5] https://cs.stanford.edu/people/karpathy/reinforcejs/gridworld_dp.html

[6] https://ocw.mit.edu/courses/16-410-principles-of-autonomy-and-decision-making-fall-2010/75e2c8c2cf31b874c239ba2e8126fb35_MIT16_410F10_lec23.pdf

[7] https://www.researchgate.net/publication/221456732_Solving_multiagent_assignment_Markov_decision_processes

[8] https://cdn.aaai.org/ojs/9041/9041-13-12569-1-2-20201228.pdf
