# Containers in the Cloud

Containers are simple and interoperable, and they enable seamless, fine-grained scaling. Kubernetes is an orchestration layer for containers. Kubernetes Engine is Kubernetes as a service, a scalable managed offering that runs on Google’s infrastructure. You direct the creation of a cluster, and Kubernetes Engine schedules your containers into the cluster and manages them automatically, based on requirements you define. This module explains how Kubernetes Engine works and how it helps deploy applications in containers.

### Key Concepts

* Define the concept of a container and identify uses for containers
* Identify the purpose of and use cases for Google Container Engine and Kubernetes
* Build a Kubernetes cluster using Kubernetes Engine.
* Deploy and manage Docker containers in Kubernetes Engine using the kubectl command.

---
## Containers, Kubernetes, and Kubernetes Engine

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* IaaS
    * Infrastructure as a service offering let you share compute resources with others by virtualizing the hardware.
    * But flexibility comes with a cost. In an environment like this, the smallest unit of compute is a Virtual Machine together with its application.
    * Virtual Machine are highly configurable, and you can install and run your tools of choice.
* The idea of a Container is to give you the independent scalability of workloads like you get in a PaaS environment, and an abstraction layer of the operating system and hardware, like you get in an Infrastructure as a Service environment.

### Practice Quiz: Containers

1. (T/F) Each container has its own instance of an operating system.
    > Answer: False.
    > Explanation: Correct! Containers start much faster than virtual machines and use fewer resources, because each container does not have its own instance of the operating system.
2. Containers are loosely coupled to their environments. What does that mean? Choose all the statements that are true. (3 correct answers)
    * a. Containers package your application into equally sized components.
    * b. Deploying a containerized application consumes less resources and is less error-prone than deploying an application in virtual machines.
    * c. Containers don't require any particular runtime binary.
    * d. Containers are easy to move around.
    * e.Containers abstract away unimportant details of their environments.
    > Answer: b. d. e.

---
## Introduction to Kubernetes and GKE

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Kubernetes Engine
    * Kubernetes is an open-source orchestrator for containers so you can better manage and scale your applications.
    * Kubernetes offers an API that lets people, that is authorized people, not just anybody, control its operation through several utilities.
    * What's a **cluster**? 
        * It's a set of master components that control the system as a whole and a set of nodes that run containers. 
        * In Kubernetes, a node represents a computing instance. 
        * In Google Cloud, nodes are virtual machines running in Compute Engine.
* Kubernetes
    * Whenever Kubernetes deploys a container or a set of related containers, it does so inside an abstraction called a **pod**. 
        * A pod is the smallest deployable unit in Kubernetes. 
        * Think of a pod as if it were a running process on your cluster. 
        * It could be one component of your application or even an entire application.
    * It's common to have only one container per pod. 
        * But if you have multiple containers with a hard dependency, you can package them into a single pod. 
        * They'll automatically share networking and they can have disk storage volumes in common. 
    * Each pod in Kubernetes gets a **unique IP address** and set of ports for your containers.
        * Because containers inside a pod can communicate with each other using the localhost network interface, they don't know or care which nodes they're deployed on. 
        * One way to run a container in a pod in Kubernetes is to use the `kubectl` run command.
        * Running the `kubectl` run command starts a deployment with a container running a pod.
    * What is deployment?
        * A deployment represents a group of replicas of the same pod. 
        * It keeps your pods running even if a node on which some of them run on fails.
    * By default, pods in a deployment or only accessible inside your cluster, but what if you want people on the Internet to be able to access the content in your nginx web server? 
        * To make the pods in your deployment publicly available, you can connect a load balancer to it by running the kubectl expose command.
        * Kubernetes then creates a service with a fixed IP address for your pods. 
        * A service is the fundamental way Kubernetes represents load balancing. 
        * To be specific, you requested Kubernetes to attach an external load balancer with a public IP address to your service so that others outside the cluster can access it.
    * So what exactly is a service? 
        * A service groups a set of pods together and provides a stable endpoint for them. 
        * In our case, a public IP address managed by a network load balancer, although there are other choices.
    * To scale a deployment, run the `kubectl` scale command.
        * Instead of issuing commands, you provide a configuration file that tells Kubernetes what you want your desired state to look like and Kubernetes figures out how to do it. 
        * These configuration files then become your management tools. 
        * To make a change, edit the file and then present the changed version to Kubernetes. 
        * Use the `kubectl get replicasets` command to view your replicas and see their updated state. 
        * Then use the `kubectl get pods` command to watch the pods come online. 
        * Check the deployments to make sure the proper number of replicas are running using `kubectl get deployments`.
        * The `kubectl get services` command confirms that the external IP of the service is unaffected.
    * What happens when you want to update the version of your application?
        * You will definitely want to update your container and get the new code out in front of your users as soon as possible, but it could be risky to roll out all those changes at once.
        * When you choose a **rolling update** for a deployment and then give it a new version of the software that it manages, Kubernetes will create pods of the new version one-by-one, waiting for each new version pod to become available before destroying one of the old version pods. 
        * Rolling updates are a quick way to push out a new version of your application while still sparing your users from experiencing downtime.

