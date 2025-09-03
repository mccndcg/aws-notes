---
description: >-
  A template to launch virtual servers (EC2 instances) in AWS, including the
  operating system, applications, and configurations.
---

# AMI

Definition: An Amazon Machine Image (AMI) is a master template for creating virtual servers (EC2 instances) that contains the operating system, application server, applications, and launch permissions needed to launch an instance. It serves as a blueprint for the EC2 instance's root volume. Five Use Cases:

1. Multi-region deployment: Copy AMIs across different AWS Regions to deploy consistent infrastructure globally.
2. Disaster recovery: Use AMIs to create point-in-time backups of critical systems, allowing for faster recovery in case of an outage.
3. Centralized "golden" images: Create and share a standardized, pre-configured, and hardened AMI across different accounts within an organization.
4. Rapid scaling: Use a custom AMI with an Auto Scaling group to quickly launch additional, identical instances to handle traffic spikes.
5. Development and testing: Standardize dev/test environments by sharing custom AMIs that contain all the necessary software and settings for a project.&#x20;

Most-Used Settings:

* Launch Permissions: Controls which AWS accounts can use the AMI to launch instances.
* Tags: Use key-value pairs to organize, manage, and track ownership of AMIs, especially at scale.
* Virtualization Type: Specifies the type of virtualization, with HVM (hardware virtual machine) being the recommended and most modern type.
* Encryption: During the AMI copy process, you can enable encryption for the underlying EBS snapshots to ensure data security.
* Block Device Mapping: Defines the storage volumes that will be attached to an instance when it is launched from the AMI.&#x20;
