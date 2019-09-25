# Optimization

In this module we will walk you through how to optimize your ML models.

---
## Introduction

> [![](https://img.youtube.com/vi/BixfDshDrmw/0.jpg)](https://youtu.be/BixfDshDrmw)

* Learn how to
    * Quantify model performance using loss function
    * Use loss functions as the basis for an algorithm called gradient descent
    * Optimize gradient descent to be as efficient as possible
    * Use performance metrics to make business decisions

---
## Defining ML Models

### Introduction

> [![](https://img.youtube.com/vi/aLZ7u19f6RA/0.jpg)](https://youtu.be/aLZ7u19f6RA)

* ML models are mathematical functions with parameters and hyper-parameters
    * Parameters: Changed during model training
    * Hyper-parameters: Set before training
* Linear models have two types of parameters: **bias and weight**
    $$
    y = b + x \times m \\
    y = b + X \times w 
    $$
    * $y$: Output
    * $b$: Bias term
    * $x$: Input
    * $m$: Weight
* How can linear models classify data?
    * Classification explained graphically

### Introducing the Natality Dataset

> [![](https://img.youtube.com/vi/NbwaprG1v-4/0.jpg)](https://youtu.be/NbwaprG1v-4)

* Problem statement: Not all babies get the care they need
    * How do we predict a baby's health *before* they are born?
        * Which of these could be a *feature* in oure model?
            * A. Mother's Age
            * B. Birth Time
            * C. Baby Weight
        * Which could be a label?
    * Exploring the data visually
        * Baby Weight vs. Mother's Age
            > Please refer to the figure in the video
    * Equation for a linear model tying mother's age and baby weiht
        $$
        y = w_1x_1 + b \\
        \leftarrow y = 0.02x + 6.83
        \leftarrow y = 0.03x + 6.49
        $$
        * The slope of the line is given by $w_1$
        * $x_1$ is the **feature** (e.g., mother's age)
        * $w_1$ is the **weight** for $x_1$
    * Can't we just solve the equation using all the data
    * Searching in parameter-space

---
## Loss Functions

> [![](https://img.youtube.com/vi/ZMhpkcSaRg0/0.jpg)](https://youtu.be/ZMhpkcSaRg0)

* Composing a loss function by calculating errors
    * **Error** = Actual (true) - Predicted Value
* One loss function metric is **Root Mean Squared Error (RMSE)**
    1. Get the errors for the training examples
    2. Compute the squares of the error values
    3. Compute the mean of the squared error values
    4. Take a square root of the mean
        $$
        \sqrt{\frac{1}{n} \times \sum^{n}_{i = 1}{(\hat{Y}_i - Y_i)^2}}
        $$
        * $\hat{Y_i}$: predicted value
        * $Y_i$: labeled value
* Lower RMSE indicates a better performing model
    * Need a way to find the best values for weight and bias
* Problem: RMSE doesn't work as well for classification
    * Introducing **Cross Entropy Loss**
        * Bad classificatons are penalized appropriately
    * Decomposing Cross Entropy Loss
        $$
        \frac{-1}{N} \times \sum^{N}_{1}{y_i \times \log{(\hat{y}_i)} + (1 - y_i) \times \log{(1 - \hat{y}_i)}}
        $$
        * Positive term
            $$
            y_i \times \log{(\hat{y}_i)}
            $$
        * Negative term
            $$
            (1 - y_i) \times \log{(1 - \hat{y}_i)}
            $$

---
## Gradient Descent

### Introduction

> [![](https://img.youtube.com/vi/YmyIPziMNkA/0.jpg)](https://youtu.be/YmyIPziMNkA)

* Learn how to
    * Take a loss function and turn it into a search strategy
    * Gradient Descent
* Loss function lead to loss surfaces
    * A simple algorithm to find the minimum
        ```
        while loss is > Epsilon:
            direction = computeDirection()
            for i in range(self.params):
                self.params[i] = self.params[i] + stepSize * direction[i]
            loss = computeLoss()
        ```
        * Epsilon is a tiny constant
* Seach for a minima by descending the gradient
    * Small step sizes can take a very long time to converge
    * Large step sizes may never converge to the true minimum
    * A correct and constant step size can be difficult to find
        * Step size or **"learning rate"** is a hyper-parameter which is set before training
        * One size does not fit all models
* The loss function slope provides direction and step size in our search
    * Our goal is to find the minimum loss which is where the loss function slope 0
    * Slope is poritive $\leftarrow$ Go left!

### Troubleshooting to Loss Curve

> [![](https://img.youtube.com/vi/maBfgz3ipgA/0.jpg)](https://youtu.be/maBfgz3ipgA)

* A typical loss curve
    * Big drops in loss metrics early on (big steps)
    * Many smaller steps as we get closer to a minima
* Adding a scaling hyper-parameter
    ```
    while loss is > Epsilon:
        derivative = computeDerivative()
            for i in range(self.params):
                self.params[i] = self.params[i] - learningRate * derivative[i]
            loss = computeLoss()
    ```

### ML Model Pitfalls

> [![](https://img.youtube.com/vi/tWOMlQfHTXk/0.jpg)](https://youtu.be/tWOMlQfHTXk)

* Problem: My model changes every time I retrain it
    * Loss surface with a global minimum
    * Loss surface with more than one minima
* Problem Model training is still too slow
    1. Calculate Derivative
        * Number of data points
        * Number of model parameters
    2. Take a Step
        * Number of model parameters
    3. Check Loss
        * Number of data points
        * Number of model parameters
        * Frequency
    4. Repeat 1-3 or Done
* Calculating the derivative on fewer data points
    * Training on the full dataset every step is expensive
    * Mini-batching reduces cost while preserving quality
    * Typical values for batch size: 10 - 1000 examples
* Checking loss with reduced frequency
    ```
    while loss is > Epsilon:
        derivative = computeDerivative()
            for i in range(self.params):
                self.params[i] = self.params[i] - learningRate * derivative[i]
            if readyToUpdateLoss():
                loss = updateLoss()
    ```
    * Popular implementations for `readyToUpdateLoss()`
        * Time-based (e.g., every hours)
        * Step-based (e.g., every 1000 steps)

---
## TensorFlow Playground

### Lab 1: Introducing the TensorFlow Playground

> [![](https://img.youtube.com/vi/uqPsqzF8Cqo/0.jpg)](https://youtu.be/uqPsqzF8Cqo)

### Lab 2: TensorFlow Playground - Advanced

> [![](https://img.youtube.com/vi/FsESKad-GkA/0.jpg)](https://youtu.be/FsESKad-GkA)

### Lab 3: Practicing with Neural Networks

> [![](https://img.youtube.com/vi/7YIryYdJyXk/0.jpg)](https://youtu.be/7YIryYdJyXk)

### Loss Curve Troubleshooting

> [![](https://img.youtube.com/vi/1JnNtc8m98s/0.jpg)](https://youtu.be/1JnNtc8m98s)

* Learn how to
    * Choose effective
    * Performance metrics
* Inappropriate Minimum?
    * Don't reflect the relationship between features and label
    * Won't gerneralized well
* Performance metrics allow us to measure what matters
    * Loss functions
        * During training
        * Harder to understand
        * Indirectly connected to business goals
    * Performance metrics
        * After training
        * Easier to understand
        * Directly connected to business goals

---
## Performance Metrics

### Introduction

> [![](https://img.youtube.com/vi/wt9O5dXwVqw/0.jpg)](https://youtu.be/wt9O5dXwVqw)

### Confusion Matrix

> [![](https://img.youtube.com/vi/-9KBF5AvcqI/0.jpg)](https://youtu.be/-9KBF5AvcqI)

* Use a confusion matrix to assess classification model performance
    | Labels \ Model Predictions | Positive | Negative |
    |---|---|---|
    | Positive | True Positives (TP) | False Negatives (FN) |
    | Negative | False Positives (FP) | True Negatives (TN) |
    * True positive: e.g., available parking space exists, model predicts it is available
    * False positive: e.g., available parking space doesn't exist, model predicts it is available
    * False negative: e.g., available parking space exists, model doesn't predict it
    * True negative: e.g., available parking space doesn't exist, model correctly doesn't predict it
* Precision: true positives / total classified as positive
    $$
    \textrm{Precision} = \frac{TP}{TP + FP}
    $$
* Recall
    $$
    \textrm{Recall} = \frac{TP}{TP + FN}
    $$
* Optimization identifies the best ML model parameters
    * Models are sets of parameters and hyper-parameters
    * Find the best parameters by optimizing loss functions through gradient descent
    * Experiment with neural networks in the TensorFlow playground

---
## Module Quiz

1. What is the main difference between RMSE and MSE?
    * A. MSE and RMSE both square the error to avoid any negative signs and then take the square root
    * B. The loss metric output for RMSE is measured in the same units as the error making it easier to directly interpret
    * C. The loss metric output for MSE is measured in the same units as the error making it easier to directly interpret
    * D. They produce the same result
    > Answer: B.
2. Which one of the following is NOT a performance metric
   * A. Cross Entropy
   * B. Precision
   * C. Recall
   * D. Accuracy
    > Answer: A.
3. Which of the following is not a step in a typical model training loop?
    * A. Take the Derivative of the Loss Function
    * B. Take a step down the loss curve
    * C. Calculate the Loss
    * D. Increase the learning rate
    > Answer: D.
