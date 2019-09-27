# Estimator API

In this module we will walk you through the Estimator API.

## Introduction

> [![](https://img.youtube.com/vi/cTvUTxNd1IE/0.jpg)](https://youtu.be/cTvUTxNd1IE)

* Learn how to
    * Create production-ready machine learning models the easy way
    * Train on large datasets that do not fit in memory
    * Monitor your training metrics in Tensorboard

---
## Estimator API in TensorFlow

> [![](https://img.youtube.com/vi/BXIGUrCLAiY/0.jpg)](https://youtu.be/BXIGUrCLAiY)

* Estimatoe wrap up a large amount of boilerplate code, on top of the model itself

#### Quiz

* Which of these abstraction levels treats TensorFlow as a numeric processing library?
    * A. Python API
    * B. `tf.layers`
    * C. `tf.estimator`
    * D. CPU
    > Answer: A.
* From small to big to prod with the Estimator API
    * Quick model
    * Checkpointing
    * Out-of-memory datasets
    * Train / eval / monitor
    * Distributed training
    * Hyper-parameter tuning on ML-Engine
    * Production: serving predictions from a trained model
* Pre-made estimators that can all be used in the same way
    * `tf.estimator.Estimator`
        * Pre-made regressors
            * `LinearRegressor`
            * `DNNRegressor`
            * `DNNLinearCombinedRegressor`
        * Pre-made classifiers
            * `LinearClassifier`
            * `DNNClassifier`
            * `DNNLinearCombinedClassifier`
        * Your custom estimator

### Pre-made Estimators

> [![](https://img.youtube.com/vi/SSA_mBC5sVs/0.jpg)](https://youtu.be/SSA_mBC5sVs)

* Case Study: Predict property value from historical data
    * Features: square footage, house / apartment
    * Feature columns tell the model what inputs to expect
        ```python
        import tensorflow as tf

        featcols = [
            tf.feature_column.numeric_column('sq_footage'),
            # One-hot encoding
            tf.feature_column.categorical_column_with_vocabulary_list('type', ['house', 'apt'])
        ]
        model = tf.estimator.LinearRegressor(featcols)
        ```
    * Under the hood: feature columns take care of packing the inputs into the input vector of the model
    * Training: feed in training input data and train for 100 epochs
        ```python
        def train_input_fn():
            features = {
                'sq_footage': [1000, 2000, 3000, 1000, 2000, 3000],
                'type': ['house', 'house', 'house', 'apt', 'apt', 'apt']}
            labels = [500, 1000, 1500, 700, 1300, 1900]
            return features, labels
        
        model.train(train_input_fn, steps=100)
        ```
    * Predictions: once trained, the model can be used for prediction
        ```python
        def pred_input_fn():
            features = {
                'sq_footage': [1500, 1800],
                'type': ['house', 'apt']
            }
            return features
        
        # Generator
        predictions = model.predict(predict_input_fn)
        ```
    * Summary: Pick an estimator, train, predict
* To use a different pre-made estimator, just change the class name and supply appropriate parameters
    ```python
    model = tf.estimator.DNNRegressor(featcols, hidden_units=[3, 2])
    ```
* For example, here are some of the things you can change about the DNN Regressor
    ```python
    tf.estimator.DNNRegressor(feature_columns=...,
        hidden_units=[10, 5],
        activation_fn=tf.nn.relu,
        dropout=0.2,
        optimizer='Adam')
    ```

### Demo: Housing Price Model

> [![](https://img.youtube.com/vi/CDYlg9Rw0qY/0.jpg)](https://youtu.be/CDYlg9Rw0qY)



### Checkpointing

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)



### Training on In-memory Datasets

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)
