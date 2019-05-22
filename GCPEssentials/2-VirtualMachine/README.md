# Creating a Virtual Machine

## GSP001

![](../../res/img/selfplacedlabs.png)

Google Compute Engine lets you create virtual machines running different operating systems, including multiple flavors of Linux (Debian, Ubuntu, Suse, Red Hat, CoreOS) and Windows Server, on Google infrastructure. You can run thousands of virtual CPUs on a system that has been designed to be fast and to offer strong consistency of performance.

In this hands-on lab you'll learn how to create virtual machine instances of various machine types using the Google Cloud Platform (GCP) Console and using the gcloud command line. You'll also learn how to connect an NGINX web server to your virtual machine.

Although you can easily copy and paste commands from the lab to the appropriate place, students should type the commands themselves to reinforce their understanding of the core concepts

### What you'll do

* Create a virtual machine with the GCP Console
* Create a virtual machine with gcloud command line
* Deploy a web server and connect it to a virtual machine

### Prerequisites

Familiarity with standard Linux text editors such as `vim`, `emacs`, or `nano` will be helpful.

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
    ![](../../res/img/Setup/Setup-1.png)
2. Copy the username, and then click `Open Google Console`. The lab spins up resources, and then opens another tab that shows the `Choose an account` page.
    * **Tip:** Open the tabs in separate windows, side-by-side.
3. On the Choose an account page, click `Use Another Account`.
    ![](../../res/img/Setup/Setup-2.png)
4. The Sign in page opens. Paste the username that you copied from the Connection Details panel. Then copy and paste the password.
    * **Important:** You must use the credentials from the Connection Details panel. Do not use your Qwiklabs credentials. If you have your own GCP account, do not use it for this lab (avoids incurring charges).
5. Click through the subsequent pages:
    * Accept the terms and conditions.
    * Do not add recovery options or two-factor authentication (because this is a temporary account).
    * Do not sign up for free trials.
6. After a few moments, the GCP console opens in this tab.
    * **Note:** You can view the menu with a list of GCP Products and Services by clicking the Navigation menu at the top-left, next to “Google Cloud Platform”.
        ![](../../res/img/Setup/Setup-3.png)

### Activate Google Cloud Shell

Google Cloud Shell is a virtual machine that is loaded with development tools. It offers a persistent 5GB home directory and runs on the Google Cloud. Google Cloud Shell provides command-line access to your GCP resources.

1. In GCP console, on the top right toolbar, click the `Open Cloud Shell` button.
    ![](../../res/img/Setup/Setup-4.png)
2. In the dialog box that opens, click `START CLOUD SHELL`:
    ![](../../res/img/Setup/Setup-5.png)
    * You can click `START CLOUD SHELL` immediately when the dialog box opens.
3. It takes a few moments to provision and connect to the environment. When you are connected, you are already authenticated, and the project is set to your `PROJECT_ID`. For example:
    ![](../../res/img/Setup/Setup-6.png)
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

### Understanding Regions and Zones

Certain Compute Engine resources live in regions or zones. A region is a specific geographical location where you can run your resources. Each region has one or more zones. For example, the `us-central1` region denotes a region in the Central United States that has zones `us-central1-a`, `us-central1-b`, `us-central1-c`, and `us-central1-f`.

![](../../res/img/GCPEssentials/GCPEssentials-2-1.png)

