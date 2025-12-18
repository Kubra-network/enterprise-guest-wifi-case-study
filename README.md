# Enterprise Guest Wi-Fi Case Study  

### Multi-Branch Retail Environment with Analytics Insights – Aruba Central (Cloud) & ALE

## Disclaimer
This case study is a **conceptual design** created for demonstration and learning purposes.  
It does not represent a real customer deployment and contains **no confidential or proprietary information**.

---

## Overview

Providing guest Wi-Fi in a single location is simple.  
Providing a **secure, seamless, and scalable guest Wi-Fi experience across multiple branches** is not.

This case study documents an **enterprise-level guest Wi-Fi design** for a multi-branch retail environment, focusing on:
- seamless guest experience across locations
- strong network isolation
- centralized cloud-based management
- privacy-aware analytics

---

## Environment & Scale

- **Industry:** Retail / Coffee Shop
- **Number of branches:** 20
- **AP density:** ~5 APs per branch
- **Management platform:** Aruba Central (Cloud)
- **Wireless access:** Aruba IAPs (Central-managed)

---

## Requirements

### Functional Requirements
- Guests authenticate once and are automatically recognized across all branches for **3 days**
- No repeated login when visiting different locations
- Consistent user experience across all branches

### Operational Requirements
- Centralized management and policy enforcement
- No per-branch SSID or captive portal configuration
- Scalable design suitable for growth

### Security & Compliance
- Full isolation between guest and corporate networks
- Internet-only access for guest users
- Anonymized analytics aligned with privacy regulations (KVKK / GDPR)

---

## High-Level Architecture

- **Access Layer:** Aruba IAPs
- **Management & Control Plane:** Aruba Central
- **Authentication:** Cloud-hosted Captive Portal
- **Segmentation:** Dedicated Guest VLAN (Isolated)
- **Analytics & Location Services:** Aruba Central Analytics + Aruba Location Engine (ALE)

---

- Guest traffic is fully separated from the corporate LAN
- No east-west traffic between guest clients
- Only northbound internet access is permitted

---

## SSID & Segmentation Design

### SSID
- **SSID Name:** `HaveSomeCoffee-Guest`
- Single SSID broadcast across all branches
- Centrally managed via Aruba Central

### VLAN
- Dedicated **Guest VLAN**
- Same VLAN ID across all branches for consistency
- Assigned dynamically using role-based policies

> Guest clients will be in the isolated Guest VLAN even after authentication, ensuring that user experience improvements do not weaken security.

---

## Authentication & Guest Recognition Flow

1. Guest connects to the `HaveSomeCoffee-Guest` SSID
2. Client is redirected to a **central captive portal**
3. Initial authentication is completed (click-through / SMS / policy-based)
4. Client is:
   - marked as authenticated
   - assigned a **Guest Role**
   - placed into the **Guest VLAN**
5. Client is automatically recognized across all branches for **3 days** without re-authentication

---

## MAC-Based Recognition (UX Optimization)

- MAC-based client recognition is used to support **seamless connection for dedicated time**
- Client MAC addresses are cached centrally for the defined validity period
- Modern client devices use **per-SSID MAC randomization**, which still enables consistent recognition as long as the SSID remains the same across all branches
- **No user-side configuration is required**

> MAC-based recognition is used solely to improve user experience and is not treated as a strong authentication mechanism.

---

## Role-Based Policy Enforcement

### Guest Role Characteristics
- Dynamic VLAN assignment → Guest VLAN
- Access restrictions:
  - ❌ Corporate / internal subnets
  - ❌ Lateral client access
  - ✅ Internet access (HTTP / HTTPS / DNS)
- Optional bandwidth shaping
- Session lifetime aligned with the 3-day guest validity period

This approach provides centralized control and predictable behavior across all branches.

---

## Security Considerations

- **Network Isolation:** Guest and corporate traffic are fully separated
- **Policy Consistency:** Central ACL enforcement via Aruba Central
- **Spoofing Risk Mitigation:** Role-based access instead of pure MAC allow-lists
- **Compliance:** Analytics data is anonymized and aggregated

> Improved user experience does not come at the cost of security.

---

## Analytics & Location Insights  
### Aruba Central Analytics + Aruba Location Engine (ALE)

### Collected Insights (Anonymized)
- Footfall (number of connected devices per branch)
- Repeat visitor patterns (frequency-based, not identity-based)
- Peak hours and peak days
- Average session duration
- Bandwidth consumption trends
- Zone / AP-level presence data

### Business Value
- **Operations:** Staff planning based on customer density
- **Retail Insights:** Identifying high-traffic branches
- **Capacity Planning:** Optimizing AP density and bandwidth usage

ALE focuses on **behavioral patterns**, not individual user tracking, ensuring privacy compliance.

---

## Why This Design?

| Challenge | Solution |
|--------|---------|
| Repeated guest login | Centralized guest identity |
| Inconsistent branch configs | Cloud-managed SSID & policies |
| Security risks | Isolated Guest VLAN + role-based access |
| Fragmented analytics | Central Analytics + ALE |
| Operational overhead | Single platform Aruba Central |

---

## Network Topology & Flow
For a detailed control plane vs. data plane view and captive portal interaction flow, see:
[Logical Network Topology & Traffic Flow](topology/logical-network-topology-traffic-flow.md)


## Conclusion

This case study demonstrates how a seemingly simple guest Wi-Fi requirement can be transformed into a **secure, scalable, and enterprise-grade architecture**.

The design balances:
- seamless guest experience
- strong network segmentation
- centralized operations
- actionable, privacy-aware analytics

---

## Author Notes

This case study reflects real-world design considerations commonly encountered in multi-branch enterprise wireless deployments.
