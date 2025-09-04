# Dedicated Host/Instace

Both **Dedicated Instances** and **Dedicated Hosts** give you physical isolation, but the **level of control** differs.

***

### **Dedicated Instance**

* Runs on hardware that is physically isolated for your account.
* AWS **manages the underlying host**; you don’t see or control it.
* You get **instance-level isolation**, but not visibility into sockets/cores.
* Pricing: small premium over shared On-Demand.
* Use case: compliance or licensing that requires instance isolation.

***

### **Dedicated Host**

* Gives you a **whole physical server** allocated to your account.
* You control **placement of instances** on the host.
* Provides **visibility into sockets, cores, and host-level topology**.
* You can bring your own licenses (BYOL) that are tied to physical cores/sockets (e.g., Oracle, SQL Server, Windows Server).
* Pricing: higher cost, but efficient if you pack many VMs onto the host.
* Use case: strict compliance, BYOL, or software vendors that require hardware affinity.

***

### **Comparison Table**

| Feature        | **Dedicated Instance**                          | **Dedicated Host**                                     |
| -------------- | ----------------------------------------------- | ------------------------------------------------------ |
| **Isolation**  | Yes (hardware dedicated to you, but abstracted) | Yes (entire host dedicated, visible to you)            |
| **Control**    | AWS places your instance on isolated hardware   | You control instance placement on host                 |
| **Visibility** | No visibility into host hardware                | Full visibility (sockets, cores, host IDs)             |
| **Licensing**  | AWS-managed licenses                            | Supports BYOL (core/socket-based)                      |
| **Pricing**    | Slightly more than standard On-Demand           | Higher, but cost-effective if fully utilized           |
| **Best For**   | Compliance with minimal overhead                | Compliance + BYOL + optimization via packing instances |

***

#### **Quick Example**

* If you just need your workloads **not to share a host with other customers** → **Dedicated Instance** is enough.
* If your vendor says _“license per physical core”_ or you need to manage placement → you need a **Dedicated Host**.

