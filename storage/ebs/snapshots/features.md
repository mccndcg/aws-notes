# Features

### 1. **Fast Snapshot Restore (FSR)**

**What it is:**\
By default, when you restore a volume from a snapshot, EBS uses **lazy loading** — data is only pulled from S3 when first accessed. This can cause initial latency. FSR pre-initializes the volume so it behaves like a fully-provisioned EBS volume immediately.

**Why it matters:**\
Critical for workloads that need consistent performance right after volume creation (databases, production systems).

**Exam example:**\
&#xNAN;_“You restored a snapshot to a new volume, but the first reads are very slow. How do you fix this?”_ → Enable **Fast Snapshot Restore**.

***

### 2. **EBS Snapshot Lifecycle Manager (DLM)**

**What it is:**\
A policy-based tool that automates the creation, retention, and deletion of EBS snapshots. You can define schedules (daily, hourly, weekly) and retention rules.

**Why it matters:**\
Ensures compliance and reduces manual management. Saves cost by automatically deleting old snapshots.

**Exam example:**\
&#xNAN;_“A company needs daily EBS backups with 30-day retention and automation.”_ → Use **DLM policies**.

***

### 3. **Recycle Bin for Snapshots**

**What it is:**\
A safety net feature that lets you configure retention periods for deleted snapshots. If a snapshot is accidentally deleted, it stays in the Recycle Bin until the retention period expires.

**Why it matters:**\
Protects against human error or malicious deletion.

**Exam example:**\
&#xNAN;_“Ops team accidentally deleted an important snapshot. How to prevent permanent loss in the future?”_ → Use **Recycle Bin**.

***

### 4. **Snapshot Sharing**

**What it is:**\
Snapshots can be shared:

* Privately (with specific AWS accounts).
* Publicly (anyone can use it to create a volume).

Encrypted snapshots require sharing the KMS CMK key as well.

**Why it matters:**\
Used for cross-account workloads, but public sharing is a **security risk** if misconfigured.

**Exam example:**\
&#xNAN;_“A security audit found sensitive data exposed. Root cause?”_ → A **public snapshot** was shared.

***

### 5. **Cross-Region Snapshot Copy**

**What it is:**\
Snapshots are Region-specific. To use in another Region, copy the snapshot. While copying, you can also encrypt or re-encrypt.

**Why it matters:**\
Key for disaster recovery and cross-region migration.

**Exam example:**\
&#xNAN;_“Company needs EBS backups in another Region for DR.”_ → Copy snapshots cross-region.

***

### 6. **Encryption with Snapshots**

**What it is:**

* Snapshots of encrypted volumes are encrypted.
* Volumes created from encrypted snapshots are encrypted.
* You can copy a snapshot to apply new encryption or switch to a different KMS CMK.

**Why it matters:**\
Snapshot encryption management is exam-favorite. Especially scenarios with multiple accounts and CMKs.

**Exam example:**\
&#xNAN;_“How to share an encrypted snapshot with another account?”_ → Share both the snapshot **and** the KMS CMK.

***

### 7. **AMI Dependency**

**What it is:**\
Amazon Machine Images (AMIs) are built from EBS snapshots of root and attached volumes.

**Why it matters:**\
When you create an AMI, AWS takes snapshots. If you delete those snapshots, the AMI may no longer work.

**Exam example:**\
&#xNAN;_“Why is an AMI not launchable after cleanup?”_ → Required EBS snapshots were deleted.

***

### 8. **Incremental Backups**

**What it is:**\
After the first snapshot, only changed blocks are stored. Deleting a snapshot does not break the chain — AWS re-links blocks.

**Why it matters:**\
Efficient storage, and avoids corruption when older snapshots are deleted.

**Exam example:**\
&#xNAN;_“If snapshot #3 is deleted, what happens to #4 and #5?”_ → They remain intact, AWS re-links needed blocks.

***

### 9. **Application Consistency**

**What it is:**\
Snapshots are crash-consistent by default. To achieve application consistency (databases, transactions), you need to freeze the filesystem or use AWS Backup / application-level scripts.

**Why it matters:**\
Some exam scenarios will mention “transactionally consistent backup” → snapshot alone isn’t enough.

**Exam example:**\
&#xNAN;_“How do you ensure a consistent snapshot for a running SQL Server instance?”_ → Use application-level tools or AWS Backup integration.

***

### 10. **Parallel Volume Creation**

**What it is:**\
You can create multiple volumes at once from the same snapshot.

**Why it matters:**\
Speeds up scaling and testing scenarios.

**Exam example:**\
&#xNAN;_“You need to launch 10 test environments quickly from one snapshot.”_ → Create multiple volumes in parallel.

***

Do you want me to condense all this into a **one-page "Snapshot Exam Cheatsheet"** (like a table with Feature | Key Point | Exam Gotcha)? That could be a great revision tool.
