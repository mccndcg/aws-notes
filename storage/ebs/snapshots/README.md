# Snapshots

## AWS Docs

{% stepper %}
{% step %}
### EventBridge events

{% embed url="https://docs.aws.amazon.com/ebs/latest/userguide/ebs-cloud-watch-events.html#volume-events" %}
{% endstep %}

{% step %}
### Lifecycle

{% embed url="https://docs.aws.amazon.com/ebs/latest/userguide/ebs-snapshot-lifecycle.html" %}
{% endstep %}

{% step %}
### Block public access

{% embed url="https://docs.aws.amazon.com/ebs/latest/userguide/block-public-access-snapshots.html" %}
{% endstep %}
{% endstepper %}

### What an EBS Snapshot Is

* A point-in-time, incremental backup of an EBS volume.
* Stored in Amazon S3 (managed and hidden from you — you can’t browse it like a normal S3 bucket).
* Can be used to create new EBS volumes, copy across Regions, or share with other accounts.

***

### Lifecycle

```mermaid
flowchart TD

    A[Volume in Use] --> B[Take Snapshot]
    B --> C{Is it First Snapshot?}
    C -->|Yes| D[Full Snapshot Stored in S3]
    C -->|No| E[Incremental Snapshot<br/>Only Changed Blocks Stored]

    D --> F[Snapshot Available]
    E --> F

    F --> G[Use Snapshot to Create Volume/AMI]
    F --> H[Copy Snapshot<br/>Cross-Region or Re-Encrypt]
    F --> I[Share Snapshot<br/>Private/Public]
    F --> J[Apply Lifecycle Policy<br/>DLM Automation]
    F --> K[Enable Fast Snapshot Restore]

    J --> F
    K --> G

    F --> L[Delete Snapshot]
    L --> M{Recycle Bin Enabled?}
    M -->|Yes| N[Snapshot in Recycle Bin<br/>Recoverable Until Retention Expires]
    M -->|No| O[Snapshot Permanently Deleted<br/>But Blocks Used by Later Snapshots are Preserved]

    N --> F

```

### Key Characteristics

* **Incremental**: After the first snapshot, only changed blocks are saved. Saves storage and time.
* **Durable**: Stored redundantly in S3 with 11 nines of durability.
* **Region-specific**: Snapshots are bound to a region but can be copied across regions.
* **Crash-consistent**: Snapshots capture all blocks at the point in time, but may not guarantee application consistency unless coordinated.

***

### Features and Advanced Options

1. **Fast Snapshot Restore (FSR)**
   * Allows restoring a snapshot so the volume is fully initialized immediately.
   * Normally, restored volumes use lazy loading (initial read can be slow).
   * Good for latency-sensitive workloads.
2. **EBS Snapshot Lifecycle Manager (DLM)**
   * Automates creation, retention, and deletion of snapshots based on policies.
   * Useful for compliance and cost management.
3. **Snapshot Sharing**
   * Snapshots can be shared with specific AWS accounts or made public.
   * Public snapshots often appear in exam questions as a data leakage risk.
4. **Snapshot Copy**
   * Copy snapshots across regions for disaster recovery or migration.
   * Can also change encryption state (copy an unencrypted snapshot to an encrypted one).
5. **Recycle Bin for Snapshots**
   * Lets you set retention policies so snapshots deleted accidentally can be recovered within a set period.

***

### Common Exam Scenarios

* **Cross-Region DR**: Copy snapshots to another region, then create volumes there.
* **Cross-Account Access**: Share snapshot with another account so they can create volumes.
* **Backup Automation**: Use Data Lifecycle Manager to create recurring snapshots.
* **Encryption**: Snapshots inherit the encryption of the source volume, but you can also re-encrypt when copying.
* **Restore Performance**: Use Fast Snapshot Restore for workloads that can’t tolerate lazy initialization.
* **Migration**: Move a workload by snapshotting a volume, copying across regions, and creating a new volume.

***

### Exam Tips

* Snapshots are **volume-level**, not instance-level. If you need an instance backup, use AMI creation (which includes snapshots of all attached volumes).
* Snapshot storage costs are based on the amount of data stored, not the logical size of the volume.
* Deleting a snapshot does not necessarily delete blocks if they are referenced by newer snapshots (chain-based).
* Snapshots are always stored in S3, but you do not interact with them as S3 objects.
* For compliance-driven questions, remember DLM and Recycle Bin.
