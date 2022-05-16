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

For high-dimensional features, we can first represent them in lower dimensions and then intersect them. A typical case is using eigenvectors to represent users and items in a recommender system and then intersecting the eigenvectors to represent the relationship between users and items.
