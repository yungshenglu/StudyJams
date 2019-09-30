# Raw Data to Features

Feature engineering is often the longest and most difficult phase of building your ML project. In the feature engineering process, you start with your raw data and use your own domain knowledge to create features that will make your machine learning algorithms work. In this module we explore what makes a good feature and how to represent them in your ML model.

## Introduction

> [![](https://img.youtube.com/vi/Hf-ZQCgwk8w/0.jpg)](https://youtu.be/Hf-ZQCgwk8w)

* Feature engineering
    * Scale to large datasets
    * Find good features
    * Preprocess with Cloud ML Engine
* Turn raw data to features
    * Raw data must be mapped into numerical feature vectors

---
## Good vs. Bad Features

> [![](https://img.youtube.com/vi/S3AQNhlNj3Y/0.jpg)](https://youtu.be/S3AQNhlNj3Y)

* Objectives
    * Turn raw dat to features
    * Compare good vs. bad features
    * Represent features
* What makes a good feature?
    1. **Be related to the objective**
        * Different problems in the same domain may need different features
    2. Be known at prediction-time
    3. Be neumeric with meaningful magnitude
    4. Hvae enough examples
    5. Bring human insight to problem

#### Quiz: Features are Related to the Objective

> [![](https://img.youtube.com/vi/8WY4E9F1tmc/0.jpg)](https://youtu.be/8WY4E9F1tmc)

* Are these features related to the objective or not?
    * **Objective:** Predict total number of customers who will use a certain discount coupon
        * A. Font of the text with which the discount is advertised on partner websites
        * B. Price of the item the coupon applies to
        * C. Number of items in stock
        > Answer: A. B.
    * **Objective:** Predict point-of-sale credit card fraudulent activity
        * A. Whether cardholder has purchased these items at this store before
        * B. Credit card chip reader speed
        * C. Category of item being purchased
        * D. Expiry date of credit card
        > A. B. C. D.

### Features Known at Predicton-time

> [![](https://img.youtube.com/vi/kiBdRXLnDvA/0.jpg)](https://youtu.be/kiBdRXLnDvA)

* What makes a good feature?
    1. Be related to the objective
        * Different problems in the same domain may need different features
    2. **Be known at prediction-time**
        * Some data could be known immediately, and some other data is not known in real time
        * Make sure that for every input that you're using for your model, for every feature, make sure that you have them the actual prediction time
    3. Be neumeric with meaningful magnitude
    4. Hvae enough examples
    5. Bring human insight to problem

#### Quiz: Features Known at Prediction-time

> [![](https://img.youtube.com/vi/efo_ko1-M9A/0.jpg)](https://youtu.be/efo_ko1-M9A)

* Is the value knowable at prediction time or not?
    * **Objective:** Predict total number of customers who will use a certain discount coupon
        * A. Total number of discountable items sold
        * B. Number of discountable items sold the previous month
        * C. Number of customers who viewed ads about item
        > Answer: B. C.
    * **Objective:** Predict whether a credit card transaction is fraudulent
        * A. Whether cardholder has purchased these items at this store before
        * B. Whether item is new at store (and can not have been purchased before)
        * C. Category of item being purchased
        * D. Online or in-person purchase
        > Answer: A. B. C. D.
* You cannot train with current data and predict with stale data

### Features Should be Numeric

> [![](https://img.youtube.com/vi/N-298tJYtY4/0.jpg)](https://youtu.be/N-298tJYtY4)

* Be numeric with meaningful magnitude
* Neural networks are weighing and adding machines

#### Quiz: Features Should be Numeric

> [![](https://img.youtube.com/vi/HK2DBmTea6U/0.jpg)](https://youtu.be/HK2DBmTea6U)

* Which of these features are numeric (or could be in a useful form)?
    * **Objective:** Predict total number of customers who will use a certain discount coupon
        * A. Percent value of the discount (e.g. 10% off, 20% off, etc.)
        * B. Size of the coupon (e.g. 4 cm2, 24 cm2, 48 cm2, etc.)
        * C. Font an advertisement is in (Arial, Times New Roman, etc.)
        * D. Color of coupon (red, black, blue, etc.)
        * E. Item category (1 for dairy, 2 for deli, 3 for canned goods, etc.)
        > Answer: A.

### Features Should Have Enough Examples

> [![](https://img.youtube.com/vi/DQnrqtiLGps/0.jpg)](https://youtu.be/DQnrqtiLGps)

* Avoud having values of which you don't have enough examples

#### Quiz: Features Should Have Enough Examples

> [![](https://img.youtube.com/vi/-Kg_MVMurPA/0.jpg)](https://youtu.be/-Kg_MVMurPA)
> [![](https://img.youtube.com/vi/7w9Y2KQ4MGU/0.jpg)](https://youtu.be/7w9Y2KQ4MGU)

* Which of these will it be *difficult* to get enough examples?
    * **Objective:** Predict customer discount coupon usage
        * A. Percent discount of coupon (20%, 30%, etc.)
        * B. Date that promotional offer starts
        * C. Number of customers who opened advertising email
        * D. All of these we should be able enough examples for
        > Answer: D.
* Which of these will it be relatively easy to get enough examples for?
    * **Objective:** Predict point-of-sale credit card fraudulent activity
        * A. Whether cardholder has purchased these items at this store before
        * B. Distance between cardholder address and store
        * C. Category of item being purchased
        * D. Online or in-person purchase
        > Answer: A. B. C. D.



### Bringing Human Insight

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)


---
## Quiz: Raw Data to Features


---
## Discussion Prompt


---
## Representing Features

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)


### ML vs. Statictics

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)


---
## Lab 1: Improve Model Accuracy with New Features

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Please follow the details in [here](./Lab-1.md)

---
## Quiz: Representing Features

