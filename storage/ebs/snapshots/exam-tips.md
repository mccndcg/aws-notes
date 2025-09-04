# Exam Tips

***

### Core Concepts

* Snapshots are **point-in-time, incremental backups** of EBS volumes.
* Always stored in **Amazon S3** (managed by AWS, not visible as S3 objects).
* Snapshots are **region-specific** but can be copied across regions.
* Restoring a snapshot creates a **new EBS volume**.

***

### Performance & Behavior

* First snapshot = full copy; subsequent snapshots = **changed blocks only**.
* Deleting a snapshot does **not break the chain** — AWS re-links needed blocks so later snapshots remain usable.
* Restored volumes use **lazy loading** (blocks are fetched on first access) unless **Fast Snapshot Restore (FSR)** is enabled.
* Multiple volumes can be created in parallel from the same snapshot.

***

### Features to Know

* **Fast Snapshot Restore (FSR):** Ensures restored volumes are fully initialized for immediate high performance.
* **Lifecycle Manager (DLM):** Automates snapshot creation/retention/deletion policies.
* **Recycle Bin:** Protects against accidental deletion with configurable retention.
* **Sharing:** Snapshots can be shared with other accounts or made public (risk of data leakage).
* **Cross-Region Copy:** Enables DR setups and snapshot encryption changes (unencrypted → encrypted).
* **AMI dependency:** An AMI includes snapshots of the root and attached EBS volumes.

***

### Security & Encryption

* Snapshots of encrypted volumes are automatically encrypted.
* Volumes restored from encrypted snapshots remain encrypted.
* You can copy a snapshot to change its encryption key (KMS).
* Sharing encrypted snapshots requires sharing the CMK as well.

***

### Exam Traps

* Snapshots are **volume-level**, not EC2 instance–level. To back up an instance, create an AMI.
* Snapshots are **crash-consistent only** by default, not application-consistent (unless you quiesce the app or use AWS Backup).
* If you need **cross-region backups**, copying snapshots is the right method, not direct volume creation.
* If a scenario needs **instant restore with predictable latency**, the answer is **FSR**, not just snapshots.
* If snapshots need to be **retained automatically for compliance**, use **DLM**.
* If the question mentions **accidental deletion recovery**, use **Recycle Bin**.
* Making a snapshot public can **leak sensitive data** — common security pitfall in exam questions.
