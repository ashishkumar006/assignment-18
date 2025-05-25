# GridWorld Value Iteration Implementation

This project implements Value Iteration for a 4x4 GridWorld environment using Python. The implementation demonstrates how an agent can learn the optimal value function for navigating from a start state to a goal state.

## Problem Description

### Environment
- **Grid Size**: 4x4
- **Start State**: Top-left corner (state 0)
- **Goal State**: Bottom-right corner (state 15)
- **Actions**: Up, Down, Left, Right (equal probability of 0.25 each)
- **Rewards**: 
  - -1 for each move
  - 0 for reaching the terminal state
- **No obstacles** in the grid

### Parameters
- **Discount Factor (γ)**: 1.0 (no discounting)
- **Convergence Threshold**: 1e-4

## Implementation Details

### Files
- `grid_world_value_iteration.ipynb`: Jupyter notebook containing the implementation with visualizations
- `grid_world_value_iteration.py`: Python script version of the implementation

### Dependencies
- NumPy: For numerical computations
- Matplotlib: For plotting
- Seaborn: For heatmap visualization

### Algorithm

The implementation uses the Value Iteration algorithm with the following components:

1. **State Space**: 4x4 grid (16 states total)
2. **Action Space**: Four actions (up, down, left, right) with equal probability (0.25)
3. **Transition Model**: Deterministic movement in chosen direction, with boundary constraints
4. **Reward Function**: -1 for each move, 0 for reaching terminal state

The algorithm iteratively updates the value function using the Bellman equation:
```
V(s) = Σ P(s'|s,a)[R(s,a,s') + γV(s')]
```
where:
- V(s): Value function for state s
- P(s'|s,a): Transition probability (0.25 for each action)
- R(s,a,s'): Reward (-1 for each move)
- γ: Discount factor (1.0)

## Running the Code

1. Install required packages:
```bash
pip install numpy matplotlib seaborn
```

2. Run either:
- The Jupyter notebook: `grid_world_value_iteration.ipynb`
- The Python script: `grid_world_value_iteration.py`

## Implementation Notes
- The algorithm uses NumPy for efficient matrix operations
- Each state update considers all possible actions with equal probability
- The value function is initialized with zeros
- Convergence is reached when the maximum change in values is less than the threshold (1e-4)
- The terminal state (bottom-right) maintains a fixed value of 0
- Boundary constraints are enforced in the transition model

## Results

The algorithm converged after 471 iterations, producing the following final value matrix:

```
[[-59.42367735 -57.42387125 -54.2813141  -51.71012579]
 [-57.42387125 -54.56699476 -49.71029394 -45.13926711]
 [-54.2813141  -49.71029394 -40.85391609 -29.99766609]
 [-51.71012579 -45.13926711 -29.99766609   0.        ]]
```

### Interpretation
- The goal state (bottom-right) has value 0
- Values become more negative as distance from goal increases
- The start state (top-left) has the most negative value (-59.42)
- The gradient of values naturally shows the optimal path to the goal
- Each value represents the expected cumulative reward when following the optimal policy from that state

## Visualization

![State Numbers and Value Function Heatmap](visualizations.png)

The visualization above shows:

1. **Left**: State number grid (0-15) showing the start state (0) in top-left and goal state (15) in bottom-right
2. **Right**: Value function heatmap where:
   - Blue colors indicate lower values (more negative, further from goal)
   - Red colors indicate higher values (closer to 0, closer to goal)
   - Each cell shows its exact value
   - The gradient from blue to red reveals the optimal path from start to goal