Resources that live in a zone are referred to as zonal resources. Virtual machine Instances and persistent disks live in a zone. To attach a persistent disk to a virtual machine instance, both resources must be in the same zone. Similarly, if you want to assign a static IP address to an instance, the instance must be in the same region as the static IP.
* Learn more about regions and zones and see a complete list in [Regions & Zones documentation](https://cloud.google.com/compute/docs/regions-zones/).

---
## Create a new instance from the Cloud Console

In this section, you'll learn how to create new pre-defined machine types with Google Compute Engine from the Cloud Console.

1. In the GCP Console, on the top left of the screen, select `Navigation menu > Compute Engine > VM Instances`:
    ![](../../res/img/GCPEssentials/GCPEssentials-2-2.png)
    * This may take a minute to initialize for the first time.
2. To create a new instance, click `Create`.
    ![](../../res/img/GCPEssentials/GCPEssentials-2-3.png)
    * There are many parameters you can configure when creating a new instance. Use the following for this lab:
        | Field | Value | Additional Information |
        |---|---|---|
        | **Name** | `gcelab` | |
        | **Region** | `us-central1` (Iowa) or `asia-south1` (Mumbai) | Learn more about regions in [Regions & Zones documentation](https://cloud.google.com/compute/docs/zones). |
        | **Zone** | `us-central1-c` or `asia-south1-c` * **Note:** remember the zone that you selected, you'll need it later. | Learn more about regions in [Regions & Zones documentation](https://cloud.google.com/compute/docs/zones). |
        | **Machine Type** | `2 vCPUs` This is a (n1-standard-2), 2-CPU, 7.5GB RAM instance. There are a number of machine types, ranging from micro instance types to 32-core/208GB RAM instance types. Learn more in the [Machine Types documentation](https://cloud.google.com/compute/docs/machine-types). | Note: A new project has a default [resource quota](https://cloud.google.com/compute/docs/resource-quotas), which may limit the number of CPU cores. You can request more when you work on projects outside of this lab. |
        | **Boot Disk** | `New 10 GB standard persistent disk` `OS Image: Debian GNU/Linux 9 (stretch)` | There are a number of images to choose from, including: Debian, Ubuntu, CoreOS as well as premium images such as Red Hat Enterprise Linux and Windows Server. See Operating System documentation for more detail. |
        | **Firewall** | Check `Allow HTTP traffic`. Check this option so to access a webserver that you'll install later. | **Note:** This will automatically create firewall rule to allow HTTP traffic on port 80. |
3. Click `Create`.
    * Wait for it to finish - it shouldn't take more than a minute.
    * Once finished, you should see the new virtual machine in the **VM Instances** page.
    * To SSH into the virtual machine, click on `SSH` on the right hand side. This launches a SSH client directly from your browser.
        ![](../../res/img/GCPEssentials/GCPEssentials-2-4.png)
    * **Note:** For more information, see the Connect to an instance using ssh documentation.

### Install a NGINX web server

Now you'll install NGINX web server, one of the most popular web servers in the world, to connect your virtual machine to something.

1. Once SSH'ed, get `root` access using `sudo`:
    ```bash
    $ sudo su -
    ```
2. As the root user, update your OS:
    ```bash
    $ apt-get update
    Get:1 http://security.debian.org stretch/updates InRelease [94.3 kB]
    Ign http://deb.debian.org strech InRelease
    Get:2 http://deb.debian.org strech-updates InRelease [91.0 kB]
    ...
    ```
3. Install NGINX:
    ```bash
    $ apt-get install nginx -y
    Reading package lists... Done
    Building dependency tree
    Reading state information... Done
    The following additional packages will be installed:
    ...
    ```
4. Check that NGINX is running:
    ```bash
    $ ps auwx | grep nginx
    root      2330  0.0  0.0 159532  1628 ?        Ss   14:06   0:00 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
    www-data  2331  0.0  0.0 159864  3204 ?        S    14:06   0:00 nginx: worker process
    www-data  2332  0.0  0.0 159864  3204 ?        S    14:06   0:00 nginx: worker process
    root      2342  0.0  0.0  12780   988 pts/0    S+   14:07   0:00 grep nginx
    ```
5. Awesome! To see the web page, go to the `Cloud Console` and click the `External IP` link of the virtual machine instance. You can also see the web page by adding the `External IP` to `http://EXTERNAL_IP/` in a new browser window or tab.
    ![](../../res/img/GCPEssentials/GCPEssentials-2-5.png)
6. You should see this default web page:
    ![](../../res/img/GCPEssentials/GCPEssentials-2-6.png)

---
## Create a new instance with gcloud

Rather than using the GCP Console to create a virtual machine instance, you can use the command line tool `gcloud`, which is pre-installed in [Google Cloud Shell](https://cloud.google.com/developer-shell/#how_do_i_get_started). Cloud Shell is a Debian-based virtual machine loaded with all the development tools you'll need (`gcloud`, `git`, and others) and offers a persistent 5GB home directory.

> **Note:** If you want to try this on your own machine in the future, read the [gcloud command line tool guide](https://cloud.google.com/sdk/gcloud/).

1. In the Cloud Shell, create a new virtual machine instance from the command line using `gcloud`, replacing `[YOUR_ZONE]` with one of the zone choices given earlier:
    ```bash
    $ gcloud compute instances create gcelab2 --machine-type n1-standard-2 --zone [your_zone]
    Created [...gcelab2].
    NAME     ZONE           MACHINE_TYPE  ...    STATUS
    gcelab2  us-central1-c  n1-standard-2 ...    RUNNING
    ```
    * The instance created has these default values:
        * The latest [Debian 9 (stretch)](https://cloud.google.com/compute/docs/images#debian) image.
        * The `n1-standard-2` machine type. In this lab you can select one of these other machine types if you'd like: `n1-highmem-4` or `n1-highcpu-4`. When you're working on a project outside of Qwiklabs, you can also specify a [custom machine type](https://cloud.google.com/compute/docs/instances/creating-instance-with-custom-machine-type).
        * A root persistent disk with the same name as the instance; the disk is automatically attached to the instance.
2. Run `gcloud compute instances create --help` to see all the defaults.
    * You can set the default region and zones that `gcloud` uses if you are always working within one region/zone and you don't want to append the `--zone` flag every time. Do this by running these commands :
        * `gcloud config set compute/zone ...`
        * `gcloud config set compute/region ...`
3. To exit help, press `CTRL + C`.
4. Check out your instances. Select `Navigation menu > Compute Engine > VM instances`. You should see the 2 instances you created in this lab.
    ![](../../res/img/GCPEssentials/GCPEssentials-2-7.png)
5. Finally, you can SSH into your instance using `gcloud` as well. Make sure you add your zone, or omit the `--zone` flag if you've set the option globally:
    ```bash
    $ gcloud compute ssh gcelab2 --zone [YOUR_ZONE]
    WARNING: The public SSH key file for gcloud does not exist.
    WARNING: The private SSH key file for gcloud does not exist.
    WARNING: You do not have an SSH key for gcloud.
    WARNING: [/usr/bin/ssh-keygen] will be executed to generate a key.
    This tool needs to create the directory
    [/home/gcpstaging306_student/.ssh] before being able to generate SSH
    Keys.
    ```
6. Now you'll type `Y` to continue. Enter through the passphrase section to leave the passphrase empty.
    ```bash
    Do you want to continue? (Y/n) Y
    Generating public/private rsa key pair.
    Enter passphrase (empty for no passphrase)
    ```
7. After connecting, you disconnect from SSH by exiting from the remote shell:
    ```bash
    $ exit
    ```

---
## Test your knowledge

Test your knowledge about GCP by taking our quiz. (Please select multiple correct options if necessary.)

* 1,2: Through which of the following ways you can create a VM instance in Google Compute Engine(GCE)?
    1. Through web console.
    2. The gcloud command line tool.

---
## Congratulations!

Google Compute Engine is the foundation to GCP's Infrastructure-as-a-Service. You created a virtual machine with Compute Engine and can now map your existing server infrastructure, load balancers, and network topology to GCP.

### Finish Your Quest

This self-paced lab is part of the Qwiklab [GCP Essentials](https://google.qwiklabs.com/quests/23) Quest. A Quest is a series of related labs that form a learning path. Completing a Quest earns you a badge to recognize your achievement. You can make your badge (or badges) public and link to them in your online resume or social media account. [Enroll in this Quest](https://google.qwiklab.com/learning_paths/23/enroll) and get immediate completion credit if you've taken this lab. [See other available Qwiklabs Quests](https://google.qwiklabs.com/catalog).

#### Take Your Next Lab

Continue your Quest with [Getting Started with Cloud Shell & gcloud](https://google.qwiklabs.com/catalog_lab/320), or check out these suggestions:

* [Getting Started with Cloud Shell & gcloud](https://google.qwiklabs.com/catalog_lab/320)
* [Provision Services with GCP Marketplace](https://google.qwiklabs.com/catalog_lab/339)

### Next Steps / Learn More

* For an overview of VMs, see [Virtual Machine Instances](https://cloud.google.com/compute/docs/instances/).
* Check out how to [migrate VMs to the GCP](https://cloud.google.com/migrate/).
* Learn more about [subnetworks and network topology](https://cloud.google.com/compute/docs/networking).
* And then be sure to choose the right VM type by reviewing [Choosing a VM Machine](https://cloud.google.com/datalab/docs/how-to/machine-type).

---
## Student Resources

* [Create a Virtual Machine, GCP Essentials](https://youtu.be/ew-r46FmzSM)