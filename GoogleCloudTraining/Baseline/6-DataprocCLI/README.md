# Dataproc: Qwik Start - Command Line

## GSP104

![](../../../res/img/selfplacedlabs.png)

Cloud Dataproc is a fast, easy-to-use, fully-managed cloud service for running [Apache Spark](http://spark.apache.org/) and [Apache Hadoop](http://hadoop.apache.org/) clusters in a simpler, more cost-efficient way. Operations that used to take hours or days take seconds or minutes instead. Create Cloud Dataproc clusters quickly and resize them at any time, so you don't have to worry about your data pipelines outgrowing your clusters.

This lab shows you how to use the Google Cloud Platform (GCP) Console to create a Google Cloud Dataproc cluster, run a simple [Apache Spark](http://spark.apache.org/) job in the cluster, then modify the number of workers in the cluster.

---
## Setup and Requirements

### Before you click the Start Lab button

Read these instructions. Labs are timed and you cannot pause them. The timer, which starts when you click Start Lab, shows how long Cloud resources will be made available to you.

This Qwiklabs hands-on lab lets you do the lab activities yourself in a real cloud environment, not in a simulation or demo environment. It does so by giving you new, temporary credentials that you use to sign in and access the Google Cloud Platform for the duration of the lab.

### What you need

To complete this lab, you need:

* Access to a standard internet browser (Chrome browser recommended).
* Time to complete the lab.
* **Note:** If you already have your own personal GCP account or project, do not use it for this lab.

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
    * * **Note:** You can view the menu with a list of GCP Products and Services by clicking the Navigation menu at the top-left, next to “Google Cloud Platform”.
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
    * `gcloud` is the command-line tool for Google Cloud Platform. It comes pre-installed on Cloud Shell and supports tab-completion.
        * You can list the active account name with this command:
            ```bash
            $ gcloud auth list
            # Output:
            Credentialed accounts:
            - <myaccount>@<mydomain>.com (active)
            # Example output:
            Credentialed accounts:
            - google1623327_student@qwiklabs.net
            ```
        * You can list the project ID with this command:
            ```bash
            $ gcloud config list project
            # Output:
            [core]
            project = <project_ID>
            # Example output:
            [core]
            project = qwiklabs-gcp-44776a13dea667a6
            ```
    * **Note:** Full documentation of gcloud is available on [Google Cloud gcloud Overview](https://cloud.google.com/sdk/gcloud).

---
## Create a cluster

1. Run the following command to create a cluster called `example-cluster` with default Cloud Dataproc settings:
    ```bash
    $ gcloud dataproc clusters create example-cluster
    ```
    * You'll be asked to choose a zone for your cluster. Enter the number and press `Enter`.
    * Your cluster will build for a couple of minutes.
        ```bash
        Waiting for cluster creation operation...done.
        Created [... example-cluster]
        ```
2. When you see a `Created` message, you're ready to move on.

---
## Submit a job

1. Run this command to submit a sample Spark job that calculates a rough value for pi:
    ```bash
    $ gcloud dataproc jobs submit spark --cluster example-cluster \
    --class org.apache.spark.examples.SparkPi \
    --jars file:///usr/lib/spark/examples/jars/spark-examples.jar -- 1000
    ```
    * The command specifies:
        * That you want to run a [spark](https://cloud.google.com/sdk/gcloud/reference/dataproc/jobs/submit/spark) job on the `example-cluster` cluster
        * The `class` containing the main method for the job's pi-calculating application
        * The location of the jar file containing your job's code
        * The parameters you want to pass to the job—in this case, the number of tasks, which is `1000`
    * **Note:** Parameters passed to the job must follow a double dash (`--`). See the [gcloud documentation](https://cloud.google.com/sdk/gcloud/reference/dataproc/jobs/submit/spark) for more information.
    * The job's running and final output is displayed in the terminal window:
        ```bash
        Waiting for job output...
        ...
        Pi is roughly 3.14118528
        ...
        Job finished successfully.
        ```

---
## Update a cluster

1. To change the number of workers in the cluster to four, run the following command:
    ```bash
    $ gcloud dataproc clusters update example-cluster --num-workers 4
    ```
    * Your cluster's updated details are displayed in the command's output:
        ```bash
        Waiting on operation [projects/qwiklabs-gcp-7f7aa0829e65200f/regions/global/operations/b86892cc-e71d-4e7b-aa5e-6030c945ea67].
        Waiting for cluster update operation...done.
        ```
2. You can use the same command to decrease the number of worker nodes:
    ```bash
    $ gcloud dataproc clusters update example-cluster --num-workers 2
    ```
    * Now you can create a Dataproc cluster and adjust the number of workers from the `gcloud` command line on the Google Cloud Platform.

---
## Test your Understanding

* T: (T/F) Clusters can be created and scaled quickly with a variety of virtual machine types, disk sizes, and number of nodes.

---
## Congratulations!

### Finish Your Quest

Continue your Quest with [Baseline: Data, ML, AI](https://google.qwiklabs.com/quests/34). A Quest is a series of related labs that form a learning path. Completing this Quest earns you the badge above, to recognize your achievement. You can make your badge (or badges) public and link to them in your online resume or social media account. [Enroll in this Quest](https://google.qwiklabs.com/learning_paths/34/enroll) and get immediate completion credit if you've taken this lab. [See other available Qwiklabs Quests](http://google.qwiklabs.com/catalog).

### Next Steps / Learn More

This lab is part of a series of labs called Qwik Starts. These labs are designed to give you a little taste of the many features available with Google Cloud. Search for "Qwik Starts" in the [lab catalog](https://google.qwiklabs.com/catalog) to find the next lab you'd like to take!

---
## Student Resources

* [Dataproc: Qwik Start - Qwiklabs Preview](https://youtu.be/UOX9G6ArJRc)
* [Run Spark and Hadoop Faster with Cloud Dataproc](https://youtu.be/h1LvACJWjKc)