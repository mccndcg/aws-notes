# gp2 vs gp3

## **gp2 vs gp3**

| Feature                 | **gp2**                            | **gp3**                                                   |
| ----------------------- | ---------------------------------- | --------------------------------------------------------- |
| **Baseline IOPS**       | 3 IOPS per GiB (up to 16,000 IOPS) | Fixed 3,000 IOPS (independent of size)                    |
| **Throughput**          | Up to 250 MB/s                     | 125 MB/s baseline, up to 1,000 MB/s (configurable)        |
| **Performance Scaling** | Performance tied to volume size    | Performance decoupled from size (configure independently) |
| **Cost**                | Older pricing model                | \~20% cheaper                                             |
| **Bursting**            | Yes (small volumes can burst IOPS) | No “bursting” model — baseline is already higher          |

***

## **Why gp2 Still Exists**

1. **Legacy Use**
   * Many older workloads were provisioned on `gp2`.
   * Customers may keep them for stability or compatibility (instead of migrating).
2. **Migration Overhead**
   * Moving from `gp2` to `gp3` is easy (via Elastic Volumes), but in regulated or production-critical environments, **even a small migration can require testing, approval, and downtime planning**.
3. **Burst Behavior**
   * Small `gp2` volumes (e.g., 100 GiB) can **burst to 3,000 IOPS temporarily** due to burst credits.
   * If your workload is **low most of the time but occasionally spikes**, `gp2`’s burst model can be “good enough” without reconfiguring IOPS on `gp3`.

***

## Exam Angle

* AWS wants you to know: **gp3 is the recommended default**.
* The only reasons to stay on `gp2` are:
  1. **Legacy compatibility**.
  2. **Burst-friendly small workloads** that don’t justify custom IOPS on `gp3`.

***

So, in real life and in the exam:

* If you see a **new workload** → **gp3**.
* If you see a **migration scenario** where they ask “should you move from gp2 to gp3?” → Yes, unless specifically blocked by compatibility.
