---
title: "Crack Machine Learning Interviews"
date: 2022-05-15 21:40:00
tags: ["Interview", "Machine Learning"]
description: "My note of reading 百面机器学习(The Quest for Machine Learning). Daily Update."
---

## Feature Engineering

### 1. Why do we need to apply normalization to numerical features?

There are two common ways of normalization:

a. Min-Max Scaling

$$X_{norm} = \frac{X-X_{min}}{X_{max}-X_{min}}$$

This method can scale the data into a range of \[0,1\).

b. Z-Score Normalization

$$z = \frac{x-\mu}{\rho}, \quad \rho=\sqrt{\sum\frac{(x_i-\mu)^2}{N}}$$

This method will scale the data and make the mean value and standard deviation of the new data become 0 and 1 respectively.

When the scales of features are different, the gradients of weights of features can be very different, leading to a different 'learning pace' of each weight, shown as a zig-zag on the gradient plot. Scaling features can make the 'learning pace' of each weight become closer and let the model converge faster.

Scaling the features can be useful when the model uses gradient descent to update the parameters. Otherwise, it may not make a difference, e.g. when the model is a decision tree. 


### 2. How do we handle categorical features?

We can use Ordinal Encoding, One-hot Encoding, and Binary Encoding based on the categorical feature itself. In deep learning, we can learn an embedding representation of a categorical feature, which can be seen as an advanced way of One-hot Encoding and Binary Encoding.

We can further encode categorical features with other features, e.g. statistical values of numerical features of each category, and target encoding.

### 3. What is Feature Intersection? How do we intersect high-dimensional features?

We can intersect different features and generate new features to improve the fitting ability of our model.

For high-dimensional features, we can first represent them in lower dimensions and then intersect them. A typical case is in the context of recommendation, we use matrix factorization to represent users and items in lower dimension vectors and then intersect the vectors to represent the relationship between users and items.

### 4. How to efficiently find the features to be intersected?

- We can intersect high-importance features based on the feature importance provided by models.
- We can generate intersected features with practical meanings, e.g. dividing price by area can get the price per sqft.
- We can train a decision tree and get inspiration from the structure of the trained tree. Every path from the root node to a leaf node can be seen as a way of intersecting features.

### 5. List some text representation models as well as their advantages and disadvantages.

### 6. How does Word2Vec work? What's the difference between it and LDA?

### 7. What problem will insufficient data bring in the context of image classification? How can we solve it?

Insufficient data may lead to model overfitting. To solve the problem, we can:

1. Simplify the model, add regularization, and dropout.
2. Data augmentation by image rotation, flipping, shifting, etc.
3. Transfer learning. Fine-tune a pre-trained model trained on the small dataset.

## Model Evaluation

> The limitation of metrics.

### 1. What's the limitation of accuracy?

When the positive samples and negative samples are imbalanced, accuracy may not correctly reflect the performance of the model.

### 2. How do we balance precision and recall rate?

We can use the Precision-Recall curve, ROC or F1 score to evaluate the performance of a ranking/classification model.

$$F1 = \frac{2\times precision \times recall}{precision + recall}$$

### 3. The RMSE of the model is high but 95% of samples in the test set are predicted with a small error, why is that? How can we solve it?

RMSE will be heavily influenced by outliers in the dataset. We can remove these outliers if they are considered noise. Otherwise, we have to improve our model. We can also use more robust metrics like Mean Absolute Percent Error (MAPE): $\sum_{i=1}^n |\frac{y_i - \hat y_i}{y_i} | \times \frac{100}{n}$.

> ROC curve.

### 4. What is the ROC curve? How do we draw it?

The x-axis of a ROC curve denotes the False Positive Rate $FPR=\frac{FP}{N}$ and the y-axis denotes the True Positive Rate $TPR = \frac{TP}{P}$. 

A ROC curve can be drawn by keeping changing the threshold and getting the FPR-TPR pairs. Or we can first sort the samples by their predicted probabilities in descending order, then starting at (0,0) we iterate through all samples, moving upward if the sample is positive and moving right if it is negative.

### 5. What's the difference between the ROC curve and the P-R curve?

The shape of the ROC curve remains almost the same when the distribution of positive and negative samples changes while the shape of the P-R curve varies in different datasets. Thus the ROC curve is more stable and can be applied in many different fields.
