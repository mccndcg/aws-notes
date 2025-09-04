# Multi-attach

## AWS Docs

{% stepper %}
{% step %}
### Concept

{% embed url="https://docs.aws.amazon.com/ebs/latest/userguide/ebs-volumes-multi.html" %}
{% endstep %}

{% step %}
### How-to

{% embed url="https://docs.aws.amazon.com/ebs/latest/userguide/working-with-multi-attach.html" %}
{% endstep %}
{% endstepper %}

Here’s the straight rundown on **Amazon EBS Multi-Attach**, in an exam-relevant way.

***

## Definition

Multi-Attach lets a single EBS volume be attached to **multiple EC2 instances** within the same Availability Zone. All attached instances can read and write to the volume at the same time.

* Only supported for **io1 and io2** volume types.
* Limit: up to **16 Nitro-based instances** in the same AZ.
* Volume must be in the **same AZ** as the instances.
* Applications must be **cluster-aware** (e.g., clustered databases, file systems) to handle concurrent writes safely. AWS does not manage write ordering or locking.
* Each attached instance sees the volume as a normal block device.

***

## Use Cases

* Shared-disk clustering (e.g., Microsoft WSFC, Oracle RAC).
* High-availability applications that need multiple EC2s accessing the same data set.
* File systems that are designed for multi-writer access (e.g., GFS2, OCFS2).

***

## Restrictions / Exam Gotchas

* Not supported on **gp2, gp3, st1, sc1**.
* Root volumes cannot be Multi-Attach.
* Snapshots work normally, but consistency depends on application-level coordination.
* AZ-bound: cannot attach across multiple Availability Zones.
* Throughput and IOPS are shared across all attached instances.

***

## Exam Tip

If you see a scenario with:

* "multiple EC2 instances need simultaneous block-level access to the same dataset" → **Multi-Attach with io1/io2**.
* If the question instead needs "file sharing" without application-level coordination → the right answer is usually **EFS**, not Multi-Attach.

***

Would you like me to draw a quick diagram showing how **Multi-Attach volumes sit between multiple EC2 instances** (useful for visual memory on the exam)?
