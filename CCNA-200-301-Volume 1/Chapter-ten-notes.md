# RSTP and EtherChannel
> Switch BID has two components: 2 byte priority + 6 byte MAC address.

> System ID extension: a 12 bit subfield of the 2 byte priority section.




# RSTP vs RPVSTP+
|RSTP  |RPVSTP+ |
|:---:|:---:|
|creates one tree. i.e. Common Spanning Tree|Creates one tree for each VLAN|
| Regardless of how many VLANs exist in the network, it only sends one group of RSTP messages (BPDUs)| Sends one group of messages per VLAN |
| RSTP uses multicast address 0180.C200.0000 that is defined in the IEEE standard | RPVSTP+ uses multicast address 0100.0CCC.CCCD chosen by CISCO |
|VLAN trunks message transmission: RSTP sends the messages in the native VLAN without VLAN headers or tags|VLAN trunks message transmission: RPVST+ sends the message of each VLAN inside that VLAN|
|RSTP ignores VLANs so it doesn't need to add type-length value|RPVST+ adds type-length value to BPDU to identify VLAN ID   |


# Layer 2 EtherChannel Configuration


> ## Layer 2 EtherChannel configuration:
> There are two ways to configure layer 2 EtherChannel:
1) By manual (static) configuration.
2) Allowing dynamic protocols to create the channel.

> ##  How to configure a Layer 2 EtherChannel manually:
1) Add the following command after each interface: **channel-group** [number] **mode on**
2) Use same channel group number on the same switch.
3) Use a different channel group number on the neighboring switch.
Example configuration on ports 0/10 and 0/12
```
Switch>enable
Switch# configure terminal
Switch(config)#interface fastEthernet 0/10
Switch(config-if)#channel-group 1 mode on
Switch(config-if)#exit
Switch(config)#interface fastEthernet 0/12
Switch(config-if)#channel-group 1 mode on
Switch(config-if)#^Z
```
To confirm the configuration use **show etherchannel [add number] summary**


> ##  How to configure a Layer 2 EtherChannel dynamically:
The etherchannel adds the link to the channel group if it passess all configuration checks, otherwise, it is placed in adown state.

Dynamic layer 2 etherchannel configuration uses one of two protocols:
1) Port Aggregation Protocol (PAgP).
2) Link Aggregation Control Protocol (LACP).

> For Port Aggregation Protocol (PAgP), at least one of the two switches must use the desirable keyword: channel-group [add number] mode **desirable**

> For Link Aggregation Control Protocol (LACP), at least one of the two switches must use the active keyword: channel-group [add number] mode **active**
