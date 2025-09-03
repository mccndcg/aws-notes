---
description: >-
  Copies an AMI to a new or different AWS Region, optionally applying encryption
  and other modifications.
---

# Copy AMI

## Definition

AMI copies duplicate an Amazon Machine Image (AMI), including its associated EBS snapshots, enabling migration and replication within the same or across different AWS Regions. Five Use Cases:

1. Multi-region deployment: Enables consistent application deployment across different AWS Regions for global availability.
2. Disaster recovery: Facilitates copying a "golden" AMI to a secondary region for faster recovery in case of regional outages.
3. Cross-account sharing: Shares custom, hardened AMIs between AWS accounts, with an additional step required for copying encrypted AMIs.
4. Enforcing encryption: Converts unencrypted AMIs to encrypted ones by selecting the encryption option during the copy process.
5. Predictable replication: Utilizes time-based copy options to guarantee a specific completion duration for critical replication and compliance tasks.&#x20;

## Most-Used Settings

* Destination Region: The target AWS Region for the new AMI.
* Encrypt: An option to encrypt the snapshots of the AMI copy, often requiring a KMS key.
* KMS Key: The key identifier used to encrypt the AMI's snapshots, particularly for cross-account or custom encryption.
* Time-based Copy: A duration-based option for expedited, predictable copies, useful for meeting strict RTOs.
* Copy Tags: A setting to duplicate user-defined tags from the source AMI to the new AMI.&#x20;

## Basic Details

<figure><img src="../../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

## Time-bad, Encryption

<figure><img src="../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

## Tagging

<figure><img src="../../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>
