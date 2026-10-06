EtherChannel & STP Redundancy Lab
A Cisco Packet Tracer mini project demonstrating LACP EtherChannel,
Port-Channel, Spanning Tree Protocol (STP), Layer-2 redundancy, and
link-failure testing.
Objectives
- Configure LACP EtherChannel between two Cisco switches
- Create a logical Port-Channel
- Configure the Port-Channel as a trunk
- Configure STP root bridge selection
- Test Layer-2 connectivity
- Simulate physical link failure
- Verify EtherChannel redundancy
- Practice Cisco IOS troubleshooting
Topology
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
EtherChannel links:
SW1 G0/1 <----> SW2 G0/1
SW1 G0/2 <----> SW2 G0/2
Devices
  Device   Model          Quantity
  Switch   Cisco 2960            2
  PC       PC-PT                 4
IP Addressing
  Device   IP Address      Subnet Mask
  PC1      192.168.10.10   255.255.255.0
  PC2      192.168.10.11   255.255.255.0
  PC3      192.168.10.12   255.255.255.0
  PC4      192.168.10.13   255.255.255.0
No default gateway is required because this project focuses on Layer-2
connectivity.
LACP Configuration --- SW1
enable
configure terminal
interface range gigabitEthernet 0/1-2
channel-group 1 mode active
exit
interface port-channel 1
switchport mode trunk
exit
end
write memory
LACP Configuration --- SW2
enable
configure terminal
interface range gigabitEthernet 0/1-2
channel-group 1 mode active
exit
interface port-channel 1
switchport mode trunk
exit
end
write memory
Both switches use mode active for LACP negotiation.
STP Configuration
SW1 --- Root Bridge
enable
configure terminal
spanning-tree vlan 1 root primary
end
SW2 --- Secondary Root
enable
configure terminal
spanning-tree vlan 1 root secondary
end
Verification
EtherChannel
show etherchannel summary
Expected:
Po1(SU)
G0/1(P)
G0/2(P)
S = Layer-2 EtherChannel, U = in use, P = successfully bundled
port.
STP
show spanning-tree vlan 1
SW1 should show:
This bridge is the root
Trunk
show interfaces trunk
Port-Channel
show interfaces port-channel 1
Connectivity Testing
From PC1:
ping 192.168.10.12
ping 192.168.10.13
From PC2:
ping 192.168.10.12
Link-Failure Test
On SW1:
enable
configure terminal
interface gigabitEthernet 0/1
shutdown
end
Test from PC1:
ping 192.168.10.12
Traffic should continue through the remaining EtherChannel member.
Verify:
show etherchannel summary
Restore the link:
configure terminal
interface gigabitEthernet 0/1
no shutdown
end
Then verify again:
show etherchannel summary
Troubleshooting
If EtherChannel does not form, check:
show etherchannel summary
show interfaces status
show interfaces port-channel 1
Make sure both sides use compatible EtherChannel settings and that the
correct physical ports are connected.
If a port appears as I instead of P, it is operating independently
rather than successfully joining the bundle.
If ping fails, verify the PC IP addresses and switch interface status.
Concepts Learned
- EtherChannel
- LACP
- Port-Channel
- STP
- Layer-2 switching
- Link redundancy
- Fault injection
- Network troubleshooting
- Cisco IOS verification
Interview Questions
What is EtherChannel?
EtherChannel combines multiple physical Ethernet links into one logical
link.
What is LACP?
LACP is a protocol used to negotiate and maintain EtherChannel links.
What does mode active mean?
It actively participates in LACP negotiation.
What is Port-Channel?
It is the logical interface representing the bundled physical links.
Why is STP important?
STP prevents Layer-2 switching loops.
What happens if one EtherChannel member fails?
Traffic can continue through the remaining active member links.
How do you verify EtherChannel?
show etherchannel summary
How do you verify STP?
show spanning-tree
Suggested Repository Structure
EtherChannel-STP-Redundancy-Lab/
├── README.md
├── topology/
│   └── EtherChannel-STP-Redundancy.pkt
├── configs/
│   ├── SW1-config.txt
│   └── SW2-config.txt
└── screenshots/
    ├── topology.png
    ├── etherchannel-summary.png
    ├── spanning-tree.png
    └── link-failure-test.png
Resume Description
EtherChannel & STP Redundancy Lab | Cisco Packet Tracer
Designed and configured a Layer-2 redundant network using LACP
EtherChannel and STP, created a Port-Channel between Cisco switches,
configured STP root bridge selection, and validated connectivity
during simulated physical link failures.

Skills Demonstrated
Cisco Packet Tracer Cisco IOS EtherChannel LACP STP
Layer-2 Switching Port-Channel Network Redundancy
Network Troubleshooting
Author
Andrews GnanaSelvin D
Computer Science Engineering Student | Aspiring Network Engineer
GitHub: Andrewsdavid2005
LinkedIn: Andrews GnanaSelvin D
Project Status
Completed | Cisco Packet Tracer | Intermediate | Layer-2
Networking & Redundancy
License
This project is created for educational, academic, networking practice,
and portfolio purposes.
