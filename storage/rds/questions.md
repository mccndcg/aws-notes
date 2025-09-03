# Questions

## EC2 + ALB + R53

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

```mermaid
flowchart TD
    subgraph Route53["Amazon Route 53 (DNS)"]
        R53["Alias Record → ALB"]
    end
subgraph PrimaryRegion["Primary Region"]
    ALB["Application Load Balancer"]
    ASG["EC2 Auto Scaling Group<br/>Across AZs"]
    RDS["Amazon RDS MySQL: Multi-AZ<br/>Read Replica Enabled"]
end

subgraph DRRegion["Disaster Recovery Region"]
    ALB_DR["Standby ALB - Disabled or Scaled-Down"]
    ASG_DR["EC2 Auto Scaling Group<br/>Warm Standby / Scaled-Down"]
    RDS_DR["Amazon RDS MySQL Read Replica<br/>Cross-Region"]
end

R53 --> ALB
ALB --> ASG
ASG --> RDS
ALB_DR --> ASG_DR
ASG_DR --> RDS_DR

RDS -.->|Cross-Region Replication ≤15 min RPO | RDS_DR
Route53 -.->|Failover Routing Policy| ALB_DR
```

#### **Pertinent Settings**

1. **Route 53**
   * Configure **Failover Routing Policy**:
     * Primary → ALB in primary region
     * Secondary → ALB in DR region
   * Enable **Health Checks** for ALB.
2. **EC2 + Auto Scaling**
   * **Primary Region**:
     * ASG sized for production load.
     * ALB with HTTPS listener, security groups allowing inbound from internet.
   * **DR Region**:
     * ASG in **warm standby mode** (minimal instances, scale-up on failover).
     * Preconfigured launch templates, IAM roles, and security groups.
3. **RDS**
   * **Primary Region**: Multi-AZ RDS MySQL for HA.
   * **Cross-Region Read Replica** in DR region.
   * Ensure replication lag ≤15 minutes to meet **RPO = 15 min**.
4. **Disaster Recovery Objectives**
   * **RTO (4 hours)**:
     * Warm standby allows scaling and promotion of DB replica within timeframe.
   * **RPO (15 minutes)**:
     * Achieved by cross-region RDS replication.

```
```
