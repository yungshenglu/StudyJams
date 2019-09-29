# Scaling TensorFlow Models

I’m here to talk about how you would go about taking your TensorFlow model and training it on GCP’s managed infrastructure for machine learning model training and deployed.

## Introduction

> [![](https://img.youtube.com/vi/XPiZR-UfWHU/0.jpg)](https://youtu.be/XPiZR-UfWHU)

* Learn how to
    * Train a model on Google Cloud
    * Monitor model training
    * Deploy a trained model as a microservice

---
## Why Cloud AI Platform?

Cloud ML Engine is now Cloud AI Platform. You can use AI Platform to train your machine learning models using the resources of Google Cloud Platform. In addition, you can host your trained models on AI Platform so that you can send them prediction requests and manage your models and jobs using the GCP services.

For the rest of this course and specialization, any reference to Cloud ML Engine refers to functionality available with AI Platform.

> [![](https://img.youtube.com/vi/BdU9-v6hj08/0.jpg)](https://youtu.be/BdU9-v6hj08)

* Many machine learning frameworks can handle toy problems
* As your data size increases, batching and distribution become important
* Hyperparameter tuning might nice
* Need to autuscale preduction code
* Cloud Machine Learning Engine - repeatable, scalable, tuned
    * In Datalab, start locally on sampled dataset
    * Then, scale it out to GCP using serverless technology

---
## Training a Model

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Training your model with Cloud Machine Learning Engine
    1. Use TensorFlow to create computation graph and training application
    2. Package your trainer application
    3. Configure and start a Cloud ML Engine job
* Create `task.py` to parse command-line parameters and send along to `train_and_evaluate`
    ```python
    parser.add_argument('--train_data_paths', required=True)
    parser.add_argument('--train_steps', ...)
    ```
    * To do the core ML, `task.py` will then invoke `model.py`
* The `model.py` contains the ML model in TensorFlow (Estimator API)
    * Fetching the data
    * Defining the features
    * Configuring the service signature
    * The actual train and eval loop
* Package up TensorFlow model as Python package
    * Sharing code between computers always involves some type of packaging
    * Python modules need to contain an `__init__.py` in every folder
* Verify that the model works as a Python package
    ```bash
    # To check all the imports are in good shapes
    $ python -m trainer.task
    ```
* Then use the **gcloud command** to submit the training job either locally or to cloud
    * Scale Tirer Options
        * `BASIC`
        * `STANDARD`
        * `BASIC_GPU`
        * `BASIC_TPU`
    * Tip: Use single-region bucket for ML
        * The default is multi-region which is better suited for web serving than ML training

---
## Monitoring and Deploying Training Jobs

> [![](https://img.youtube.com/vi/wBXL73f0rGY/0.jpg)](https://youtu.be/wBXL73f0rGY)

* Monitoring training jobs with gcloud
    * Get details of current state of job
        ```bash
        $ gcloud ml-engine jobs describe job_name
        ```
    * Get latest logs from job
        ```bash
        $ gcloud ml-engine jobs stream-jobs job_name
        ```
    * Filter jobs based on creation time or name
        ```bash
        $ gcloud ml-engine jobs list --filter='createTime>2017-01-1ST19:00'
        $ gcloud ml-engine jobs list --filter='jobId:census*' --limit=3
        ```
    * Monitor training jobs with GCP console
        * You can also view CPU and Memory utilization charts for this training job with Stack Driver Monitoring
    * Monitor training jobs with TensorBoard
        * Configure your trainer to save summary data that you can examine ad visualize using TensorBoard
* Cloud ML Engine makes deploying models and scaling the infrastructure easy
    ![](../../../res/img/Coursera/TensorFlow/TensorFlow-4-1.pngs)
* Deploy the saved model to GCP
    ```bash
    MODEL_NAME="taxifare"
    MODEL_VERSION="v1"
    MODEL_LOCATION="gs://${BUCKET}/taxifare/smallinput/taxi_trained/export/Servo/.../"

    $ gcloud ml-engine models create ${MODEL_NAME} -regions $REGION
    $ gcloud ml-engine versions create ${MODEL_VERSION} --model ${MODEL_NAME} --origin ${MODEL_LOCATION} --runtime-version 1.4
    ```
    * Could also be a locally-trained model
* Client code can make REST calls
    ```python
    credentials = GoogleCredentials.get_application_default()
    api = disovery.build('ml', 'v1', credentials=credentials)
    request_data = [
        {
            'pickup_longitude': -73.885262,
            'pickup_latitude': 40.773008,
            'dropoff_longitude': -73.987232,
            'dropoff_latitude': 40.732403,
            'passenger_count': 2
        }
    ]
    parent = 'projects/%s/models/%s/versions/%s' % ('cloud-training-demos', 'taxifare', 'v1')
    response = api.projects().predict(body={
        'instances': request_data
    }, name=parent).execute()
    ```

---
## Lab 5: Exploring and Creating ML Datasets

> [![](https://img.youtube.com/vi/mIJ1fHP7gKA/0.jpg)](https://youtu.be/mIJ1fHP7gKA)
> [![](https://img.youtube.com/vi/jitEBAUQ9Lc/0.jpg)](https://youtu.be/jitEBAUQ9Lc)

* Please follow the details in [here](./Lab-5.md)

---
## Module Quiz

1. True or False: In the packaging model recommended in this module, the `task.py` file you create contains the actual ML model in TensorFlow
    * True - this is contained in `task.py`
    * False - this is actually contained in `model.py`
    > Answer: False.
2. In `model.py`, what parts of the model are included? (choose all that apply)
    * A. Training and evaluation input functions
    * B. Feature columns
    * C. Feature engineering
    * D. Serving input function
    * E. Train and evaluate loop
    * F. The API keys for Cloud AI Platform
    > Answer: A. B. C. D. E.
3. What does the scale-tier represent in CAIP training jobs? (Select the 2 correct responses)
    * A. The type of hardware you want your model to run on
    * B. The number of steps your model should scale to
    * C. The number of distributed machines your model should use
    > Answer: A. C.
4. True or False: the gcloud command line can used to submit the training job, either locally or to cloud
    * True
    * False - gcloud can only submit jobs to the cloud
    > Answer: True
5. True of False: a model can have multiple different versions that you can choose from to be deployed
    * True
    * False
    > Answer: True
