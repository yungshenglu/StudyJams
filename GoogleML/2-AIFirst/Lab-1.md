# Lab 1: Framing an ML Problem

In this lab activity, you will choose 2 from a set of provided use cases and think about the problems from an ML perspective.

## Discussion Prompt

Pick TWO use cases from the slide content presented below (e.g. aircraft scheduling, credit worthiness evaluation) and answer the following questions for each use case. Please copy the questions into your response.

### Cloud Machine Learning Use Cases

* Manufacturing
    * Predictive mantenance or condition monitoring
    * Warranty reserve estimation
    * Propensity to buy
    * Deman forecasting
    * Process optimization
    * Telematics
* Retail
    * Predictive inventory planning
    * Recommendation engines
    * Upsell and cross-channel marketing
    * Market segmentation and targeting
    * Customer ROI and lifetime value
* Healthcare and Life Sciences
    * Alerts and diagnostics from real-time patient data
    * Disease identification and risk satisfaction
    * Patient triage optimization
    * Proactive health management
    * Healthcare provider sentiment analysis
* Travel and Hospitality
    * Aircraft scheduling
    * Dynamic pricing
    * Social media - consumer feedback and interaction analysis
    * Customer complaint resolution
    * Traffic patterns and congestion management
* Financial Services
    * Risk analytics and regulation
    * Customer segmentation
    * Cross-selling and upselling
    * Sales and marketing campaign management
    * Credit worthiness evaluation
* Energy, Feedstock and Utilities
    * Power usage analytics
    * Seismic data processing
    * Carbon emissions and trading
    * Customer-specific pricing
    * Smart grid management
    * Energy demand and supply optimization

---
## Questions

### Use Case 1:

* If the use case was an ML problem....
    1. What is being predicted?
    2. What data is needed?
* Now imagine the ML problem is a question of software:
    1. What is the API for the problem during prediction?
    2. Who will use this service? How are they doing it today?
* Lastly, cast it in the framework of a data problem. What are some key actions to collect, analyze, predict, and react to the data/predictions (different input features might require different actions)
    1. What data are we analyzing?
    2. What data are we predicting?
    3. What data are we reacting to?

### Use Case 2:

* If the use case was an ML problem....
    1. What is being predicted?
    2. What data is needed?
* Now imagine the ML problem is a question of software:
    1. What is the API for the problem during prediction?
    2. Who will use this service? How are they doing it today?
* Lastly, cast it in the framework of a data problem. What are some key actions to collect, analyze, predict, and react to the data/predictions (different input features might require different actions)
    1. What data are we analyzing?
    2. What data are we predicting?
    3. What data are we reacting to?

---
## Example Solution

### Demand forecasting in manufacturing

1. What is being predicted?
    * How many units of widgets X should we manufacture this month?
2. What data is needed?
    * Historical data on # of units sold, price it was sold out, # of units returned, price of competitor product, # of units of all items that use widget X that were sold (e.g., if widget is a phone display panel, how many smartphone were sold, regardless of which display panel they carried?), economic figures (e.g., customer confidence, interest rate, this-month-last-year
3. What is the API for the problem during prediction?
    ```
    predictDemand(widgetID, month=CurrentTime.month)
    ```
4. Who will use this service? How are they doing it today?
    * Product managers, logistics managers
    * They examine trends of e.g., phone sales, overall economy, trade publications and make a decision
5. Data problem:
    * Collect: economic data, competitor data, ndustry data, our figures
    * Analyze: craft features that our experts are looking at today from this data and use as inputs to model
    * React: automatic?