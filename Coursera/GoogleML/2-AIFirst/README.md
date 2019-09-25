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

> [![](https://img.youtube.com/vi/JsTZhTfl4k8/0.jpg)](https://youtu.be/JsTZhTfl4k8)

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

### Demo: ML in Google Photos

> [![](https://img.youtube.com/vi/KIYXWr6wogI/0.jpg)](https://youtu.be/KIYXWr6wogI)

### Demo: Google Translate and Gmail

> [![](https://img.youtube.com/vi/ddv15t4uWhk/0.jpg)](https://youtu.be/ddv15t4uWhk)

* Google Translate
    * Model 1: Identify the Sign
    * Model 2: OCR the Characters
    * Model 3: Identify Language
    * Model 4: Translate Language
    * Model 5: Superimpose Text
    * Model 6: Select Correct Font
* Gmail - Smart Reply Inbox
    * 20% of all responses sent on mobile

---
## Replacing Heuristic Rules

> [![](https://img.youtube.com/vi/a3nUQat-k5o/0.jpg)](https://youtu.be/a3nUQat-k5o)

* What kinds of problems can ML solve?
    > "Machine learning. This is the next transformation... the programming paradigm is changing. Instead of programming a computer, you teach a computer to learn something and it does what you want" - Eric Schmidt / Google
    * Anything for which you are writing rules for today
* Machine learning scales better than hand-coded rules
    * E.g., RankBrain (a deep neural network for searching ranking) improved performance significantly
* Machine learning replaces hardcoded heuristic rules

---
## It's All about Data

> [![](https://img.youtube.com/vi/nTZu0coVuLY/0.jpg)](https://youtu.be/nTZu0coVuLY)

* ML converts examples into knowledge
    * Examples equals labeled data
* Google learning involves blending **all the users' preferences**

---
## Lab 1: Framing an ML Problem

> [![](https://img.youtube.com/vi/bySIxv-PAqA/0.jpg)](https://youtu.be/bySIxv-PAqA)
> [![](https://img.youtube.com/vi/2prjhxpZ1P0/0.jpg)](https://youtu.be/2prjhxpZ1P0)

* Please follow the details in [here](./Lab-1.md)

### Demo: ML in applications

> [![](https://img.youtube.com/vi/4Z8so_uuxgk/0.jpg)](https://youtu.be/4Z8so_uuxgk)

* Infuse your apps with ML
    * E.g., "How much is this car worth?"
        * Old way: Upload photos and specify model name
        * New way: AUCNET

---
## Pre-trained Models

> [![](https://img.youtube.com/vi/iKCjSjzns4E/0.jpg)](https://youtu.be/iKCjSjzns4E)

* There are pre-trained machine learning services available on Google Cloud
    * Custom ML models
        * TensorFlow
        * Machine Learning Engine
    * Pre-trained ML models
        * Vision API
        * Speech API
        * Jobs API
        * Translation API
        * Natual Language API
        * Video Intelligence API
* "Ocado" routes emails based on NLP
    * Improves natural language processing of customer service claims
* "Let your users talk to you"
    > 50% of enterprises will be spending more per annum on bots and chatbot creation than traditional mobile app development by 2021 - Gartner

---
## ML Marketplace is Evolving

> [![](https://img.youtube.com/vi/fcYW53SPpkw/0.jpg)](https://youtu.be/fcYW53SPpkw)

* The ML marketplace is moving towards increasing levels of ML abstraction
    * AUCNET: Custom image model to price cars
    * Ocado: Build off NLP API to route customer emails
    * GIPHY: Use Vision API as-is to find text in memes
    * UNIQLO: Use Dialogflow to create a new shopping experience

---
## Build a Data Strategy Around ML

> [![](https://img.youtube.com/vi/7skNt4ea0Cs/0.jpg)](https://youtu.be/7skNt4ea0Cs)

* "If ML is a rocket engine, data is the fuel."
* **Simple ML and More Data > Fancy ML and Small Data**

---
## Training and Serving Skew

> [![](https://img.youtube.com/vi/Ysh2F7hDngI/0.jpg)](https://youtu.be/Ysh2F7hDngI)

* Typical sutomer journey involves going from manual data analysis to ML
    * E.g., Global Fishing Watch
        * Enables automation of previously manual global fishing data analyses
        * Processess 22 million fishing data points daily
    * Several reasons why you want to go through manual data analysis to get ML
        1. Collecting data is often the longest and hardest part
        2. Cannot analyze your data to get reasonable inputs towards making decision
        3. To build a good machine learning model, you have to know your data
        4. ML is a journey towards automation and scale
    * **"If you can't do analytics, you can't do ML."**
* For machine learning, you need to build a **streaming pipeline** in addition to a **batch pipeline**
* Mant ML projects fail because of **training-serving skew**
* **Sophistication around real-time data** is key
* Performance metrics for training are different than for predictions
    * Training should scale to handle a lot of data
    * Predictions should scale to handle large number of queries per second

---
## An ML Strategy

> [![](https://img.youtube.com/vi/6Jq7TwwLCjY/0.jpg)](https://youtu.be/6Jq7TwwLCjY)

* "Connect simple ML models into a pipeline"
* Freedom to experiment (and fail) is important
    * "Take your time and succeed"
    * "Fail fast and iterate"
* "Unstructured dta accounts for 90% of enterprise data"
* Build on top of Google
    * Unstructured data $\leftarrow$ ML API
    * The result of ML API $\leftarrow$ Cloud ML Engine

---
## Lab 2: Transform Your Business

### Use ML Creatively

> [![](https://img.youtube.com/vi/z5DgpGFk0_E/0.jpg)](https://youtu.be/z5DgpGFk0_E)

* "What's the customer experiencing right now?"
    * E.g., Generating Music
* Your business can benefit from ML
    * Infuse your apps with ML
        * Simplify user input 
        * Adapt to user
    * Fine-tune your business
        * Streamline your business processes
        * Create a new business
    * Delight your users
        * Anticipate users' needs
        * Creatively fulfill intent

### Lab Introduction

> [![](https://img.youtube.com/vi/fhbqod0lcxA/0.jpg)](https://youtu.be/fhbqod0lcxA)

* Please follow the details in [here](./Lab-2.md)

---
## Module Quiz

1. Which of the following scenarios may require a supervised learning model to be retrained as a new model?
    * A. The model was trained on unlabeled data and we now wish to train it on labeled data.
    * B. The model was trained on labeled data and we now wish to train it on more labeled data.
    * C. The model was trained on unlabeled data and we now wish to add labels to the data.
    * D. The model was trained on labeled data and we now wish to correct the labels of the data.
    > Answer: D.
2. A team is preparing to develop and deploy an ML model for use on a shopping website. They have collected a little data to train the model. The team plans on gathering more data once the model is developed. Now they are ready for the next phase, training. Which of these scenarios will most likely lead to a successful deployment of the ML model?
    * A. The team should take time to focus on training the perfect model, because deployment is quick and easy.
    * B. The team should take time to gather more data because the quality and architecture of the model are affected by the amount of data.
    * C. The team should focus on deployment of the model. The model can be weak to start, then be improved when more user data has been accumulated.
    > Answer: B.
3. An online shopping company has a team of customer representatives read emails from customers. Depending upon the content of the email, the representative routes the email to the appropriate department. The company would like to alleviate the customer representatives task by automating it. Your team has been asked to create an app to read customer emails and determine which department should handle it. Which of these would be a good way to structure the app (chose all that apply)?
    * A. The team should develop one all-encompassing model that will scan the email content, categorize the content, and determine the appropriate team to receive the email.
    * B. Team should develop several models, one for each task. They should develop these models from the ground up and not use pre-existing models, to insure the models are properly trained.
    * C. The team should use several models in the app, one for each task. If there are any pre-existing models the team should use them.
    > Answer: C.
