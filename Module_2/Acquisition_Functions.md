# ACQUISITION FUCNTION 
The essential ingredients of a BO algorithm are the surrogate model (SM) and the acquisition function (AF). The surrogate model is often a Gaussian Process that can fit the observed data points and quantify the uncertainty of unobserved areas. So, SM is our effort to approximate the unknown black-box function f(x).

<img width="1858" height="1183" alt="image" src="https://github.com/user-attachments/assets/ec35ce0b-0269-485e-9aef-501e8573ae03" />

## Upper Confidence Bound (UCB)
<img width="178" height="35" alt="Screenshot 2025-10-05 at 22 03 48" src="https://github.com/user-attachments/assets/8d1503f9-7fc6-4222-8a36-2598a38c3f95" />

With UCB, the exploitation vs. exploration tradeoff is straightforward and easy to tune via the parameter λ
When λ is small, BO will favor solutions that are expected to be high-performing, i.e., have high μ(x). On the contrary, when λ is large, BO rewards the exploration of currently uncharted areas in the search space.

## Probability of Improvement (PI)
![IMG_7811](https://github.com/user-attachments/assets/87265bfb-86ba-4251-91af-917ca6557c72)

## Expected Improvement (EI)
![IMG_7810](https://github.com/user-attachments/assets/2b989cf7-bf4a-4fa3-8167-9fcafd88179b)
![IMG_7809](https://github.com/user-attachments/assets/3bb5811f-8149-4c37-bf6b-7f2ffe258c06)

The exploration and exploitation can be adjusted with an epsilon term:

<img width="580" height="66" alt="Screenshot 2025-10-05 at 22 09 25" src="https://github.com/user-attachments/assets/4a5422a9-7b28-487d-9999-721d79e02bec" />


REFERENCE:
1. https://ekamperi.github.io/machine%20learning/2021/06/11/acquisition-functions.html


