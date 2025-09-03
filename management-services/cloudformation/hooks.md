# Hooks

## AWS Docs

{% stepper %}
{% step %}
### Concepts

{% embed url="https://docs.aws.amazon.com/cloudformation-cli/latest/hooks-userguide/hooks-concepts.html" %}
{% endstep %}

{% step %}
### Guard Hooks

{% embed url="https://docs.aws.amazon.com/cloudformation-cli/latest/hooks-userguide/guard-hooks-write-rules.html" %}
{% endstep %}
{% endstepper %}

CloudFormation hooks have **limited response capabilities** - they primarily serve as **validation and enforcement mechanisms** rather than automatic correction tools. Here's how they work:

## Hook Response Actions

CloudFormation hooks can respond in **two ways** when they detect issues:

#### 1. **WARN Mode**

* Issues warnings to users but **allows the operation to continue**
* Useful for non-critical validations or informational checks
* The stack operation proceeds despite the hook detecting non-compliance

#### 2. **FAIL Mode**

* **Prevents the action from proceeding entirely**
* Stops provisioning resources and can trigger stack rollback
* Helpful for enforcing strict compliance or security policies

## What Hooks Cannot Do

**No Automatic Corrections**: CloudFormation hooks **cannot automatically fix or correct** non-compliant configurations. They can only:

* Inspect and validate resource configurations before provisioning
* Either allow the operation to continue (WARN) or stop it entirely (FAIL)

**No Resource Modification**: Hooks cannot modify the template, change resource properties, or make corrections to bring resources into compliance.

## Hook Capabilities

**Proactive Validation**: Hooks run **immediately before** CloudFormation creates, updates, or deletes stacks or resources, providing early detection of issues.

**Inspection Only**: They can inspect:

* Templates
* Resource configurations
* Change sets
* Stack properties

**Binary Decision**: Hooks make a simple pass/fail decision - they cannot perform remediation actions.

## Alternative Approaches for Corrections

If you need automatic corrections, you would need to implement them **outside of hooks**:

**Custom Resources**: Use Lambda-backed custom resources that can perform corrective actions during stack operations.

**Separate Remediation Process**: Create a separate workflow that:

1. Uses hooks to detect issues (WARN mode)
2. Triggers external remediation processes
3. Re-runs the stack operation after corrections

**Template Preprocessing**: Modify templates before submission to CloudFormation to ensure compliance.

In summary, CloudFormation hooks are **validation and enforcement tools**, not correction mechanisms. They can stop operations or issue warnings, but they cannot automatically fix non-compliant configurations.

```mermaid
flowchart TD
    Start[Start Stack Operation -Create/Update/Delete-] --> IdentifyHooks[Identify Hook Configurations for Resources]

    IdentifyHooks --> CheckActions[Does Hook Target Current Action?]

    CheckActions -->|Yes| InvokeHook[Invoke Hook Handler]
    CheckActions -->|No| SkipHook[Skip Hook]

    InvokeHook --> EvaluateResource[Check Resource Properties / Policy]

    EvaluateResource -->|Pass| NextResource[Proceed to Next Resource / Stack Operations]
    EvaluateResource -->|Fail| BlockStack[Block Stack Operation / Trigger Rollback]

    NextResource --> MoreResources{More Resources with Hooks?}
    MoreResources -->|Yes| IdentifyHooks
    MoreResources -->|No| ContinueStack[Continue Normal Stack Creation / Update]

    SkipHook --> NextResource

    ContinueStack --> Complete[Stack Operation Complete]
    BlockStack --> Rollback[Rollback Stack if enabled]
    Rollback --> End[Stack Operation Halted / Rolled Back]
    Complete --> End --> IdentifyHooks[Identify Hook Configurations for Resources]

    IdentifyHooks --> InvokeHook[Invoke Hook Handler]
    InvokeHook --> EvaluateResource[Check Resource Properties / Policy]

    EvaluateResource -->|Pass| NextResource[Proceed to Next Resource / Stack Operations]
    EvaluateResource -->|Fail| BlockStack[Block Stack Operation / Trigger Rollback]

    NextResource --> MoreResources{More Resources with Hooks?}
    MoreResources -->|Yes| InvokeHook
    MoreResources -->|No| ContinueStack[Continue Normal Stack Creation / Update]

    ContinueStack --> Complete[Stack Operation Complete]
    BlockStack --> Rollback[Rollback Stack if enabled]
    Rollback --> End[Stack Operation Halted / Rolled Back]
    Complete --> End

```
