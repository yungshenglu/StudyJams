# Lab 3: Rent a VM

> * Last Tested Date: MAR 08, 2018
> * Last Updated Date: MAR 11, 2019

## Overview

In this lab, you spin up a virtual machine, configure its security, access it remotely, and then carry out the steps of an ingest-transform-and-publish data pipeline manually.

### What You Learn

In this lab, you:

* Create a Compute Engine instance with the necessary Access and Security
* SSH into the instance
* Install the software package Git (for source code version control)
* Ingest data into a Compute Engine instance
* Transform data on the Compute Engine instance
* Store the transformed data on Cloud Storage
* Publish Cloud Storage data to the web

---
## Introduction

In this lab you spin up a virtual machine, configure its security, access it remotely, and then carry out the steps of an ingest-transform-and-publish data pipeline manually.

![](../../../res/img/GoogleML/GoogleML-1-9.png)

The point is to ingest earthquake data from the US Geographic Service and create a map like the one shown. The map will be inserted into a web page, and then you will publish that web page. In order to carry out the compute, you will spin up a virtual machine and access it remotely. You will install some software on it, download some scripts, and then run them to do the actual data processing. The resulting files will be copied to Cloud Storage, from which you can set the access control to publish the files for anyone to access.

1. Create a Compute Engine instance with the necessary Access and Security
2. SSH into the instance and install the software package Git (gor source code version control)
3. Ingest data into a instance and then transform it
4. Store and transform data on Cloud Storage; publish data to the web

And that’s it—Google Cloud Platform will take care of the rest. Your files will be globally available and edge-cached so that people halfway across the world can access them quickly.

---
## Setup

For each lab, you get a new GCP project and set of resources for a fixed time at no cost.
1. Make sure you signed into Qwiklabs using an incognito window.
2. Note the lab's access time (for example, `02:00:00` and make sure you can finish in that time block.
    * There is no pause feature. You can restart if needed, but you have to start at the beginning.
3. When ready, click `START LAB`
4. Note your lab credentials. You will use them to sign in to Cloud Platform Console. 
    ![](../../../res/img/GoogleML/GoogleML-4L-1.png)
5. Click `Open Google Console`.
6. Click `Use another account` and copy/paste credentials for **this** lab into the prompts.
    * If you use other credentials, you'll get errors or **incur charges**.
7. Accept the terms and skip the recovery resource page.
    * Do not click `End Lab` unless you are finished with the lab or want to restart it. This clears your work and removes the project.

---
## Create Compute Engine instance with the necessary API access

To create a Compute Engine instance:

1. Browse to https://cloud.google.com/
2. Click on `Go To Console`.
3. Click on the `Navigation menu` (three horizontal lines):
    ![](../../../res/img/GoogleML/GoogleML-4L-2.png)
4. Select `Compute Engine`.
5. Click `Create` and wait for a form to load. You will need to change some options on the form that comes up.
6. For **Identity and API access**, in **Access scopes**, select `Allow full access to all Cloud APIs`:
    ![](../../../res/img/GoogleML/GoogleML-4L-3.png)
7. Now, click `Create`

---
## SSH into the Instance

You can remotely access your Compute Engine instance using Secure Shell (SSH):

1. Click on SSH:
    ![](../../../res/img/GoogleML/GoogleML-4L-4.png)
    * **Note:** SSH keys are automatically transferred, and that you can ssh directly from the browser, with no extra software needed.
2. To find some information about the Compute Engine instance, type the following into the command-line:
    ```bash
    $ cat /proc/cpuinfo
    ```

---
## Install Software

1. Type the following into command-line:
    ```bash
    $ sudo apt-get update
    $ sudo apt-get -y -qq install git
    ```
2. Verify that git is now installed
    ```bash
    $ git --version
    ```

---
## Ingest USGS Data

1. On the command-line, type:
    ```bash
    $ git clone https://github.com/GoogleCloudPlatform/training-data-analyst
    ```
    * This clones the code repository.
2. Navigate to the folder corresponding to this lab:
    ```bash
    $ cd training-data-analyst/courses/machine_learning/deepdive/01_googleml/earthquakes
    ```
