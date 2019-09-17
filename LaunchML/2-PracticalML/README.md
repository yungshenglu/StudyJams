# Practical ML

In this module, we will introduce some of the main types of machine learning and review the history of ML leading up to the state of the art so that you can accelerate your growth as an ML practitioner.

## Introduction

> [![](https://img.youtube.com/vi/AKuwHQK1zV4/0.jpg)](https://youtu.be/AKuwHQK1zV4)

* Learn how to
    * Differentiate between the major categories of ML problems
    * Place major ML methods in the context of their historical develpment
    * Identify why deep learning is currently popular

---
## Supervised Learning

> [![](https://img.youtube.com/vi/Xg1qzBsiQCU/0.jpg)](https://youtu.be/Xg1qzBsiQCU)

* Two types of ML algorithms
    * **Unsupervised learning**
        * Data is not labeled
    * **Supervised learning**
        * Data is already labeled
        * Learning from the past examples to predict future values
* **Regression and classification** are **supervised** ML model types
    * E.g., Regression model predicts the tip amount
    * E.g., Classification model predicts the sex of the customer
* The type of ML problem depends on 
    * Whether or not you have labeld data and 
    * What you are interested in predicting
    ```
    Is data labeled?
    ├── Yes ── Predicting continuous value?
    │           ├── Yes ── Regression
    │           └── No  ── Classification
    └── No  ── Clustering
    ```
* Q: Imagine you are in banking and you are creating an ML model for detecting if transactions are fraudulent or not. Is this classification or regression, and why?
    * A. Regression, categorical label
    * B. Regression, continuous label
    * C. Classification, categorical label
    * D. Classification, continuous label
    > Answer: C.

---
## Regression and Classification

> [![](https://img.youtube.com/vi/ZWh9aAkIn1s/0.jpg)](https://youtu.be/ZWh9aAkIn1s)

* Use **regression** for predicting **continuous** label values
* Use **classification** for predicting **categorical** label values
* A data warehouse can be a source of structured data training examples for your ML model
    * E.g., Since baby weight is a continuous value, use regression to predict
* Q: Is this dataset a good candidate for inear regression and/or linear classification? (Hint: please refer to the figure in the video)
    * A. Linear regression
    * B. Linear classification
    * C. Both
    * D. None of the above
    > Answer: C.

---
## ML History

### Linear Regression

> [![](https://img.youtube.com/vi/vzTuKqOhp8Q/0.jpg)](https://youtu.be/vzTuKqOhp8Q)

* Linear regression was invented when computations were done by hand
    * 1800s - For predicting planets and pea growth
    * Continuous to work well for large datasets
* In linear regression, the prediction is a weighted sum of inputs
    $$
    \hat{y} = w_0x_1 + w_1x_1 + w_2x_2 + ... \\
    \hat{y} = Xw
    $$
    * This can be condensed down into a simple matrix equation
* The typical loss for linear regression is mean squared error (MSE)
    $$
    L = || y - Xw || ^ 2
    $$
    * This is the L2 norm of the residuals squared
* Linear regression does have a closed form solution, but it is not practical for large datasets
    $$
    w = (X^T X)^{-1} X^T y
    $$
    * $w$: weight vector
    * $X^T X$: Gram matrix
    * $X^T y$: Moment marix
* Q: What is a hyperparameter that helps determine gradient descent's step size along the hypersurface to hopefully speed up convergence?
    * A. Collinearity measure
    * B. Learning rate
    * C. Gram matrix discriminant
    * D. Condition number
    > Answer: B.

### Perceptron

> [![](https://img.youtube.com/vi/i0P7H_XknU4/0.jpg)](https://youtu.be/i0P7H_XknU4)

* The perceptron was a computational model of a neuron
    * 1940s - Precursor to neural networks
    * Perceptron Motivation: **Neurons**
        * Dendrite
        * Nucleus
        * Myelin Sheath
        * Axon    
* The single layer perceptron was modeled on the human brain, but there are simple functions (like XOR) that it cannot learn
    * Inputs
    * Weights
    * Weighted Sum
    * Unit Step Function
    * Outputs
* Q: What component of a biological neuron is analogous to the input portion of a perceptron?
    * A. Axon
    * B. Nucleus
    * C. Dendrites
    * D. Myelin Sheath
    > Answer: C.

### Neural Networks

> [![](https://img.youtube.com/vi/hQ8xrYWAfqU/0.jpg)](https://youtu.be/hQ8xrYWAfqU)

* Neural networks combine layers of perceptrons, making them more powerful but also harder to train effectively
    * 1960s - Neural Networks
* Neural Networks: **Multi-layer perceptron**
    * Common activation functions
        * $\textrm{Sigmoid} = \sigma(x) = \frac{1}{1 + e^{-x}}$
        * $\tanh(x) = \frac{2}{1 + e^{-2x}} - 1$
        * $ReLU = f(x) = \begin{cases} 0 \ for \ x < 0 \\ x \ for \ x \ge 0 \end{cases}$
        * $ELU = f(x) = \begin{cases} \alpha(e^x - 1) \ for \ x < 0 \\ x \ for \ x \ge 0 \end{cases$
* Q: If I wanted my outputs to be in the form of probabilities which activation function should I use in the final layer?
    * A. Sigmoid
    * B. Tanh
    * C. ReLU
    * D. ELU
    > Answer: A.

### Decision Trees

> [![](https://img.youtube.com/vi/_x6vSFxOAO4/0.jpg)](https://youtu.be/_x6vSFxOAO4)

* Decision trees build piecewise linear decision boundaries, are easy to train, and are easy for human to interpret
    * 1980s - Decision trees
    * E.g., Decision Trees and the Titanic
* Q: In a decision classification tree, what does each decision or node consist of?
    * A. Linear classifier of all features
    * B. Mean squared error minimizer
    * C. Linear classifier of one feature
    * D. Euclidean distance minimizer
    > Answer: C.

### Kernel Methods

> [![](https://img.youtube.com/vi/Q-Kt0ciV7JU/0.jpg)](https://youtu.be/Q-Kt0ciV7JU)

* Support vector machines are nonlinear models that build maximum marginal boundaries in hyperspace
    * 1990s - Support Vector Machines (SVMs)
    * SVMs maximize the margine between two classes
* Kernels transform the input space into a more useful feature space
    * E.g., Gaussian RBF Kernel
* Q: We've seen how SVMs use kernels to map the inputs to a higher simensional feature space. What thing in neural networks also can map to a higher dimensional vector space?
    * A. Activation function
    * B. More layers
    * C. More neurons per layer
    * D. Loss function
    > Answer: C.

### Random Forests

> [![](https://img.youtube.com/vi/JgsbX95lkcs/0.jpg)](https://youtu.be/JgsbX95lkcs)

* Random forests, bagging, and boosting are very effective predictors built by combining lots of very simple predictors
    * 2000s - Random Forests, Boosted Trees
    * In many real-world problems, the highest quality is often attained with these methods
    * Random forest: Strong learner from many weak learners
* Q: Which of the following is most likely false of random forests when comparing against individual decision trees?
    * A. Better gerneralization through bagging/subspacing
    * B. Has wisdom of the crowd through voting/aggregating
    * C. Similar bias but lower variance
    * D. Easier to visually interpret
    > Answer: D.

### Modern Neural Networks

> [![](https://img.youtube.com/vi/cBAuDqIbq8M/0.jpg)](https://youtu.be/cBAuDqIbq8M)

* With the advantage of technical improvements, more data, and computational power, neural networks made a comback
    * 2010s - Neural Networks (again)
    * E.g., Inception/GoogLeNet Deep Neural Networks
* Q: What is important when creating deep neural networks?
    * A. Lots of data
    * B. Having good gerneralization
    * C. Experimentation
    * D. All of the above
    > Answer: D.
* Deep neural networks showed dramatic improvements in areas such as image classifcation
* Google production ML systems are informed by lots of past experience with a variety of ML models
* Neural networks are outperforming most other approaches in many domains
    * Large amounts of data
    * Available computational power
    * Available infrastructure
    * Tasks and goals we care about
* Note that there are no models that are universary better, they're just different

---
## Module Quiz

1. What is the key difference between supervised and unsupervised models?
    * A. Unsupervised learning requires even more labeled training data since the model is less controlled during training
    * B. Supervised models are better for prediction than unsupervised because the label is known
    * C. Unsupervised models need fewer data points for accurate modelling as compared to supervised learning
    * D. Supervised models learn to predict based on known labels whereas unsupervised models are more concerned with discovering patterns in the dataset
    > Answer: D.
2. (True or Fals)e A decision tree is always a good model to pick because it is to visually appealing to business users
    > Answer: False.
3. Select the model you would try first if you had labeled, non-continuous value data?
    * A. Linear Regression
    * B. Classification
    * C. Neither
    * D. Either one
    > Answer: B.