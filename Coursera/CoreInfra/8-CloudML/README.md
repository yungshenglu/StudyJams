## Big Data and Machine Learning in the Cloud

GCP's big-data and machine learning offerings are intended to help customers get the most out of data. These tools are intended to be simple and practical to embed in your applications. This module describes the available big-data and machine learning services and explains the usefulness of each.

### Key Concepts

* Understand the purpose of and use cases for the products in the Google Cloud big data platform..
* Understand the purpose of and use cases for the products in the Google Cloud machine learning platform.
* Load data into a BigQuery table from Cloud Storage.
* Use SQL queries to analyze data in BigQuery.

---
## Module Introduction

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Google believes that in the future, every company will be a data company. 
    * Because making the fastest and best use of data is a critical source of competitive advantage. 
    * Google Cloud provides a way for everybody to take advantage of Google's investments in infrastructure and data processing innovation. 
    * Google Cloud has automated out the complexity of building and maintaining data and analytics systems.

---
## Google Cloud Big Data Platform

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Google Cloud's big data services are fully managed and scalable
    * Cloud Dataproc
        * Managed Hadoop MapReduce, Spark, Pig, and Hive serviec
    * Cloud Dataflow
        * Stream and batch processing; unified and simplified pipelines
    * BigQuery
        * Analytics database; stream data at 100,000 rows per second
    * Cloud Pub/Sub
        * Scalable and flexible enterprise messaging
    * Cloud Datalab
        * Interactive data exploration
* Cloud Dataproc is managed Hadoop
    * Fast, easy, managed way to run Hadoop and Spark/Hive/Pig on GCP
    * Create clusters in 90 seconds or less on average
    * Scale clusters up and down even when jobs are running
* Why use Cloud Dataproc?
    * Easily migrate on-premises Hadoop jobs to the cloud
    * Save money with preemptible instances
    * use Spark Machine Learning Libraries (MLlib) to run classification algorithms

### Cloud Dataflow

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Cloud Dataflow offers managed data pipelines
    * Processes data using Compute Engine instances
        * Clusters are sized for you
        * Automated scaling, no instances provisioning required
    * Write code once and get batch and streaming
        * Transform-based programming model
* Why use Cloud Dataflow?
    * ETL (extract/transform/load) pipelines to move, filter, enrich, shape data
    * Data analysis: batch computation or continuous computation using streaming
    * Orchestration: create pipelines that coordinate services, including external services
    * Integrates with GCP services like Cloud Storage, Cloud Pub/Sub, BigQuery, and Bigtable
        * Open source Java and Python SDKs

### BigQuery

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* BigQuery is fully managed data warehouse
    * Provides near real-time interactive analysis of massive datasets (hundreds of TBs) using SQL syntax (SQL 2011)
    * No cluster maintenance is required
* BigQuery runs Google's high-performance infrastructure
    * Compute and storage are separated with a terabit network in between
    * You only pay for storage and processing used
    * Automatic discount for long-term data storage

### Cloud Pub/Sub and Cloud Datalab

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Cloud Pub/Sub is scalable, reliable messaging
    * Supports many-to-many asynchronous messaging
    * Application components make push/pull subscriptions to topics
    * Includes support for offline consumers
* Why use Cloud Pub/Sub?
    * Building block for data ingestion in Dataflow, Internet of Things (IoT), Marketing Analytics
    * Foundation for Dataflow streaming
    * Push notifications for cloud-based applications
    * Connect applications across Google Cloud Platform (push/pull between Compute Engine and App Engine)
* Cloud Datalab offers interactive data exploration
    * Interactive tool for large-scale data exploration, transformation, analysis, and visualization
    * Integrated, open source
        * Built on Jupyter (formerly IPython)
    * Analyze data in BigQuery, Compute Engine, and Cloud Storage using Python, SQL, and JavaScript
    * Easily deploy models to BigQuery

