# Awwvision: Cloud Vision API from a Kubernetes Cluster

## GSP066

![](../../../res/img/selfplacedlabs.png)

The Awwvision lab uses [Kubernetes](https://kubernetes.io/) and [Cloud Vision API](https://cloud.google.com/vision) to demonstrate how to use the Vision API to classify (label) images from Reddit's [/r/aww](https://reddit.com/r/aww) subreddit and display the labelled results in a web app.

Awwvision has three components:

1. A simple [Redis](http://redis.io/) instance.
2. A web app that displays the labels and associated images.
3. A worker that handles scraping Reddit for images and classifying them using the Vision API. [Cloud Pub/Sub](https://cloud.google.com/pubsub) is used to coordinate tasks between multiple worker instances.

---
## Setup

### Before you click the Start Lab button

Read these instructions. Labs are timed and you cannot pause them. The timer, which starts when you click Start Lab, shows how long Cloud resources will be made available to you.

This Qwiklabs hands-on lab lets you do the lab activities yourself in a real cloud environment, not in a simulation or demo environment. It does so by giving you new, temporary credentials that you use to sign in and access the Google Cloud Platform for the duration of the lab.

### What you need

To complete this lab, you need:

* Access to a standard internet browser (Chrome browser recommended).
* Time to complete the lab.

> **Note:** If you already have your own personal GCP account or project, do not use it for this lab.

### How to start your lab and sign in to the Console

1. Click the `Start Lab` button. If you need to pay for the lab, a pop-up opens for you to select your payment method. On the left you will see a panel populated with the temporary credentials that you must use for this lab.
    ![](../../../res/img/Setup/Setup-1.png)
2. Copy the username, and then click `Open Google Console`. The lab spins up resources, and then opens another tab that shows the **Choose an account** page.
    * **Tip:** Open the tabs in separate windows, side-by-side.
3. On the **Choose an account** page, click `Use Another Account`.
    ![](../../../res/img/Setup/Setup-2.png)
4. The Sign in page opens. Paste the username that you copied from the Connection Details panel. Then copy and paste the password.
    * **Important:** You must use the credentials from the Connection Details panel. Do not use your Qwiklabs credentials. If you have your own GCP account, do not use it for this lab (avoids incurring charges).
5. Click through the subsequent pages:
    * Accept the terms and conditions.
    * Do not add recovery options or two-factor authentication (because this is a temporary account).
    * Do not sign up for free trials.
6. After a few moments, the GCP console opens in this tab.
    * **Note:** You can view the menu with a list of GCP Products and Services by clicking the Navigation menu at the top-left, next to “Google Cloud Platform”.
        ![](../../../res/img/Setup/Setup-3.png)

### Activate Google Cloud Shell

Google Cloud Shell is a virtual machine that is loaded with development tools. It offers a persistent 5GB home directory and runs on the Google Cloud. Google Cloud Shell provides command-line access to your GCP resources.

1. In GCP console, on the top right toolbar, click the `Open Cloud Shell` button.
    ![](../../../res/img/Setup/Setup-4.png)
2. In the dialog box that opens, click `START CLOUD SHELL`:
    ![](../../../res/img/Setup/Setup-5.png)
    * You can click `START CLOUD SHELL` immediately when the dialog box opens.
3. It takes a few moments to provision and connect to the environment. When you are connected, you are already authenticated, and the project is set to your `PROJECT_ID`. For example:
    ![](../../../res/img/Setup/Setup-6.png)
4. `gcloud` is the command-line tool for Google Cloud Platform. It comes pre-installed on Cloud Shell and supports tab-completion.
    * You can list the active account name with this command:
        ```bash
        $ gcloud auth list
        # Output
        Credentialed accounts:
        - <myaccount>@<mydomain>.com (active)
        # Example output
        Credentialed accounts:
        - google1623327_student@qwiklabs.net
        ```
    * You can list the project ID with this command:
        ```bash
        $ gcloud config list project
        # Output
        [core]
        project = <project_ID>
        # Example output
        [core]
        project = qwiklabs-gcp-44776a13dea667a6
        ```
    * Full documentation of `gcloud` is available on [Google Cloud gcloud Overview](https://cloud.google.com/sdk/gcloud).

---
## Create a Kubernetes Engine cluster

In this lab you will use [gcloud](https://cloud.google.com/sdk/gcloud), Google Cloud's command-line tool, to set up a [Kubernetes Engine](https://cloud.google.com/kubernetes-engine) cluster. You can specify as many nodes as you want, but you need at least one. The cloud platform scope is used to allow access to the Pub/Sub and Vision APIs.

1. In Cloud Shell, run the following to create a cluster in the `us-central1-a` zone:
    ```bash
    $ gcloud config set compute/zone us-central1-a
    ```
2. Then start up the cluster by running:
    ```bash
    $ gcloud container clusters create awwvision \
    --num-nodes 2 \
    --scopes cloud-platform
    ```
3. Run the following to use the container's credentials:
    ```bash
    $ gcloud container clusters get-credentials awwvision
    ```
4. Verify that everything is working using the `kubectl` command-line tool:
    ```bash
    $ kubectl cluster-info
    ```

---
## Create a virtual environment

1. Execute the following command to download and update the packages list.
    ```bash
    $ sudo apt-get update
    ```
2. Python virtual environments are used to isolate package installation from the system.
    ```bash
    $ sudo apt-get install virtualenv
    $ virtualenv -p python3 venv
    ```
    > **Note**: If prompted `[Y/n]`, press `Y` and then Enter.
3. Activate the virtual environment.
    ```bash
    $ source venv/bin/activate
    ```

---
## Get the Sample

1. Now add sample data to your project by running:
    ```bash
    $ git clone https://github.com/GoogleCloudPlatform/cloud-vision
    ```

---
## Deploy the sample

1. In Cloud Shell, change to the `python/awwvision` directory in the cloned cloud-vision repo:
    ```bash
    $ cd cloud-vision/python/awwvision
    ```
2. Once in the `awwvision` directory, run make all to build and deploy everything:
    ```bash
    $ make all
    ```

As part of the process, Docker images will be built and uploaded to the [Google Container Registry](https://cloud.google.com/container-registry/docs) private container registry. In addition, `yaml` files will be generated from templates, filled in with information specific to your project, and used to deploy the `redis`, `webapp`, and `worker` Kubernetes resources for the lab.

---
## Check the Kubernetes resources on the cluster

After you've deployed, check that the Kubernetes resources are up and running.

1. First, list the [pods](https://kubernetes.io/docs/concepts/workloads/pods/pod) by running:
    ```bash
    $ kubectl get pods
    ```
2. You should see something like the following, though your pod names will be different. Make sure all of your pods have a Running before executing the next command.
    ```bash
    NAME                     READY     STATUS    RESTARTS   AGE
    awwvision-webapp-vwmr1   1/1       Running   0          1m
    awwvision-worker-oz6xn   1/1       Running   0          1m
    awwvision-worker-qc0b0   1/1       Running   0          1m
    awwvision-worker-xpe53   1/1       Running   0          1m
    redis-master-rpap8       1/1       Running   0          2m
    ```
3. Next, list the [deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment) by running:
    ```bash
    $ kubectl get deployments -o wide
    ```
4. You can see the number of replicas specified for each, and the images used.
    ```bash
    NAME               DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE       CONTAINERS         IMAGES                                SELECTOR
    awwvision-webapp   1         1         1            1           1m        awwvision-webapp   gcr.io/your-project/awwvision-webapp   app=awwvision,role=frontend
    awwvision-worker   3         3         3            3           1m        awwvision-worker   gcr.io/your-project/awwvision-worker   app=awwvision,role=worker
    redis-master       1         1         1            1           1m        redis-master       redis                                 app=redis,role=master
    ```
5. Once deployed, get the external IP address of the webapp [service](https://kubernetes.io/docs/concepts/services-networking/service) by running:
    ```bash
    $ kubectl get svc awwvision-webapp
    ```
6. It may take a few minutes for the assigned external IP to be listed in the output. You should see something like the following, though your IPs will be different.
    ```bash
    NAME               CLUSTER_IP      EXTERNAL_IP    PORT(S)   SELECTOR                      AGE
    awwvision-webapp   10.163.250.49   23.236.61.91   80/TCP    app=awwvision,role=frontend   13m
    ```

---
## Visit your new web app and start its crawler

1. Copy and paste the external IP of the `awwvision-webapp` service into a new browser to open the webapp, then click `Start the Crawler` button.
2. Next, click `go back` and you should start to see images from the [/r/aww](https://reddit.com/r/aww) subreddit classified by the labels provided by the Vision API. You will see some of the images classified multiple times, when multiple labels are detected for them. (You can reload in a bit, in case you brought up the page before the crawler was finished).
3. Your results will look something like this:
    ![](../../../res/img/MachineLearningAPIs/MachineLearningAPIs-6-1.png)

### Test your Understanding

Below are a multiple choice questions to reinforce your understanding of this lab's concepts. Answer them to the best of your abilities.

* 0: ____ allows developers to easily integrate vision detection features within applications, including image labeling, face and landmark detection and much more.
    1. Cloud ML
    2. Cloud Vision API
    3. Compute

---
## Congratulations

### Finish Your Quest

This self-paced lab is part of the Qwiklabs [Machine Learning APIs](https://google.qwiklabs.com/quests/32), [Kubernetes Solutions](https://google.qwiklabs.com/quests/45), and [Advanced ML: ML Infrastructure](https://google.qwiklabs.com/quests/84) Quests. A Quest is a series of related labs that form a learning path. Completing a Quest earns you a badge to recognize your achievement. You can make your badge (or badges) public and link to them in your online resume or social media account. Enroll in one of the above Quests and get immediate completion credit if you've taken this lab. [See other available Qwiklabs Quests](http://google.qwiklabs.com/catalog).

### Take your next lab

Try out another lab on Machine Learning APIs, like [Running Dedicated Game Servers in Google Kubernetes Engine](https://google.qwiklabs.com/catalog_lab/764) or [Distributed Load Testing using Kubernetes](https://google.qwiklabs.com/catalog_lab/936).

### Next steps

Sign up for the full [Coursera Course on Machine Learning](https://www.coursera.org/specializations/machine-learning-tensorflow-gcp).
