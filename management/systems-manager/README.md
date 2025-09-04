# Systems Manager

{% stepper %}
{% step %}
### Definition

{% embed url="https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html" %}
{% endstep %}

{% step %}
### Example Deployment

{% embed url="https://docs.aws.amazon.com/systems-manager/latest/userguide/getting-started-launch-managed-instance.html" %}
{% endstep %}
{% endstepper %}

## Scope

{% hint style="info" %}
prompt: what services can systems manager monitor
{% endhint %}

Systems Manager doesn't actively "monitor" in the same way that Amazon CloudWatch or other dedicated services do. Instead, it provides tools to collect and act on data from the following services and resources:&#x20;

### AWS resources

Systems Manager uses the SSM Agent to manage a wide range of compute resources. For these "managed instances," it can gather data and perform actions.&#x20;

* Amazon EC2 instances: The primary target for Systems Manager. It can manage their configuration, collect inventory, install patches, and provide secure shell access.
* On-premises servers and virtual machines (VMs): By installing the SSM Agent and registering them through a Hybrid Activation, you can manage on-prem resources just like EC2 instances.
* Multi-cloud VMs: Similarly, you can use Systems Manager to extend management to virtual machines in other cloud environments.
* Containers: Through integration with Amazon Elastic Container Service (ECS) and Amazon Elastic Kubernetes Service (EKS) container insights, Systems Manager can display operational data and manage applications running in containers.
* Databases: For example, it can manage Microsoft SQL Server workloads deployed with AWS Launch Wizard.&#x20;



### Operational data from other AWS services

Systems Manager integrates with other AWS services to centralize operational data and provide a unified dashboard.

* AWS CloudTrail: Systems Manager can display API call logs from CloudTrail, giving you a history of changes to your resources.
* AWS Config: It can show resource configuration changes over time by pulling data from Config.
* Amazon CloudWatch: Dashboards in Systems Manager can be integrated with CloudWatch to show metrics, alarms, and logs.
* AWS Personal Health Dashboard: You can pull performance and availability alerts into your Systems Manager dashboard.
* AWS Organizations: For accounts within an AWS Organization, Systems Manager can offer a comprehensive, aggregated view of compliance and inventory.&#x20;
