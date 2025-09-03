# Security Account Delegation

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

Delegating AWS Firewall Manager to a security account means assigning a specific AWS member account, rather than the AWS Organizations management account, to centrally configure and manage firewall rules for all other accounts in the organization. How it works&#x20;

* Centralization of security: The delegated security account acts as the central point for creating and applying security policies for services like AWS WAF, AWS Shield Advanced, and AWS Network Firewall across the entire AWS Organization.
* Role-based access: By delegating, you can grant granular administrative permissions to security professionals without giving them access to the organization's management account.
* Separation of duties: This process separates the responsibilities for organization-wide account management (handled by the management account) from the day-to-day security and compliance tasks (handled by the delegated security account).&#x20;

## Benefits

* Enhanced security: Delegation enforces the principle of least privilege, as administrators in the security account only get permissions relevant to their security duties. This reduces the risk of accidental or malicious changes to the core organizational structure.
* Improved compliance and auditing: It provides clearer accountability for security-related actions. Audit logs will show that security policy changes came from the delegated security account, simplifying compliance reporting.
* Operational flexibility: Delegation allows different security teams to manage different policies or organizational units (OUs) from their designated security accounts, providing greater autonomy without sacrificing central control.&#x20;

## Multi-admin support

A delegated administrator account is a type of "multi-admin support." AWS allows you to create up to 10 Firewall Manager administrator accounts from within your AWS Organization, enabling you to scope responsibilities based on OUs, policy types, or AWS Regions.&#x20;
