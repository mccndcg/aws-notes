---
description: >-
  A managed, high-performance relational database engine that separates compute
  and storage, providing auto-scaling, high availability, and MySQL/PostgreSQL
  compatibility.
---

# Aurora Cluster

## AWS Documentation

### Cluster Definition

{% embed url="https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.html" %}

### High availability Architecture

{% embed url="https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Concepts.AuroraHighAvailability.html" %}

## Definition

An Amazon Aurora cluster is a highly scalable and fault-tolerant relational database that consists of a <mark style="background-color:yellow;">primary read/write database instance</mark>, up to <mark style="background-color:yellow;">15 read-only</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**replica**</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">instances</mark>, and a virtual, self-healing storage volume shared by all instances. This architecture allows for independent scaling of compute and storage, ensuring high performance, durability, and availability.

## Key Concepts

* Decoupled storage and compute: Aurora's architecture separates the database instances (compute) from the storage layer. The underlying storage volume is virtual, distributed, and shared among all instances in the cluster.
* High-durability storage: Aurora automatically and synchronously replicates your data six times across three Availability Zones (AZs). This provides high durability and protects against data loss, even if an entire AZ fails.
* Automatic failover with replicas: For high availability, you can deploy up to 15 read-only Aurora Replicas across different AZs. If the primary (writer) instance fails, Aurora automatically promotes a replica to be the new primary, typically within 60 to 120 seconds.
* Failover priority: You can assign a promotion priority tier to each replica, ranging from 0 (highest) to 15 (lowest). This allows you to control which replica is promoted during a failover event.
* Endpoints for minimal downtime: To ensure failover is seamless for applications, you use two key endpoints:
  * Cluster Endpoint: The single DNS endpoint for all read and write traffic. It always points to the current primary instance, redirecting write traffic automatically after a failover.
  * Reader Endpoint: A load-balancing endpoint that distributes read-only traffic across all available replicas.
* Automatic storage repair and backups: The storage layer is self-healing, continuously scanning for and repairing disk errors. Aurora also performs continuous, incremental backups to Amazon S3 without impacting performance.
* Zero-downtime patching: During some patching operations, Aurora uses a zero-downtime patching (ZDP) feature to preserve client connections and minimize interruptions.&#x20;

## Clarifications

{% hint style="warning" %}
Does aurora reader replicas store data on their own?
{% endhint %}

No, Aurora reader replicas do not store data on their own. All instances in an Aurora cluster, both the primary (writer) and the replicas (readers), share a single, virtual, distributed, and self-healing storage volume. How the shared storage works

* Decoupled architecture: Aurora's core innovation is its decoupled compute and storage architecture. The database instances (compute) and the storage layer are separate components that scale independently.
* Shared access: All database instances—the primary for reads and writes, and the replicas for reads—access this same storage volume simultaneously.
* Logical replication: Because they share storage, Aurora replicas do not need to perform traditional, resource-intensive replication by copying data from the primary. They only need to read data from the shared volume as needed to fulfill read queries.
* Reduced latency: This approach results in significantly lower replication lag compared to traditional databases, where replicas must process and apply changes separately.&#x20;

The shared storage architecture is key to Aurora's high performance, durability, and fault tolerance. It simplifies adding new reader instances, which can be done quickly because no data needs to be copied or synchronized.&#x20;

{% hint style="warning" %}
if the cluster endpoint enables one to read, what is the use for a reader endpoint
{% endhint %}

While the Aurora cluster endpoint can be used for both reads and writes, using the dedicated reader endpoint for read operations is crucial for performance, scalability, and high availability. Here's a breakdown of why the reader endpoint is so important:

**Load balancing**

* The reader endpoint automatically distributes incoming read-only connections across all available reader instances using a DNS round-robin method.
* This prevents any single instance from being overwhelmed by read traffic.
* The cluster endpoint, in contrast, connects only to the primary instance. If you use it for reads, you are not taking advantage of any reader replicas and are creating a bottleneck on the primary.&#x20;

**Performance**

* By offloading read queries to dedicated reader instances, the primary instance can focus its resources on processing critical write operations.
* This separation of workloads prevents heavy read traffic from degrading the performance of write-heavy transactions.&#x20;

**Scalability**

* You can easily scale your read capacity by adding more reader instances to the cluster. The reader endpoint will automatically begin including these new instances in its load-balancing distribution.
* This allows you to handle a higher volume of read-only queries, which is essential for scaling a read-heavy application.&#x20;

**High availability**

* When a failover occurs, a reader instance is promoted to be the new primary. Since the reader endpoint load-balances across all replicas, the application can continue serving read traffic from the remaining replicas with minimal disruption.
* If you rely on the cluster endpoint for all reads, a failover would temporarily interrupt all read and write operations until the new primary is promoted.&#x20;

The best practice is to configure your application to use the correct endpoint for each database operation:&#x20;

* For writes: Use the cluster endpoint, which always points to the primary instance.
* For reads: Use the reader endpoint, which load-balances connections to the reader instances.&#x20;
