# Exam Tips

Perfect — let’s tighten it up into **exam-focused tips for EC2** so you don’t get tripped up on the **AWS DevOps Professional exam**.

***

#### 1. **Instance Families**

* **T-Series** → Burstable, cost-saving for dev/test. Watch out for **CPU credits**.
* **M-Series** → General purpose, balanced workloads.
* **C-Series** → Compute-heavy workloads (HPC, gaming, analytics).
* **R-Series** → Memory-heavy (databases, caching, SAP HANA).
* **I/D/H-Series** → Storage optimized (high IOPS, databases, warehousing).
* **P/G/Inf/Trn/F-Series** → GPU/ML/accelerated computing.

👉 **Exam trap**: "Which instance type for a Redis cluster?" → R-Series.\
👉 **Exam trap**: "Which for fault-tolerant rendering farm with GPUs?" → G-Series (not C).

***

#### 2. **Storage Behavior**

* **EBS** = persistent, survives stop/start.
* **Instance Store** = ephemeral, lost on stop/terminate.
* **EFS / FSx** = shared, network-attached.

👉 **Exam trap**: “Data disappears after stopping instance” → It was **instance store**.

***

#### 3. **Pricing Models**

* **On-Demand** = flexibility, no commitment.
* **Reserved Instances / Savings Plans** = steady workloads.
* **Spot** = cheap but **interruptible** (2-min notice).
* **Dedicated Hosts/Instances** = compliance/licensing.
* **Capacity Reservation** = guaranteed availability in an AZ.

👉 **Exam trap**: “Company needs guaranteed availability in AZ but no long-term commitment” → **On-Demand Capacity Reservation**, not RI.

***

#### 4. **Scaling & Availability**

* **Auto Scaling Groups (ASG)** = automatic horizontal scaling.
* **Mixed Instance Policies** = ASG with multiple instance types + Spot/On-Demand.
* **Placement Groups**:
  * Cluster → low latency HPC.
  * Spread → HA across racks.
  * Partition → Hadoop/big data.

👉 **Exam trap**: “Hadoop cluster with thousands of nodes” → **Partition Group**.

***

#### 5. **Networking & Performance**

* **Enhanced Networking (ENA)** → high throughput, low latency.
* **Elastic Fabric Adapter (EFA)** → tightly coupled HPC/ML.
* **Security Groups** = stateful, best practice over NACLs.
* **PrivateLink** = secure VPC-to-service connectivity.

👉 **Exam trap**: “How to get sub-millisecond latency for HPC across EC2 nodes?” → **Cluster placement + EFA**.

***

#### 6. **Security & Access**

* Always use **IAM roles for EC2** (never hardcode creds).
* Use **Systems Manager Session Manager** for access (no SSH keys).
* Use **KMS** for EBS encryption.

👉 **Exam trap**: “How to manage SSH access securely without open ports?” → **SSM Session Manager**.

***

## 🎯 **Pro Exam Strategy**

* If the scenario is **mission-critical** → On-Demand or Reserved (never Spot).
* If the scenario is **batch/fault-tolerant** → Spot.
* If the scenario is **BYOL licensing** → Dedicated Host.
* If the scenario is **scheduled peak (e.g., Black Friday)** → Capacity Reservation.
* Always match **workload type → instance family**.

***

👉 Do you want me to make a **cheat sheet table** mapping “workload → correct EC2 choice” (both family + pricing model)? That’s a killer exam prep resource.
