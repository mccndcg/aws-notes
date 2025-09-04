# Exam Tips

### General

* EBS volumes are **AZ-specific** — they do not span Availability Zones.
* Durability is **99.999%** — but still use snapshots (stored in S3) for backup and cross-AZ or cross-region recovery.
* **EC2 termination vs EBS delete**: By default, the root EBS volume is deleted when the instance is terminated unless you disable `DeleteOnTermination`.
* Encryption is **seamless** using KMS; can encrypt at rest and in transit automatically.

***

### Volume Types

* **gp3**: Default choice for most workloads. Cheaper and faster than gp2, with ability to provision IOPS/throughput separately.
* **gp2**: Older generation, IOPS tied to volume size. Still appears in exam scenarios for legacy systems.
* **io1/io2**: Provisioned IOPS SSDs, for latency-sensitive workloads (databases). io2 provides higher durability and better baseline.
* **io2 Block Express**: Next-gen architecture for extreme performance (up to 256K IOPS, 64 TiB volumes).
* **st1**: Throughput-optimized HDD for streaming workloads (big data, log processing).
* **sc1**: Cold HDD for rarely accessed data, lowest cost.

***

### Performance and Limits

* gp3: Baseline 3,000 IOPS and 125 MB/s, can scale up to 16,000 IOPS and 1,000 MB/s.
* gp2: Performance is volume-size dependent; max 16,000 IOPS at 16 TiB.
* io1/io2: Can scale to 64,000 IOPS on Nitro-based instances.
* Block Express: Up to 256,000 IOPS and 4,000 MB/s.
* Bursting applies to smaller gp2 volumes (credits system).

***

### Snapshots

* Snapshots are **incremental** — only changed blocks are saved.
* Can create volumes in a different AZ or Region from a snapshot.
* Fast Snapshot Restore (FSR) enables low-latency, fully-initialized volumes from snapshots.

***

### Other Features

* Multi-Attach: io1 and io2 volumes can be attached to multiple Nitro-based instances in the same AZ. Useful for clustered workloads.
* Elastic Volumes: Can change type, size, and IOPS of most volumes without downtime.
* Data Lifecycle: Snapshots can be managed automatically using Data Lifecycle Manager (DLM).

***

### Common Exam Traps

* If the question asks about **cost-optimized general workloads** → gp3.
* If it mentions **very high IOPS, sub-millisecond latency, or mission-critical DBs** → io2/io2 Block Express.
* If it involves **throughput-intensive workloads** (like Hadoop, Kafka, data warehouse) → st1.
* If it involves **archival, rarely accessed data** → sc1.
* If the scenario requires **attaching the same volume to multiple instances** → io1/io2 with Multi-Attach.
* If a snapshot is used to create a new volume in another AZ or Region → that’s valid (they’re stored in S3).
* Always look for **DeleteOnTermination** in questions about preserving data after EC2 shutdown.
