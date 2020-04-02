# Storage in the Cloud

Every application needs to store data. Different applications and workloads require different storage and database solutions. This module describes and differentiates among GCP's core storage options: Cloud Storage, Cloud SQL, Cloud Spanner, Cloud Datastore, and Google Bigtable.

### Key Concepts

* Summarize the purpose of and use cases for: Cloud Storage, Cloud SQL, Cloud Spanner, and Cloud Bigtable
* Choose between the various storage options on Google Cloud Platform
* Build a BigQuery table using data from Cloud Storage.
* Use SQL queries to analyze data stored in BigQuery.

---
## Module Introduction

> [![](https://img.youtube.com/vi/6XWGhu1mPac/0.jpg)](https://youtu.be/6XWGhu1mPac)

* Core storage options
    * Cloud Storage
    * Cloud SQL
    * Cloud Spanner
    * Cloud Data Store
    * Google Big Table

---
## Cloud Storage

> [![](https://img.youtube.com/vi/IAU5A0_mhFE/0.jpg)](https://youtu.be/IAU5A0_mhFE)

* Cloud Storage
    * You save to your storage here, you keep this arbitrary bunch of bytes I give you and the storage lets you address it with a unique key. 
* Cloud Storage is binary large-object storage
    * High performance, internet-scale
    * Simple administration
        * Does not require capacity management
    * Data encryption at rest
    * Date encryption in transit by default from Google to endpoint
    * Online and offline import services are available
* You can use Cloud Storage for lots of things
    * Serving website content
    * Storing data for archival and disaster recovery
    * Distributing large data objects to your end users via Direct Download
* The storage objects are **immutable**, which means that you do not edit them in place but instead you create new versions.
    * You can turn on object versioning on your buckets if you want. 
    * If you do, Cloud Storage keeps a history of modifications.
    * You can list the archived versions of an object, restore an object to an older state or permanently delete a version as needed. 
    * If you don't turn on object versioning, new always overrides old.
* Your Cloud Storage files are organized into buckets
    | Bucket attributes | Bucket contents |
    |---|---|
    | Globally unique name | Files (in a flat namespace) |
    | Storage class | |
    | Location (region or multu-region) | |
    | IAM policies or Access Control Lists (ACLs) | Access Control Lists |
    | Object versioning setting | |
    | Object lifecycle management rules | |
    * ACLs define who has access to your buckets and objects as well as what level of access they have
    * Each ACL consists of two pieces of information
        * Scope: defines who can perform the specified actions
        * Permission: defines what actions can be performed
* Cloud Storage also offers lifecycle management policies
    * No need to worry about junk accumulating
    * Example:
        * Delete objects older than 365 days
        * Delete objects created before January 1, 2013
        * Keep only the three most recent versions of each object in a bucket that has versioning enabled.

### Cloud Storage Interactions

> [![](https://img.youtube.com/vi/MKorUHd2tGs/0.jpg)](https://youtu.be/MKorUHd2tGs)

* Choosing among Cloud Storage classes
    | | Multi-regional | Regional | Nearline | Coldline |
    |---|---|---|---|---|
    | Intended for data that is... | Most frequently accessed | Accessed frequently within a region | Accessed less than once a month | Accessed less than once a year |
    | Availability SLA | 99.95% | 99.90% | 99.00% | 99.00% |
    | Access APIs | Consistent APIs ||||
    | Access time | Millisecond access ||||
    | Stroage price | Decreasingly (Price per GB stored per month) |
    | Retrieval price | Increasingly (Total price per GB transferred) |
    | Use cases | Content storage and delivery | In-region analytics, transcoding | Long-tail content, backups | Archiving, disaster recovery |
* There are several ways to bring data into Cloud Storage
    * **Online transfer**
        * Self-managed copies using command-line tools or drag-and-drop
    * **Storage Transfer Service**
        * Scheduled, managed batch transfers
    * **Transfer Appliance (Beta)**
        * Rackable appliances to securely ship your data
* Cloud Storage works with other GCP services
    * BigQuery: Import and export tables
    * App Engine: Object storage, logs, and Datastore backups
    * Compute Engine: Startups scripts, images, and general object storage
    * Cloud SQL: Import and export tables

### Practice Quiz: Cloud Storage

1. Your Cloud Storage objects live in buckets. Which of these characteristics do you define on a per-bucket basis? Choose all that are correct (3 correct answers).
    * a. A default file type for the objects in the bucket
    * b. An encryption-at-rest setting (on or off)
    * c. A default storage class
    * d. A globally-unique name
    * e. A geographic location
    > Answer: c. d. e.
2. (T/F) Cloud Storage is well suited to providing the root file system of a Linux virtual machine.
    > Answer: False.
3. Why would a customer consider the Coldline storage class?
    * a. To improve security.
    * b. To save money on storing infrequently accessed data.
    * c. To save money on storing frequently accessed data.
    * d. To use the Coldline Storage API.
    > Answer: b.

---
## Cloud Bigtable

> [![](https://img.youtube.com/vi/JhUC06wpAsw/0.jpg)](https://youtu.be/JhUC06wpAsw)

* Cloud Bigtable is managed NoSQL
    * Fully managed NoSQL, wide-column database service for terabyte applications
    * Cloud Bigtable is ideal for storing large amounts of data with very low latency
    * Accessed using HBase API
    * Native compatibility with big data, Hadoop ecosystem
* Why choose Cloud Bigtable?
    * Managed, scalable storage
    * Data encryption in-flight and at rest
    * Control access with IAM
    * Bigtable drives major applications such as Google Analytics and Gmail
* Bigtable Access Patterns
    * Application API
        * Data can be read from and written to Cloud Bigtable through a data service layer like Managed VMs, the HBase REST Server, or a Java Server using the HBase client
        * Typically this will be to serve data to applications, datahboards, and data services
    * Streaming
        * Data can be streamed in (written event by event) through a variety of popular stream processing framwworks like Cloud Dataflow Streaming, Sprark Streaming, and Storm
    * Batch Processing
        * Data can be read from and written to Cloud Bigtable through batch processes like Hadoop MapReduce, Dataflow, or Spark
        * Often, summarized or newly calculated data is written back to Cloud Bigtable or to a downstream database

### Practice Quiz: Cloud Bigtable

1. (T/F) Each table in NoSQL databases such as Cloud Bigtable has a single schema that is enforced by the database engine itself.
    > Answer: False.
2. Some developers think of Cloud Bigtable as a persistent hashtable. What does that mean?
    * a. Each item in the database consists of exactly the same fields, and can be looked up based on a variety of keys.
    * b. Each item in the database can be sparsely populated, and is looked up with a single key.
    > Answer: b.

---
## Cloud SQL and Cloud Spanner

> [![](https://img.youtube.com/vi/l4E_FaEwzmQ/0.jpg)](https://youtu.be/l4E_FaEwzmQ)

* Cloud SQL is a managed RDBMS
    * Offers MySQL and PostgreSQLBeta databases as a service
    * Automatic replication
        * Cloud SQL provides several replica services like read, failover, and external replicas.
    *  Managed backups
        * Cloud SQL also helps you backup your data with either on-demand or scheduled backups.
    * Vertical scaling (read and write)
    * Horizontal scaling (read)
    * Google security
* Cloud SQL instances are accessible by other GCP services and even external services
    * Cloud SQL can be used with App Engine using standard drivers.
        * You can configure a Cloud SQL instance to follow an App Engine application
    * Comput Engine instances can be authorized to access Cloud SQL instances using an external IP address
        * Cloud SQL instances can be configured with a preferred zone
    * Cloud SQL can be used with external applications and clients
        * Standard tools can be used to administer databases
        * External read replicas can be configured
* Cloud Spanner is a horizontally sclable RDBMS
    * Strong global consistency
    * Managed instances with high availability
    * SQL queries
        * ANSI 2011 with extensions
    * Automatic replication

### Practice Quiz: Cloud SQL and Cloud Spanner

1. Which database service can scale to higher database sizes?
    * a. Cloud SQL.
    * b. Cloud Spanner.
    > Answer: b.
2. Which database service presents a MySQL or PostgreSQL interface to clients?
    * a. Cloud SQL.
    * b. Cloud Spanner.
    > Answer: a.
3. Which database service offers transactional consistency at global scale?
    * a. Cloud SQL.
    * b. Cloud Spanner.
    > Answer: b.

---
## Cloud Datastore

> [![](https://img.youtube.com/vi/qhneVMLcuAY/0.jpg)](https://youtu.be/qhneVMLcuAY)

* Cloud Datastore is a horizontally scalable NoSQL DB
    * Designed for application backends
    * Supports transactions
    * Includes a free daily quota
* Cloud Datastore automatically handles sharding and replication
    * Providing you with a highly available and durable database that scales automatically to handle load.

### Practice Quiz: Cloud Datastore

1. How are Cloud Datastore and Cloud Bigtable alike? Choose all that are correct (2 correct answers)
    * a. They both have a free daily quota.
    * b. They both offer SQL-like queries.
    * c. They are both highly scalable.
    * d. They are both NoSQL databases.
    > Answer: c. d.
2. (T/F) Cloud Datastore databases can span App Engine and Compute Engine applications.
    > Answer: True.

---
## Comparing Storage Options

> [![](https://img.youtube.com/vi/ZG-6WYlgaKU/0.jpg)](https://youtu.be/ZG-6WYlgaKU)

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
## Lab 3: Getting Started with Cloud Storage and Cloud SQL

> [![](https://img.youtube.com/vi/KHqYEYOLozk/0.jpg)](https://youtu.be/KHqYEYOLozk)

* Please follow the details in [here](./Lab-3.md)

---
## Quiz: Google Cloud Platform Storage Options

1. You are developing an application that transcodes large video files. Which storage option is the best choice for your application?
    * a. Cloud Datastore
    * b. Cloud Spanner
    * c. Google Drive
    * d. Cloud Storage
    > Answer: d.
2. You manufacture devices with sensors and need to stream huge amounts of data from these devices to a storage option in the cloud. Which Google Cloud Platform storage option is the best choice for your application?
    * a. Cloud Bigtable
    * b. BigQuery
    * c. Cloud Datastore
    * d. Cloud Spanner
    > Answer: a.
3. Which statement is true about objects in Cloud Storage?
    * a. They are immutable, and new versions overwrite old unless you turn on versioning.
    * b. They can be edited in place.
    * c. They are immutable, and versioned by default.
    * d. They are immutable unless you turn on versioning.
    > Answer: a.
4. You are building a small application. If possible, you'd like this application's data storage to be at no additional charge. Which service has a free daily quota, separate from any free trials?
    * a. Cloud Datastore
    * b. Cloud SQL
    * c. Bigtable
    * d. Cloud Spanner
    > Answer: a.
5. How do the Nearline and Coldline storage classes differ from Multi-regional and Regional? Choose all that are correct (2 responses).
    * a. Data in Nearline and Coldline is not retrievable immediately.
    * b. Nearline and Coldline have lower durability. x
    * c. Nearline and Coldline use a differently-architected API. x
    * d. Nearline and Coldline assess lower storage fees.
    * e. Nearline and Coldline assess additional retrieval fees.
    > Answer: a. e.
6. Your application needs a relational database, and it expects to talk to MySQL. Which storage option is the best choice for your application?
    * a. Cloud Spanner
    * b. Bigtable
    * c. Cloud Storage
    * d. Cloud SQL
    > Answer: d.
7. Your application needs to store data with strong transactional consistency, and you want seamless scaling up. Which storage option is the best choice for your application?
    * a. Cloud Storage
    * b. Cloud Datastore
    * c. Cloud Spanner
    * d. Cloud SQL
    > Answer: c.
8. Which GCP storage service is often the ingestion point for data being moved into the cloud, and is frequently the long-term storage location for data?
    * a. Cloud Spanner
    * b. Cloud Datastore
    * c. Local SSD
    * d. Cloud Storage
    > Answer: d.
