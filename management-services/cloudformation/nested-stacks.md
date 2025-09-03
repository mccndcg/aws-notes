# Nested Stacks

## AWS Docs

{% stepper %}
{% step %}
Split template into reusable pieces

{% embed url="https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-nested-stacks.html" %}

{% embed url="https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/resource-import-nested-stacks.html" %}
{% endstep %}
{% endstepper %}

A **nested stack** in AWS CloudFormation is essentially a **stack within a stack**. It allows you to break complex architectures into smaller, reusable components. Here’s a detailed breakdown:

***

## **Definition**

* A **nested stack** is a **CloudFormation stack defined as a resource inside another parent stack**.
* It references a separate template (child template) from the parent stack.
* The parent stack manages the creation, update, and deletion of all its nested stacks automatically.

***

## **Why Use Nested Stacks**

1. **Modularity:**
   * Break large infrastructure into smaller, reusable templates.
   * Each nested stack can represent a logical part of your architecture, e.g., networking, databases, or compute resources.
2. **Reusability:**
   * Use the same nested stack in multiple parent stacks.
   * Example: A “VPC template” can be reused across multiple environments (dev, staging, prod).
3. **Simplified Maintenance:**
   * Changes to a child template can be updated independently without rewriting the entire parent template.
4. **Stack Limits Management:**
   * AWS CloudFormation has a **limit on the number of resources per stack** (currently 500).
   * Nested stacks help you **work around resource limits** by splitting resources across child stacks.

***

## **How It Works**

1. Create a **child template** (e.g., networking.yml defining a VPC and subnets).
2. In the **parent template**, include a **`AWS::CloudFormation::Stack` resource** pointing to the child template.
3. When you create the parent stack:
   * CloudFormation automatically creates the nested stacks as resources.
   * Updates or deletions of the parent stack propagate to the nested stacks.

***

## **Example Use Case**

* **Scenario:** Deploying a 3-tier web application.
* **Parent Stack:** “WebAppStack”
* **Nested Stacks:**
  * `NetworkingStack` → VPC, subnets, security groups
  * `DatabaseStack` → RDS instances and backups
  * `ApplicationStack` → EC2 instances, Auto Scaling Groups, and load balancers
* **Benefit:** Each nested stack can be updated independently, reused for other apps, and keeps the parent template clean and manageable.

***

## **Key Points**

| Feature                  | Explanation                                                                                            |
| ------------------------ | ------------------------------------------------------------------------------------------------------ |
| **Resource Management**  | Nested stacks behave like normal resources in the parent stack.                                        |
| **Outputs & Parameters** | Child stack outputs can be referenced by the parent stack using `!GetAtt` or `Outputs`.                |
| **Rollback & Updates**   | Parent stack controls rollback; if a nested stack fails, the parent stack can automatically roll back. |
| **Limits**               | Nested stacks count towards the parent stack’s resource limit, but help organize resources better.     |

***
