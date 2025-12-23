# Logical Network Topology & Traffic Flow

This document describes the logical network topology and guest traffic flow for the enterprise guest Wi-Fi design.

---

## High-Level Logical Topology

Guest Client -> Wi-Fi (Get IP & pre-authenticated role ) -> Aruba AP -> Aruba Central (control plane) -> Guest VLAN (Isolated) & Authenticated Guest Role ->  Gateway / Firewall -> Internet

## Key Design Points

### Network Segmentation
- Guest traffic is fully isolated from the corporate network
- No lateral (east-west) communication between guest clients
- Only northbound internet access is permitted

### Role-Based Traffic Control
- Clients are dynamically assigned a **Authenticated Guest Role**
- VLAN assignment and access rules are enforced centrally
- Authentication state does not change the VLAN (isolation is preserved)

### HTTPS Redirection
- Captive portal redirection supports HTTPS traffic
- Pre-auth traffic is restricted to:
  - DNS
  - Captive portal services
- All other traffic is blocked until authentication is completed

### Centralized Enforcement
- No local per-branch policy differences
- All roles, VLAN mappings, and access rules are managed via Aruba Central

---

## Security Considerations

- MAC-based recognition is used only for session continuity and user experience
- Authentication state is combined with role-based access control
- Guest VLAN is never bridged with internal networks
- Analytics data collection remains anonymized

---

## Summary

This topology ensures:
- Consistent guest experience across all branches
- Strong isolation between guest and internal networks
- Centralized control and simplified operations
- Secure HTTPS-based captive portal authentication
