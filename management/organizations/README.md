---
description: Centralized account and policy management for multiple AWS accounts./h1
---

# Organizations

## **Definition**

AWS Organizations is a service that allows you to centrally create, group, and manage multiple AWS accounts. It provides consolidated billing, service control policies (SCPs), and account governance. Organizations is essential for enterprises to enforce security, compliance, and cost management across environments at scale.

## Capabilities & Where to Configure

| Capability                                                                                                                  | Pertinent Setting / Location                                              |
| --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| **Multi-Account Management** Create, invite, or remove AWS accounts and manage them under a single organization.            | **Organizations Console → Accounts**                                      |
| **Organizational Units (OUs)** Group accounts hierarchically for easier policy application and governance.                  | **Organizations Console → Organizational units**                          |
| **Consolidated Billing** Combine charges from all accounts into a single bill with shared volume discounts.                 | **Billing Console → Payer Account → Linked Accounts**                     |
| **Service Control Policies (SCPs)** Define guardrails that restrict what actions accounts can perform, regardless of IAM.   | **Organizations Console → Policies → Service Control Policies**           |
| **Tag Policies** Enforce consistent tagging across accounts for cost allocation and compliance.                             | **Organizations Console → Policies → Tag Policies**                       |
| **AI Services Opt-out Policies** Control whether accounts can use AWS AI/ML services for privacy/security reasons.          | **Organizations Console → Policies → AI services opt-out**                |
| **Backup Policies** Standardize backup rules and schedules across multiple accounts.                                        | **Organizations Console → Policies → Backup Policies**                    |
| **Delegated Administrator Accounts** Assign a member account to manage specific AWS services at the org level.              | **Organizations Console → Settings → Delegated administrators**           |
| **Integration with AWS SSO / IAM Identity Center** Centralize workforce authentication and map user access across accounts. | **IAM Identity Center Console → Settings → AWS Organization Integration** |
| **CloudTrail Organization Trails** Capture and consolidate API activity logs across all accounts for auditing.              | **CloudTrail Console → Trails → Organization Trails**                     |

## Common Integrations

* **Input (services feeding into Organizations):**
  * **IAM** – Defines roles and permissions within each account.
  * **Billing/Cost Explorer** – Supplies usage and cost data to be consolidated.
  * **Control Tower** – Automates account creation and enrollment into Organizations.
* **Process (services that interact with Organizations policies):**
  * **Service Control Policies (SCPs)** – Apply guardrails across accounts.
  * **Tag Policies** – Standardize resource tagging across the org.
  * **CloudFormation StackSets** – Deploy stacks across multiple accounts.
* **Output (services that consume Organizations structure/policies):**
  * **AWS SSO (IAM Identity Center)** – Centralized access mapped to org accounts.
  * **Security Hub / GuardDuty** – Use Organizations to manage security findings org-wide.
  * **CloudTrail** – Consolidates audit logs across accounts.
