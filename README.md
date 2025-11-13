# Dual-Lan-Vlan-Communication Project (Router-on-a-Stick)
## Overview
This project simulates a small enterprise network that utilizes VLANs to segment departments and employs inter-VLAN routing to facilitate controlled communication between them.  
It was built using Cisco Packet Tracer to demonstrate VLAN creation, trunking, and Layer 3 routing.

---

## Topology
![Network Topology](Topology.png)

Devices:
- 2 (Switch1, Switch2)
- 1 Router (Router1)
- 2 PCs (1 in each VLAN)

## Objectives
1. Configure VLANs to separate traffic between departments.  
2. Enable inter-VLAN communication using router-on-a-stick.  
3. Verify connectivity with ping and traceroute.  
4. Document topology, IP addressing, and configurations.

## Network Design
| Device | VLAN | Department | Network | Default Gateway |
|------|------|-------------|----------|----------------|
| PC1 | 10 | Admin | 192.168.10.10/24 | 192.168.10.1 |
| PC2 | 20 | Finance | 192.168.20.10/24 | 192.168.20.1 |

## Summary

### **Router Configuration**
```bash
Router#config t
Router(config)#int g0/0/1.10
Router(config-subif)#description Default Gateway for Admin
Router(config-subif)#encapsulation dot1Q 10
Router(config-subif)#ip add 192.168.10.1 255.255.255.0
Router(config-subif)#exit
Router(config)#int g0/0/1.20
Router(config-subif)#description Default Gateway for Finance
Router(config-subif)#encapsulation dot1Q 20
Router(config-subif)#ip add 192.168.20.1 255.255.255.0
Router(config-subif)#exit
Router(config)#int g0/0/1.99
Router(config-subif)#description Default Gateway for Management
Router(config-subif)#encapsulation dot1Q 99
Router(config-subif)#ip add 192.168.99.1 255.255.255.0
Router(config-subif)#exit
Router(config)#int g0/0/1
Router(config-if)#description Trunk Link to S1
Router(config-if)#no shut
```
### **Switch Configuration**
```bash
Switch(config)#vlan 10
Switch(config-vlan)#name Admin
Switch(config-vlan)#exit
Switch(config)#vlan 20
Switch(config-vlan)#name Finance
Switch(config-vlan)#exit
Switch(config)#vlan 99
Switch(config-vlan)#name Management
Switch(config-vlan)#exit
Switch(config)#int vlan 99
Switch(config-if)#ip add 192.168.99.2 255.255.255.0
Switch(config-if)#no shut
Switch(config-if)#exit
Switch(config)#ip default-gateway 192.168.99.1
Switch(config)#int fa0/6
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 10
Switch(config-if)#no shut
Switch(config-if)#exit
Switch(config)#int fa0/1
Switch(config-if)#switchport mode trunk
Switch(config-if)#no shut
Switch(config-if)#exit
Switch(config)#int fa0/5
Switch(config-if)#switchport mode trunk
Switch(config-if)#no shut
Switch(config-if)#end
```
### Verify Inter-VLAN Routing by Pinging from PC1
![Verification]()
