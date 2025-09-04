# Pricing

## **EC2 Pricing Options**

#### **1. On-Demand Instances**

* **How it works:** Pay for compute capacity by the second (Linux) or by the hour (Windows). No commitments.
* **Pros:** Maximum flexibility, easy to spin up/tear down.
* **Cons:** Most expensive per-unit cost.
* **Use Case:** Short-lived workloads, development/testing, or unpredictable traffic.
* **Example:** A startup testing their app on a few instances for a week.

***

#### **2. Reserved Instances (RI)**

* **How it works:** Commit to a specific instance type and region for **1 or 3 years**. Get up to **72% discount** vs On-Demand.
* **Types:**
  * **Standard RI:** Biggest discount, fixed configuration.
  * **Convertible RI:** Can change instance families/OS, slightly less discount.
* **Pros:** Huge savings for steady-state workloads.
* **Cons:** Less flexibility, locked in for term.
* **Use Case:** Production databases, ERP apps, or any service running 24/7.
* **Example:** An e-commerce platform always running a set of m5.large instances.

***

#### **3. Savings Plans**

* **How it works:** Commit to a **$ per hour spend** for 1 or 3 years. Apply across EC2, Fargate, and Lambda.
* **Types:**
  * **Compute Savings Plan:** Applies broadly to any instance/service.
  * **EC2 Instance Savings Plan:** Limited to family/region, bigger discount.
* **Pros:** Flexibility across services, big discounts.
* **Cons:** Commitment to spending, not tied to specific instances.
* **Use Case:** Organizations that want RI-level discounts but flexibility to use different compute services.
* **Example:** A SaaS company committing $20/hr for compute, spread across EC2 + Fargate.

***

#### **4. Spot Instances**

[spot-instances.md](spot-instances.md "mention")

* **How it works:** Bid on spare AWS capacity, with up to **90% discount**. AWS can reclaim capacity with 2-minute notice.
* **Pros:** Cheapest way to run EC2.
* **Cons:** Not reliable for critical workloads, can be interrupted.
* **Use Case:** Fault-tolerant workloads, batch jobs, CI/CD, big data processing, ML training.
* **Example:** A company running 1,000 nodes to render a 3D animation overnight.

***

#### **5. Dedicated Hosts & Dedicated Instances**

* **How it works:** Physical servers dedicated for your use, either host-level control (Dedicated Host) or isolated tenancy (Dedicated Instance).
* **Pros:** Compliance and licensing control.
* **Cons:** Expensive, less elastic.
* **Use Case:** Meeting regulatory requirements or Bring-Your-Own-License (BYOL) software.
* **Example:** A bank needing to run Oracle databases under strict licensing rules.

***

#### **6. Free Tier**

* **How it works:** New AWS accounts get **750 hours per month** of `t2.micro` or `t3.micro` for 12 months.
* **Pros:** Free way to learn or run small apps.
* **Cons:** Limited power and duration.
* **Use Case:** Beginners, students, prototyping.
* **Example:** A personal blog hosted on a free-tier EC2.

***

## **Quick Comparison Table**

| Pricing Model               | Discount vs On-Demand | Commitment              | Best For                            |
| --------------------------- | --------------------- | ----------------------- | ----------------------------------- |
| **On-Demand**               | None                  | None                    | Short-term, unpredictable workloads |
| **Reserved Instance**       | Up to 72%             | 1 or 3 years            | Steady-state workloads              |
| **Savings Plans**           | Up to 72%             | 1 or 3 years            | Flexible but predictable spend      |
| **Spot**                    | Up to 90%             | None, but interruptible | Fault-tolerant/batch workloads      |
| **Dedicated Host/Instance** | None (premium)        | Hourly or long-term     | Compliance/licensing needs          |
| **Free Tier**               | 100%                  | 12 months               | Testing/learning                    |

***

👉 If you’d like, I can **map each pricing option to real-world workload examples** (like web app, batch job, ML training, database, etc.) so you can see where each fits best. Want me to build that matrix?
