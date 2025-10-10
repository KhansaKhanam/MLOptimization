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

## REVISITING KG (KNOWLEDGE GRADIENT)
![IMG_7832](https://github.com/user-attachments/assets/fc1ef7cd-9f2b-4acc-9c4e-39619e2906bd)
![IMG_7833](https://github.com/user-attachments/assets/d6e1bed8-3a6a-43c2-9eff-2457c5b72f4d)

Two main approaches for solving KG:
1. Stochastic Gradient Descent + Envelope Theorem
2. Sample Average Approximation

1. **Stochastic Gradient Descent + Envelope Theorem -**
   1. The expectation of KG is approximated with the monte-carlo sampling of the random variable Z ~ N(0,1) -<img width="493" height="83" alt="Screenshot 2025-10-10 at 19 17 35" src="https://github.com/user-attachments/assets/4aa44749-c168-4bfa-be92-56d0a7a141f4" />
   2. Each sample of Z solves an inner minimization problem dependent on x(n+1) which is complex for differentiation. The **Envelope Theorem** helps us simplify this by stating that the gradient of the outer function with respect to parameters depend on the gradient of the objective evaluated at the inner minimizer.
      <img width="457" height="105" alt="Screenshot 2025-10-10 at 19 22 19" src="https://github.com/user-attachments/assets/2f48de18-19f1-470e-a667-e223816ab9db" />
   3. Using gradient estimate update x(n+1) iteratively = <img width="316" height="59" alt="Screenshot 2025-10-10 at 19 23 51" src="https://github.com/user-attachments/assets/48253429-4016-422a-8227-6c683789072b" />
   4. SUMMARY: for each x(n+1) draw many x(m) evaluated by monte-carlo method and find gradient of inner function with respect to x(n+1) keeping x(m) or the x obtained from monte-carlo method a constant; average gradient over samples - update x(n+1)

2. **Sample Average Approximation -**
   1. Commonly used approach for its parallelism, stability, and better scalability besides higher dimensionality 

