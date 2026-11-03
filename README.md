# Autonomous Aircraft Landing using Proximal Policy Optimization (PPO)

A **reinforcement learning** project built with MATLAB (Reinforcement Learning Toolbox), implementing a PPO agent for the autonomous control and landing of a 2D lunar lander vehicle.

**Author:** Davide Romano  
**Institution:** Università degli Studi di Napoli Federico II — Bachelor's Degree in Computer Engineering  
**Academic Year:** 2024/2025

---

## The Problem

Landing an aircraft or spacecraft autonomously is a complex control problem. Traditional control systems often rely on modular, rigid architectures. In contrast, Reinforcement Learning (RL) allows an agent to learn an optimal control strategy directly through continuous interaction with the environment. 

The main challenges in this scenario include:
- Managing non-linear physical dynamics under gravity.
- Balancing horizontal and vertical velocity constraints to ensure a safe touchdown (soft landing).
- Maintaining a stable vertical orientation ($\theta \approx 0$).

## Approach & Architecture

We model the problem using an **Actor-Critic** architecture trained via **Proximal Policy Optimization (PPO)**, leveraging a clipped surrogate objective function and Generalized Advantage Estimation (GAE) to ensure stable and efficient policy updates.

### 1. Environment (Lander Vehicle)
- **Observation Space (6 components):** Position $(x, y)$, orientation ($\theta$), linear velocities $(\dot{x}, \dot{y})$, and angular velocity ($\dot{\theta}$).
- **Action Space (Discrete):** 9 discrete combinations of thrust levels ($T_1, T_2$) for two symmetric thrusters.

### 2. Reward Function
The reward function is carefully designed to guide the agent by combining:
- Progress tracking (distance and velocity reduction relative to target $(0,0)$).
- Orientation penalties (discouraging tilting).
- Energy penalties (discouraging excessive thruster power consumption).
- A heavy sparse reward (+500) for achieving a successful **soft landing** (touchdown with horizontal and vertical velocities $< 0.5\text{ m/s}$).

## Training Setup

- **Algorithm:** PPO (Actor-Critic with feedforward neural networks, 400 hidden units per layer).
- **Hyperparameters:** Experience horizon $T = 900$, discount factor $\gamma = 0.998$, clip factor $\epsilon = 0.04$, learning rates $5 \times 10^{-4}$ (actor) and $9 \times 10^{-3}$ (critic).
- **Stopping Criteria:** Maximum episodes or reaching an average reward threshold of 450.

## Results

Simulations across diverse initial conditions demonstrate that the trained PPO agent successfully:
- Corrects initial positional and angular deviations.
- Gradually reduces descent speed and stabilizes the vehicle's orientation.
- Achieves a high success rate of safe **soft landings**, proving the effectiveness of PPO in complex continuous control tasks.

## Future Work

- Exploring continuous action spaces for smoother thruster modulation.
- Dynamic hyperparameter tuning to further improve sample efficiency.
- Hardware-in-the-loop testing or transfer to more advanced flight simulators.

## References

- Sutton, R. S., & Barto, A. G. *Reinforcement Learning: An Introduction*, Bradford Books, 2018.
- Schulman, J., et al. *Proximal Policy Optimization Algorithms*, arXiv preprint arXiv:1707.06347, 2017.
- MathWorks. *Reinforcement Learning Toolbox Documentation*.

---

*Davide Romano, 2025*