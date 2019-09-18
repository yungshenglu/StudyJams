# What It Means to be AI First

## Introduction

> [![](https://img.youtube.com/vi/hX1VgdQLvqU/0.jpg)](https://youtu.be/hX1VgdQLvqU)

* AI vs. ML
    * AI is a discpline; ML is a toolset
    * Artificial Intelligence is a discipline; machine learning is a specific way of solving AI problems

---
## Two Stages of ML

> [![](https://img.youtube.com/vi/oJ_RdjvaehA/0.jpg)](https://youtu.be/oJ_RdjvaehA)

* Stage 1: **Train an ML model with examples** (Training)
    * A ML model is a **mathematical function**
    * Many tiny adjustments to model function so output is closer to label for a given input
    * ML relies on **labeled examples**
* Stage 2: **Predict with a trained model** (Inference)
    * Model generalized about new data
    * Having labeled data is a precondition for successful machine learning
* Data scientists must focus on both the **training** and **inference** stages of ML
    * Pitfall: Overemphasize model training

---
## ML in Google Products

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Neural networks are one important technology we use
    * Early on, neural networks had fewer layers
    * Training deep neural networks required **computing power**
    * Availability of data
        * As you add more layers, there are more and more weights to adjust
    * Computational tricks
        * If you just add layers, the neural networks will take a long time to train
        * Some of the layers will become all zero or they'll blow up and become all NaN! or not a number
* Usage of deep learning at Google has accelerated rapidly
    * Google infuses machine learning into almost all its products
* Problem: Predicting Stock Outs
    * One solution may have many models
        1. Predict product demand
        2. Predict inventory
        3. Predict restocking time
    * Many ML models per product