### Introduction to Hybrid and Multi-Cloud Computing (Anthos)

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Distributed systems housed on-premises is the traditional approach but it lacks flexibility and agility
    * Distributed systems housed on-premises are difficult to upgrade
        * Increasing capacity means buying more servers
        * Lead time for new capacity could be set up to a year or more
    * Distributed systems housed on-premises are costly to upgrade
        * Upgrades are expensive
        * The practical life of a server is short
* Modern distributed systems allow a more agile approach to managing your compute resources
    * Move only some of your compute workloads to the Cloud
    * Move at your own pace
    * Take advantage of Cloud's scalability and lower costs
    * Add specialized services to your compute resources stack
* Anthos is Google's modern solution for hybrid and multi-cloud systems and  services management
    * Kubernetes and GKE On-Prem create the foundation
    * On-premises and Cloud environments stay in sync.
    * A rich set of tools is provided for
        * Managing services on-premises and in the Cloud
        * Monitoring systems and services
        * Migrating applications from VMs into your clusters
        * Maintaining consistent polices across all clusters, whether on-premises or in the Cloud
* You can learn more about Anthos from these links
    * Anthos General Overview: https://cloud.google.com/anthos/
    * Anthos Technical Documentation: https://cloud.google.com/anthos/docs/

### Practice Quiz: Kubernetes

1. What is a Kubernetes pod?
    * a. A group of containers
    * b. A group of nodes
    * c. A group of clusters
    > Answer: a.

2. What is a Kubernetes cluster?
    * a. A group of machines where Kubernetes can schedule workloads
    * b. A group of containers that provide high availability for applications
    > Answer: a.

### Practice Quize: Kubernetes Engine

1. Where do the resources used to build Kubernetes Engine clusters come from?
    * a. Bare-metal servers
    * b. Compute Engine
    * c. App Engine
    > Answer: b.
2. (T/F) Google keeps Kubernetes Engine refreshed with successive versions of Kubernetes.
    > Answer: True.

---
## Lab 4: Getting Started with Kubernetes Engine

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)
> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Please follow the details in [here](./Lab-4.md)

---
## Quiz: Containers, Kubernetes, and Kubernetes Engine

1. Identify two reasons for deploying applications using containers. (Choose 2 responses.)
    * a. Tight coupling between applications and operating systems
    * b. Consistency across development, testing, production environments
    * c. Simpler to migrate workloads
    * d. No need to allocate resources in which to run containers
    > Answer: b. c.
2. (T/F) Kubernetes allows you to manage container clusters in multiple cloud providers.
    > Answer: True.
3. (T/F) Google Cloud Platform provides a secure, high-speed container image storage service for use with Kubernetes Engine.
    > Answer: True.
4. In Kubernetes, what does "pod" refer to?
    * a. A group of clusters that work together
    * b. A popular management subsystem
    * c. A popular logging subsystem
    * d. A group of containers that work together
    > Answer: d.
5. Does Google Cloud Platform offer its own tool for building containers (other than the ordinary docker command)?
    * a. Yes; the GCP-provided tool is an option, but customers may choose not use it.
    * b. No; all customers use the ordinary docker command.
    Yes. Kubernetes Engine customers must use the GCP-provided tool.
    > Answer: a.
6. Where do your Kubernetes Engine workloads run?
    * a. In clusters built from Compute Engine virtual machines
    * b. In clusters that are built into GCP, not separately manageable
    * c. In clusters implemented using App Engine
    * d. In clusters implemented using Cloud Functions
    > Answer: a.
