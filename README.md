# Week 1 — OSI, VLANs, Static Routes & ACLs

[Network Topology](./images/topology.png)

Networking Fundamentals Lab Report

Author: Robert Smith
Tools Used: Cisco Packet Tracer, Wireshark
Goal: Build foundational networking knowledge and apply concepts in hands-on labs to prepare for advanced studies in cybersecurity and ethical hacking.

<b>🧠 Day 1 — OSI & TCP/IP Layers + Basic Topology</b>

Study Topics:

Reviewed all 7 OSI layers and 4 TCP/IP layers.

Learned the functions and protocols associated with each layer (e.g., IP, TCP, Ethernet, HTTP).

Hands-On Lab:

Built a basic network in Cisco Packet Tracer consisting of:

1 Router (Router0)

1 Switch (Switch0)

2 PCs (PC0, PC1)

Assigned static IPs and verified connectivity using ping.

Key Commands:

# Basic connectivity test
PC> ping 192.168.1.2


Outcome:
✅ Successfully established Layer 3 connectivity between two hosts through a switch and router.

🧮 Day 2 — IPv4 Binary & Subnetting

Study Topics:

Studied IPv4 address structure, binary notation, and subnet masks.

Learned how to calculate subnets, host ranges, and broadcast addresses.

Lab Work:

Solved 20 subnetting problems manually.

Practiced converting IPs to binary and calculating subnet boundaries.

Example Calculation:

Network: 192.168.10.0/26
Subnet mask: 255.255.255.192
Host range: 192.168.10.1 – 192.168.10.62
Broadcast: 192.168.10.63


Outcome:
✅ Achieved strong understanding of subnetting fundamentals and binary operations.

🧩 Day 3 — Static IP Configuration & Packet Capture

Lab Objective:
Manually configure IP addresses and capture ARP/ICMP behavior.

Tasks:

Assigned static IPs on PCs and router interfaces in Packet Tracer.

Captured packets in Wireshark while sending pings between hosts.

Identified ARP requests/responses and ICMP Echo/Reply packets.

Key Concepts Observed:

ARP: Resolves MAC addresses before ICMP communication.

ICMP: Used to verify reachability.

Outcome:
✅ Demonstrated end-to-end IP configuration and packet-level analysis.

🧱 Day 4 — VLANs & Inter-VLAN Routing

Lab Objective:
Segment a LAN using VLANs and enable communication between them via a router-on-a-stick configuration.

Setup:

Router (Router0)

Switch (Switch0)

PC0 (VLAN10)

PC1 (VLAN20)

Router Configuration:

interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
!
interface g0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0


Switch Configuration:

vlan 10
vlan 20
int g0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20

[VLAN Configuration](./images/vlan-setup.png)

**Explanation:** The screenshot shows VLAN10 and VLAN20 assignments on Switch0 and trunking to Router0.


Outcome:
✅ VLANs successfully isolated, and inter-VLAN routing verified using ping between VLAN10 and VLAN20 hosts.

🌐 Day 5 — Static Routing & Traceroute Validation

Objective:
Implement static routing between two routers and verify multi-network reachability.

Setup:

Router1: Networks 192.168.10.0/24, 192.168.20.0/24

Router2: Network 192.168.30.0/24

Connection between routers: 10.0.0.0/30

Router1 Configuration:

ip route 192.168.30.0 255.255.255.0 10.0.0.2


Router2 Configuration:

ip route 192.168.10.0 255.255.255.0 10.0.0.1
ip route 192.168.20.0 255.255.255.0 10.0.0.1


Validation:

Used tracert from PC1 → PC3 to confirm hops through routers.

Observed proper routing table entries via show ip route.

Outcome:
✅ End-to-end connectivity confirmed across routers via static routes.

🔐 Day 6 — Basic Access Control List (ACL)

Objective:
Introduce traffic filtering using ACLs on a Cisco router.

Scenario:

Permit VLAN10 to access all networks.

Deny VLAN20 from accessing VLAN30.

Configuration (Router1):

access-list 100 deny ip 192.168.20.0 0.0.0.255 192.168.30.0 0.0.0.255
access-list 100 permit ip any any
interface g0/1
 ip access-group 100 out


Verification:

PC2 (VLAN20) → PC3 (VLAN30): ❌ Ping failed as expected.

PC1 (VLAN10) → PC3 (VLAN30): ✅ Ping successful.

Outcome:
✅ ACL successfully restricted inter-VLAN access based on policy.

🧾 Summary of Skills Gained
Concept	Status	Tools Used
OSI/TCP-IP Model	✅	Notes, Diagram
Subnetting	✅	Manual, Binary Practice
Static IPs	✅	Packet Tracer
VLANs	✅	Packet Tracer
Inter-VLAN Routing	✅	Router-on-a-Stick
Static Routes	✅	Packet Tracer
ACL Configuration	✅	Packet Tracer
💡 Next Steps (Day 7+)

Configure Dynamic Routing (RIP, OSPF)

Implement NAT & DHCP

Explore extended ACLs with more granular filtering

Begin Layer 2 security features (Port Security, STP basics)
