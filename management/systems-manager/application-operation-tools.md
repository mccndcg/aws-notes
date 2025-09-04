# Application/Operation Tools

## AWS Docs

{% stepper %}
{% step %}
### Application

{% embed url="https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-application-management.html" %}
{% endstep %}

{% step %}
### Operations

{% embed url="https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-ops-center.html" %}
{% endstep %}
{% endstepper %}

## Application Tools

| Tool                    | What It Does (Terse)                                                                                                                                                                                                                                                                                                                                   | When You’d Use It                                                                                                   |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------- |
| **AWS AppConfig**       | Safely deploy feature flags and configuration changes with validation, phased rollouts, and auto-rollback. ([AWS Documentation](https://docs.aws.amazon.com/appconfig/latest/userguide/what-is-appconfig.html?utm_source=chatgpt.com), [Amazon Web Services, Inc.](https://aws.amazon.com/systems-manager/features/appconfig/?utm_source=chatgpt.com)) | Use when you need real-time config updates or gradual feature rollouts without redeployment.                        |
| **Application Manager** | Discovers and groups app resources, displays health, logs, alarms, compliance, and costs in one place. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/application-manager.html?utm_source=chatgpt.com))                                                                                                             | Use when you want an app-centric overview and management interface across CloudFormation, ECS/EKS, and alarms.      |
| **Parameter Store**     | Secure, hierarchical storage for configs and secrets (String, SecureString), with versioning, labels, validation, notifications, and sharing. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html?utm_source=chatgpt.com))                                                          | Use to centrally store and retrieve configuration values or secrets, including version control and access policies. |

## Operation Tools

| Tool                 | What It Does (Terse)                                                                                                                                                                                                                                                                                                                                                                                                           | When You’d Use It                                                                               |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------- |
| **Explorer**         | Aggregates OpsData (inventory, Config, patch compliance, OpsItems, etc.) across accounts/regions into a customizable dashboard. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/Explorer.html?utm_source=chatgpt.com), [Amazon Web Services, Inc.](https://aws.amazon.com/blogs/aws/aws-systems-manager-explorer-a-multi-account-multi-region-operations-dashboard/?utm_source=chatgpt.com)) | Use for high-level visibility, trends, and multi-account health monitoring.                     |
| **Incident Manager** | Automates incident response—detection, escalation, runbooks, notifications, chat, and post-incident actions. ([Amazon Web Services, Inc.](https://aws.amazon.com/systems-manager/features/incident-manager/?utm_source=chatgpt.com), [AWS Documentation](https://docs.aws.amazon.com/incident-manager/latest/userguide/what-is-incident-manager.html?utm_source=chatgpt.com))                                                  | Use when you need structured incident response workflows with automation and communication.     |
| **OpsCenter**        | Central hub for viewing, investigating, and resolving operational work items (OpsItems); integrates alerts and remediation runbooks. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/OpsCenter.html?utm_source=chatgpt.com), [AWS Workshop](https://mng.workshop.aws/ssm/capability_hands-on_labs/opscenter.html?utm_source=chatgpt.com))                                                    | Use when you want to centralize and manage operational issues across services in one interface. |
