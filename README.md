Floating Static Routes in Networking
Introduction to Dynamic Routing vs Static Routing
Static routing involves manually configuring network routes, while dynamic routing automatically adapts to network changes. Dynamic routing is superior in most modern networks because:

Automatically adapts to topology changes (link failures, new connections)

Scales better in large networks

Reduces administrative overhead (no manual route updates)

Provides optimal path selection based on current conditions

Static routing is still useful for:

Small, stable networks

Default routes

Backup routes (floating static routes)

Security-sensitive connections

Dynamic Routing Protocols: Types and Examples
1. Interior Gateway Protocols (IGPs) - For within an autonomous system
A. Link-State Protocols
Maintain complete topological maps of the network

Use Dijkstra's algorithm to calculate shortest paths

Faster convergence than distance-vector

More resource-intensive

Examples:

OSPF (Open Shortest Path First)

Uses cost metric (based on interface bandwidth)

Hierarchical design with areas

Example: router ospf 1 → network 192.168.1.0 0.0.0.255 area 0

IS-IS (Intermediate System to Intermediate System)

Originally for OSI networks but adapted for IP

Uses CLNS addressing

Common in ISP backbones

B. Distance-Vector Protocols
Know only about directly connected neighbors

Share entire routing tables periodically

Simpler but slower convergence

Examples:

RIP (Routing Information Protocol)

Uses hop count as metric (max 15 hops)

Example: router rip → version 2 → network 192.168.1.0

EIGRP (Enhanced Interior Gateway Routing Protocol)

Cisco proprietary (though partially opened)

Uses composite metric (bandwidth, delay, reliability, load)

Example: router eigrp 100 → network 10.0.0.0

2. Exterior Gateway Protocols (EGPs) - For between autonomous systems
Path-Vector Protocol:

BGP (Border Gateway Protocol)

The protocol that makes the Internet work

Uses path attributes (AS_PATH, NEXT_HOP, LOCAL_PREF)

Example: router bgp 65001 → neighbor 192.168.1.1 remote-as 65002

Key Routing Concepts
Administrative Distance (AD)
A measure of route trustworthiness (lower is better):

Route Source	Default AD
Connected interface	0
Static route	1
EIGRP summary	5
eBGP	20
EIGRP internal	90
IGRP	100
OSPF	110
IS-IS	115
RIP	120
EIGRP external	170
iBGP	200
Unknown	255
Metrics
Different protocols use different metrics to determine best path:

Hop Count (RIP): Number of routers to destination

Cost (OSPF): Based on interface bandwidth (10^8/BW)

Composite Metric (EIGRP): (K1×BW) + (K2×BW)/(256-LOAD) + (K3×DLY)

Path Attributes (BGP): AS_PATH length, LOCAL_PREF, MED, etc.

Floating Static Routes
Floating static routes are backup routes with higher AD than dynamic routes. They "float" below dynamic routes and become active only when the primary route fails.

Example Configuration:

ip route 192.168.2.0 255.255.255.0 192.168.1.2 150
(Where 150 is higher than your dynamic protocol's AD)

Use Cases:

Backup for dynamic routing failures

Connection to stub networks

Temporary routes during maintenance

Conclusion
While dynamic routing protocols provide automated, scalable path selection in networks, floating static routes serve as an important redundancy mechanism. Understanding both dynamic routing protocols and static route options is essential for robust network design.

For implementation examples and configuration snippets, see the code files in this repository.
