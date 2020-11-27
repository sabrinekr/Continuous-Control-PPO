# Introduction
For this project, we implemented a DDPG agent to solve the [Reacher](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Learning-Environment-Examples.md#reacher) environment.

[![Trained Agent](https://github.com/hortovanyi/DRLND-Continuous-Control/blob/master/output/reacherp_ddpg_agent_small.gif?raw=true)](https://www.youtube.com/watch?v=N1vWkCfbEGQ)

In this environment, a double-jointed arm can move to target locations. A reward of +0.1 is provided for each step that the agent's hand is in the goal location. Thus, the goal of your agent is to maintain its position at the target location for as many time steps as possible.

The observation space consists of 33 variables corresponding to position, rotation, velocity, and angular velocities of the arm. Each action is a vector with four numbers, corresponding to torque applicable to two joints. Every entry in the action vector should be a number between -1 and 1.

# Learning Algorithm
The deep deterministic policy gradient (DDPG) algorithm is a policy-gradient actor-critic algorithm proposed by Google Deep Mind to solve continuous action space problems. It's also an off-policy and model free algorithm and is presented as the DQN of the continuous action space and it can only be used for it. 
The DDPG involves four neural networks: the critic neural network, the actor neural network, the critic target neural network and the actor target neural network.

It also uses a replay buffer R.

* The actor neural network: The actor neural network maps the states into actions. It will take as an input the current state and will output one action from a continuous action space. The weights of the actor neural network are first initialized randomly. Then, they are updated using the deterministic policy gradient theorem.

* The critic neural network: The critic neural network takes as input the current state and the action given by the actor and outputs the estimated Q-value of the action-state couple. The goal of the critic neural network is to evaluate the policy given by the actor neural network using the temporal difference error. The weights of the critic neural network are first initialized randomly, then they are updated using the gradients from the loss function L.


* Target networks: In order to avoid the divergence of our learning algorithm the ddpg uses actor target network and critic target network. The actor target network and the critic target network are initialized with respectively the same weights of the actor network and the critic network. Then, they are soft updated.

* Exploration: In a discrete action space we explore the environment with different methods such as the epsilon-greedy policy and the Boltzman strategy. Without exploration the policy is deterministic and to make the ddpg explore more effectively we add noise to the action returned by the network.

# Model architecture
The actor has a target and local networks having the same architecture:
* 1 fully connected layer of size 128 followed by ReLu activation function. 
* Batch normalisation on the first layer output.
* 1 fully connected layer of size 128 followed by ReLu activation function.
* 1 fully connected layer of size 4 (the size of the action space) followed by tanh activation function. 

The critic has a target and local networks having the same architecture:
* 1 fully connected layer of size 128 followed by ReLu activation function. 
* Batch normalisation on the first layer output.
* 1 fully connected layer of size 128 followed by ReLu activation function.
* 1 fully connected layer of size 1.


# Hyperparameters 
Our agent was trained using the follwing hyperparameters: 
* Buffer size: the size of the experience replay buffer is 100 000
* Batch size: the batch size of the training is 128
* Gamma: the discount factor 0.99
* TAU learning rate coefficient for soft update of target parameters is 0.001
* The learning rate of the actor is 2e-4
* The learning rate of the critic is 2e-4


# Results

The agent was able to solve the environment after 514 episodes with the average score of 13.08 during the last 100 episodes.

![Image of Yaktocat](https://github.com/sabrinekr/Continuous-Control-PPO/blob/main/images/ddpg.png?raw=true)

# Ideas for Future Work
We still can improve our results by using the following algorithms: 
* PPO
* A3C
* D4PG