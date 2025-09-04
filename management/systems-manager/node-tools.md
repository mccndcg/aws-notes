# Node Tools

{% stepper %}
{% step %}
### List

{% embed url="https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-instances-and-nodes.html" %}
{% endstep %}
{% endstepper %}

{% hint style="info" %}
prompt: create a terse description of aws system manager node tools
{% endhint %}

## Description

* **What they are:**\
  A set of lightweight agents and plugins installed on EC2 instances, on-prem servers, or hybrid machines that allow AWS Systems Manager (SSM) to manage and automate them.
* **Key components:**
  * **SSM Agent** – runs on the node to process commands and automation.
  * **Session Manager Plugin** – enables secure shell access without SSH keys.
  * **Distributor Packages** – deliver and update software/agents.
* **Use case:**\
  Required for running Systems Manager features like **Run Command, Session Manager, Patch Manager, State Manager, and Inventory** on your instances.

## Components

| Tool               | What it does                                                                                                                                                                                                                                             | When you’d use it                                                                                                                                                                                                                                    |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Compliance         | Scans managed nodes for patch/association compliance; aggregates across accounts/Regions and can trigger remediation. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-compliance.html))                | You need a fleet-wide view of what’s noncompliant and to kick off fixes via Run Command/State Manager/EventBridge. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-compliance.html))               |
| Distributor        | Packages and publishes software/agents to managed nodes; installs one-off (Run Command) or on a schedule (State Manager). ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/distributor.html))                           | You want to deploy or update in-house or AWS/third-party agents across Windows/Linux fleets. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/distributor.html))                                                    |
| Fleet Manager      | Unified UI to view health, troubleshoot, and perform common management tasks on AWS and on-prem nodes. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/fleet-manager.html?utm_source=chatgpt.com))                     | You need point-and-click fleet ops (file system, logs, local users, services) without SSH/RDP. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/fleet-manager-manage-os-user-accounts.html?utm_source=chatgpt.com)) |
| Hybrid Activations | Registers non-EC2 machines (on-prem, other clouds, edge devices/VMs) as managed nodes using activation code/ID. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/activations.html))                                     | You must bring external servers/devices under SSM management (often with advanced-instances tier). ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/activations.html))                                              |
| Inventory          | Collects/centralizes node metadata (apps, files, network, services, tags), stores in S3, query via Athena; supports custom inventory. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-inventory.html)) | You need searchable asset/config data across fleets for audits, queries, and change tracking. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-inventory.html))                                     |
| Patch Manager      | Automates OS/app patching; uses patch policies/baselines; scan or scan-and-install; produces compliance reports. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager.html))                                  | You want scheduled, controlled patching across accounts/Regions with compliance visibility. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager.html))                                                   |
| Run Command        | Remotely and securely run commands/scripts at scale on managed nodes (one-time admin/config tasks). ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/run-command.html))                                                 | You need ad-hoc changes (install, bootstrap, gather logs, join domain) without opening inbound ports. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/run-command.html))                                           |
| Session Manager    | Browser/CLI interactive shell and port forwarding with no inbound ports/bastions/SSH keys; rich logging options. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html))                                | You want just-in-time, auditable access to nodes (EC2 or hybrid) with PrivateLink/VPC endpoints. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html))                                            |
| State Manager      | Keeps resources in a desired state via “associations” (targeting + schedule); pairs well with Automation. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-state.html?utm_source=chatgpt.com))          | You need ongoing, hands-off configuration enforcement (e.g., ensure agents/services/ports are set). ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-state.html?utm_source=chatgpt.com))            |
