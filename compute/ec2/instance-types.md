# Instance Types

## Naming

<mark style="color:green;">\<Instance Family></mark><mark style="color:red;">\<Generation></mark><mark style="color:blue;">\<Additional Capability></mark>.<mark style="color:purple;">\<Size></mark>&#x20;

eg: R 5 dn . 8xlarge

## Capabilities

Here’s the **complete set of suffixes** AWS uses:

* **a** → AMD processors (e.g., `m5a`)
* **ad** → AMD with local NVMe instance storage (e.g., `m5ad`)
* **d** → Local NVMe-based instance storage (SSD) (e.g., `m5d`)
* **g** → AWS Graviton ARM-based processors (e.g., `m6g`)
* **gd** → Graviton + local NVMe storage (e.g., `m6gd`)
* **i** → Intel-based processors (explicit, less common now)
* **n** → Enhanced networking / higher bandwidth (e.g., `m5n`)
* **dn** → Both local NVMe SSD + enhanced networking (e.g., `r5dn`)
* **zn** → High-frequency Intel with high networking (e.g., `z1dn`)

***

## **Special Families with Built-in Capabilities**

Some capabilities are **baked into the family name**, not a suffix:

* **t4g** = Graviton burstable (suffix g is part of family name here).
* **inf1 / inf2** = AWS Inferentia accelerators.
* **trn1** = Trainium ML training.
* **f1** = FPGA acceleration.
* **g4 / g5** = GPU instances.
* **p3 / p4** = GPU compute (ML training).
* **vt1** = Video transcoding.

***

| Category                  | Families (Examples & Notes)                                                                                                                                                                                                                           |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **General Purpose**       | `T` (e.g., `t3.micro`, burstable), `M` (e.g., `m6g.large`, balanced), `A` (e.g., `a1.medium`, ARM/Graviton)                                                                                                                                           |
| **Compute Optimized**     | `C` (e.g., `c6i.4xlarge`, compute-heavy workloads)                                                                                                                                                                                                    |
| **Memory Optimized**      | `R` (e.g., `r6g.large`, memory-intensive DBs), `X` (e.g., `x2gd.16xlarge`, SAP HANA), `z1d` (high-frequency CPUs + memory), `u` (bare metal, ultra high memory)                                                                                       |
| **Storage Optimized**     | `I` (e.g., `i3.large`, NVMe SSD), `D` (e.g., `d2.2xlarge`, HDD storage), `H` (e.g., `h1.4xlarge`, high throughput HDD)                                                                                                                                |
| **Accelerated Computing** | `P` (e.g., `p4d.24xlarge`, ML training GPUs), `G` (e.g., `g5.2xlarge`, graphics/ML inference), `Inf` (e.g., `inf1.xlarge`, Inferentia AI chip), `Trn` (e.g., `trn1.32xlarge`, Trainium for ML), `F1` (FPGA instances), `VT1` (video transcoding GPUs) |

### ⚡ Exam Tip

AWS often asks about **which suffix matters in a workload scenario**:

* If you see **“local NVMe storage required”** → pick **d** or **ad**.
* If you see **“must use ARM/Graviton for cost savings”** → pick **g** or **gd**.
* If you see **“network throughput is key”** → pick **n**.
* If you see **“BYOL licensing for Intel-only”** → pick **i** or non-ARM.
