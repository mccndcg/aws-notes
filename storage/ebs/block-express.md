---
description: >-
  Next-generation EBS storage architecture built on Scalable Reliable Datagrams
  (SRD) for ultra-high performance.
---

# Block Express

## Key Features

* Performance: Up to 64 TiB per volume, 256,000 IOPS, and 4,000 MB/s throughput.
* Latency: Sub-millisecond consistency, even under heavy load.
* Protocol: Uses SRD (Scalable Reliable Datagram) in the Nitro System for volume communication.
* Reliability: Same durability as standard io2 volumes (99.999%).
* Use cases: Enterprise databases (Oracle, SQL Server, SAP HANA), large-scale transaction systems, and high-performance storage arrays.

***

## Block Express vs Standard EBS

| Feature        | Standard EBS (gp3, io1, io2)     | Block Express (io2 Block Express)                 |
| -------------- | -------------------------------- | ------------------------------------------------- |
| Max size       | 16 TiB                           | 64 TiB                                            |
| Max IOPS       | 64,000                           | 256,000                                           |
| Max throughput | 1,000 MB/s                       | 4,000 MB/s                                        |
| Latency        | 1–2 ms typical                   | Sub-millisecond                                   |
| Protocol       | TCP over Nitro                   | SRD over Nitro                                    |
| Best for       | General workloads, mid-scale DBs | Ultra-high performance databases, enterprise apps |
