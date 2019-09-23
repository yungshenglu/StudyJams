# Python Notebooks in the Cloud

## Introduction

> [![](https://img.youtube.com/vi/j6nWcy2O7x8/0.jpg)](https://youtu.be/j6nWcy2O7x8)

* Learning Objectivies
    * Carry out data science tasks in notebooks
    * Rehost notebooks on the cloud
    * Execute ad-hoc queries at scale
    * Invoke pre-trained ML models from Datalab
* Two things follow from the tact that Cloud Datalab runs on a VM
    * You can actually control and change what sort of machine is running your notebook
    * Virtual machines are ephemeral

---
## Cloud Datalab

> [![](https://img.youtube.com/vi/K0poOMxHh44/0.jpg)](https://youtu.be/K0poOMxHh44)

* Increasingly, data analysis and machine learning are carried out in self-descriptive, sharable, executable notebooks
* A typical notebook contains code, chart, and explanations

### Demo: Cloud Datalab

> [![](https://img.youtube.com/vi/nOJiHT-cEUQ/0.jpg)](https://youtu.be/nOJiHT-cEUQ)

---
## Development Process

> [![](https://img.youtube.com/vi/DbTd6NCXMN4/0.jpg)](https://youtu.be/DbTd6NCXMN4)

* Datalab notebooks are developed in an iteraitve, collaborative process
* Development process in Cloud Datalab
    1. Write code in Python
    2. Run cell (`Shift + Enter`)
    3. Examine output
    4. Write commentary in markdown
    5. Share and collaborate
* Datalab notebooks let you change the underlying hardware

### Demo: Rehosting Cloud Datalab

> [![](https://img.youtube.com/vi/sxeF3SmOeLE/0.jpg)](https://youtu.be/sxeF3SmOeLE)

---
## Working with Managed Services

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* You can develop locally with Datalab and then scale out data processing to the cloud
* Datalab integrates well with Google Cloud Platform products
    * Exploring and Analyzing: BigQuert, Google Cloud Storage
    * Machine Learning and Modeling: TensorFlow and GCML
    * Visualizing: Google Charts of Plotly or matplotlib
    * Seamless product combination: CMLE, Dataflow, CloudStorage
    * Integration: Authentication and code source control

---
## Computation and Storage

> [![](https://img.youtube.com/vi/NJuauvwZvKY/0.jpg)](https://youtu.be/NJuauvwZvKY)

* Google Cloud provides an earth-scale computer
    * Networking
    * Data storage
    * Compute power
* Compute Engine provides customizable machine types and dlexible compute options
* Cloud Storage is durable, persistent, and organized in buckets
* Control latency and availability with zones and regions
    * Choose the closet zone/region so as to reduce latency
    * Distribute your apps and data across zones to reduce service disruptions
    * Distribute your apps and data across regions for global availability

---
## Lab 3: Rent a VM

### Introduction to Qwiklabs

> [![](https://img.youtube.com/vi/VOfzQYCERvs/0.jpg)](https://youtu.be/VOfzQYCERvs)

* Please follow the details in [here](./Lab-3.md)

### Lab Debrief

> [![](https://img.youtube.com/vi/hpMHcNZ1u0g/0.jpg)](https://youtu.be/hpMHcNZ1u0g)



---
## Cloud Shell

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

---
## Third Wave of Cloud

### Elastic Fully-Managed Services

> [![](https://img.youtube.com/vi/9d96GmsSAAs/0.jpg)](https://youtu.be/9d96GmsSAAs)

* Spinning up VMs yourself doesn't scale
    * What you want are managed services that atoscale for you

### Serverless Data Analysis

> [![](https://img.youtube.com/vi/m4K8d663Skk/0.jpg)](https://youtu.be/m4K8d663Skk)

* BigQuery is a data warehouse
* Third wave cloud
    * Fully-managed services that autoscales for you
    * All you need to do is to write some code and have it be executed by managed infrastructure

### BigQuery and Cloud Datalab

> [![](https://img.youtube.com/vi/533qJeSZvFU/0.jpg)](https://youtu.be/533qJeSZvFU)

* BigQuert offers...
    1. Interactive anaysis of petabyte scale databases
    2. Familiar, SQL 2011 query lanuage anf functions
    3. Many ways to ingest, transform, load, export data to/from BigQuery
    4. Inexpensive data storage; queries charged on amount of data processed
    5. Integration with Datala for your data analysis needs

---
## Lab 4: Analyzing Data Using Datalab and BigQuery

> [![](https://img.youtube.com/vi/t_yqVSC8mMk/0.jpg)](https://youtu.be/t_yqVSC8mMk)

* Please follow the details in [here](./Lab-4.md)

### Lab Debrief

> [![](https://img.youtube.com/vi/jjXyJeoJTTo/0.jpg)](https://youtu.be/jjXyJeoJTTo)

---
## Machine Learning with Sara Robinson

> [![](https://img.youtube.com/vi/XXYrDsUdN-U/0.jpg)](https://youtu.be/XXYrDsUdN-U)

* Two ways to add ML to your apps
    * Custom ML models
        * TensorFlow
        * Machine Learning Engine
    * Friendly ML
        * Vision API
        * Speech API
        * Translation API
        * Natual Language API
        * Video Intelligence API

---
## Pre-trained ML APIs

### Vision API in Action

> [![](https://img.youtube.com/vi/AKjMbJ4IH90/0.jpg)](https://youtu.be/AKjMbJ4IH90)

* Cloud Vision is an API that lets user perform complex image detection with a single REST API request
* Vision API 
    * Provides label and web detection
    * Extract text or images by using OCR (Optical Character Recognition)
    * Logo detection will identify company logos and an image
    * Landmark detection can tell if an image contains a common landmark
    * Crop hints can help you crop your photos to focus on a particular subject
* More about Vision API: cloud.google.com/vision

### Video Intelligence API

> [![](https://img.youtube.com/vi/1dZ7gZQux4I/0.jpg)](https://youtu.be/1dZ7gZQux4I)

* Cloud Video Intelligence is an PI that lets user understand your video's entitire at shot, frame, or video level
    * Label detection
    * Video and science-level annotations
    * Shot change detection
    * Explicit content detection
    * Regionalization

### Cloud Speech API

> [![](https://img.youtube.com/vi/Zh4qYnPTMas/0.jpg)](https://youtu.be/Zh4qYnPTMas)

* Cloud Speech is an API that lets user perform speech to text transcription in over 100 languages
    * Speech to text transcription
    * Speech timestamps
    * Profanity filtering
    * Batch and streamig transcription
* Demo: Speech timestamps
    1. Extract audio from a video
    2. Send audio to Cloud Speech for tanscription and timestamps
    3. Visualize and search videos in a UI
* More about Cloud Speech API: cloud.google.com/speech
* Cloud Translation - An API lets user translate text into over 100 different languages
    * Translate text
    * Detect language
    * More about Cloud Translation - cloud.google.com/translation

### Translation and NL

> [![](https://img.youtube.com/vi/-Z6czbDXnUs/0.jpg)](https://youtu.be/-Z6czbDXnUs)

* Cloud Natual Language is an API that lets user understand text with a single REST API request
    * Extract entities
    * Detect sentiment
    * Analyze syntax
    * Classify content
* Analyze syntax
    * Dependency parse tree
        * How the different words in a sentence relate to each other and which words depend on other words
    * Parse label
        * The role of each word in a sentence
    * Lemma
        * The lemma is the canonical form of the word
    * Additional morphology details
        * Vary based on the language that the user send the text for the natual language API in
* Classify content using Cloud Natual Language
* Wootric: analyzing and routing feedback
    * Make sense of millions of qualitative customer feedback each week using **entity** and **sentiment analysis**
    * Route and respond to feedback in near realtime, compared to manually classifying each response
* More about Cloud Natual Language - cloud.google.com/natual-language

---
## Lab 5: Invoking Machine Learning APIs

> [![](https://img.youtube.com/vi/CLL8O7LWp08/0.jpg)](https://youtu.be/CLL8O7LWp08)

* Please follow the details in [here](./Lab-5.md)

### Lab Solution

> [![](https://img.youtube.com/vi/fwwWtdeGSLs/0.jpg)](https://youtu.be/fwwWtdeGSLs)

---
## Module Quiz

1. You are going to develop an ML model. You are in Canada and the rest of the team is in Mexico. Your team wants to use Google Cloud Platform with Python Notebook. Which of the following statements support your decision.
    * A. Datalab notebooks run on virtual machines
    * B. Datalab notebooks are hosted in the cloud
    * C. Datalab notebooks contain both markup and output
    > Answer: B.
2. Your team has decided to use the Compute Engine, Cloud Storage, and Datalab for ML model development Which of the following statements are applicable to your situation (choose all that apply)
    * A. You must choose your virtual machine configuration carefully, changing it later will be difficult
    * B. Every member of the team, regardless of their location, can directly read data from Cloud Storage
    * C. Latency of data access can be a concern, so carefully select the zone for data storage
    > Answer: B. C.
3. Rewrite this sentence by filling in the blanks with a single word each:
    The third wave of cloud is _________________ so you can focus on data ___________ instead of infrastructure.
    Word bank: insights, hardware, infrastructure, scalable, cloud-first, serverless, machine learning, GCP, iPython Notebooks
    * A. serverless, insights
    * B. scalable, hardware
    * C. iPython Notebooks, hardware
    * D. insights, GCP
    > Answer: A.
