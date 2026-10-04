# Recovering Wheat Variety Structure Using Unsupervised Learning

**Course:** Machine Learning with Python (Final Project Portfolio - Option 3)

## Project Overview
This repository contains my final project exploring unsupervised learning and clustering. The project simulates a real-world scenario where an agricultural co-op receives unlabelled deliveries of mixed wheat grain and needs to discover the underlying varieties using data analytics rather than manual labelling.

## Problem Statement
The co-op wants to know how many distinct wheat varieties are plausibly present in a delivery and how cleanly they separate based on a few simple geometric measurements. The goal of this project is to find that structure using clustering alone, without consulting any true labels, and then judge how much of that discovered structure reflects reality.

## Data Set
The project uses the **Seeds dataset**, which contains 210 wheat kernels. Each kernel is described by seven continuous geometric variables:
1. Area
2. Perimeter
3. Compactness
4. Kernel length
5. Kernel width
6. Asymmetry coefficient
7. Groove length

The true variety labels (representing 3 distinct types of wheat) were strictly set aside and not used during the exploratory or clustering phases.

## Method & Workflow
1. **Preprocessing:** All seven numerical features were scaled using `StandardScaler` to ensure that features measured on larger scales did not dominate the distance calculations.
2. **Dimensionality Reduction:** Principal Component Analysis (PCA) was used to reduce the data to two components, allowing for 2D visual exploration of the dataset's shape.
3. **Clustering:** K-Means clustering was applied. To determine the optimal number of clusters, I evaluated both the **Elbow Method** (inertia) and the **Silhouette Score** across a range of $k$ values, ultimately deciding on $k=3$.
4. **Evaluation:** Only after clustering was complete were the true labels revealed. The cluster assignments were validated against the true labels using a cross-tabulation matrix and a calculated purity score.

## Key Results
* **Optimal Clusters:** The elbow method showed a distinct bend at $k=3$, which aligned well with the agricultural context of finding "several distinct varieties."
* **Purity Score:** The clustering model achieved a purity score of approximately **0.89 (89%)**, indicating a high level of agreement between the unsupervised clusters and the true labels.
* **Separation:** The cross-tabulation and labeled PCA scatter plots revealed that one variety separated almost perfectly, while the remaining two had a slightly overlapping boundary.

## Interpretation
The K-Means model successfully recovered the majority of the real class structure without ever seeing the labels. This indicates that geometric measurements alone are sufficient for the co-op to reasonably sort the grain. However, the minor overlap between two of the varieties means that an automated sorting process based *solely* on these clusters carries a small risk of cross-contamination. Furthermore, visualizing the 7-dimensional clustering on a 2D PCA plot requires caution, as points that appear to overlap on a flat graph may actually be well-separated in higher dimensions.

## Reflection
Using PCA to visualize the data worked very well for getting an initial sense of the dataset's shape and density. The most challenging part of the project was choosing the number of clusters, as the silhouette score peaked at 2 while the elbow method pointed to 3. This required making a judgment call based on domain context rather than relying purely on a single metric. 

If I had more time to improve the workflow, I would experiment with Density-Based Spatial Clustering (DBSCAN) or Gaussian Mixture Models (GMMs) to see if they handle the overlapping boundaries between the two less-distinct wheat varieties better than the spherical clusters assumed by K-Means.
