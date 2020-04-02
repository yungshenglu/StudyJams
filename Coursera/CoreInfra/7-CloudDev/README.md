# Developing, Deploying and Monitoring in the Cloud

Popular tools for development, deployment, and monitoring just work in GCP. Customers also have options for tools in each of these three areas that are tightly integrated with GCP. This module covers those tools.

### Key Concepts

* Understand options for software developers to host their source code.
* Understand the purpose of template-based creation and management of resources.
* Understand the purpose of integrated monitoring, alerting, and debugging.
* Build a Deployment Manager deployment.
* Update a Deployment Manager deployment.
* View the load on a VM instance using Stackdriver.

---
## Development in the Cloud

> [![](https://img.youtube.com/vi/qqVRbVJNZQs/0.jpg)](https://youtu.be/qqVRbVJNZQs)

* Cloud Source Repositories
    * Fully featured Git repositories hosted on Google Cloud Platform
* Cloud Functions (Beta)
    * Create single-purpose functions that respond to events without a server or runtime
    * Written in JavaScript; execute in managed Node.js environment on Google Cloud Platform

### Practice Quiz: Development in the Cloud

1. Why would a developer choose to store source code in Cloud Source Repositories? Choose all the answers that are correct (2 correct answers).
    * a. To reduce work
    * b. To have total control over the hosting infrastructure
    * c. To keep code private to a GCP project
    > Answer: a. c.
    > Explanation: That's right! Cloud Source Repositories manages the hosting infrastructure for you. Cloud Source Repositories integrates with Google Cloud IAM.

---
## Deployment: Infrastructure as Code

> [![](https://img.youtube.com/vi/euX84ofqevI/0.jpg)](https://youtu.be/euX84ofqevI)

* Deployment Management
    * Provides repeatable deployment
    * Create a `.yaml` template describing your environment and use Deployment Manager to create resources

### Practice Quiz: Cloud Functions

1. What is the advantage of putting event-driven components of your application into Cloud Functions?
    * a. Cloud Functions handles scaling these components seamlessly.
    * b. Cloud Functions means that processing always happens free of charge.
    > Answer: a.
    > Explanation: Correct! Your code executes whenever an event triggers it, no matter whether it happens rarely or many times per second. That means you don't have to provision compute resources to handle these operations.

---
## Monitoring: Proactive Instrumentation

> [![](https://img.youtube.com/vi/MdTx1qfefzY/0.jpg)](https://youtu.be/MdTx1qfefzY)

* Stackdriver is GCP's tool for monitoring, logging and diagnostics.
    * Monitoring
    * Logging
    * Debug
    * Error Reporting
    * Trace
* Stackdriver pffers capabilities in six areas
    * Monitoring
        * Platform, system, and application metrics
        * Uptime/health checks
        * Dashboards and alerts
    * Logging
        * Platform, system, and application logs
        * Log search, view, filter, and export
        * Log-based metrics
    * Trace
        * Latency reporting and sampling
        * Per-URL latency and statistics
    * Error Reporting
        * Error notifications
        * Error dashboard
    * Debugger
        * Debug applications
    * Profiler (Beta)
        * Continuous profiling of CPU and memory consumption

---
## Lab 6: Getting Started with Deployment Manager and Stackdriver

> [![](https://img.youtube.com/vi/DmijmmRKCqg/0.jpg)](https://youtu.be/DmijmmRKCqg)

* Please follow the details in [here](./Lab-6.md)

---
## Quiz: Developing, Deploying, and Monitoring in the Cloud

1. Why might a GCP customer choose to use Cloud Source Repositories?
    * a. They don't want to host their own git instance, and they want to integrate with IAM permissions.
    * b. They want to host and manage their own git instance, and they want to integrate with IAM permissions.
    * c. They don't want to host their own git instance, and they don't want to integrate with IAM permissions.
    * d. They want to host and manage their own git instance, and they don't want to integrate with IAM permissions.
    > Answer: d.
2. Why might a GCP customer choose to use Cloud Functions?
    * a. Cloud Functions is the primary way to run Node.js applications in GCP.
    * b. Their application contains event-driven code that they don't want to have to provision compute resources for.
    * c. Cloud Functions is a free service for hosting compute operations.
    * d. Their application has a legacy monolithic structure that they want to break apart into microservices with little developer effort.
    > Answer: b.
3. Why might a GCP customer choose to use Deployment Manager?
    * a. Deployment Manager is an infrastructure management system for Kubernetes pods.
    * b. Deployment Manager enforces maximum resource utilization and spending limits on your GCP resources.
    * c. Deployment Manager is an infrastructure management system for GCP resources.
    * d. Deployment Manager is a version control system for your GCP infrastructure layout.
    > Answer: c.
4. You want to define alerts on your GCP resources, such as when health checks fail. Which is the best GCP product to use?
    * a. Deployment Manager
    * b. Stackdriver Monitoring
    * c. Stackdriver Trace
    * d. Cloud Functions
    * e. Stackdriver Debugger
    > Answer: b.
5. Which statements are true about Stackdriver Logging? Choose all that are true (2 statements)
    * a. Stackdriver Logging lets you view logs from your applications, and filter and search on them.
    * b. Stackdriver Logging requires the use of a third-party monitoring agent.
    * c. Stackdriver Logging requires that you store your logs in BigQuery or Cloud Storage.
    * d. Stackdriver Logging lets you define uptime checks.
    * e. Stackdriver Logging lets you define metrics based on your logs.
    > Answer: a. e.
