# Cloud Natural Language API: Qwik Start

## GSP097

![](../../../res/img/selfplacedlabs.png)

Google Cloud Natural Language API lets you extract information about people, places, events, (and more) mentioned in text documents, news articles, or blog posts. You can use it to understand sentiment about your product on social media, or parse intent from customer conversations happening in a call center or a messaging app. You can even upload text documents for analysis.

### Cloud Natural Language API features

* **Syntax Analysis**: Extract tokens and sentences, identify parts of speech (PoS) and create dependency parse trees for each sentence.
* **Entity Recognition**: Identify entities and label by types such as person, organization, location, events, products and media.
* **Sentiment Analysis**: Understand the overall sentiment expressed in a block of text.
* **Content Classification**: Classify documents in predefined 700+ categories.
* **Multi-Language**: Enables you to easily analyze text in multiple languages including English, Spanish, Japanese, Chinese (Simplified and Traditional), French, German, Italian, Korean and Portuguese.
* **Integrated REST API**: Access via REST API. Text can be uploaded in the request or integrated with [Google Cloud Storage](https://cloud.google.com/storage/).

In this lab you'll use the `analyze-entities` method to ask the Cloud Natural Language API to extract "entities" (e.g. people, places, and events) from a snippet of text.

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
## Create an API Key

1. First, you will set an environment variable with your `PROJECT_ID` which you will use throughout this codelab:
    ```bash
    $ export GOOGLE_CLOUD_PROJECT=$(gcloud config get-value core/project)
    ```
2. Next, create a new service account to access the Natural Language API:
    ```bash
    $ gcloud iam service-accounts create my-natlang-sa \
    --display-name "my natural language service account"
    ```
3. Then, create credentials to log in as your new service account. Create these credentials and save it as a JSON file `~/key.json` by using the following command:
    ```bash
    $ gcloud iam service-accounts keys create ~/key.json \
    --iam-account my-natlang-sa@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com
    ```
4. Finally, set the `GOOGLE_APPLICATION_CREDENTIALS` environment variable. The environment variable should be set to the full path of the credentials JSON file you created, which you can see in the output from the previous command:
    ```bash
    $ export GOOGLE_APPLICATION_CREDENTIALS="/home/USER/key.json"
    ```

---
## Make an Entity Analysis Request

Now you'll try out the Natural Language API's entity analysis with the following sentence:
* `Michelangelo Caravaggio, Italian painter, is known for 'The Calling of Saint Matthew'`

1. Run the following `gcloud` command:
    ```bash
    $ gcloud ml language analyze-entities --content="Michelangelo Caravaggio, Italian painter, is known for 'The Calling of Saint Matthew'."
    ```
    * You should see a response similar to the following:
        ```json
        {
            "entities": [
                {
                    "name": "Michelangelo Caravaggio",
                    "type": "PERSON",
                    "metadata": {
                        "wikipedia_url": "http://en.wikipedia.org/wiki/Caravaggio",
                        "mid": "/m/020bg"
                    },
                    "salience": 0.83047235,
                    "mentions": [
                        {
                        "text": {
                            "content": "Michelangelo Caravaggio",
                            "beginOffset": 0
                        },
                        "type": "PROPER"
                        },
                        {
                        "text": {
                            "content": "painter",
                            "beginOffset": 33
                        },
                        "type": "COMMON"
                        }
                    ]
                },
                {
                    "name": "Italian",
                    "type": "LOCATION",
                    "metadata": {
                        "mid": "/m/03rjj",
                        "wikipedia_url": "http://en.wikipedia.org/wiki/Italy"
                    },
                    "salience": 0.13870546,
                    "mentions": [
                        {
                        "text": {
                            "content": "Italian",
                            "beginOffset": 25
                        },
                        "type": "PROPER"
                        }
                    ]
                },
                {
                    "name": "The Calling of Saint Matthew",
                    "type": "EVENT",
                    "metadata": {
                        "mid": "/m/085_p7",
                        "wikipedia_url": "http://en.wikipedia.org/wiki/The_Calling_of_St_Matthew_(Caravaggio)"
                    },
                    "salience": 0.030822212,
                    "mentions": [
                        {
                        "text": {
                            "content": "The Calling of Saint Matthew",
                            "beginOffset": 69
                        },
                        "type": "PROPER"
                        }
                    ]
                }
            ],
            "language": "en"
        }
        ```
    * Read through your results. For each "entity" in the response, you'll see:
        * The entity `name` and type, a person, location, event, etc.
        * `metadata`, an associated Wikipedia URL if there is one
        * `salience`, and the indices of where this entity appeared in the text. Salience is a number in the `[0,1]` range that refers to the centrality of the entity to the text as a whole.
        * `mentions`, which is the same entity mentioned in different ways.
2. You've sent your first request to the Cloud Natural Language API.

---
## Congratulations!

### Finish Your Quest

Continue your Quest with [Baseline: Data, ML, AI](https://google.qwiklabs.com/quests/34). A Quest is a series of related labs that form a learning path. Completing this Quest earns you the badge above, to recognize your achievement. You can make your badge (or badges) public and link to them in your online resume or social media account. [Enroll in this Quest](https://google.qwiklabs.com/learning_paths/34/enroll) and get immediate completion credit if you've taken this lab. [See other available Qwiklabs Quests](http://google.qwiklabs.com/catalog).

### Next Steps / Learn More

This lab is part of a series of labs called Qwik Starts. These labs are designed to give you a little taste of the many features available with Google Cloud. Search for "Qwik Starts" in the [lab catalog](https://google.qwiklabs.com/catalog) to find the next lab you'd like to take!

---
## Student Resources

* [Gain Valuable Insights from Text with Cloud Natural Language](https://youtu.be/3iOtK0sRNMI)
* [Cloud Natural Language: Qwik Start - Qwiklabs Preview](https://youtu.be/Bl96IyJqKQQ)
