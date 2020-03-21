# Lab 1: Getting Started with Cloud Marketplace (formerly Cloud Launcher)

In this lab you will load server log data into BigQuery and perform SQL queries on it.

## Overview

In this lab, you use Cloud Marketplace to quickly and easily deploy a LAMP stack on a Compute Engine instance. The Bitnami LAMP Stack provides a complete web development environment for Linux that can be launched in one click.

| Component	| Role |
|---|---|
| Linux	| Operating system |
| Apache HTTP Server | Web server |
| MySQL	| Relational database |
| PHP	| Web application framework |
| phpMyAdmin | PHP administration tool |

For more information on the Bitnami LAMP stack, see https://docs.bitnami.com/google/infrastructure/lamp/

---
## Objectives

In this lab, you learn how to perform the following task:

* Launch a solution using Cloud Marketplace.

---
## Task 1: Sign in to the Google Cloud Platform (GCP) Console

### Before you click the Start Lab button

Read these instructions. Labs are timed and you cannot pause them. The timer, which starts when you click Start Lab, shows how long Cloud resources will be made available to you.

This Qwiklabs hands-on lab lets you do the lab activities yourself in a real cloud environment, not in a simulation or demo environment. It does so by giving you new, temporary credentials that you use to sign in and access the Google Cloud Platform for the duration of the lab.

### What you need

To complete this lab, you need:

* Access to a standard internet browser (Chrome browser recommended).
* Time to complete the lab.

> **Note:** If you already have your own personal GCP account or project, do not use it for this lab.

---
## Task 2: Use Cloud Marketplace to Deploy a LAMP Stack

1. In the GCP Console, on the **Navigation menu**, click `Marketplace`.
2. In the search bar, type LAMP
3. In the search results, click `LAMP Certified by Bitnami`.
    * If you choose another LAMP stack, such as the Google Click to Deploy offering, the lab instructions will not work as expected.
4. On the LAMP page, click `Launch`.
    * If this is your first time using Compute Engine, the Compute Engine API must be initialized before you can continue.
5. For `Zone`, select the deployment zone that Qwiklabs assigned to you.
6. Leave the remaining settings as their defaults.
7. If you are prompted to accept the GCP Marketplace Terms of Service, do so.
8. Click `Deploy`.
9. If a **Welcome to Deployment Manager** message appears, click `Close` to dismiss it.
    * The status of the deployment appears in the console window: `lampstack-1 is being deployed`. When the deployment of the infrastructure is complete, the status changes to `lampstack-1 has been deployed`.
    * After the software is installed, a summary of the details for the instance, including the site address, is displayed.

---
## Task 3: Verify your Deployment

1. When the deployment is complete, click the `Site address` link in the right pane.
    * Alternatively, you can click `Visit the site` in the `Get started with LAMP Certified by Bitnami` section of the page. A new browser tab displays a congratulations message. This page confirms that, as part of the LAMP stack, the Apache HTTP Server is running.
2. Close the congratulations browser tab.
3. On the GCP Console, under `Get started with LAMP Certified by Bitnami`, click `SSH`.
    * In a new window, a secure login shell session on your virtual machine appears.
4. In the just-created SSH window, to change the current working directory to `/opt/bitnami`, execute the following command:
    ```bash
    $ cd /opt/bitnami
    ```
5. To copy the `phpinfo.php` script from the installation directory to a publicly accessible location under the web server document root, execute the following command:
    ```bash
    $ sudo cp docs/phpinfo.php apache2/htdocs
    ```
    * The phpinfo.php script displays your PHP configuration. It is often used to verify a new PHP installation.
6. To close the SSH window, execute the following command:
    ```bash
    $ exit
    ```
7. Open a new browser tab.
8. Type the following URL, and replace `SITE_ADDRESS` with the URL in the `Site address` field in the right pane of the `lampstack` page.
    ```
    http://SITE_ADDRESS/phpinfo.php
    ```
9. Close the `phpinfo` tab.

---
## Congratulations!

In this lab, you deployed a LAMP stack to a Compute Engine instance.

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
## More resources

Read the [Google Cloud Platform documentation on Cloud Marketplace](https://cloud.google.com/marketplace/docs/).
