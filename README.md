# BlackJack - Reinforcement Learning Agent


## I. Overview

Reinforcement Learning(RL) is a type of machine learning technique that enables an agent to learn in an interactive environment by trial and error using feedback from its own actions and experiences. Both supervised and reinforcement learning use mapping between input and output. But supervised learning is where feedback provided to the agent is correct set of actions for performing a task while reinforcement learning uses rewards and punishment as signals for positive and negative behavior. As compared to unsupervised learning, reinforcement learning is different in terms of goals. While the goal in unsupervised learning is to find similarities and differences between data points, in reinforcement learning the goal is to find a suitable action model that would maximize the total cumulative reward of the agent.

I will be using our knowledge of reinforcement learning to design a RLAgent to play Blackjack game.  Blackjack is a game of cards where any number of players can be involved in the game against a dealer and the aim is to obtain a sum of cards equal to or less than 21. If the player gets cards whose sum is greater than 21, the player is busted. We have been given an option to implement either Q-learning or SARSA for the assignment. Also towards the end we are asked to implement the maze agent and test it against different maze input sizes and for that we will be using the codes provided by the professor in the class notes. 





## II. Problems

### Blackjack

Blackjack is a card game which is played with the goal to get a sum of cards equal to or less than 21 without going over. There can be any number of players playing against a single dealer. In our game, face cards have point value of 10. Aces can either count as 11 or 1, and it's called 'usable' at 11. This game is placed with an infinite deck. 

The game starts with each player getting two face up cards and dealer having one face up and face down card and the player needs to bet an amount of money within range of 1 to max bet (10). Note: Face up means that you will know what the card is.
The player can request additional cards (hit=1) until they decide to stop (stick=0) or exceed 21 (bust). After the player sticks, the dealer reveals their facedown card, and draws until their sum is 17 or greater (fixed policy). If the dealer goes bust the player wins. You won't see the dealer's facedown card, just you will know if you have or lost and you will get appropriate reward of +1 if you win, -1 if you loose or 0 if the match is drawn. (It is freedom of choice for you to change the reward function. If you want to change, you should explain the reason of the change.)

If the player wins, the amount he has bet will be doubled and given back. If the player and dealer have the same sum, then its a draw and the player will get back the money he has bet. If the player loses then, the money he bet will be lost. If neither player nor dealer busts, the outcome (win, lose, draw) is decided by whose sum is closer to 21. You are free to change the reward function to make it learn more efficiently. (i.e., the amount of money the user is winning after each round).

## Methods

### SARSA

State–action–reward–state–action (SARSA) is an algorithm for learning a Markov decision process policy, used in the reinforcement learning area of machine learning. A SARSA agent interacts with the environment and updates the policy based on actions taken, hence this is known as an on-policy learning algorithm. The Q value for a state-action is updated by an error, adjusted by the learning rate alpha. Q values represent the possible reward received in the next time step for taking action a in state s, plus the discounted future reward received from the next state-action observation.


### Q-learning

Q-learning is a model-free reinforcement learning algorithm. The goal of Q-learning is to learn a policy, which tells an agent what action to take under what circumstances. It does not require a model (hence the connotation "model-free") of the environment, and it can handle problems with stochastic transitions and rewards, without requiring adaptations. For any finite Markov decision process (FMDP), Q-learning finds a policy that is optimal in the sense that it maximizes the expected value of the total reward over any and all successive steps, starting from the current state. Q-learning can identify an optimal action-selection policy for any given FMDP, given infinite exploration time and a partly-random policy. "Q" names the function that returns the reward used to provide the reinforcement and can be said to stand for the "quality" of an action taken in a given state.


### Choice of TD learning and Reason

#### Temporal Difference:

Temporal difference (TD) learning refers to a class of model-free reinforcement learning methods which learn by bootstrapping from the current estimate of the value function. These methods sample from the environment, like Monte Carlo methods, and perform updates based on current estimates, like dynamic programming methods. While Monte Carlo methods only adjust their estimates once the final outcome is known, TD methods adjust predictions to match later, more accurate, predictions about the future before the final outcome is known. 

#### Choice of Temporal Difference Learning Approach:

##### Q-learning: 

This assignment requires us to select one of the two approaches, that is, SARSA or Q-learning. 
SARSA uses its current policy and Q-value of the next state to update the Q-value of a given state. This makes it "on-policy" learning whereas Q-learning uses an epsilon-greedy policy and Q-value of the next state to update the Q-value of a given state. This makes it "off-poicy" learning.

For this assignment, I choose to use Q-learning because then my model can explore all possible states to select the most optimal path by exploring all the paths. I chose to use Q-learning because it has the ability to find the optimal path independent of the policy used in traversing and updating the Q-values of the states. Thus, this will help me find an optimal path instead of a near optimal path.



### Choice of Function Approximation and Reason

Q-learning can be combined with function approximation as it makes it possible to apply the algorithms to larger problems even when the state space is continuous. I am using Q-table as my function approximator. It is basically a lookup table where we calculate the maximum expected future rewards for action at each state. So, basically it will guide us to the best action at each state. We are using q-table because it works as a reference table for our agent to select the best action based on the q-value. I would have opted for neural network as function approximator, but due to limited time I could not implement that. Hence I am using Q-table as my approximator.

