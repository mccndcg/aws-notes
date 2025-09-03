# Provisioned vs Reserved

{% hint style="success" %}
**Provisioned**: minimum

**Reserved**: maximum
{% endhint %}

|                           | Provisioned Concurrency                                                                                                           | Reserved Concurrency                                                                                                     |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Purpose                   | Guarantees that a specified number of function instances are initialized and ready to respond instantly, eliminating cold starts. | Limits the maximum number of concurrent executions for a function to prevent it from consuming too many resources.       |
| Effect on Performance     | Reduces latency significantly by keeping instances warm. Ideal for latency-sensitive applications.                                | Ensures a function always has some capacity, but does not prevent cold starts.                                           |
| Effect on Other Functions | Allocates a dedicated pool of "warm" instances that no other function can use, even when idle.                                    | Allocates a maximum share of the account's total concurrency, which other functions cannot use.                          |
| Cost                      | Incurs additional charges for the time instances are kept warm, even if idle.                                                     | No extra charge for the reservation itself. You pay only for standard Lambda invocation costs.                           |
| Use Cases                 | Real-time APIs, web applications, or other applications requiring consistent, low-latency performance.                            | Managing resource allocation for critical functions or preventing one function from consuming all available concurrency. |
