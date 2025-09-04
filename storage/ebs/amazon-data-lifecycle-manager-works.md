# Amazon Data Lifecycle Manager works

{% embed url="https://docs.aws.amazon.com/ebs/latest/userguide/dlm-elements.html" %}

### Exam Tips on Lifecycle Manager (DLM)

1. **Purpose & Scope**
   * Automates **snapshot** and **AMI** creation, retention, and deletion.
   * If exam scenario says _“eliminate manual snapshot management”_ → think **DLM**.
2. **Granularity**
   * Policies can be applied to:
     * Individual volumes
     * Volumes with specific **tags**
     * Whole instance (via AMI lifecycle policies).
   * Exam catch: “How to ensure only tagged production volumes are backed up?” → **DLM tag-based policy**.
3. **Retention Rules**
   * Define **how long** snapshots/AMIs are kept (e.g., 30 days, 3 copies).
   * Expired snapshots are automatically deleted.
   * Watch for exam wording around _compliance retention_.
4. **Cross-Region & Cross-Account Copy**
   * DLM can automatically copy snapshots to another Region/account.
   * Big exam angle: Disaster Recovery requirements → **cross-region DLM policy**.
5. **Encryption**
   * Snapshots created from encrypted volumes stay encrypted.
   * DLM supports **copying with new CMKs** when replicating across Regions/accounts.
6. **IAM Permissions**
   * Policies are resource-based.
   * Users/roles need proper IAM permissions to manage or execute lifecycle policies.
   * Exam scenario might test “policy not working” → check **IAM permissions**.
7. **Policy Types**
   * **EBS Snapshot Policies** – recurring snapshots of volumes.
   * **AMI Policies** – periodic AMI creation of instances.
   * Exam might ask: _“Company needs to rotate EC2 AMIs weekly while keeping last 2 versions.”_ → Use **DLM AMI policy**.
8. **Integration with Recycle Bin**
   * If snapshots are deleted by a lifecycle policy, Recycle Bin can retain them for recovery.
   * Exam angle: “How to protect against accidental DLM deletions?” → enable **Recycle Bin**.
9. **CloudWatch Events / EventBridge**
   * DLM actions can emit CloudWatch Events (success, failure).
   * Useful for exam scenarios about _auditing snapshot automation_.
10. **Not Application-Aware**

* DLM ensures crash-consistent snapshots, not application-consistent.
* Exam gotcha: If transactional consistency is required (e.g., SQL backups), DLM alone is not enough.
