# Summary

Here we recap the major points you learned in each module on Feature Engineering: Selecting Good Features, Preprocessing at Scale, Using Feature Crosses, and Practicing with TensorFlow.

> [![](https://img.youtube.com/vi/Qgw4dEWLw68/0.jpg)](https://youtu.be/Qgw4dEWLw68)

* You learned how to
    * Convert raw data into features
    * Preprocess data in such a way that the preprocessing is also done during serving
    * Choose among the various feature columns in TensorFlow
    * Memorize large datasets using feature crosses and simple models
    * Simplify preprocessing pipelines using TensorFlow Transform
* Raw data to features
    * Feature engineering is necessary because raw data doesn't come to us as feature vectors
    * Process of creating features from raw data is feature engineering
* Things that rae commonly done in preprocessing
    * In BigQuery or Beam
        * Removes examples that you don't want to train on
        * Compute vocabularies for categorical columns
        * Compute aggregate statistics for numeric columns
    * In Beam only
        * Compute time-windowed statistics (e.g., number of products sold in previous hour) for use as input features
    * In TensorFlow or Beam
        * Scaling, discretization, etc. of numeric features
        * Splitting, lower-casing, etc. of textual features
        * Resizing of input images
        * Normalizing volumn level of input audio
* Creating an embedding column from a feature cross
