## Getting Started with Google Cloud Platform

GCP customers use projects to organize the resources they use. They use Google Cloud Identity and Access Management, also called “IAM,” to control who can do what with those resources. They use any of several technologies to connect with GCP. This module covers each of these topics, and it introduces a service called Cloud Launcher that is an easy way to get started with GCP.

### Key Concepts

* Identify the purpose of projects, folders, and organization nodes on Google Cloud Platform
* Describe the purpose of and use cases for Identity and Access Management
* List the methods of interacting with Google Cloud Platform
* Build a solution deployment using Cloud Launcher.

---
## Module Introduction

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Projects are the main may you organize the resources you use in GCP
* The principle of least privilege is very important in managing any kind of compute infrastructure, whether it's in the Cloud or on-premises.
* Cloud security requires collaboration
    * Google is responsible for managing its infrastructure security
    * You are responsible for securing your data
    * Google helps you with best practices, template, products, and solutions
* When you move an application to Google Cloud Platform, Google handles many of the lower layers of security. 
    * Because of its scale, Google can deliver a higher level of security at these layers than most of its customers could afford to do on their own. 

---
## The Google Cloud Platform Resource Hierarchy

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Resource hierarchy levels define trust boundaries
    * Group your resources according to your organization structure
    * Levels of the hierarchy provide trust boundaries and resource isolation
    * Policies are inherited downwards in the hierarchy
* All GCP services you use are associated with a project
    * Track resource and quota usage
    * Enable billing
    * Manage permissions and credentials
    * Enable services and APIs
* Projects have three identifying attributes
    | Project ID | Project Name | Project Number |
    |---|---|---|
    | Globally unique | Need not be unique | Globally unique |
    | Chosen by you | Chosen by you | Assigned by GCP |
    | Immutable | Mutable | Immutable |
    * In general, project IDs are made to be human readable strings and you'll use them frequently to refer to projects.
* Folders offer flexible management
    * Folders group projects underan organization
    * Folders can contain projects, other folders, or both
    * Use folders to assign policies
    * To use folders, you need an organization node at the top of the hierarchy
* The organization node organizes projects
    * The organization node is the root node of Google CLoud resources
    * Notable organization roles:
        * Organization Policy Administator: Broad control over all cloud resources
        * Project Creator: Fine-grained control of project creation
* An example IAM resource hierarchy
    * A policy is set on a resource
        * Each policy contains a set of roles and role memberd
    * Resources inherit policies from parent
        * Resource policies are a union of parent and resource
    * A less restrictive parent policy overrides a more restrictive resource policy 
    * The policies implemented at a higher level in this hierarchy can't take away access that's granted at a lower level


### Practice Quiz: The Google Cloud Platform Resource Hierarchy

1. Choose the correct completion: Services and APIs are enabled on a per-__________ basis.
    * a. Organization
    * b. Folder
    * c. Project
    * d. Billing account
    > Answer: c.
2. (T/F): Google manages every aspect of Google Cloud Platform customers' security.
    > Answer: False.
3. Your company has two GCP projects, and you want them to share policies. What is the less error-prone way to set this up?
    * a. Duplicate all the policies on one project onto the other.
    * b. Place both projects into a folder, and define the policies on the folder.
    > Answer: b.

---
## Identity and Access Management (IAM)

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* IAM lets administrators authorize who can take action on specific resources
* Google Cloud Identity and Access Management defines...
    * An IAM policy has a "who" part, a "can do what" part, and an "on which resource" part
    * The "who" part of an IAM policy can be defined either by a Google Account, a Google group, a Service account, an entire G Suite, or a Cloud Identity domain
    * The "can do what" part is defined by an IAM role
        * An IAM role is a collection of permissions. 
* IAM policies can apply to any of four types of principals
    * Google account or Gloud Identity user
    * Service account
    * Google group
    * Cloud Identity or G Suite domain
* There are three types of IAM roles
    * Primitive
        * IAM primitive roles apply across all GCP services in a project
            * Primitive roles are broad
            * You apply them to a GCP project and they affect all resources in that project
        * IAM primitive roles offer fixed, coarse-grained levels of access
    * Prefedined
        * IAM predefined roles apply to a particular GCP service in a project
    * Custom

### IAM Roles

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* IAM predefined roles offer more fine-grained permissions on particular services
    * You have to decide to use custom roles. You'll need to manage their permissions. Some companies decide they'd rather stick with the predefined roles. 
    * Custom roles can only be used at the project or organization levels. They can't be used at the folder level.
* Service Accounts control server-to-server interactions
    * Provide an identity for carrying out **server-to-server** interactions in a project
    * Used to **authenticate** from one service to another
    * Used to **control privileges** used by resources
        * So that applications can perform actions on behalf of authenticated end users
    * Identified with an **email** address
        * `PROJECT_NUMBER-compute@developer.gserviceaccount.com`
        * `PROJECT_ID@appspot.gserviceaccount.com`
* Service Accounts and IAM
    * Service accounts authenticate using keys
        * Google manages keys for Compute Engine and App Engine
    * You can assign a predefined or custom IAM role to the service account
    * Example:
        * VMs running `component_1` are granted **Editor** access to `project_b` using Service Account 1.
        * Vms runngin `component_2` are granted **ObjectViewer** access to `bucket_1` using Service Account 2.
        * Service account permissions can be changed without recreating VMs

### Practice Quiz: Resources and IAM

1. When would you choose to have an organization node? (Choose all that are correct. Choose 2 responses.)
    * a. When you want to create folders.
    * b. When you want to organize resources into projects.
    * c. When you want to apply organization-wide policies centrally.
    * d. There is no choice; organization nodes are mandatory.
    > Answer: a. c.
