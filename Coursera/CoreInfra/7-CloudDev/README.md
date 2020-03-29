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

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

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

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

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

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

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

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Please follow the details in [here](./Lab-6.md)

---
## Quiz: Developing, Deploying, and Monitoring in the Cloud

1. 
