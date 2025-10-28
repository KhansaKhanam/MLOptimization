# Metastatic-Cancer-Bayesian-Optimization

## Unlocking Cancer's Shape-Shifting Secrets: How Cells Decide Between Staying Put and Breaking Free
Cancer metastasis—the spread of cancer from its original site to distant organs—remains one of the deadliest aspects of cancer progression. But what determines whether cancer cells stay clustered in a compact mass or break apart to invade surrounding tissues? This fundamental question has puzzled researchers for decades, and understanding the answer could be key to developing better cancer treatments.

## The Mystery of Cancer Cell Behavior
When cancer cells grow in 3D cultures, they don't all behave the same way. Some form tight, round clusters called spheroids—these are the well-behaved cells that stay put. Others spread out into elongated, finger-like network structures that aggressively invade their surroundings. This morphological switch from compact to invasive isn't random—it's driven by specific biological factors that we're only beginning to understand.

The challenge? Most computational models to date have focused on either individual cell migration or collective movement, but haven't captured this critical phenotypic transition from non-invasive spheroids to invasive networks. It's like trying to understand a story by reading only the first or last chapter—you miss the crucial transformation in the middle.

## Building a Digital Twin of Cancer
In our recent research, we developed a computational agent-based model (ABM) using CompuCell3D—an open-source biological simulation platform—to create a "digital twin" of 3D cancer cell cultures. Think of it as a virtual laboratory where we can watch a single cancer cell divide, grow, and either form a compact spheroid or spread into an invasive network over the course of a week.
Our model focuses on breast cancer cells (specifically the MDA-MB-231 cell line) and simulates two key factors that influence cancer cell behavior:

* **Cell-cell adhesion energy:** How strongly cancer cells stick to each other
* **Chemoattractant secretion:** Chemical signals that cells release to guide their movement through the extracellular matrix

By varying these parameters in our simulations, we could recreate both the non-invasive spheroid phenotype and the invasive network phenotype observed in real experiments.

## What the Simulations Revealed
Our findings paint a clear picture of the molecular tug-of-war that determines cancer cell fate:
#### Strong Bonds Keep Cells Together
When cell-cell adhesion energy is high—meaning cells stick tightly to their neighbors—they form compact, circular spheroids with limited ability to invade. These strong cellular bonds act like molecular glue, constraining cell movement and maintaining a cohesive structure. The result? Low invasion and high circularity (nearly perfect circles when measured).

#### Chemical Signals Drive Invasion
Increasing the chemoattractant secretion rate tells a different story. As cells release more chemical signals into their environment, they transition from rounded spheroids to elongated, interconnected networks. These chemical gradients essentially create a roadmap for invasion, encouraging cells to stretch out, connect with distant neighbors, and infiltrate the surrounding matrix. Higher secretion rates correlated directly with increased invasion and decreased circularity.

## Why This Matters
Understanding these biophysical and biochemical mechanisms isn't just academically interesting—it has real implications for cancer treatment. If we can identify the molecular switches that control whether cancer cells adopt invasive or non-invasive phenotypes, we might be able to:

* Predict which tumors are likely to metastasize based on their adhesion and secretion profiles
* Target the specific pathways that enable phenotypic transitions
* Develop therapies that "lock" cancer cells into non-invasive spheroid states

## Guidelines for using the simulation data in Bayesian Optimization
The simulation data is organized into folders named according to the varying parameter values, while all other parameters were held constant. The folder naming convention follows the structure:
Phenotype_λ_Jcc_k
	•	Example: Spheroid_500_10_0005, Network_1000_15_0005.
Each folder also contains a JSON file that stores the specific parameter values used in that simulation experiment. These serve as a record of the parameter estimation setup and can be directly linked to the corresponding simulation outputs.
To evaluate model performance, the sum of squared error (SSE) is calculated at time steps that align with the in-vitro experimental data (e.g., hours 12, 24, 36, 48, and 60). This ensures that the comparison between simulation and experiment is meaningful and consistent.
The provided Jupyter Notebook includes:
	•	A detailed workflow for calculating SSE across the relevant time steps.
	•	Instructions on extracting and utilizing the simulation parameters from the JSON files.
	•	An outline of the variables and metrics to be used in the Bayesian Optimization pipeline, where the objective function is defined as the minimization of SSE.
This setup enables a systematic search for the optimal parameter combination that best reproduces experimental outcomes while leveraging the Bayesian Optimization framework.

## *Notes:*
1. Labelling for Phenotype: 1-Spheroid; 2-Network
2. **EXTRACT DATA FOR EACH PHENTOTYPE(spheroids/networks) WITH 32 PARAMETER COMBINATIONS AND THEIR 20 REPLICATES FROM THE ZIP FILE**
TERMINAL COMMANDS: 
> unzip <zip_filename.zip> -d <folder_name you want to extract into>
    NOTE: Will remove the exttacted file while pushing it on github to save space but you can only follow the next steps by extracting the folder first 

MAIL ME @ khansakh@protonmail.com for the BO_data.zip
