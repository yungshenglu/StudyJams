# Lab 4: Getting Started with Kubernetes Engine

In this lab, you create a Kubernetes Engine cluster containing several containers, each containing a web server. You place a load balancer in front of the cluster and view its contents.

---
## Objectives

In this lab, you learn how to perform the following tasks:
* Provision a [Kubernetes](http://kubernetes.io/) cluster using [Kubernetes Engine](https://cloud.google.com/container-engine).
* Deploy and manage Docker containers using `kubectl`.

---
## Task 1: Sign in to the Google Cloud Platform (GCP) Console

### Before you click the Start Lab button

Read these instructions. Labs are timed and you cannot pause them. The timer, which starts when you click Start Lab, shows how long Cloud resources will be made available to you.

This Qwiklabs hands-on lab lets you do the lab activities yourself in a real cloud environment, not in a simulation or demo environment. It does so by giving you new, temporary credentials that you use to sign in and access the Google Cloud Platform for the duration of the lab.

### What you need

To complete this lab, you need:

* Access to a standard internet browser (Chrome browser recommended).
* Time to complete the lab.

> Note: If you already have your own personal GCP account or project, do not use it for this lab.

---
## Task 2: Confirm that needed APIs are enabled

1. Make a note of the name of your GCP project. This value is shown in the top bar of the Google Cloud Platform Console. It will be of the form `qwiklabs-gcp-` followed by hexadecimal numbers.
2. In the GCP Console, on the **Navigation menu**, click `APIs & Services`.
3. Scroll down in the list of enabled APIs, and confirm that both of these APIs are enabled:
    * Kubernetes Engine API
    * Google Container Registry API
4. If either API is missing, click `Enable APIs and Services` at the top. Search for the above APIs by name and enable each for your current project. (You noted the name of your GCP project above.)

---
## Task 3: Start a Kubernetes Engine cluster

1. In GCP console, on the top right toolbar, click the `Open Cloud Shell` button.
    ![](../../../res/img/Coursera/CoreInfra/CoreInfra-5L-1.png)
2. Click `Continue`.
    ![](../../../res/img/Coursera/CoreInfra/CoreInfra-5L-2.png)
3. For convenience, place the zone that Qwiklabs assigned you to into an environment variable called `MY_ZONE`. At the Cloud Shell prompt, type this partial command:
    ```bash
    $ export MY_ZONE=
    ```
    * followed by the zone that Qwiklabs assigned to you. Your complete command will look like this:
        ```bash
        $ export MY_ZONE=us-central1-a
        ```
4. Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster `webfrontend` and configure it to run 2 nodes:
    ```bash
    $ gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2
    ```
    * It takes several minutes to create a cluster as Kubernetes Engine provisions virtual machines for you.
5. After the cluster is created, check your installed version of Kubernetes using the `kubectl version` command:
    ```bash
    $ kubectl version
    ```
    * The `gcloud container clusters` create command automatically authenticated `kubectl` for you.
6. View your running nodes in the GCP Console. On the **Navigation menu**, click `Compute Engine` > `VM Instances`.
    * Your Kubernetes cluster is now ready for use.

---
## Task 4: Run and deploy a container

1. From your Cloud Shell prompt, launch a single instance of the nginx container. (Nginx is a popular web server.)
    ```bash
    $ kubectl run nginx --image=nginx:1.10.0
    ```
    * In Kubernetes, all containers run in pods. This use of the `kubectl run` command caused Kubernetes to create a deployment consisting of a single pod containing the nginx container. A Kubernetes deployment keeps a given number of pods up and running even in the event of failures among the nodes on which they run. In this command, you launched the default number of pods, which is 1.
    > Note: If you see any deprecation warning about future version you can simply ignore it for now and can proceed further.
2. View the pod running the nginx container:
    ```bash
    $ kubectl get pods
    ```
3. Expose the nginx container to the Internet:  
    ```bash
    $ kubectl expose deployment nginx --port 80 --type LoadBalancer
    ```
    * Kubernetes created a service and an external load balancer with a public IP address attached to it. The IP address remains the same for the life of the service. Any network traffic to that public IP address is routed to pods behind the service: in this case, the nginx pod.
4. View the new service:
    ```bash
    $ kubectl get services
    ```
    * You can use the displayed external IP address to test and contact the nginx container remotely.
    * It may take a few seconds before the `External-IP` field is populated for your service. This is normal. Just re-run the `kubectl get services` command every few seconds until the field is populated.
5. Open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed.
6. Scale up the number of pods running on your service:
    ```bash
    $ kubectl scale deployment nginx --replicas 3
    ```
    * Scaling up a deployment is useful when you want to increase available resources for an application that is becoming more popular.
7. Confirm that Kubernetes has updated the number of pods:
    ```bash
    $ kubectl get pods
    ```
8. Confirm that your external IP address has not changed:
    ```bash
    $ kubectl get services
    ```
9. Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding.

---
## Congratulations!

In this lab, you configured a Cloud SQL instance and connected an application in a Compute Engine instance to it. You also worked with a Cloud Storage bucket.

---
## End your Lab

When you have completed your lab, click `End Lab`. Qwiklabs removes the resources you’ve used and cleans the account for you.

You will be given an opportunity to rate the lab experience. Select the applicable number of stars, type a comment, and then click `Submit`.

The number of stars indicates the following:

* 1 star = Very dissatisfied
* 2 stars = Dissatisfied
* 3 stars = Neutral
* 4 stars = Satisfied
* 5 stars = Very satisfied

You can close the dialog box if you don't want to provide feedback.

For feedback, suggestions, or corrections, please use the Support tab.

> Copyright 2019 Google LLC All rights reserved. Google and the Google logo are trademarks of Google LLC. All other company and product names may be trademarks of the respective companies with which they are associated.

---
## More Resources

Read the [Google Cloud Platform documentation on Kubernetes Engine](https://cloud.google.com/kubernetes-engine/docs/).
