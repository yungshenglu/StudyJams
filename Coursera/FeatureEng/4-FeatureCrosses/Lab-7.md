# Lab 7: Improve ML Model with Feature Engineering

> * Last Tested Date: DEC 06, 2018
> * Last Updated Date: JUL 01, 2019

## Overview

This lab is part of a lab series, where you go from exploring a taxicab dataset to training and deploying a high-accuracy distributed model with Cloud ML Engine.

### What You Learn

In this lab, you will improve the ML model using feature engineering. In the process, you will learn how to:

* Work with feature columns
* Add feature crosses in TensorFlow
* Read data from BigQuery
* Create datasets using Dataflow
* Use a wide-and-deep model

---
## Setup

For each lab, you get a new GCP project and set of resources for a fixed time at no cost.
1. Make sure you signed into Qwiklabs using an incognito window.
2. Note the lab's access time (for example, `02:00:00` and make sure you can finish in that time block.
    * There is no pause feature. You can restart if needed, but you have to start at the beginning.
3. When ready, click `START LAB`
4. Note your lab credentials. You will use them to sign in to Cloud Platform Console. 
    ![](../../../res/img/Coursera/FeatureEng/FeatureEng-2L-1.png)
5. Click `Open Google Console`.
6. Click `Use another account` and copy/paste credentials for **this** lab into the prompts.
    * If you use other credentials, you'll get errors or **incur charges**.
7. Accept the terms and skip the recovery resource page.
    * Do not click `End Lab` unless you are finished with the lab or want to restart it. This clears your work and removes the project.

---
## Create Storage Bucket

1. In In your GCP Console, click on the **Navigation menu**, and select `Storage`.
2. Click on `Create bucket`.
3. Choose a **Regional** bucket and set a unique name (use your project ID because it is unique). Then, click `Create`.

---
## Launch AI Platform Notebooks

To launch AI Platform Notebooks

1. Click on the **Navigation Menu**. Navigate to `AI Platforms`, then to `Notebooks`.
    ![](../../../res/img/Coursera/FeatureEng/FeatureEng-2L-2.png)
2. On the Notebook instances page, click `+ NEW INSTANCE`. Select `TensorFlow 1.x`.
    ![](../../../res/img/Coursera/FeatureEng/FeatureEng-2L-3.png)
    * In the pop-up, confirm the name of the deep learning VM and click `Create`.
        ![](../../../res/img/Coursera/FeatureEng/FeatureEng-2L-4.png)
    * The new VM will take 2-3 minutes to start.
3. Click `Open JupyterLab`. A JupyterLab window will open in a new tab.

---
## Clone Course Repository within Your AI Platform Notebooks Instance

To clone the `training-data-analyst` notebook in your JupyterLab instance:

1. In JupyterLab, click the `Terminal` icon to open a new terminal.
    ![](../../../res/img/Coursera/FeatureEng/FeatureEng-2L-6.png)
2. At the command-line prompt, type in the following command and press `Enter`.
    ```bash
    $ git clone https://github.com/GoogleCloudPlatform/training-data-analyst 
    ```
3. Confirm that you have cloned the repository by double clicking on the `training-data-analyst` directory and ensuring that you can see its contents. The files for all the Jupyter notebook-based labs throughout this course are available in this directory.
    ![](../../../res/img/Coursera/FeatureEng/FeatureEng-2L-7.png)

---
## Feature Engineering

1. In the notebook interface, navigate to `training-data-analyst > courses > machine_learning > deepdive > 04_features > taxifeateng` and open `feateng.ipynb`.
2. In the notebook interface, click on `Edit > Clear All Outputs` (click on `Edit`, then in the drop-down menu, select `Clear All Outputs`).
    * The solution video will demo notebooks that contain hyper-parameter tuning and training on 500 million rows of data. The changes to the model are minor -- essentially just command-line parameters, but the impact on model accuracy is huge.

---
## End Your Lab

1. When you have completed your lab, click `End Lab`. Qwiklabs removes the resources you’ve used and cleans the account for you.
2. You will be given an opportunity to rate the lab experience. Select the applicable number of stars, type a comment, and then click `Submit`.
    * The number of stars indicates the following:
        * 1 star = Very dissatisfied
        * 2 stars = Dissatisfied
        * 3 stars = Neutral
        * 4 stars = Satisfied
        * 5 stars = Very satisfied
3. You can close the dialog box if you don't want to provide feedback.
4. For feedback, suggestions, or corrections, please use the `Support` tab.

---
> ©2019 Google LLC All rights reserved. Google and the Google logo are trademarks of Google LLC. All other company and product names may be trademarks of the respective companies with which they are associated.
