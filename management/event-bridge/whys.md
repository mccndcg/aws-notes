# whys

{% hint style="warning" %}
how does eventbridge gather logs
{% endhint %}

AWS EventBridge is **not primarily a logging service**, so it doesn’t “gather logs” in the way CloudWatch does. Instead, it **collects and routes events**, which are structured messages representing state changes, actions, or notifications from AWS services, SaaS partners, or custom applications. Here’s a detailed breakdown:

***

#### 1. **Event Sources**

EventBridge ingests events from multiple sources:

| Source                        | Description                                                                                                   |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **AWS Services**              | Most AWS services can emit events automatically (e.g., S3 object created, CodeCommit push, EC2 state change). |
| **SaaS Partner Integrations** | SaaS apps like Shopify, Zendesk, PagerDuty can send events via EventBridge partner event sources.             |
| **Custom Applications**       | Developers can push custom events via the **AWS SDK**, **CLI**, or **API** to a custom event bus.             |
| **CloudWatch Alarms**         | CloudWatch alarms can act as event sources, triggering EventBridge rules when thresholds are breached.        |

#### 2. **Event Delivery / Routing**

1. **Event Ingestion**
   * Events are sent to an **Event Bus** (default, partner, or custom).
   * EventBridge automatically validates and timestamps each event.
2. **Filtering and Transformation**
   * **Rules** determine which events get routed to which targets.
   * Optional **input transformation** allows changing event content before delivery.
3. **Target Dispatch**
   * Events are delivered to one or more **targets**, such as Lambda, Step Functions, SQS, SNS, Kinesis, or API destinations.
   * Event delivery is near real-time.

***

#### 3. **Event Logging / Monitoring**

While EventBridge doesn’t collect logs per se, it **tracks events** and integrates with other AWS services for observability:

| Feature                    | Description                                                                                           |
| -------------------------- | ----------------------------------------------------------------------------------------------------- |
| **CloudWatch Metrics**     | Tracks number of events published, matched, or failed per event bus.                                  |
| **CloudTrail Integration** | Records API calls that put events onto EventBridge, providing an audit trail of event publishing.     |
| **Event Replay / Archive** | Allows storing events in an **archive** for later replay, useful for debugging or auditing workflows. |

💡 **Summary:**

* EventBridge **gathers events**, not logs.
* Sources can be **AWS services, SaaS apps, custom applications, or CloudWatch alarms**.
* Events are **routed, filtered, and optionally transformed** to targets.
* Observability is provided via **CloudWatch metrics** and **CloudTrail logging**, while archives allow replaying past events.
