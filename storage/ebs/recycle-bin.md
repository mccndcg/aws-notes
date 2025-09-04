# Recycle Bin

1. **Purpose & Scope**
   * Provides a safety net: when a snapshot (or AMI) is deleted, it goes into the **Recycle Bin** instead of being permanently removed.
   * Snapshots stay recoverable until the **retention period** expires.
2. **Retention Rules**
   * You define **retention periods** (from 1 day to 1 year).
   * Different rules can be based on **tags** or resource types.
   * Exam catch: _“How to ensure production snapshots are kept 90 days after deletion?”_ → Apply a **tag-based Recycle Bin rule**.
3. **Integration with Lifecycle Manager (DLM)**
   * If a snapshot is deleted by a DLM policy, it still goes to Recycle Bin.
   * Exam scenario: “Snapshots deleted by lifecycle rules should still be recoverable” → **Recycle Bin**.
4. **Supported Resources**
   * **EBS Snapshots** and **AMIs** (since AMIs are backed by snapshots).
   * Exam trick: Recycle Bin does _not_ apply to everything (e.g., not S3 objects).
5. **IAM Permissions**
   * Separate IAM actions control who can configure rules and who can restore items.
   * Exam scenario may test “why can’t a user recover snapshots?” → missing **`recyclebin:RestoreResources`** permission.
6. **Region-Specific**
   * Recycle Bin is **regional** — retention rules apply per Region.
   * Exam catch: deleting in one Region doesn’t affect another.
7. **Data Cost**
   * Snapshots in Recycle Bin still incur **standard snapshot storage costs** until permanently deleted.
   * Exam angle: “Does Recycle Bin reduce storage costs?” → **No**, just defers deletion.
8. **Recovery Process**
   * From Recycle Bin, you can restore snapshots back to the active state.
   * Once retention expires, recovery is impossible.

***

### Common Exam Gotchas

* **Recycle Bin ≠ Snapshot Lock**:
  * Recycle Bin = soft delete (recoverable).
  * Snapshot Lock = hard retention (can’t delete until lock expires, even by admins).
* **Recycle Bin ≠ Backup**:
  * It’s a safety net, not a backup scheduling tool.
  * If exam says “automate backups,” answer **DLM**, not Recycle Bin.
* **Retention Misunderstanding**:
  * Snapshots are restorable only within the defined retention period. After that, they’re gone permanently.
