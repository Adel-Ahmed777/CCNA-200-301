# Spanning tree protocol

# Spanning tree protocol process:
> 1) Electing root bridge.

> 2) Choosing root ports.

> 3) Choosing designated ports.



# 1) How is the root switch chosen [election process]?
> 1) All switches in the network participate in the election process.

> 2) The switch with the lowest BID value becomes the root bridge. BID has two values [Priority value - MAC address].
   >>1) The switch with the lowest priority value is chosen as root.
   >>2) If a tie occurs, the switch with lowest mac address is chosen as root.

# 2) How to identify root ports?
Once the root bridgeh is elected, all other non-root switches need to determine the quickest path from them to the root switch.
## Steps to choose a root port:
> 1) The port that is directly connected to the root bridge or one with the shortest path becomes **root port**.

> 2) If there are many links, the port with lowest cost becomes the **root port**.

> 3) If many links have the same cost, then check the neigbour bridge ID and choose the lowest Bridge ID.


# 3) How to identify designated ports?
> By default, on the root bridge, all ports are designated ports.

> The switch with the lowest cost to reach the root port, out of all switches, becomes the **designated port** on that link.


# STP vs RSTP
|STP  |RSTP |
|:---:|:---:|
|Slow network failure recovery|faster network failure recovery|
| port states: Blocking-->Listening-->Learning-->Forwarding| port states: Discarding-->Learning-->Forwarding|
| port roles: Root port - Designated port - Blocking port | port roles: Root port - Designated port - Alternated port - Backup port  |
|Convergence time: 50 seconds|Convergence time: 21 seconds|
|IEEE 802.1d|IEEE 802.1w   |
|Only root bridge generates BPDU   |All bridges generate BPDU   |

# STP optional features

> EtherChannel: Port aggregation feature. When a port or cable failes, EtherChannel stops STP Convergence from being needed by grouping physical ethernet links together.

> PortFast: Transition feature that allows a switch to transition from blocking to forwarding.

> BPDU Guard: Prevents BPDU related attacks.     
