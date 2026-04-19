# Lab 00 — Basic LAN Setup

## Objective
Build a simple Local Area Network with one switch and three PCs.
Assign static IP addresses and verify connectivity between all devices.

## Topology
![Topology](./lab-00-basic-lan/screenshots/topology.png)

## Network Details
| Device | Interface | IP Address | Subnet Mask |
|--------|-----------|------------|-------------|
| PC0 | FastEthernet0 | 192.168.2.1 | 255.255.255.0 |
| PC1 | FastEthernet0 | 192.168.2.3 | 255.255.255.0 |
| PC2 | FastEthernet0 | 192.168.2.x | 255.255.255.0 |

## What I Configured
- Connected 3 PCs to a Cisco 2960-24TT switch
- Assigned static IP addresses to each PC manually
- Verified end-to-end connectivity using ping

## Verification
![Ping Test](./lab-00-basic-lan/screenshots/ping-test.png)

Ping from PC1 to PC0 (192.168.2.1): **4/4 packets received, 0% loss**

## Key Learnings
- How a Layer 2 switch forwards frames using MAC address table
- Importance of being in the same subnet for hosts to communicate
- How to assign static IPs in Packet Tracer
- Using ping to verify Layer 3 connectivity
