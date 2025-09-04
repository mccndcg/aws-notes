# Change Mgmt. Tools

## AWS Docs

{% stepper %}
{% step %}
### List

{% embed url="https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-actions-and-change.html" %}
{% endstep %}
{% endstepper %}

## Summary

| Tool                    | What It Does (Terse)                                                                                      | When You’d Use It                                                                                                                                                                                                                                                        |
| ----------------------- | --------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Automation**          | Executes predefined workflows ("runbooks") to make safe, repeatable changes to AWS resources.             | Use to standardize and automate repetitive ops tasks like AMI creation, backups, or EC2 restarts. ([AWS Documentation](https://docs.aws.amazon.com/es_es/whitepapers/latest/aws-systems-manager-operational-capabilities/change-management.html?utm_source=chatgpt.com)) |
| **Change Calendar**     | Defines date/time windows when change actions can or cannot occur (like blackout or maintenance periods). | Use when you need to restrict changes during business-critical periods (e.g., holiday season or service events). ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-tools.html?utm_source=chatgpt.com))                   |
| **Maintenance Windows** | Schedules recurring or one-time tasks (like patching or script runs) on a defined schedule.               | Use to ensure maintenance tasks run only during approved times to minimize disruption. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-tools.html?utm_source=chatgpt.com))                                             |
| **Change Manager**      | Offers an enterprise-scale workflow for requesting, approving, and reporting changes using Automation.    | Use when you require structured change approvals, audit trails, calendar gating, and multi-account coordination. ([AWS Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/change-manager.html?utm_source=chatgpt.com))                          |
