<img width="1024" height="88" alt="image" src="https://github.com/user-attachments/assets/f85ffdfe-624a-452a-8a6d-b828ce1360e5" />

<img width="230" height="32" alt="image" src="https://github.com/user-attachments/assets/090373c5-26fe-4af2-86a8-da0639a5d70f" />

indicates noise thats distributed normally. IID indicates choosing noise values from an equal distribution so no value knows about the other. 

<img width="704" height="134" alt="image" src="https://github.com/user-attachments/assets/da893ac7-d5be-4932-a0f7-70d9985fce20" />

The observation y(x) returned for x follows a gaussian distribution with some noise spread around it
<img width="704" height="134" alt="image" src="https://github.com/user-attachments/assets/4deb63f6-130c-49d0-94fa-2535cda02b20" />

1. the probability of seeing all our data points given all the x's and the model is just multiplying together the probabilities for each datapoint, assuming each noise is IID Gaussian.
2. Minimizing the mean squared error (in case of linear regression) is same as maximizing the posterior probability, when the prior assumption was for a weight value close to 0
3. how likely w is after seeing data and w before any data was run on (prior) 
    
<img width="630" height="52" alt="image" src="https://github.com/user-attachments/assets/ac1cd42d-887b-46f5-815e-56729283a7cc" />

<img width="376" height="124" alt="image" src="https://github.com/user-attachments/assets/8e7b4407-2b05-4487-8bdf-d7ed138a4534" />

1. **MARGINALIZATION:** for when you are concerned in only one event. 
    
    Eg: students who passed their exams given how much they studied and you are only interested in students who passed the exam. Then you sum up the pass across all levels of studying. 
    