3. Examine the ingest code using `less`:
    ```bash
    $ less ingest.sh
    ```
    * The `less` command allows you to view the file (Press the `spacebar` to scroll down; the letter `b` to back up a page; the letter `q` to quit).
    * The program `ingest.sh` downloads a dataset of earthquakes in the past 7 days from the US Geological Survey. Where is this file downloaded? To disk or to Cloud Storage? __________________________
4. Run the ingest code:
    ```bash
    $ bash ingest.sh
    ```
5. Verify that some data has been downloaded:
    ```bash
    $ head earthquakes.csv
    ```
    * The head command shows you the first few lines of the file.

---
## Transform the data

You will use a Python program to transform the raw data into a map of earthquake activity:

1. The transformation code is explained in detail in this notebook: https://github.com/GoogleCloudPlatform/datalab-samples/blob/master/basemap/earthquakes.ipynb
    * Feel free to read the narrative to understand what the transformation code does. The notebook itself was written in Datalab, a GCP product that you will use later in this set of labs.
2. First, install the necessary Python packages on the Compute Engine instance:
    ```bash
    $ bash install_missing.sh
    ```
3. Then, run the transformation code:
    ```bash
    $ ./transform.py
    ```
4. You will notice a new image file if you list the contents of the directory:
    ```bash
    $ ls -l
    ```

---
## Create Bucket

Create a bucket using the GCP console:

1. Browse to the GCP Console by visiting http://cloud.google.com and clicking on `Go To Console`
2. Click on the `Navigation menu` (3 bars) at the top-left and select `Storage`
3. Click on Create bucket.
4. Choose a globally unique bucket name (your project name is unique, so you could use that). You can leave it as **Multi-Regional**, or improve speed and reduce costs by making it `Regional`. Then, click `Create`.
    * **Note:** Please pick a region from the following: `us-east1`, `us-central1`, `asia-east1`, `europe-west1`. These are the regions that currently support Cloud ML Engine jobs. Please verify [here](https://cloud.google.com/ml-engine/docs/environment-overview#cloud_compute_regions) since this list may have changed after this lab was last updated. For example, if you are in the US, you may choose `us-east1` as your region.
5. Note down the name of your bucket: _______________________________
    * In this and future labs, you will insert this whenever the directions ask for `<YOUR-BUCKET>`.

---
## Store Data

To store the original and transformed data in Cloud Storage

1. In the SSH window of the Compute Engine instance, type the following command to copy the files to Cloud Storage
    ```bash
    $ gsutil cp earthquakes.* gs://<YOUR-BUCKET>/earthquakes/
    ```
2. On the GCP console, click on your bucket name, and notice there are three new files present in the earthquakes folder.

---
## Publish Cloud Storage Files to Web

To publish Cloud Storage files to the web:

1. In the SSH window of the Compute Engine instance, type:
    ```bash
    $ gsutil acl ch -u AllUsers:R gs://<YOUR-BUCKET>/earthquakes/*
    ```
2. Click on the `Public link` corresponding to `earthquakes.htm`
    ![](../../../res/img/GoogleML/GoogleML-4L-5.png)
3. What is the URL of the published Cloud Storage file? How does it relate to your bucket name and content? ______________________________________________________
4. What are some advantages of publishing to Cloud Storage? _____________________________________________

---
## Clean Up

To delete the Compute Engine instance (since we won't need it any more):

1. On the GCP console, click the `Navigation Menu` (three horizontal bars) and select `Compute Engine`
2. Click on the checkbox corresponding to the instance that you created (the default name was `instance-1`)
3. Click on the `Delete` button in the top-right corner
4. Does deleting the instance have any impact on the files that you stored on Cloud Storage? ___________________

---
## Summary

In this lab, you used Google Cloud Platform (GCP) as rented infrastructure. You can spin up a Compute Engine VM, install custom software on it, and run your processing jobs. However, using GCP in this way doesn't take advantage of the other benefits that Google Cloud Platform provides -- namely the ability to forget about infrastructure and work with your scientific computation problems simply as software that requires to be run.

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