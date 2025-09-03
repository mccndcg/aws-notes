---
description: >-
  Copies an AMI to a new or different AWS Region with a guaranteed completion
  time for predictable replication.
---

# Time-based Copy

## Time-based

A time-based copy of an AMI is a copy operation where you specify aguaranteed completion duration for the process. It allows you to control how long it takes to replicate an AMI and its associated EBS snapshots, both within and across AWS Regions. This is different from a standard copy, which operates on a "best-effort" basis without a predictable completion time. How it works

* When you initiate a time-based AMI copy, you define a target completion duration (e.g., 15 minutes to 48 hours in 15-minute increments).
* AWS automatically calculates and provisions the necessary throughput to ensure that the copy of each underlying EBS snapshot finishes within that timeframe.
* This feature is an extension of the time-based copy for EBS snapshots, leveraging the same underlying technology to prioritize data transfer.&#x20;

Benefits

* Compliance: Meets regulatory requirements (like HIPAA or GDPR) for disaster recovery and data replication that mandate strict time windows.
* Predictability: Ensures predictable copy times, which is crucial for disaster recovery planning and meeting Recovery Time Objectives (RTOs) and Recovery Point Objectives (RPOs).
* Reliability: Provides guaranteed, time-bound replication, removing the uncertainty of standard copy operations.
* Faster cross-region copy: By paying a premium, you can accelerate the copy of a large AMI across regions to meet a tight deadline.&#x20;

Pricing

* Time-based copies incur an additional fee based on the requested completion duration and the amount of data copied.
* Requesting a shorter completion duration will result in a higher cost per GiB of data transferred.
* You are billed for the actual completion duration, so if a throughput quota is unexpectedly exceeded, the cost adjusts.&#x20;
