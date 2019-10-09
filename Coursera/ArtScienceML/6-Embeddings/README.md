# Embeddings

In this module, you will learn how to use embeddings to manage sparse data, to make machine learning models that use sparse data consume less memory and train faster. Embeddings are also a way to do dimensionality reduction, and in that way, make models simpler and more generalizable.

## Introduction

> [![](https://img.youtube.com/vi/xxOVT5RjihM/0.jpg)](https://youtu.be/xxOVT5RjihM)

* Learn how to...
    * Use embeddings to 
        * Manage sparse data
        * Reduce dimensionality
        * Increase model generalization
        * Cluster observations
    * Create reusable embeddings
    * Explore embeddings in TensorBoard

### Review of Embeddings

> [![](https://img.youtube.com/vi/v6EDGjOjW0s/0.jpg)](https://youtu.be/v6EDGjOjW0s)

* Creating an embedding column from a feature cross
* The weights in the embedding column are learned from data
* The model learns how to embed the feature cross in lower-dimensional space
* Embedding a feature cross in TensorFlow
    ```python
    import tf.feature_column as fc

    day_hr = fc.crossed_column(
        [dayofweek, hourofday],
        24 * 7
    )

    day_hr_em = fc.embedding_column(
        day_hr,
        2
    )
    ```
* Transfer learning of embeddings from similar ML models
    ```python
    import tf.feature_column as fc

    day_hr = fc.crossed_column(
        [dayofweek, hourofday],
        24 * 7
    )

    day_hr_em = fc.embedding_column(
        day_hr,
        2,
        ckpt_to_load_from='london/*ckpt-1000*',
        tensor_name_in_ckpt='dayhr_embed',
        trainable=Falses
    )
    ```
    * First layer: the feature cross
    * Second layer: a mystery box labeled latent factor
    * Third layer: the embedding
    * Fourth layer: 
        * one side: image of traffic
        * second side: image of people watching TV

---
## Recommendations

> [![](https://img.youtube.com/vi/rBXVSCLWQWw/0.jpg)](https://youtu.be/rBXVSCLWQWw)

* Cases: How do you recommend movies to customers?
    ![](../../../res/img/Coursera/ArtScienceML/ArtScienceML-6-1.png)
    * One approach is to organize movies by similarity (1D)
        ![](../../../res/img/Coursera/ArtScienceML/ArtScienceML-6-2.png)
    * Using a second dimension gives us more freedom in organizing moview
        ![](../../../res/img/Coursera/ArtScienceML/ArtScienceML-6-3.png)
* A d-dimensional embedding assumes that user interest in movies can be approximated by d aspects
    ![](../../../res/img/Coursera/ArtScienceML/ArtScienceML-6-4.png)

---
## Data-driven Embeddings

> [![](https://img.youtube.com/vi/oYWnyg7WhoY/0.jpg)](https://youtu.be/oYWnyg7WhoY)

* Cases: How do you recommend movies to customers?
    * We could give the axes names, but it is not essential...
        ![](../../../res/img/Coursera/ArtScienceML/ArtScienceML-6-5.png)
    * The coordinates are called the 2D embedding for the movie
        ![](../../../res/img/Coursera/ArtScienceML/ArtScienceML-6-6.png)
* It's easier to train a model with d inputs tha a model with N inputs
    ![](../../../res/img/Coursera/ArtScienceML/ArtScienceML-6-7.png)
* Embeddings can be learned from data
    ![](../../../res/img/Coursera/ArtScienceML/ArtScienceML-6-8.png)

---
## Sparse Tensors

> [![](https://img.youtube.com/vi/Eb_27I-dP0g/0.jpg)](https://youtu.be/Eb_27I-dP0g)

* Storing the input vector as a one-hot encoded array is a bad idea
* Desnse representations are inefficient in space and compute
    ![](../../../res/img/Coursera/ArtScienceML/ArtScienceML-6-9.png)
    * Use a sparse representation to hold the example
        ![](../../../res/img/Coursera/ArtScienceML/ArtScienceML-6-10.png)
* Representing feature columns as sparse vectors
    * If you know the keys beforehand:
        ```python
        tf.feature_column.categorical_column_with_vocabulary_list(
            'employeeId',
            vocabulary_list=['8345', '72345', '87654', '98723', '23451']
        )
        ```
    * If your data is already indexed; i.e, has integers in $[0 - N)$:
        ```python
        tf.feature_column.categorical_column_with_identity(
            'employeeId',
            num_buckets=5
        )
        ```
    * If you don't have a vocabulary of all possible values:
        ```python
        tf.feature_column.categorical_column_with_hash_bucket(
            'employeeId',
            hash_bucket_size=500
        )
        ```
* Code to create an embedded feature column in TensorFlow
    ![](../../../res/img/Coursera/ArtScienceML/ArtScienceML-6-11.png)

---
## Train and Embedding

> [![](https://img.youtube.com/vi/s-JOHzeuAzE/0.jpg)](https://youtu.be/s-JOHzeuAzE)

* Embeddings are feature columns that function like layers
    ![](../../../res/img/Coursera/ArtScienceML/ArtScienceML-6-12.png)
* The weights in the embedding layer are learned through backprop just as with other weights
    ![](../../../res/img/Coursera/ArtScienceML/ArtScienceML-6-13.png)
* Embeddings can be thought of as latent features
    ![](../../../res/img/Coursera/ArtScienceML/ArtScienceML-6-14.png)

---
## Similarity Property

> [![](https://img.youtube.com/vi/N5E46YaCLK4/0.jpg)](https://youtu.be/N5E46YaCLK4)

* Embeddings provide dimensionality reduction
    ![](../../../res/img/Coursera/ArtScienceML/ArtScienceML-6-15.png)
    * We take the 784 numbers and we represent them as a sparse tensor
        ![](../../../res/img/Coursera/ArtScienceML/ArtScienceML-6-16.png)
* The result of embedding is such that similar items are close to each other
* You can take advantage of this similarity property of embeddings
    ![](../../../res/img/Coursera/ArtScienceML/ArtScienceML-6-17.png)
* A good starting point for number of embedding dimensions
    ![](../../../res/img/Coursera/ArtScienceML/ArtScienceML-6-18.png)

---
## Module Quiz

1. What does the word "embedding" mean in the context of Machine Learning?
    * A. What that means is that you convert words into vectors. This allow you to do calculations on them and find similarities between them. Well-trained models with word embeddings have shown powerful understanding of the language.
    * B. What that means is that you convert words into sequence models. This allow you to do calculations on them and find similarities between them. Well-trained models with word embeddings have shown powerful understanding of the language.
    * C. What that means is that you convert Tensor vectors into words. This allow you to do calculations on them and find similarities between them. Well-trained models with word embeddings have shown powerful understanding of the language.
    > Answer: A.
2. Which of these statements are true?
    * A. Creating embeddings can be the first step to solving a clustering problem
    * B. Embeddings learned on one problem can be reused in another problem
    * C. Embeddings can be learned directly from the data
    * D. Embeddings can be used to project data to a lower dimensional representation
    * E. Embeddings learned on one problem can be used as a starting point when training a related problem
    * F. Embeddings require you to have labeled data
    > Answer: A. B. C. D. E.
