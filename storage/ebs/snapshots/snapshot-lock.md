# Snapshot Lock

{% stepper %}
{% step %}
### Concepts

{% embed url="https://docs.aws.amazon.com/ebs/latest/userguide/snapshot-lock-concepts.html" %}
{% endstep %}

{% step %}
### Considerations

{% embed url="https://docs.aws.amazon.com/ebs/latest/userguide/snapshot-lock-considerations.html" %}
{% endstep %}
{% endstepper %}

### Snapshot Lock Overview

* **What it is:** A feature (in preview/gradual rollout) that lets you place retention-based locks on EBS snapshots.
* **Purpose:** Prevents users (even with admin privileges) from deleting or tampering with critical snapshots before the lock period expires.
* **Modes:**
  * **Governance Mode**: Users with special permissions can still override.
  * **Compliance Mode**: Even root/admins cannot delete until the lock expires (regulatory compliance use case).
* **Cooling-off period:**
  * When you first apply a Snapshot Lock policy (governance or compliance mode), AWS enforces a **72-hour cooling-off period** before the policy becomes immutable.
  * During this time, you can still change or delete the lock.
  * After the cooling-off, the lock is enforced, and deletion is impossible (depending on mode).
  * **Why it exists:**
    * Prevents accidental or rushed lock settings that might otherwise trap snapshots forever.
    * Gives admins a safe rollback window before compliance mode takes over.

### Exam Tips

1. **Snapshot Lock ≠ Recycle Bin**
   * Recycle Bin = soft delete (recoverable until retention).
   * Lock = hard guarantee, snapshot _cannot_ be deleted/altered.
   * Exam trick: If they ask about "preventing deletion for compliance," answer **Snapshot Lock**, not Recycle Bin.
2. **Retention Periods**
   * Lock enforces minimum/maximum retention (days to years).
   * Great for exam scenarios with financial or healthcare compliance (SOX, HIPAA).
3. **Cross-Service Confusion**
   * Similar to **S3 Object Lock** (governance/compliance mode).
   * On exams, AWS likes to test if you mix them up. Remember: EBS snapshots = _Snapshot Lock_.
4. **Not a Backup Solution**
   * Locks don’t create snapshots, they just protect existing ones.
   * If the exam scenario is about automation → **Lifecycle Manager**;\
     if about immutability → **Snapshot Lock**.
5. If the question mentions **regulatory compliance** (e.g., financial, healthcare):\
   → Answer = **Snapshot Lock in compliance mode**.
6. If the question mentions **soft recovery from accidental deletion**:\
   → Answer = **Recycle Bin**.
7. If the question mentions **automated backup scheduling**:\
   → Answer = **Lifecycle Manager (DLM)**.
8. Watch for **cooling-off trick**:
   1. If the exam asks, _“Can you immediately enforce a compliance lock that even admins can’t override?”_
   2. Correct answer: _No, a 72-hour cooling-off period applies first._
