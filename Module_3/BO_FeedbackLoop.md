# Bayesian Optimization Feedback Loop

## Overview
<img width="781" height="473" alt="Screenshot 2025-10-09 at 18 02 34" src="https://github.com/user-attachments/assets/5344fa27-e048-4919-a4b3-8b7b5dd8698e" />

## EACH ITERATION OF BO (MAJOR TASKS):
1. Training Kernel hyperparameters at every iteration to achieve maximum results - this can be achieved by using maximum log-likelihood - a better trick is to "warm-start" hyperparameters instead of starting from scratch
2. Maximize the acquisiton function - we expect f(x) to be non-convex and almost always differentiable - important to use multi-start procedure to globalize the solution

## HOW TO MEASURE PERFORMANCE:
We use simple regret to measure performance by comparing each f(x) with optimal solution.
<img width="1178" height="170" alt="Screenshot 2025-10-09 at 19 15 11" src="https://github.com/user-attachments/assets/6380be3d-89a5-4a0f-8003-72e2acfd5f75" />

it is important do many iterations of switching the optimal value everytime. This allows us estimate performance across different seed values and initial conditions. Average simple regret from multiple replicates to evaluate the robustness and effectiveness of the algorithm

In summary, simple regret measures the best solution found so far in BO, averaged performance is reported through multiple independent runs to account for sensitivity to initial data, and rigorous statistical conclusions about variability across runs are often not performed.

## WHY GLOBAL OPTIMIZATION IS DIFFICULT:
1. McCormick relaxations used to bound the posterior mean and covariance functions in Gaussian process models tend to be very weak because these functions are sums of terms with alternating signs. This weak bounding makes it difficult to construct tight underestimators that guide optimization efficiently.
2. Constructing better underestimators cheaply is an active research area but remains an open challenge.
3. Due to these weaknesses, multi-start local optimization methods have become the de facto practical choice. They are easily parallelized by running multiple local optimization runs simultaneously.
4. Gradient-based first-order methods like ADAM also benefit from hardware acceleration such as GPUs, making them fast in wall-clock time.
5. Global Bayesian optimization often suffers from curse of dimensionality, heterogeneity of objective functions, and high computational cost for large scale problems. Local Bayesian optimization variants that apply multiple local models and combine their results show promise but are still not fully mature.

Therefore, the current best practical approach to global optimization of complex black-box functions is to use multi-start local optimizers (which can be Bayesian or gradient-based) that exploit parallelism and hardware acceleration, rather than relying exclusively on global surrogate-based methods that present optimization difficulties and weak bounding

## ADAPTIVE MODIFICATIONS TO IMPROVE PERFORMANCE:
1. Selecting different kernels for training different GP models and find the one that best performs for our needs
2. To do this, you can adapt different acquisition function per iteration and assign weights as per their success
3. 
