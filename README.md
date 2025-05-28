# TML25_A1_19

# White-box Membership Inference Attacks on Neural Networks

## Assignment Overview

This repository contains our implementation for white-box **Membership Inference Attacks (MIA)** on a ResNet neural network. We focused on extracting and leveraging gradient-based features, with the primary attack method based on the LiRA approach ([PoPETs 2025-0068](https://petsymposium.org/popets/2025/popets-2025-0068.pdf)), and also compared to classical shadow modeling from Shokri et al.

---

##  Motivation

Recent research by Carlini, Tramèr, and Papernot shows that models like **XGBoost** perform well for MIAs—especially when target models are overfitted and tend to memorize data. ResNet is typically more regularized and theoretically harder to attack, but in our experiments, the provided ResNet was not very regularized. We therefore chose XGBoost as our main attack model, as it excels when the target model memorizes its training data.
Interestingly, we also found that the best performing attack in our tests was actually a vanilla MLP (Multi-Layer Perceptron) trained directly on aggregated gradient features, even without the use of shadow models. This suggests that, for our setup, simple neural approaches can sometimes outperform more complex ensemble methods, especially when the gradient features are informative.
---

##  Repository Structure

-Assignment1_TML25_19.ipynb # Main Jupyter notebook (all code & results)
-public.pt / private.pt # Datasets for shadow/target models
-test_XGBoost.csv # XGBoost membership scores (for server)
-test_MLP.csv # MLP membership scores (for server)
-test_Lira.csv # LiRA scores (for server)
-shadow_attack_X.npy # Shadow set attack features
-shadow_attack_y.npy # Shadow set attack labels
-README.md # This file


---

##  How to Run

1. **Open and run** `Assignment1_TML25_19.ipynb` in Jupyter.
2. The notebook will:
   - Load and process the datasets
   - Extract gradient-based features (LiRA approach)
   - Train shadow models and attack models (XGBoost, MLP, etc.)
   - Generate all necessary predictions and visualizations

---

## Methods

- **Data Loading:** Custom PyTorch Dataset classes for .pt files.
- **Gradient-Based Feature Extraction:** Compute per-sample gradients, aggregate them as features (LiRA).
- **Shadow Model Training:** Multiple shadow models trained as in [Shokri et al., 2017].
- **Attack Model Training:** Tested XGBoost, MLP, Random Forest, Logistic Regression.
- **LiRA Attack:** Likelihood ratio using KDE over loss values for members/non-members.
- **Evaluation:** Metrics (AUC, TPR@FPR=0.05), histograms, ROC curves.

---

## Results

- **XGBoost** attack model had the best performance on our shadow validation set.
- **Random Forest** overfitted and is **not recommended** for server submission.
- See the notebook for AUC/TPR scores and visualizations.

---

## Visualizations

The notebook produces:
- Histograms of membership scores (members vs non-members)
- ROC curves for each attack model

---

## Key References

- **Yan Pang, Tianhao Wang, Xuhui Kang, Mengdi Huai, Yang Zhang (2024):** [White-box Membership Inference Attacks against Diffusion Models](https://petsymposium.org/popets/2025/popets-2025-0068.pdf)
- **Shokri et al. (2017):** [Membership Inference Attacks Against Machine Learning Models](https://arxiv.org/pdf/1610.05820)

---

## Authors & Submission

- Javed Akthar 
- Hina Lilaram 




