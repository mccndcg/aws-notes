---
description: >-
  Protects the data on an AMI's underlying EBS snapshots using AWS KMS keys,
  ensuring all instances launched from it have encrypted volumes.
---

# Encryption

## Definition

An encrypted AMI (Amazon Machine Image) is a virtual machine template that has its associated EBS snapshots encrypted with an AWS KMS key. When you launch an EC2 instance from an encrypted AMI, its root volume is automatically encrypted, ensuring data at rest is protected. Five Use Cases:

1. Enforcing data security: Ensures all instances launched from a specific AMI, including their root volumes, are encrypted, which is a key security best practice.
2. Meeting compliance requirements: Facilitates compliance with industry regulations like HIPAA, PCI DSS, and GDPR by mandating encryption for data at rest.
3. Secure cross-account sharing: Allows for secure sharing of "golden" AMIs containing hardened, pre-configured software between different AWS accounts by managing access to the KMS key.
4. Protecting sensitive data: Safeguards sensitive intellectual property or customer data stored within the AMI and on volumes of launched instances from unauthorized access.
5. Simplifying multi-region deployments: Streamlines multi-region deployment of consistently configured and secure instances by ensuring the encryption is maintained across regions.&#x20;

## Most-Used Settings

* KMS Key: The customer-managed or AWS-managed key used to encrypt the underlying EBS snapshots. For cross-account sharing, a customer-managed key is required.
* Encryption checkbox: A setting available when copying an existing AMI, which allows you to encrypt the target EBS snapshots.
* Default EBS encryption: An account-level setting that automatically encrypts all newly created EBS volumes and snapshots, ensuring that any new AMIs created from those volumes are also encrypted.
* Cross-account KMS permissions: The KMS key policy must explicitly allow the target account to use the key for decryption, which is necessary for launching instances from a shared encrypted AMI.
* Launch template settings: When launching instances, a launch template can be configured to use a specific encrypted AMI and potentially override the key used for encryption.&#x20;
