# EtherChannel & STP Redundancy Lab

## Project Overview

This project demonstrates **EtherChannel, LACP, Port-Channel, Spanning Tree Protocol (STP), and Layer-2 network redundancy** using Cisco Packet Tracer.

Two Cisco 2960 switches are connected using multiple physical links. These links are combined into a single logical EtherChannel using LACP. STP is also configured to establish a primary and secondary root bridge.

The project includes link-failure testing to demonstrate network redundancy and fault tolerance.

---

## Objectives

- Configure LACP EtherChannel between two Cisco switches
- Create a logical Port-Channel
- Configure Port-Channel as a trunk
- Configure STP root bridge and secondary root bridge
- Configure Layer-2 connectivity
- Test network connectivity
- Simulate physical link failure
- Verify EtherChannel redundancy
- Perform basic Cisco IOS troubleshooting

---

## Network Topology

```text
       PC1                         PC3
        |                           |
      Fa0/1                       Fa0/1
        |                           |
     +------+                   +------+
     | SW1  |===================| SW2  |
     +------+   EtherChannel     +------+
        |                           |
      Fa0/2                       Fa0/2
        |                           |
       PC2                         PC4
