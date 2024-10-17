# Connect-4 Reinforcement Learning Project

## Background and Motivation
Connect Four is a strategic, two-player game played on a 7x6 vertical grid. Each player has 21 tokens—one player uses blue, and the other uses red. Players alternate turns, dropping their tokens into one of the seven columns, where it falls to the lowest available position. Columns become unavailable when they are filled with six tokens.

Although the game doesn't enforce who goes first, we assume that the lighter-colored tokens begin, much like in chess. We utilize chess-style notation to reference board positions, with rows numbered 1 to 7 (bottom to top) and columns numbered 1 to 6 (left to right).

## Problem Statement
The primary objective is for each player to align four of their tokens in a row—vertically, horizontally, or diagonally. The game state is checked after each move, with the game ending under the following conditions:
- A player connects four tokens in a straight line.
- The board becomes fully occupied (42 moves) without a player connecting four, resulting in a draw.

Our goal is to develop an AI using Reinforcement Learning techniques to play against human players, aiming to maximize its winning potential.

## Purpose and Motivation
This project aims to explore and analyze different AI strategies for Connect 4, specifically focusing on comparing AlphaGo, Monte Carlo Tree Search (MCTS), Q-Learning, and Deep Q-Networks (DQN).

## Unique Contribution
While previous Connect 4 implementations have primarily used AlphaGo and MCTS approaches, this project introduces the use of Q-Learning and DQN techniques to train the AI.

## Methodology

### Environment
The AI operates within the standard Connect 4 grid.

### Agent Training
To train the AI agent, users can select the "Train Computer" mode. The program runs a specified number of training games, after which the AI is ready for human competition. Training resets each time this mode is selected. The state space includes all board states, with the first player seeing even token counts and the second player seeing odd counts. Possible actions are represented by the numbers 1 through 7, indicating the columns. Rewards are structured as follows: +1 for a win, -1 for a loss, 0.5 for a tie, and 0 for any other outcome.

### Policies
The AI follows an epsilon-greedy policy, where the epsilon value controls the balance between exploring random moves and exploiting the best-known moves from the Q-function. Early on, exploration is encouraged, but over time, the focus shifts to optimizing moves.

### Q-Learning
The AI leverages Q-Learning to update its strategy, using the following update formula:
\[ Q(s, a) = Q(s, a) + \alpha (\text{max}(Q(s', a')) + \gamma R - Q(s, a)) \]
where:
- \( Q \) is the Q-value.
- \( s \) is the current state.
- \( a \) is the action taken.
- \( \alpha \) is the learning rate.
- \( R \) is the reward.
- \( \gamma \) is the discount factor.

### DQN (Deep Q-Network)
The DQN approach uses a neural network to predict Q-values for each possible action. The board's state is fed into the network, which outputs the Q-values. The loss function measures the mean squared error between the predicted Q-values and the target values. Experience replay and a target network are employed to stabilize the training process.

### Game Logic with DQN
1. Create a game object with specified board parameters.
2. Initialize two player objects, each with a customizable AI brain.
3. Use an environment object to manage player actions and interactions with the game.
4. Run the environment to play out the game, process moves, and update states.

### Q-Learning Logic
1. Initialize the AI using Q-Learning with parameters like epsilon, alpha, and gamma.
2. Evaluate the best action using the Q-table for the current state.
3. Update the Q-table based on received rewards and future state predictions to refine decision-making.

## Results
Below are visualizations illustrating the results from the Q-Learning and DQN approaches, showing the AI's performance under different scenarios:

![Q-Learning Performance Graph](https://user-images.githubusercontent.com/41890348/75622168-66e5bf00-5b52-11ea-83b6-dca4a4cdada0.png)

![DQN Training Loss](https://user-images.githubusercontent.com/41890348/75622284-7dd8e100-5b53-11ea-9d8d-8b52c31e6fa1.png)

![DQN Performance Comparison](https://user-images.githubusercontent.com/41890348/75622285-7f0a0e00-5b53-11ea-8ae3-c3c9ebdbb4c7.png)

## Conclusion
A significant challenge with DQNs focused on win/loss conditions is evaluating progress. To address this, we suggest using a baseline AI that maximizes short-term gains for benchmarking. Stability in training is essential, requiring proper data formatting, reward normalization, and an appropriate learning rate (starting around 0.001). Fine-tuning these factors helps avoid instability and improves the AI's learning over longer training sessions.
