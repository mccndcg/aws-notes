# Network - NAT Gateway

### Definition

A **NAT Gateway** is an AWS Network Address Translation (NAT) service that allows resources in a private subnet to initiate outbound traffic to the internet or other AWS services, while simultaneously preventing any inbound, unsolicited traffic from the internet. Think of it like a one-way security checkpoint for your network.

***

### How a NAT Gateway works

1. Outbound traffic: A resource in a private subnet (like an EC2 instance or a Lambda function) sends an outbound request to the internet.
2. Network address translation: The traffic is routed to the NAT Gateway, which replaces the resource's private IP address with the NAT Gateway's public Elastic IP address.
3. Traffic sent to internet: The NAT Gateway then sends the request to its internet destination on behalf of the private resource.
4. Inbound traffic (response only): When the external service sends a response, it comes back to the NAT Gateway's public IP address. The NAT Gateway remembers which private resource initiated the request and forwards the response back to it, translating the IP address back to the original private one.
5. No unsolicited inbound traffic: The NAT Gateway is stateful, meaning it only allows traffic that is a response to a request initiated from within the private subnet. It automatically blocks any new, unsolicited inbound connection attempts from the internet.&#x20;

***

### Key takeaways

* Purpose: A NAT Gateway is used to provide internet access to resources in private subnets without compromising security by exposing them to the public internet.
* Placement: The NAT Gateway itself is deployed in a public subnet, and its public IP is attached to an Elastic IP address.
* Route table: You configure the route table for your private subnet to direct all internet-bound traffic (destination `0.0.0.0/0`) to the NAT Gateway.
* Managed service: It is a managed AWS service that is highly available and automatically scales to meet traffic demands. This saves you from the overhead of managing your own NAT instances.&#x20;
