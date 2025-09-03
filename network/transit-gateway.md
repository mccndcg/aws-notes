---
description: Central hub for large-scale VPC and hybrid network connectivity.
---

# Transit Gateway

## **Definition**

Transit Gateway is a managed AWS service that acts as a scalable routing hub, enabling thousands of VPCs, on-premises networks, and remote branches to interconnect using a hub-and-spoke model. It replaces complex VPC peering meshes, supports transitive routing, integrates with Direct Connect and VPNs, and provides centralized policy and monitoring for traffic flow.

## Comparisons

| Service              | Similarity to TGW                                                    | Difference from TGW                                                            |
| -------------------- | -------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| **VPC Peering**      | Connects VPCs privately without traversing the internet.             | One-to-one only, no transitive routing, hard to scale with many VPCs.          |
| **PrivateLink**      | Provides private connectivity without public internet exposure.      | Service-to-service access only (via ENIs), not full VPC routing.               |
| **Site-to-Site VPN** | Extends AWS networks to on-premises securely.                        | Point-to-point only, limited bandwidth, higher latency vs. TGW’s scalable hub. |
| **Direct Connect**   | Enables hybrid connectivity between AWS and data centers.            | Dedicated physical link, not a routing hub—best paired with TGW for scale.     |
| **Cloud WAN**        | Provides centralized, managed network for connecting VPCs and sites. | Global scope with orchestration and policies; TGW is regional and manual.      |

## Cross-cloud Equivalents

| Cloud Provider   | Similar Service                                            | Description / Key Difference                                                                                                                                                                                                                                  |
| ---------------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Google Cloud** | **Cloud Interconnect + Network Connectivity Center (NCC)** | NCC is Google’s hub-and-spoke model for connecting VPCs and hybrid networks. Works with Cloud Interconnect for private physical links. TGW and NCC are conceptually similar, but NCC is newer and less feature-rich for large-scale multi-account setups.     |
| **Azure**        | **Azure Virtual WAN (vWAN)**                               | Provides centralized hub for connecting VNets, on-premises, and remote users. Includes VPN, ExpressRoute (Direct Connect equivalent), and firewall integration. More global by design compared to TGW, which is region-scoped (unless paired with Cloud WAN). |
