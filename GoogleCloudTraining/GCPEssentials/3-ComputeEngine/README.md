# Compute Engine: Qwik Start - Windows

## GSP093

![](../../../res/img/selfplacedlabs.png)

Google Compute Engine lets you create and run virtual machines on Google infrastructure. Compute Engine offers scale, performance, and value that allows you to easily launch large compute clusters on Google's infrastructure.

You can run your Windows applications on Google Compute Engine and take advantage of many benefits available to virtual machine instances such as reliable [storage options](https://cloud.google.com/compute/docs/disks/), the speed of the [Google network](https://cloud.google.com/compute/docs/vpc), and [Autoscaling](https://cloud.google.com/compute/docs/autoscaler/).

In this hands-on lab, you will learn how to launch a Windows Server instance in Google Compute Engine, and connect to it using the Remote Desktop Protocol.

If you aren't using Windows on your local machine, install a third-party RDP client such as [Chrome RDP](https://chrome.google.com/webstore/detail/chrome-rdp/cbkkbcmdlboombapidmoeolnmdacpkch) by FusionLabs.

---
## Setup and Requirements

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

---
## Create a virtual machine instance

1. In the GCP Console, go to `Compute Engine > VM instances`, then click `Create`.
    ![](../../../res/img/GCPEssentials/GCPEssentials/GCPEssentials-3-1.png)
2. In the `Boot disk` section, click `Change` to begin configuring your boot disk.
    ![](../../../res/img/GCPEssentials/GCPEssentials/GCPEssentials-3-2.png)
3. Choose `Windows Server 2012 R2 Datacenter`, then `Select`. Leave all other settings at their defaults.
    ![](../../../res/img/GCPEssentials/GCPEssentials/GCPEssentials-3-3.png)
4. Click the `Create` button to create the instance.

### Activate Google Cloud Shell

Google Cloud Shell is a virtual machine that is loaded with development tools. It offers a persistent 5GB home directory and runs on the Google Cloud. Google Cloud Shell provides command-line access to your GCP resources.

1. In GCP console, on the top right toolbar, click the `Open Cloud Shell` button.
    ![](../../../res/img/GCPEssentials/GCPEssentials/GCPEssentials-2-4.png)
2. In the dialog box that opens, click `START CLOUD SHELL`:
    ![](../../../res/img/GCPEssentials/GCPEssentials/GCPEssentials-2-5.png)
    * You can click `START CLOUD SHELL` immediately when the dialog box opens.
3. It takes a few moments to provision and connect to the environment. When you are connected, you are already authenticated, and the project is set to your `PROJECT_ID`. For example:
    ![](../../../res/img/GCPEssentials/GCPEssentials/GCPEssentials-2-6.png)
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
## Test the status of Windows Startup

Allow a short time for the Windows Server instance to start up. Once it has been provisioned, it will be listed on the VM Instances page with a green status icon.

However it may not yet be ready to accept RDP connections, as it takes a while for all the OS components to initialize.

1. To see whether the server is ready for an RDP connection, run the following command at your Cloud Shell terminal command line:
    ```bash
    $ gcloud compute instances get-serial-port-output instance-1 --zone us-central1-a
    ```
2. Repeat the command until you see the following in the command output, which tells you that the OS components have initialized and the Windows Server is ready to accept your RDP connection (attempt in the next step).
    ```bash
    Finished running startup scripts.
    ```

---
## Connect to your instance

1. Click the name of your virtual machine:
    ![](../../../res/img/GCPEssentials/GCPEssentials/GCPEssentials-3-4.png)
2. Under the `Remote Access` section, click the `Set Windows Password` button.
    ![](../../../res/img/GCPEssentials/GCPEssentials/GCPEssentials-3-5.png)
    * A username will be generated.
3. Click `Set to generate a password` for this Windows instance. This may take several minutes to complete.
4. Copy the password and save it so you can log into the instance.
    ![](../../../res/img/GCPEssentials/GCPEssentials/GCPEssentials-3-6.png)

---
## Remote desktop (RDP) into the Windows Server

It's time to RDP into the Windows Server. You can RDP directly from the browser using the Chrome RDP for [Google Cloud Platform extension](https://chrome.google.com/webstore/detail/chrome-rdp-for-google-clo/mpbbnannobiobpnfblimoapbephgifkm).

1. Click on `RDP` to connect.
    ![](../../../res/img/GCPEssentials/GCPEssentials/GCPEssentials-3-7.png)
2. This prompts you to install the RDP Extension. Once installed, GCP opens up a login page where you use your Windows user and password to log in. Paste in the password you saved earlier.
    ![](../../../res/img/GCPEssentials/GCPEssentials/GCPEssentials-3-8.png)
3. Click `Continue` to confirm you want to connect.
    ![](../../../res/img/GCPEssentials/GCPEssentials/GCPEssentials-3-9.png)
    * When Server Manager opens you are connected to `instance-1`, the VM instance on the Windows Server.

---
## Copy and pasting with the RDP client

1. Once you are securely logged in to your stance, you may find yourself copying and pasting commands from the lab manual.
2. To paste, hold the `CTRL + V` keys (if you are a Mac user, using `CMND + V` will not work.) If you are in a Powershell window, be sure that you have clicked in to the window or else the paste shortcut won't work.
3. If you are pasting into putty, **right click**.

---
## Test your Understanding

Below are a multiple choice questions to reinforce your understanding of this lab's concepts. Answer them to the best of your abilities.

* 2: We can create Windows instance in GCP by changing its ____ in VM instance console.
    1. Machine Type
    2. Boot disk to Windows image
    3. API Access
    4. Firewall rules
* 4: Which command is used to check whether the server is ready for an RDP connection?
    1. `gcloud compute instances list`
    2. `gcloud compute ssh`
    3. `gcloud compute instances create`
    4. `gcloud compute instances get-serial-port-output`

---
## Congratulations!

### Finish Your Quest

Continue your Quest with [Baseline: Infrastructure](https://google.qwiklabs.com/quests/33) or [GCP Essentials](https://google.qwiklabs.com/quests/23). A Quest is a series of related labs that form a learning path. Completing this Quest earns you the badge above, to recognize your achievement. You can make your badge (or badges) public and link to them in your online resume or social media account. Enroll in a Quest and get immediate completion credit if you've taken this lab. [See other available Qwiklabs Quests](http://google.qwiklabs.com/catalog).

### Next Steps / Learn More

This lab is also part of a series of labs called Qwik Starts. These labs are designed to give you a little taste of the many features available with Google Cloud. Search for "Qwik Starts" in the [lab catalog](https://google.qwiklabs.com/catalog) to find the next lab you'd like to take!

---
## Student Resources

* [Launch a Windows Server Instance, GCP Essentials](https://youtu.be/EFPaP20APuw)