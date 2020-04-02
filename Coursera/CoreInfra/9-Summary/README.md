## Summary and Review

This module reviews the GCP services covered in this course and reminds learners of the differences among them. The module compares GCP compute services, GCP storage services, and important Google VPC networking capabilities.

### Key Concepts

* Compare GCP's compute services.
* Compare GCP's storage services.
* Compare Google VPC's networking capabilities.

---
## Course Review

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* Comparing compute options
    | | Compute Engine | Kubernetes Engine | App Engine Flex | App Engine Standard | Cloud Functions (Beta) |
    |---|---|---|---|---|---|
    | Service Model | IaaS | Hybrid | PaaS | PaaS | Serverless |
    | Use Cases | General computing workloads | Container-based workloads | Web and mobile applications; container-based workloads | Web and mobile applications | Ephemeral functions responding to events |
    | | Toward managed infrastructure | | | Toward dynamic infrastructure |
* Comparing load-balancing options
    | Global HTTP(S) | Global SSL Proxy | Global TCP Proxy | Regional | Regional Internal |
    |---|---|---|---|---|
    | Layer 7 load balancing based on load | Layer 4 load balancing of non-HTTPS SSL traffic based on load | Load balancing of any traffic (TCP, UDP) | Load balancing of traffic inside a VPC |
    | Can route different URLs to different back ends | Supported on specific port numbers | Supported on specific port numbers | Supported on any port number | Use for the internal tiers of multi-tier applications | 
* Compare interconnect options
    * VPN
        * Secure multi-Gbps connection over VPN tunnels
    * Direct Peering
        * Private connection between you and Google for your hybrid cloud workloads
    * Carrier Peering
        * Connection through the largest partner network of service providers
    * Dedicated Interconnect
        * Connect N x 10G transport circuits for private cloud traffic to Google Cloud at Google POPs 
* Comparing storage options: technical details
    | | Cloud Datastore | Bigtable | Cloud Storage | Cloud SQL | Cloud Spanner | BiqQuery |
    |---|---|---|---|---|---|---|
    | Type | NoSQL document | NoSQL wide column | Blobstore | Relational SQL for OLTP | Relational SQL for OLTP | Relational SQL for OLAP | 
    | Transactions | Yes | Single-row | No | Yes | Yes | No |
    | Complex queries | No | No | No | Yes | Yes | Yes |
    | Capacity | Terabytes+ | Petabytes+ | Petabytes+ | Terabytes | Petabytes | Petabytes+ |
    | Unit size | 1 MB/enity | ~10 MB/cell ~100 MB/row | 5TB/object | Determined by DB engine | 10,240 MiB/row | 10 MB/row |
    | Best for | Semi-structured application data, durable key-value data | "Flat" data, Heavy read/write events, analytical data | Structured and unstructured binary or object data | Web frameworks, existing applications | Large-scale database applications (> ~2 TB) | Interactive querying, offline analytics |
    | Use cases | Getting started, App Engine applications | AdTech, Financial and IoT data | Images, large media files, backups | User credentials, customer orders | Whenever high I/O. global consistency is needed | Data warehousing |

---
## Quiz: Summary and Review

1. Which compute service lets customers run virtual machines that run on Google's infrastructure?
    * a. Cloud Functions
    * b. Compute Engine
    * c. App Engine
    * d. Kubernetes Engine
    > Answer: b.
2. Which compute service lets customers deploy their applications in containers that run in clusters on Google's infrastructure?
    * a. App Engine
    * b. Compute Engine
    * c. Cloud Functions
    * d. Kubernetes Engine
    > Answer: d.
3. Which compute service lets customers focus on their applications, leaving most infrastructure and provisioning to Google, while still offering various choices of runtime?
    * a. Kubernetes Engine
    * b. App Engine
    * c. Cloud Functions
    * d. Compute Engine
    > Answer: b.
4. Which compute service lets customers supply chunks of code, which get run on-demand in response to events, on infrastructure wholly managed by Google?
    * a. Cloud Functions
    * b. Compute Engine
    * c. Kubernetes Engine
    * d. App Engine
    > Answer: a.
5. For what kind of traffic would the regional load balancer be the first choice? Choose all that are correct (2 answers).
    * a. TCP traffic on arbitrary port numbers
    * b. UDP traffic
    * c. TCP traffic (non-SSL) on popular well-known port numbers
    * d. TCP/SSL traffic on popular well-known port numbers
    > Answer: a. b.
6. Choose a simple way to let a VPN into your Google VPC continue to work in spite of routing changes,
    * a. Direct Peering
    * b. Cloud Router
    * c. Carrier Peering
    * d. Dedicated Interconnect
    > Answer: b.
7. Which of these storage needs is best addressed by Cloud Datastore?
    * a. Structured objects, with transactions and SQL-like queries
    * b. Structured objects, with lookups based on a single key
    * c. Immutable binary objects
    * d. A relational database with SQL queries and horizontal scalability
    > Answer: a.
8. Which of these storage needs is best addressed by Cloud Spanner?
    * a. Structured objects, with lookups based on a single key
    * b. Structured objects, with transactions and SQL-like queries
    * c. Immutable binary objects
    * d. A relational database with SQL queries and horizontal scalability
    > Answer: d.
9. Which of these storage needs is best addressed by Cloud Bigtable?
    * a. A relational database with SQL queries and horizontal scalability
    * b. Structured objects, with transactions and SQL-like queries
    * c. Structured objects, with lookups based on a single key
    * d. Immutable binary objects
    > Answer: c.
10. Which of these storage needs is best addressed by Cloud Storage?
    * a. A relational database with SQL queries and horizontal scalability
    * b. Immutable binary objects
    * c. Structured objects, with transactions and SQL-like queries
    * d. Structured objects, with lookups based on a single key
    > Answer: b.

---
## Next Steps

> [![](https://img.youtube.com/vi//0.jpg)](https://youtu.be/)

* What's next in the Application Development track?
    * Cloud Infrastructure
        * Google Cloud Platform Fundamentals: Core Infrastructure
        * Architecting with Google Cloud Platform
    * Application Development
        * Google Cloud Platform Fundamentals: Core Infrastructure
        * Developing Applications with Google Cloud Platform