2. **CONDITIONAL PROBABILITY:** concerned about a certain specific event governed by a condition. 
    
    Eg: P(positive/disease) = [p(disease/positive) * p(positive) / p(disease)
    
3. CONJUGACY - If you start with a prior (belief) and after seeing data, your updated belief (posterior) is still in the same "shape" or "family" of distributions (just with new numbers), your prior is **conjugate** to your likelihood.
    
    Eg: prior: coin flipping gives 0.5 head and 0.5 tail
    
    likelihood: you get 7 heads and 4 tails 
    
    posterior: updated belief would still yield head or tail even after likelihood 
    
    **Conjugate priors** make Bayesian analysis much easier because the "type" of your beliefs doesn't change as you update with more data—only their exact parameters do
    
4. BAYESIAN MODEL AVERAGING - instead of choosing just 1 best model it averages across all possible models, assigning weights interms of how probable they're 

<img width="1062" height="162" alt="image" src="https://github.com/user-attachments/assets/2c960383-8cde-41f6-8007-2a263227a7fa" />

- **Sum rule (marginalization):**
    - Integrate (or sum) over all possible weights w**w** to get predictions, considering all scenarios.
- **Product rule (conditional probability):**
    - Use Bayes’ theorem to get each weight’s probability given the data.

**epistemic uncertainty -** grasps not just best case but also confidence and uncertainty ****

1. **Bayesian method** - that considers prior assumption is more appealing to use incase of less data - maximum likelihood is not ideal cause it is overconfident and believes any assumption to be the absolute truth.
2. **BAYESIAN MODELLING:**
    1. **parameter space view:**
        1. We use multiple data to configure the ideal parameter like slope or bias and these are based off prior and can be misleading to posterior data
    2. **function space view:**
        1. what are the different function or graph lines that can explain my data and their associated likelihood- will open room to better explanation for uncertainty at each x.
        2. more focused on output prediction than parameters 
    3. **gaussian process**: is a random collection of finite variables that follow a gaussian distribution
        1. kernel value decreases with inputs being far apart 
        2. the prior Gaussian distribution for various function values [f(x), f(x’)] for inputs (x, x’) follows a multivariate gaussian distribution 
        3. the distance of covariance is smaller when inputs are closer 
            
            <img width="792" height="816" alt="image" src="https://github.com/user-attachments/assets/474c1458-dcdc-4e69-9186-939c81511f24" />
     
3. **PROPERTIES OF GAUSSIAN VARIABLES:**
    1. **Linear Transformation:** turning gaussian random normal distribution into a linear form will still be a normal distribution with mean and std shifted .
    2. **Gaussian marginalization:** marginalization refers to excluding some data and only focusing on data that matters to us. Even then the distribution will look gaussian normal.
    3. **Gaussian conditional:** the conditional of a gaussian distribution is also gaussian normal.
       
4. **the KERNEL:**
    1. where does the kernel (covariance matrix) come from ?
        1. kernels are flexible and can be selected in a way that it represents any model (linear, neural or anything)
        2. **types:**
            1. **Squared Exponential Kernel:**
                1. Not always ideal, since it assumes the functions corresponding to inputs follow a smooth curve progression, matern Kernels can model rougher functions 
                2. (theta)^2 - variance across all function outputs 
                3. l - length scale 
                
                the overall output determines how similar two data points are (x, x’)
                
                1. if similar k(x,x’) approx. to (theta)^2
                2. else, its close to 0 which indicate x and x’ are independent of each other

<img width="648" height="128" alt="image" src="https://github.com/user-attachments/assets/4bcd8f58-f4e5-478b-8ddb-a7a536c1641d" />

**WHY IS SE KERNEL SO POPULAR?** 

1. **Kernel trick:** instead of performing intensive computations(expensive ) on infinite data you can build a similar function capturing kernel functions saving from time-intensive, expensive calculations
2. they are simple, as they dont consider rough edges(smooth functions)
3. good generalization
    
<img width="1070" height="190" alt="image" src="https://github.com/user-attachments/assets/5e854c84-a265-4522-8516-f2f54e207fcb" />

**KERNEL HYPERPARAMETER TUNING:**

impossible to find right parameters cause generalizing across large infinite dataset is difficult, rather we can set initial parameters and compare them.

**some tips:**

- standardize input data and set length scales close to 1
- standardize output data and set func variance close to 1
- set initial noise level high, even when its low in the input data → to make optimization easier to generalize
- when using gradient descent method to find local minima, its good to random restart or use other tricks to deviate from minimum

**GAUSSIAN ASSUMES HOMOSKEDASTIC NOISE BUT WHAT IN CASE OF HETEROSKEDASTIC NOISE ?**

**how to model heteroskedastic noise in GP**

1. Real scenarios dont have gaussian noise, they are often not following normal distribution 
2. model noise variance as input dependent. 
    
<img width="274" height="88" alt="image" src="https://github.com/user-attachments/assets/9323106e-35f8-4965-9f43-cb41da73ae64" />

z(x) indicates log of noise variance and has its separate prior and kernel function independent from the f(x)

1. Approximate inference methods are used, such as:
- **Markov Chain Monte Carlo (MCMC)**
- **Laplace approximation**
  
<img width="1140" height="266" alt="image" src="https://github.com/user-attachments/assets/84a62aa0-d5f9-43f3-8853-b69c0bbc3dc7" />

These allow estimating the posterior over f and z jointly and provide predictive distributions that account for varying noise.

**LARGE DATASET AND EXPENSIVE COMPUTATION - Sparse approximation of smaller dataset**( pick data good enough to get closer to the maximum likelihood of full GP)

**HIGH-DIMENSIONALITY PROBLEM:**

1. some kernels like RBF kernel, estimate hyper parameters for each dimension, and with many dimensions the computational cost for hyper parameter estimation increases and causes issues with inference and also with generalizability. Hence we only use dimensions that are absolutely important, but how do we determine them ?
2. inverse length scale - determines how 1/l change affects the dimensions, if large difference then dimension counts else dismiss.

**SAAS prior (sparse axis aligned subspace) :**

1. uses inverse squared length scale → p = l^-2
2. uses Hamiltonian Montecarlo to pick sampled from posterior 

**GAUSSIAN PROCESS LIMITATIONS:**

Only smoothly fixes a function covering all datapoints, so it not very effective in case of high dimensional and structured inputs like images - **DEEP KERNEL LEARNING (can handle non-stationary data)**

**SOFTWARES:**

1. GPy - good for small datasets 
2. scikit-learn - less flexible ; good for basic regression and integration with other ML models
3. George - good for large datasets
4. GPflow - complex to setup
5. GPyTorch - more ideal; PyTorch; ideal for large datasets 

***CODE  - Gaussian Processes***

https://colab.research.google.com/drive/1NMSfcDHKNEzSmkZrPx51fdKKu59vfXHd?authuser=1

**Bayesian Optimization -**

Surrogate model (understanding mentioned as comments) - https://github.com/KhansaKhanam/MLOptimization/blob/main/Module_1/probablistic_surrogate_models.ipynb
