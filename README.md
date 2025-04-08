# Reinforcement Learning Agent Training on Gym Environments

This repository contains the implementation and results of training a reinforcement learning agent on three Gym environments: CartPole, LunarLander, and BipedalWalker. The training utilizes a genetic algorithm approach with transfer learning techniques between similar environments.

## Environments

### 1. CartPole and LunarLander
- Both environments use discrete actions, making them similar in terms of agent structure
- Implemented approach:
  - Pretraining on CartPole (10 epochs) for quick initial policy setup
  - Weight transfer (transfer learning) to LunarLander:
    - Weights from 1st and 2nd columns of CartPole (responsible for "left/right" actions) are copied to 2nd and 4th columns of LunarLander
    - This works because these actions have similar semantics in both environments
  - Fine-tuning on LunarLander (90 epochs):
    - With 20% probability after each epoch, weights are partially updated from CartPole to maintain learning stability

### 2. BipedalWalker
- Requires continuous control (joint torque regulation), making it fundamentally different
- Implemented approach:
  - Separate training cycle - no weight transfer from discrete environments
  - Training for 100 epochs with early stopping:
    - Early stopping triggered when reaching a total reward of 300+ points (environment's success criterion)

## Genetic Algorithm Implementation

The training process uses a genetic algorithm with the following steps:

1. Create an initial population of `POP_SIZE` random individuals
2. For each individual, compute the fitness function that determines its effectiveness
3. Select `NSURV` most fit individuals for reproduction
4. Form a new generation:
   - `NSURV` individuals move to the new population unchanged
   - Population is replenished to `POP_SIZE` with offspring (crossover and mutation with `MUTATION_RATE` chance)
5. Repeat steps 2-4 until termination condition is met (either by epoch count or by achieving target performance)

## Repository Contents

- Jupyter notebook (`*.ipynb`) with complete training implementation and results
- Demonstration videos (`*.mp4`) showing the trained agent's performance in each environment

## Requirements

To run the notebook, you'll need:
- Python 3.6+
- gymnasium
- numpy
- (other dependencies listed in the notebook)

## Results

The notebook contains detailed training logs, performance metrics, and visualizations of the learning process across all three environments. The demonstration videos showcase the final performance of the trained agents.
