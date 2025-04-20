Rapid Spanning Tree Protocol (RSTP) Lab Report
Introduction
The Spanning Tree Protocol (STP) is a network protocol that ensures a loop-free topology for Ethernet networks. The original STP (IEEE 802.1D) was later enhanced by the Rapid Spanning Tree Protocol (RSTP, IEEE 802.1w), offering improved network convergence and efficiency. This lab focuses on RSTP, comparing it with classic STP, outlining its configuration, advantages, port states, and roles.

Differences and Similarities: RSTP vs. Classic STP
Similarities:

Both protocols are designed to prevent Layer 2 loops in network topologies by creating a tree structure of active links.
They both use Bridge Protocol Data Units (BPDUs) for exchanging information between switches.
Both select a Root Bridge, and each switch uses STP/RSTP logic to determine port roles and state.
Differences:

Convergence Time:
STP convergence is slow (30-50 seconds); RSTP greatly reduces convergence to a few seconds.
Port States:
STP uses five port states (Blocking, Listening, Learning, Forwarding, Disabled).
RSTP uses only three (Discarding, Learning, Forwarding).
Port Roles:
STP has three (Root, Designated, Non-designated/Blocking), while RSTP has four (Root, Designated, Alternate, Backup).
BPDU Handling:
In STP, only the Root Bridge sends BPDUs; in RSTP, every switch can send BPDUs (proposals and agreements), speeding up convergence.
Link Types:
RSTP treats ports differently based on their connection type (point-to-point or edge), which affects the speed of transition to forwarding state.
Edge Ports:
RSTP introduces the concept of edge ports for immediate transition to forwarding state, useful for end devices.
Advantages of RSTP
Faster Convergence: Reduces network downtime by quickly reconfiguring the topology after changes.
Simpler Port States: Easier to understand and troubleshoot.
Immediate Edge Port Forwarding: Devices like computers and printers come online faster.
Backward Compatibility: RSTP can coexist with classic STP on legacy devices.
RSTP Port States
Discarding: (Replaces Blocking and Listening in STP) – Port does not forward traffic and does not learn MAC addresses.
Learning: Port does not yet forward traffic but begins learning MAC addresses.
Forwarding: Port forwards frames and learns addresses.
RSTP Port Roles
Root Port: The port on a switch with the best path to the root bridge.
Designated Port: The port on a network segment that has the best path to the root bridge for that segment.
Alternate Port: A backup to the root port (goes into forwarding if the root port fails).
Backup Port: A backup to the designated port on the same segment (rare).
Configuration Example (Cisco Syntax)
RSTP is enabled using MSTP (Multiple Spanning Tree Protocol) command or by specifying rapid-pvst mode:


Switch(config)# spanning-tree mode rapid-pvst
! Or for MSTP:
Switch(config)# spanning-tree mode mst
To configure a port as an edge port (like STP PortFast):


Switch(config-if)# spanning-tree portfast
To verify RSTP operation:


Switch# show spanning-tree
Switch# show spanning-tree detail
Typical Lab Scenario Steps
Set up the topology with at least three switches interconnected redundantly.
Configure switches for RSTP/rapid-pvst mode.
Identify root bridge by setting bridge priorities if needed.
Connect hosts to edge ports.
Simulate a topology change (e.g., disconnect a link) and observe the rapid convergence.
Conclusion
RSTP significantly improves network reliability and performance over classic STP by reducing reconvergence times during network changes. Its simpler, faster, and more robust mechanisms—such as fewer port states, new port roles, and immediate edge port forwarding—make it the recommended standard for modern switched networks.