---
## Google Cloud Machine Learning Platform

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Machine Learning APIs enables apps that see, hear, and understand
* Cloud Machine Learning Platform
    * TensorFlow is an open source software library that's exceptionally well suited for machine learning applications like neural networks. 
        * It was developed by Google Brain for Google's internal use and then open source so that the world could benefit. 
    * Open source tool to build and run neural network models
        * Wide platform support: CPU or GPU; mobile, server, or cloud
    * Fully managed machine learning service
        * Familiar notebok-based developer experience
        * Optimized for Google infrastructure; integrates with BigQuery and Cloud Storage
    * Pre-trained machine learning models built by Google
        * Speech: Stream results in real time, detects 80 languages
        * Vision: Identify objects, landmarks, text, and content
        * Translate: Language translation including detection
        * Natural language: Structure, meaning of text
* Why use the Cloud Machine Learning platform?
    * For structured data
        * Classification and regression
        * Recommendation
        * Anomaly detection
    * For unstructured data
        * Image and video analytics
        * Text analytics

### Machine Learning APIs

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Cloud Vision API
    * Analyze images with a simple REST API
        * Logo detection, label detection, etc.
    * With the Cloud Vision API, you can:
        * Gain insight from images
        * Detect inappropriate content
        * Analyze sentiment
        * Extract text
* Cloud Speech API
    * Can return text in real time
    * Highly accurate, even in noisy environments
    * Access from any devices
* Cloud Translation API
    * Translate arbitary strings between thousands of languages pairs
    * Programmatically detect a document's language
    * Support for dozens of languages
* Cloud Natural Language API
    * Uses machine learning models to reveal structure and meaning of text
    * Extract information about items mentioned in text documents, news, articles, and blog posts
* Cloud Video Intelligence API (Beta)
    * Annotate the contents of videos
    * Detect scene changes
    * Flag inappropriate content
    * Support for a variety of video formats

---
## Lab 7: Getting Started with BigQuery

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Please follow the details in [here](./Lab-7.md)

---
## Quiz: Big Data and Machine Learning

1. Name two use cases for Google Cloud Dataproc (Select 2 answers).
    * a. Migrate on-premises Hadoop jobs to the cloud
    * b. Manage datasets of unpredictable size
    * c. Manage data that arrives in realtime
    * d. Data mining and analysis in datasets of known size
    > Answer: a. d.
2. Name two use cases for Google Cloud Dataflow (Select 2 answers).
    * a. Orchestration
    * b. Extract, Transform, and Load (ETL)
    * c. Reserved compute instances
    * d. Manual resource management
    > Answer: a. b.
3. Name three use cases for the Google Cloud Machine Learning Platform (Select 3 answers).
    * a. Data preparation
    * b. Sentiment analysis
    * c. Content personalization
    * d. Fraud detection
    * e. Query architecture
    > Answer: b. c. d.
4. Which statements are true about BigQuery? Choose all that are true (2 statements).
    * a. BigQuery lets you run fast SQL queries against large databases.
    * b. Once in BigQuery, data is not accessible from other GCP services.
    * c. BigQuery is a good choice for online transaction processing.
    * d. BigQuery is a good choice for data analytics warehousing.
    * e. BigQuery requires that you provision database instances ahead of use.
    > Answer: a. d.
5. Name three use cases for Cloud Pub/Sub (Select 3 answers).
    * a. Analyzing streaming data
    * b. Executing ad-hoc SQL queries
    * c. Internet of Things applications
    * d. Decoupling systems
    * e. Storage of binary web content
    > Answer: a. c. d. 
6. What is TensorFlow?
    * a. A managed service for building data pipelines
    * b. A managed service for building machine learning models
    * c. An open-source software library that’s useful for building machine learning applications
    * d. A hardware device designed to accelerate machine learning workloads
    > Answer: c.
7. What does the Cloud Natural Language API do?
    * a. It translates arbitrary strings into any supported language.
    * b. It extracts text in various languages from images.
    * c. It performs sentiment analysis on audio and video content.
    * d. It analyzes text to reveal its structure and meaning.
    > Answer:
