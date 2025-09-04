# Nitro-instances

Nitro-based instances are EC2 instance families that run on the **AWS Nitro System**, which is a combination of dedicated hardware and lightweight hypervisor. Instead of relying on a traditional software hypervisor, Nitro offloads virtualization, networking, and security to dedicated hardware cards. This design gives instances near bare-metal performance and stronger isolation.

***

## Key Features

* **Performance**: Almost no overhead compared to bare metal.
* **Security**: Hardware-level isolation of compute, storage, and networking.
* **Special Capabilities**:
  * Required for EBS Multi-Attach.
  * Supports Elastic Fabric Adapter (EFA) for HPC workloads.
  * Enables higher IOPS and throughput limits on EBS volumes (e.g., io2 scaling up to 64K IOPS, Block Express volumes up to 256K IOPS).
  * Nitro Enclaves for secure enclaves inside EC2.
* **Bare Metal Options**: Nitro lets AWS expose full physical servers to customers while still keeping security guarantees.

***

## Exam-Relevant Instance Families

All **newer EC2 families** are Nitro-based. Examples:

* General purpose: A1, T3, T4g, M5, M6g, M7g
* Compute optimized: C5, C6g, C7g
* Memory optimized: R5, R6g, X2
* Storage/accelerated: I3en, I4i, P4d, G5, DL1
* Bare metal variants: `m5.metal`, `c6g.metal`, etc.

***

## Exam Tips

* If you see **EBS Multi-Attach**, **Nitro is required**.
* If you see **64K+ IOPS EBS performance** or **io2 Block Express**, assume Nitro-based.
* If the question mentions **bare-metal instances** with full hardware access, that’s enabled by Nitro.
* Security questions: Nitro has no administrative backdoor; AWS employees cannot log into your host.
* If you see HPC, machine learning, or networking-heavy workloads with EFA — those run on Nitro.
