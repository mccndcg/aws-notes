# Monitoring

You can utilize several AWS services to get updates from CloudFormation. Here are the main options:

### Amazon EventBridge (Primary Event Service)

**Real-time Event Streaming**: CloudFormation automatically sends events to EventBridge whenever stack operations occur. EventBridge is the primary service for receiving CloudFormation updates.

**Event Types Available**:

* **Resource Status Change**: Updates when individual resources are created, updated, or deleted
* **Stack Status Change**: Notifications when stack operations start, complete, or fail
* **Stack State Change**: General stack state transitions
* **Drift Detection Status Change**: Updates when drift detection operations complete
* **StackSet Status Change**: Changes to StackSet operations
* **StackSet Stack Instance Status Change**: Updates to individual stack instances
* **StackSet Operation Status Change**: StackSet operation progress
* **Hook Invocation Progress**: Updates from CloudFormation hooks

**Event Pattern Example**:

```
{
  "source": ["aws.cloudformation"],
  "detail-type": ["CloudFormation Stack Status Change"]
}

```

### Amazon Simple Notification Service (SNS)

**Direct Integration**: You can configure CloudFormation stacks to send notifications directly to SNS topics.

**Use Cases**:

* Email notifications for stack operations
* SMS alerts for critical stack failures
* Integration with chat applications and ticketing systems
* Webhook notifications to external systems

### AWS CloudTrail

**API Call Tracking**: CloudTrail captures all CloudFormation API calls and can trigger events.

**Event Pattern for CloudTrail Events**:

```
{
  "source": ["aws.cloudformation"],
  "detail-type": ["AWS API Call via CloudTrail"],
  "detail": {
    "eventSource": ["cloudformation.amazonaws.com"]
  }
}
```

### Amazon CloudWatch

**Metrics and Alarms**: CloudWatch can monitor CloudFormation metrics and trigger alarms.

**Capabilities**:

* Monitor stack operation duration
* Track resource creation/deletion counts
* Set up alarms for failed operations
* Custom metrics from CloudFormation events

### Integration Patterns

**EventBridge + Lambda**: Use EventBridge rules to trigger Lambda functions for custom processing of CloudFormation events.

**EventBridge + SNS**: Route CloudFormation events through EventBridge to SNS for notifications.

**EventBridge + SQS**: Queue CloudFormation events for batch processing.

**EventBridge + Step Functions**: Trigger complex workflows based on stack operations.

### Event Details Available

**Stack Information**:

* Stack ID and name
* Stack status and state
* Operation timestamps
* Client request tokens

**Resource Information**:

* Resource types and logical IDs
* Resource status changes
* Drift detection results
* Resource counts

**Error Information**:

* Failure reasons
* Status details
* Operation results

### Best Practices

**Event Filtering**: Use EventBridge event patterns to filter for specific stack names, resource types, or operation types.

**Multiple Targets**: Configure EventBridge rules to send the same event to multiple targets (SNS, Lambda, SQS, etc.).

**Error Handling**: Implement dead letter queues and retry logic for event processing.

**Monitoring**: Set up CloudWatch alarms to monitor your event processing systems.

EventBridge is the most comprehensive solution as it provides real-time, structured events with detailed information about all CloudFormation operations, making it the recommended primary service for getting CloudFormation updates.