2. Order these IAM role types from broadest to finest-grained.
    * a. Primitive roles, predefined roles, custom roles
    * b. Custom roles, predefined roles, primitive roles
    * c. Predefined roles, custom roles, primitive roles
    > Answer: a.
3. Can IAM policies that are implemented higher in the resource hierarchy take away access that is granted by lower-level policies?
    * a. Yes.
    * b. No.
    > Answer: b.

---
## Interacting with Google Cloud Platform

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* There are four ways to interact with GCP
    * Cloud Platform Console
        * Web user interface
    * Cloud Shell and Cloud SDK
        * Command-line interface
    * Cloud Console Mobile App
        * For iOS and Android
    * REST-based API
        * For custom applications
* Google Cloud Platform Console
    * Access to Google Cloud Platform APIs
    * Offer access to Cloud Shell
        * A temporary virtual machine with Google Cloud SDK preinstalled
* Google Cloud SDK
    * Includes command-line tools for Cloud Platform products and servies
        * `gcloud`, `gsutil` (Cloud Storage), `bq` (BigQuery)
    * Available via Cloud Shell 
    * Available as Docker image
* RESTful API
    * Programmatic access to products and services
        * Typically use JSON as an interchange format
        * Use OAuth 2.0 for authentication and authorization
    * Enabled through the Google Cloud Platform
    * Most APIs include daily quotas and rates (limits) that can be raised by request
        * Important to plan ahead tp manage your required capacity
    * Experiment with APIs Explorer
* Use APIs Explorer to help you write down your code
    * The APIs Explorer is an interactive tool that lets you easily try Google APIs using a browser
    * With the APIs Explorer, you can:
        * Browse quickly through available APIs and versions
        * See methods available for each API and what parameters they support along with inline document
        * Execute requests for any method and see responses in real time
        * Easily make authenticated and authorized API calls
* Use client libraries to control GCP resources from within your code
    * Cloud Client Libraries
        * Community-owned, hand-crafted client libraries
    * Google API client Libraries
        * Open source, generated
        * Support various language
            * Java, Python, JavaScript, PHP, .NET, Go, Node.js, Ruby, Objective-C, Dart
* Google Console Mobile App
    * Manage virtual machines and database instances
    * Manage apps in Google App Engine
    * Manage your billing
    * Visualize your projects with a customizable dashboard

---
## Cloud Marketplace (formerly Cloud Launcher)

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Cloud Lanchergives quick access to solutions
    * A solution marketplace containing pre-packaged, ready-to-deploy solution
        * Some offered by Google
        * Others by third-party vendors
* GCP updates the base images for these software packages to fix critical issues and vulnerabilities
    * But it doesn't update the software after it's been deployed. 
    * Fortunately, you'll have access to the deployed systems, so you can maintain them.

---
## Lab 1: Getting Started with Google Launcher

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)
> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Please follow the details in [here](./Lab-1.md)

---
## Quiz: Getting Started with Google Cloud Platform

1. (T/F) In Google Cloud IAM: if a policy applied at the project level gives you Owner permissions, your access to an individual resource in that project might be restricted to View permission if someone applies a more restrictive policy directly to that resource.
    > Answer: False.
2. (T/F) All Google Cloud Platform resources are associated with a project.
    > Answer: True.
3. Service accounts are used to provide which of the following? (Choose all that are correct. Choose 3 responses.)
    * a. Authentication between Google Cloud Platform services
    * b. A way to restrict the actions a resource (such as a VM) can perform
    * c. A way to allow users to act with service account permissions
    * d. A set of predefined permissions
    > Answer: a. b. c.
4. How do GCP customers and Google Cloud Platform divide responsibility for security?
    * a. Google takes care of the lower parts of the stack, and customers are responsible for the higher parts.
    * b. All aspects of security are the customer's responsibility.
    * c. Google takes care of the higher parts of the stack, and customers are responsible for the lower parts.
    * d. All aspects of security are Google's responsibility. x
    > Answer: a.
5. Which of these values is globally unique, permanent, and unchangeable, but chosen by the customer?
    * a. The project number
    * b. The project's billing credit-card number
    * c. The project ID
    * d. The project name
    > Answer: c.
6. Consider a single hierarchy of GCP resources. Which of these situations is possible? (Choose all that are correct. Choose 3 responses.)
    * a. There is no organization node, but there is at least one folder.
    * b. There is an organization node, and there are no folders.
    * c. There are two or more organization nodes
    * d. There is no organization node, and there are no folders.
    * e. There is an organization node, and there is at least one folder.
    > Answer: b. d. e.
7. What is the difference between IAM primitive roles and IAM predefined roles?
    * a. Primitive roles affect all resources in a GCP project. Predefined roles apply to a particular service in a project.
    * b. Primitive roles are changeable once assigned. Predefined roles can never be changed.
    * c. Primitive roles only apply to the owner of the GCP project. Predefined roles can be associated with any user.
    * d. Primitive roles can only be granted to single users. Predefined roles can be associated with a group.
    * e. Primitive roles only allow viewing, creating, and deleting resources. Predefined roles allow any modification.
    > Answer: a.
8. Which statement is true about billing for solutions deployed using Cloud Marketplace (formerly known as Cloud Launcher)?
   * a. You pay only for the underlying GCP resources you use, with the possible addition of extra fees for commercially licensed software.
   * b. You pay only for the underlying GCP resources you use; Google pays the license fees for commercially licensed software.
   * c. Cloud Marketplace solutions are always free.
   * d. After a trial period, each Cloud Marketplace solution assesses a fixed recurring monthly fee.
   > Answer: a.