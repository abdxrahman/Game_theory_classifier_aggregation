# Byzantine-Robust Classifier Aggregation via Game Theory

## Overview
This project implements a game-theoretic framework for robust multi-agent classifier aggregation. The system addresses the vulnerability of standard ensemble methods to Byzantine failures—scenarios where high-accuracy models are compromised or provide malicious outputs. By modeling aggregation as a non-zero-sum game, the framework incentivizes strategic diversity and ensures graceful degradation under attack.

## System Components
The architecture consists of three agents evaluated on the CIFAR-10 dataset:
* **Expert**: ResNet18 architecture (84.56% baseline accuracy).
* **Specialist**: Custom CNN (58.84% baseline accuracy).
* **Byzantine Agent**: Shallow CNN (44.73% baseline accuracy).

## Methodology

### 1. Game Formulation
Agents choose from a strategy space $S = \{Honest, Bluff, Conservative\}$. These postures modify the influence (confidence scores) each agent exerts on the final Softmax aggregation.

### 2. Utility Function
The utility for each agent is defined by:
* **Success Rewards**: A base reward $\alpha$ and a strategic diversity bonus.
* **Failure Penalties**: A high-cost penalty $\gamma$ for incorrect collective outputs, specifically targeting high-influence (Bluff) failures.
* **Anti-Coordination**: Penalties for redundant strategy profiles to prevent herding.

### 3. Equilibrium Computation
The Nash Equilibrium is reached using the **Fictitious Play** algorithm. Over 2,000 iterations, agents converge to a Mixed Strategy Nash Equilibrium (MSNE) that optimizes for system survival rather than peak performance.

## Key Results
* **Byzantine Robustness**: In a "Worst-Case" scenario where the Expert model is 100% compromised, the system maintains approximately 44.75% accuracy.
* **Graceful Degradation**: While non-robust architectures suffer total collapse (0% accuracy), this framework ensures functional persistence.
