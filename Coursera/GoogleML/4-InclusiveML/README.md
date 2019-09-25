# Inclusive ML

## Introduction

> [![](https://img.youtube.com/vi/VyADk1itsYk/0.jpg)](https://youtu.be/VyADk1itsYk)

* Learn how to
    * Identify the origins of bias in ML
    * Make models inclusive
    * Evaluate ML models with biases
* Agenda
    * Evaluating metrics with inclusion for your ML system
    * Equality of opportunity
    * How to find errors in your dataset usign *Facets*

---
## Machine Learning and Human Bias

> [![](https://img.youtube.com/vi/AE1fXtL5hNg/0.jpg)](https://youtu.be/AE1fXtL5hNg)

---
## Evaluating Metrics for Inclusion

> [![](https://img.youtube.com/vi/dsO9yPI9hk0/0.jpg)](https://youtu.be/dsO9yPI9hk0)

* A common way that evaluate performance in ML is **confusion matrix**
* The conusion matrix leads to evaluation metric insights
    * True Positives (TP)
    * False Negatives (FN)
    * False Positives (FP)
    * True Negatives (TN)
* **False positives** and **false negatives** errors occur when predictions and labels disagree
    * False Negatives (FN): Model says No
    * False Positives (FP): Model says Yes

---
## Statistical Measurements and Acceptable Tradeoffs

> [![](https://img.youtube.com/vi/H9xBCsMj4x8/0.jpg)](https://youtu.be/H9xBCsMj4x8)

* Evaluation metrics can help highlight area where machine learning could be more inclusive
    * **False negative rate** is the fraction of true faces that are not detected by the ML system
        $$
        \textrm{FN \ Rate} = \frac{\textrm{FN}}{\textrm{FN} + \textrm{TP}}
        $$
    * **False positive rate** is the fraction of the faces that the ML model detects that are not really faces
        $$
        \textrm{FP \ Rate} = \frac{\textrm{FP}}{\textrm{FP} + \textrm{TP}}
        $$
* Summary
    * False positive rate ($\alpha$) (Type I Error)
        $$
        = 1 − \textrm{Specificity} = \frac{\textrm{FP}}{\textrm{FP + TN}} = \frac{180}{180 + 1820} = 9\%
        $$
    * False negative rate ($\beta$) (Type II Error) 
        $$    
        = 1 − \textrm{Sensitivity} = \frac{\textrm{FN}}{\textrm{TP + FN}} = \frac{10}{20 + 10} = 33\%
        $$
    * True positive rate (TPR), Recall, Sensitivity, probability of detection 
        $$
        = \frac{\sum{\textrm{TP}}}{\sum{Condition \ positive}}
        $$
    * Accuracy (ACC)
        $$
        = \sum{\textrm{TP} + \frac{\sum{\textrm{TN}}}{\sum{\textrm{Total \ Population}}
        $$
    * Precision
        $$
        = \frac{\sum{\textrm{TP}}}{\sum{\textrm{Predicted \ condition \ positive}}}
        $$
    * For more details, read under Confusion Matrix: https://en.wikipedia.org/wiki/Sensitivity_and_specificity
* Sometimes false positives are better than false negatives
    * E.g., Privacy in images
* Sometimes false negatives are better than false positives
    * FN: E-mail that is SPAM is not caught, so you see it in your inbox
    * FP: E-mail flagged as SPAM is removed from your inbox
* Find the threshold that brings the precision or recall to acceptable values
* Check the precision/recall you obtain with that threshold in each of your subgroups
* Choose your evaluation metrics in light of acceptable tradeoffs between FP and FN

---
## Equality of Opportunity

> [![](https://img.youtube.com/vi/9TwBebaCUsM/0.jpg)](https://youtu.be/9TwBebaCUsM)

* The equality of opportunity approach strives to give individuals an equal chance of desired outcome
* Case
    * The impact of threshold on credit score is evaluated based on its impact on customers and on load repayment
* Classification and discrimination must obey the equality of opportunity principle

---
## Simulating Decsions

> [![](https://img.youtube.com/vi/vuml5OFZHrQ/0.jpg)](https://youtu.be/vuml5OFZHrQ)

* Simulating decisions with no constraints can lead to unequal distribution
* Simulating decisions with group unaware bolds everyone to the same standard, which can be unfair to some group
* Simulating decisions equal opportunity results in an identical true positive rate for all groups

---
## Finding Errors in Your Dataset Using Facets

> [![](https://img.youtube.com/vi/Snq986HZJKU/0.jpg)](https://youtu.be/Snq986HZJKU)

* Facets gives users a quick understanding of the distribution of values across features of their datasets
* With Facets, common data issues that can hamper ML are pushed to the forefront
    * E.g, unexpected feature values, features with high percentages of missing values, feature with unbalanced distrobutions or distribution skew between datasets
* In Facets features are sorted by **non-uniformity**, with the feature with the most non-uniform distribution at the top
* Facets features are sorted by distrobution distance

---
## Module Quiz

1. You have been hired as a consultant by a concession operator. The company created an ML model to infer the demand for ice cold slushie drinks at international golf tournaments. The model has been trained on a million sales of the drinks at past golf tournaments, using tournament attendance, the price of drinks, and size of the drink ordered. Unfortunately, it appears the model is not accurately predicting sales of slushies. Which of the following are reasonable conclusions?  
   * A. The people at past golf tournaments were really thirsty, so sales were up.
   * B. Outdoor temperatures could be affecting sales. Cold days may not be the best time to sell ice cold drinks and maybe ice cold slushies are not as refreshing in Alaska as in Mexico
    * C. Slushies are a trend whose time has passed.
    > Answer: B
2. You fixed the ice cold slushie model, it is now accurately predicting total sales of slushies. The model also infers the demand for each of the three slushie flavors (coffee, bubblegum, and watermelon) and places a reorder when the flavor supply drops below 10 bottles. Unfortunately, the model has only been accurate with the watermelon flavor. Both the coffee and bubblegum flavors are overstocked at some tournaments and understocked at others. Which of the following are reasonable conclusions? (Select all 2 correct answers)
    * A. Coffee and bubblegum are a trendy flavors, you can never accurately predict demand for these flavors.
    * B. Coffee and bubblegum are flavors that appeal to different subgroups - adults and kids. You should examine attendance by adults and kids at tournaments to see if there is a correlation with sales.
    * C. Coffee and bubblegum may be regional favorites. You should look for a correlation between consumption of these flavors and the geographic location of the tournaments.
    > Answer: B. C.
3. You have modified the model to account for adult and child attendance at golf tournaments. The model is accurately predicting sales and correctly ordering the coffee and watermelon flavors. There is still a problem with the bubblegum supply, it is constantly in overstock. Which of the following are reasonable conclusions? (Select all 2 correct answers)
    * A. Bubblegum flavoring is preferred by children, who usually order the kid size drink. Which requires the least amount of flavoring. So when we are down to 10 bottles of the other flavors, we are down to a 40 drink supply. Ten bottles for kid size drinks is 100 drinks.
    * B. Bubblegum is a strong flavor, you use less of it to flavor drinks. So it is possible the 10 bottle minimum might be too high.
    * C. The flavoring bottles are stored together in the concession and coffee and watermelon bottles break more often than bubblegum ones.
    > Answer: A. B.



92 90 64
19 13 11

