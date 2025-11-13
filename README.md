# Dual-Lan-Vlan-Communication Project
## Overview
This project simulates a small enterprise network that utilizes VLANs to segment departments and employs inter-VLAN routing to facilitate controlled communication between them.  
It was built using Cisco Packet Tracer to demonstrate VLAN creation, trunking, and Layer 3 routing.

---

## Topology
![Network Topology](./topology/vlan_topology.png)

Devices:
- 2 Layer 2 Switches (Switch1, Switch2)
- 1 Router (Router0)
- 4 PCs (2 in each VLAN)

## Objectives
1. Configure VLANs to separate traffic between two departments.  
2. Enable inter-VLAN communication using router-on-a-stick.  
3. Verify connectivity with ping and traceroute.  
4. Document topology, IP addressing, and configurations.

## Network Design
| VLAN | Department | Network | Default Gateway |
|------|-------------|----------|----------------|
| 10 | Admin | 192.168.10.0/24 | 192.168.10.1 |
| 20 | Finance | 192.168.20.0/24 | 192.168.20.1 |

## Summary

### **Router Configuration**
```bash
interface g0/0
 no shutdown
!
interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
!
interface g0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
