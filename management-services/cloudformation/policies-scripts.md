# Policies, scripts

## AWS Docs

{% stepper %}
{% step %}
### Concepts

{% embed url="https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/cfn-helper-scripts-reference.html" %}
{% endstep %}
{% endstepper %}

{% hint style="info" %}
prompt: give me sample questions in the aws devops exam regarding cloudformation scripts such as cfn-signal
{% endhint %}

## CreationPolicy

Scenario: A CloudFormation template creates an Auto Scaling group of EC2 instances. A user data script on each instance downloads, installs, and configures a large application that takes approximately 10 minutes to complete. The CloudFormation stack consistently rolls back with the error message `Received 0 SUCCESS signal(s) out of 1`. Which two actions should a DevOps engineer take to ensure the stack successfully completes? (Choose two.)&#x20;

A. Update the Auto Scaling group resource with a `DependsOn` attribute pointing to a new `AWS::CloudFormation::WaitConditionHandle` resource.\
B. Add a `CreationPolicy` with a `Timeout` of 15 minutes to the Auto Scaling group resource.\
C. Add a `LifecycleHook` resource to the Auto Scaling group to pause instance creation.\
D. Update the user data script to run the `cfn-signal` helper script with the success status once the application installation is complete.\
E. Add a `WaitCondition` resource with a `Timeout` of 15 minutes that is signaled by the user data script.&#x20;

Correct Answers (B and D): To prevent premature stack completion, you must configure a `CreationPolicy` on the resource to wait for a success signal. The `Timeout` value should be long enough for the user data script to finish. The script itself must then explicitly send the `SUCCESS` signal using the `cfn-signal` command.&#x20;

## UpdatePolicy

Scenario: A team is using a CloudFormation template to manage an Auto Scaling group. They update the template to change a software version in the `AWS::CloudFormation::Init` metadata. After applying the stack update, the instances are replaced, but the stack immediately reports `UPDATE_COMPLETE`, even though the new application is still installing. This can lead to service outages. How can the DevOps engineer ensure the stack update only completes after the new instances are successfully updated and ready?&#x20;

A. Implement a `RollingUpdate` policy with a `WaitOnResourceSignals` attribute on the Auto Scaling group, and ensure the `cfn-signal` script is called in the user data.\
B. Set the `MinSuccessfulInstancesPercent` property to 100 within the `UpdatePolicy` of the Auto Scaling group.\
C. Create a `LifecycleHook` resource to pause the Auto Scaling group during the instance update and use the `complete-lifecycle-action` command.\
D. Create an Amazon CloudWatch alarm to track the health of the target group and add a `WaitCondition` that monitors the alarm state. Explanation:

Correct Answer (A): For updates, you use an `UpdatePolicy`. Specifically, a `RollingUpdate` policy with `WaitOnResourceSignals` will cause CloudFormation to pause the update process until it receives the required signals from the new instances. The `cfn-signal` command, called by the user data (or `cfn-init`), sends these signals.&#x20;

## Troubleshooting signals

Scenario: During the creation of an Auto Scaling group, the CloudFormation stack fails with a timeout error, indicating it never received a signal. A DevOps engineer investigates and finds that the instances are being created and the `cfn-init` script is running. What is a common cause for this type of error?&#x20;

A. The IAM role attached to the EC2 instances does not have permissions to write to the CloudFormation API endpoint.\
B. The security group associated with the EC2 instances is blocking outbound traffic to the CloudFormation API endpoint.\
C. The `cfn-signal` command is missing the `--resource` or `--stack` parameters.\
D. The `cfn-init` script failed to run the `cfn-signal` command due to a syntax error.

Correct Answers (C and potentially B): This is a troubleshooting question that requires knowledge of the helper script's dependencies.

* C is the most likely cause. For `cfn-signal` to work, it must be provided with the correct `stack-name` and `resource` logical ID to signal. The `--stack` and `--resource` parameters are crucial.
* B is a possible cause, especially in custom VPC configurations. The instance must be able to reach the public internet (or a VPC endpoint) to communicate with the CloudFormation service and send the signal.&#x20;

## Concepts

* `CreationPolicy` vs. `UpdatePolicy`: Know when to use each to control stack completion behavior for new resource creation versus updates.
* `cfn-signal`: Understand its purpose (to send a success or failure signal) and how it must be paired with a waiting policy.
* `cfn-init`: Understand that `cfn-init` is used for instance configuration and that `cfn-signal` is typically called at the end of the `cfn-init` process to report success.
* `WaitOnResourceSignals`: Know that this is the specific `UpdatePolicy` attribute that instructs CloudFormation to wait for signals during a rolling update.
* Troubleshooting: Be able to identify common reasons for signaling failures, such as networking issues, missing IAM permissions, or incorrect helper script parameters.&#x20;
