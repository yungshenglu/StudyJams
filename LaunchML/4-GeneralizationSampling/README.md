# Generalization and Sampling

Now it’s time to answer a rather weird question: when is the most accurate ML model not the right one to pick? As we hinted at in the last module on Optimization -- simply because a model has a loss metric of 0 for your training dataset does not mean it will perform well on new data in the real world.

---
## Introduction

> [![](https://img.youtube.com/vi/i9XVL0AOZS8/0.jpg)](https://youtu.be/i9XVL0AOZS8)

* When is the most accurate ML model *not* the right one to pick?
* Learn how to
    * Assess if your model is overfitting
    * Gauge when to stop model training
    * Create repeatable training, evaluation, and test datasets
    * Establish performance benchmarks

---
## Generalization

> [![](https://img.youtube.com/vi/J4kkubtOxg0/0.jpg)](https://youtu.be/J4kkubtOxg0)

* Predicting the duration of pregnancy based on mother's weight gain
    * What is the error measure to optimize?
* Loss Metrics
    * MSE = Mean Squared Error
    * RMSE = Root Mean Squared Error
* How do I prevent overfitting?
    * Split the dataset and experiment with models
        * Training dataset
        * Validation dataset

---
## Sampling

> [![](https://img.youtube.com/vi/Ta3vF2969qs/0.jpg)](https://youtu.be/Ta3vF2969qs)

* Training Steps
    1. Start with a NN model with one set f hyper-parameters
    2. Train model using training dataset
    3. (Loop to 2) Increase model complexity
    4. (2 to 4) Is it overfitting?
        * Evaluate using validation dataset
        * (Yes) Use model with hyper-parameters of last non-overfit model for prediction
        * (No) (4 to 3)
* Evaluate the final model with independent test data
    * Experimental
        * Training dataset
        * Validation dataset
    * Test
* Evaluate the final model with cross-validation
    * Training dataset
    * Validation dataset
* If you have **lots of data**, use a held-out test dataset
* If you have **little data**, use cross-validation

---
## Creating Repeatable Samples in BigQuery

> [![](https://img.youtube.com/vi/IN8Cptm6DT8/0.jpg)](https://youtu.be/IN8Cptm6DT8)


---
## Demo: Splitting Datasets in BigQuery

> [![](https://img.youtube.com/vi/uJdQOydETmss/0.jpg)](https://youtu.be/uJdQOydETms)

---
## Lab 4: Creating repeatable splits in BigQuery

> [![](https://img.youtube.com/vi/0ii0fLqR2RY/0.jpg)](https://youtu.be/0ii0fLqR2RY)
> [![](https://img.youtube.com/vi/Hk2Q7VE7Jlo/0.jpg)](https://youtu.be/Hk2Q7VE7Jlo)

* Please follow the details in [here](./Lab-4.md)

---
## Lab 5: Exploring and Creating ML Datasets

> [![](https://img.youtube.com/vi/qAbnzDfqQns/0.jpg)](https://youtu.be/qAbnzDfqQns)
> [![](https://img.youtube.com/vi/ocg5wJA6_IE/0.jpg)](https://youtu.be/ocg5wJA6_IE)

* Please follow the details in [here](./Lab-5.md)

---
## Module Quiz

1. (T/F) In ML, you could train using all your data and decide not to hold out a test set and still get a good model
    > Answer: True.
2. You are tasked with splitting your dataset into 80% training and 20% evaluation for your ML model. Your partner wrote the below SQL script for you to use. Should you use it to create your datasets? Why or why not
    ```
    #standardSQL
    WITH
    alldata AS (
    SELECT
        IF (RAND() < 0.8,
        'train',
        'eval') AS dataset,
        arrival_delay,
        departure_delay
    FROM
        `bigquery-samples.airline_ontime_data.flights`
    WHERE
        departure_airport = 'DEN'
        AND arrival_airport = 'LAX' ),
    training AS (
    SELECT
        SAFE_DIVIDE( SUM(arrival_delay * departure_delay) , SUM(departure_delay * departure_delay)) AS alpha
    FROM
        alldata
    WHERE
        dataset = 'train' )
    ```
    * A. Yes use it - the RAND() function is only called once at the very beginning so all the data is put into training and evaluation in a repeatable fashion
    * B. Almost - instead of using a WITH clause, if you stored the training and testing data permanently then you will always have the exact same dataset to train and evaluate on.
    * C. Yes use it - this will yield 80% training, 20% validation due to the RAND() filter logic
    * D. No - the use of RAND(), even if only called once to divide the training and validation dataset, makes the experiment not repeatable for anyone else trying to start with the same datapoints. Consider using a hash function and a modulo operator instead.
    > Answer: D.
3. What is a way to approximate or model real world unknown data? (choose all that apply)
    * A. You can't because real world data cannot be modeled
    * B. Split your dataset into three training buckets: training, validation, and production. Train the model on each of the three datasets to find which dataset performs the best. Then, use only that dataset to train your production model.
    * C. Split your dataset into separate buckets and train your model only on a portion of that dataset (keeping the rest as held out which will model unseen data)
    * D. Increase the breadth and quality of the data you have available. The better the data, the easier it will be for the model to learn.
    > Answer: C. D.    
4. What's a recommended way to split your dataset in a repeatable fashion using SQL?
    * A. Use a hash function and a RAND() function
    * B. There is no way to get the same data values again
    * C. Use a modulo operator and a hash function
    * D. Use a modulo operator and a RAND() function
    * E. Use a RAND() function to ensure a random sample
    > Answer: C.
5. Check all the common pitfalls for splitting a dataset even if done properly:
    * A. You might not have enough data to split the dataset into training, validation, and testing
    * B. You can no longer predict using the field you split the data on
    * C. Your splitting field may not be noisy enough for granular divides of your dataset
    * D. Your validation dataset will never be as good as your training dataset
    > Answer: A. B. C. 
6. What can you do if your model passes validation but fails testing? (Select all 2 correct answers)
    * A. Stop model training and work to collect new data points before trying the same model again
    * B. Start from the beginning with a brand new model type
    * C. Re-train the same model again with different hyperparameters to optimize for a lower loss metric on your testing dataset
    > Answer: A. B.