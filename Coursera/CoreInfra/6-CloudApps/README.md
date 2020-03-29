# Applications in the Cloud

App Engine is a Platform-as-a-Service ("PaaS") offering. The App Engine platform manages the hardware and networking infrastructure required to run your code. App Engine provides built-in services that many web applications need. This module describes how App Engine works.

### Key Concepts

* Explain the purpose of and use cases for Google App Engine and Google Cloud Datastore
* Compare the App Engine Standard environment with the App Engine Flexible environment
* Express the purpose of and use cases for Google Cloud Endpoints
* Express the purpose of and use cases for Apigee Edge.
* Preview an App Engine application using Cloud Shell.
* Launch an App Engine application and then disable it.

---
## Module Introduction

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Recall that a PaaS is a platform as a service. 
    * The App Engine platform manages the hardware and networking infrastructure required to run your code. 
    * To deploy an application on App Engine, you just hand App Engine your code and the App Engine service takes care of the rest.
* App Engine is a PaaS for building scalable applications
    * App Engine makes deployment maintenance, and scalability easy so you focus on innovation
    * App Engine provides you with a built-in services that many web applications need. 
    * Especially suited for building scalable web applications and mobile backends
* App engine will scale your application automatically in response to the amount of traffic it receives.

### Practice Quiz: App Engine

1. (T/F) App Engine is a better choice for a web application than for long-running batch processing.
    > Answer: True.
    > Explanation: That's correct! App Engine will scale your application automatically in response to the amount of traffic it receives. That’s why App Engine is especially suited for applications where the workload is highly variable, like a web application.
2. App Engine just runs applications; it doesn't offer any services to the applications it runs.
    > Answer: False.
    > Explanation: That's correct! App Engine offers NoSQL databases, in-memory caching, load balancing, health checks, logging, and user authentication to applications running in it.

---
## App Engine Standard Environment

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* App Engine standard environment
    * Easily deploy your applications
    * Autoscale workloads
    * Free daily quota
    * Usage based pricing
        * What's distinctive about the Standard Environment though, is that low utilization applications might be able to run at no charge. 
    * SDKs for development, testing and deployment
* App Engine standard environment: Requirements
    * Specific versions of Java, Python, PHP and Go are supported
    * The Standard Environment also enforces restrictions on your code by making it run in a so-called "Sandbox." 
        * No writing to local files
        * All requests time out at 60s
        * Limits on third-party software
* Example App Engine standard workflow: Web applications
    1. Develop & test the web application locally
    2. Use the SDK to deploy to App Engine
    3. App Engine automatically scales & reliably serves your web application
    4. App Engine can access a variety of services using dedicated APIs

---
## App Engine Flexible Environment

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* App Engine flexible environment
    * Build and deploy containerized apps with a click
    * No sandbox constraints
    * Can access App Engine resources
* Comparing the App Engine environments
    | | Standard Environment | Flexible Environment |
    |---|---|---|
    | Instance startup | Milliseconds | Minutes |
    | SSh access | No | Yes (although not by default) |
    | Write to local disk | No | Yes (but writes are ephemeral) |
    | Support for 3rd-party binaries | No | Yes |
    | Network access | Via App Engine services | Yes |
    | Pricing model | After free daily use, par per instance class, with automatic shutdown | Pay for resource allocation per hour, no automatic shutdown |
* Deploy Apps: Kubernetes Engine vs. App Engine
    | | Kubernetes Engine | App Engine Flexible | App Engine Standard |
    |---|---|---|---|
    | Language support | Any | Any | Java, Python, Go, PHP |
    | Service model | Hybrid | PaaS | PaaS |
    | Primary use case | Container-based workloads | Web and mobile applications, container-based workloads | Web and mobile applications |
    | | To managed infrastructure | | Toward dynamic infrastructure |

### Practice Quiz: App Engine Flexible and Standard Environment

1. Which of these criteria would make you choose App Engine Flexible Environment, rather than Standard Environment, for your application? Choose all that are correct (2 correct responses).
    * a. Finer-grained scaling
    * b. Daily free usage quota
    * c. Ability to ssh in
    * d. Wider range of choices for application language
    > Answer: c. d.
    > Explanation: At the time of this writing, App Engine Standard Environment supports Java, Python, PHP, and Go, but in the Flexible Environment, you upload your own runtime to run code in a language of your choice. App Engine Flexible Environment lets you ssh into the virtual machines in which your application runs.
2. (T/F) App Engine Flexible Environment applications let their owners control the geographic region where they run.
    > Answer: True.
    > Explanation: That's correct! You get to choose which region your applications run in.

---
## Cloud Endpoints and Apigee Edge

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Application Programing Interfaces hide detail, enforce contracts
* Cloud Endpoints helps you create and maintain APIs
    * Distributed API management through an API console
    * Expose your API using a RESTful interface
    * Control access and validate calls with JSON Web Tokens and Google API keys
        * Identify web, mobile users with AuthO and Firebase Authentication
    * Generate client libraries
* Cloud Endpoints: Supported platform
    | Runtime environment | Clients |
    |---|---|
    | App Engine Flexible Environement | Android |
    | Kubernetes Engine | iOS |
    | Compute Engine | JavaScript |
* Apigee Edge helps you secure and monetize APIs
    * A platform for making APIs available to your customers and partners
    * Containes analytics, monetization, and a developer portal

---
## Lab 5: Getting Started with App Engine

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Please follow the details in [here](./Lab-5.md)

---
## Quiz: Applicatios in the Cloud

1. Which statements are true about App Engine? Choose all that are true (2 correct answers).
    * a. App Engine manages the hardware and networking infrastructure required to run your code.
    * b. App Engine requires you to supply or code your own application load balancing and logging services.
    * c. App Engine charges you based on the resources you pre-allocate rather than based on the resources you use.
    * d. It is possible for an App Engine application's daily billing to drop to zero.
    * e. Developers who write for App Engine do not need to code their applications in any particular way to use the service.
    > Answer: a. d.
2. Name 3 advantages of using the App Engine Flexible Environment over App Engine Standard. Choose all that are true (3 correct answers).
    * a. Your application can write to local disk
    * b. Your application can execute code in background threads
    * c. You can install third-party binaries
    * d. You can SSH in to your application
    * e. Google provides automatic in-place security patches
    > Answer: a. c. d.
3. Name 3 advantages of using the App Engine Standard Environment over App Engine Flexible. Choose all that are true (3 correct answers).
    * a. You can choose any programming language
    * b. Billing can drop to zero if your application is idle
    * c. Google provides and maintains runtime binaries
    * d. You can install third-party binaries
    * e. Scaling is finer-grained
    > Answer: b. c. e.
4. You want to do business analytics and billing on a customer-facing API. Which GCP service should you choose?
    * a. Apigee Edge
    * b. Cloud Endpoints
    > Answer: a.
5. You want to support developers who are building services in GCP through API logging and monitoring. Which GCP service should you choose?
    * a. Cloud Endpoints
    * b. Apigee Edge
    > Answer: a.
6. You want to gradually decompose a pre-existing monolithic application, not implemented in GCP, into microservices. Which GCP service should you choose?
    * a. Apigee Edge
    * b. Cloud Endpoints
    > Answer: a.
