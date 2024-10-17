# Connect-4-Reinforcement-learning

# Background and Motivation:
Connect Four is a two players game which takes place on a 7x6 rectangular board placed vertically between them. One player has 21 blue coins and the other 21 red coins. Each player can drop a coin at the top of the board in one of the seven columns; the coin falls down and fills the lower unoccupied square. Of course a player cannot drop a coin in a certain column if it's already full (i.e. it already contains six coins). 
Even if there's no rule about who begins first, we assume, as in chess, that the lighter side makes the first move. We also use the chess notation to represent a square on the board. That is, we number rows from 1 to 7 starting from the bottom and the columns from 1 to 6 starting from the leftmost.
# Problem statement
   The rules of the game are as follows:
   Every player tries to connect their coin type in a sequence of 4.
     After every move by any player, the status of the game is checked whether it is over. 
     A  game is considered over in the following scenarios:
  Either of the players have 4 coins on the board in a sequence vertically, horizontally or   diagonally
The board is full that is after 42 moves none of the players got a sequence of 4. In this case the game is a tie.
Using the above rules, the problem statement is to develop an AI using Reinforcement Learning and train it to play with human players and try to maximize the number of wins by the AI.
# Purpose/Motivation
The purpose/ motivation of this project is mainly to identify and understand the difference in implementation and results of Connect 4 using AlphaGo, Monte Carlo Tree Search, Q Learning and DQN.
# Differentiator/Contribution (what is different about your project from what is currently available in the literature)
Connect 4 has already been implemented using AlphaGo and Monte Carlo Tree Search. We implemented the game using QLearning and DQN.
# Methodology
## Environment
The connect 4 board
## Agent
To train the agent, select Train Computer in the main menu. It will play iterations games which was passed as an argument to the program.After training the computer, when 'vs Computer' option is selected, a human can play against the trained computer.Each time 'Train Computer' mode is selected, it trains from the beginning.
The state space is all the states which each player sees. For the first player it consists all the boards with an even number of disks, while for the second player it is all the boards with an odd number of disks.The action space will be the numbers 1–7 for each column a player can play.The reward will be 1 for winning, -1 for losing, 0.5 for a tie and 0 otherwise.
Note here that like in every 2-players’ game, the next state is not determined by the action taken because it depends also on the opponent’s action. The transition probability between 2 states depends on both the player’s and the opponent’s policies.
## Policies
The playing policy is e-greedy where the epsilon is chosen randomly.The epsilon factor determines whether to take a random move or an optimal move based on the Q function learnt.The discount factor decays after every iteration during training.In the beginning we have encouraged exploration (random values)Latter stage of training, we encouraged the computer to learn to play against more optimal players.
## Q-Learning
The state space is all the states which each player sees. For the first player it consists all the boards with even number of disks, while for the second player it is all the boards with odd number of disks.The action space will be the numbers 1–7 for each column a player can play.The reward will be 1 for winning, -1 for losing, 0.5 for a tie and 0 otherwise. The targets were calculated according to the Q learning algorithm:
Q(s,a) = Q(s,a) + α(max(Q(s’,a’))+gR-Q(s,a)) where Q is the Q function, s is the state, a is the action, α is the learning rate, R is the reward and g is the discount factor.
## DQN
The Neural network to approximate the Q-value function.The state is given as the input and the Q-value of all possible actions is generated as the output.The loss function here is mean squared error of the predicted Q-value and the target Q-value – Q*. 

<img width="677" alt="Screen Shot 2020-03-01 at 12 19 15 AM" src="https://user-images.githubusercontent.com/41890348/75622168-66e5bf00-5b52-11ea-83b6-dca4a4cdada0.png">
Experience replay has the largest performance improvement in DQN. Target network improvement is significant but not as critical as the replay. But it gets more important when the capacity of the network is small

# DQN-Game Logic
First, a game object is created with arguments like board_size.
Next, two player objects are created which will play against each other. Every player object has its default brain which could be overridden by creating a custom brain object and assigning it to the player. Brain object is the place where the algorithms reside.
Next, an environment object is created and two players along with the game objects are put in this environment by passing them as arguments.
Finally, this environment is run which runs the game, takes actions from the players, and sends them back next state of the game and rewards of their actions.
#Q-Learning Logic 
Creating a class that represents an AI using Q-learning algorithm start by initialize a Q-learner with parameters epsilon, alpha and gamma and its coin type( 0 or 1). Then, get Q function returns a probability for a given state and action where the greater the probability the better the move. After that, choose action function will return an action based on the best move recommendation by the current Q-Table with an epsilon chance of trying out a new move.
Lastly, learn function is to determine the reward based on its current chosen action and update the Q table using the reward received and the maximum future reward based on the resulting state due to the chosen action.

# Results
<img width="546" alt="Screen Shot 2020-03-01 at 12 27 07 AM" src="https://user-images.githubusercontent.com/41890348/75622284-7dd8e100-5b53-11ea-9d8d-8b52c31e6fa1.png">
<img width="613" alt="Screen Shot 2020-03-01 at 12 26 53 AM" src="https://user-images.githubusercontent.com/41890348/75622285-7f0a0e00-5b53-11ea-8ae3-c3c9ebdbb4c7.png">
<img width="707" alt="Screen Shot 2020-03-01 at 12 24 58 AM" src="https://user-images.githubusercontent.com/41890348/75622286-803b3b00-5b53-11ea-912a-66e9f365351c.png">

# Conclusion
One major challenge of DQNs with only win / loss conditions is measuring the network performance over time. We have found a few ways to do this, including having the agent play a short term reward maximizing symbolic AI every N games as validation. If  agent cannot beat an agent that only thinks in the short term, then we need to continue making changes to the network structure, hyper-parameters, and feature representation. Beating this short sighted AI consistently should be our first goal.We must also make sure our training data and labels are formatted in a way to ensure stability. Rewards should be normalized in the [-1., 1.] range, and any discounted future reward which is outside of this range should be clipped.Another factor to consider is the optimizer learning rate. A high learning rate can create instabilities in the neural networks state approximation behavior, resulting in all kinds of catastrophic forgetfulness. Starting at 0.001 is a good idea, and if you note instabilities with this try decreasing it from there. We find that 0.0001 works optimally for longer training sessions.
