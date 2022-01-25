# Inter VLAN Routing
![](https://github.com/Adel-Ahmed777/CCNA-200-301/blob/main/CCNA%20Labs/Lab%20Images/Inter-Vlan.jpg?raw=true)

# Lab Activities:
- You are the Network Administrator at Ranet, and have to config both switch "Ranet-SW" and router
"Ranet-GW" via its console terminal as below:
    1. Set Ranet-SW to seperate VLAN to be VLAN 10
       and VLAN 20 and set its member as:
          VLAN 10: Fa0/1, Fa0/2
          VLAN 20: Fa0/3, Fa0/4
    2. Enable feature "Portfast" on all access ports.
    3. Set both Ranet-SW and Ranet-GW to route
       between VLAN 10 and VLAN 20:
          - Use interface Fa0/0.1 and Fa0/0.2 on
            Ranet-GW as sub-interface for VLAN 10 and
            VLAN 20 respectively
          - Please note that all hosts in each VLAN set
            IP Default Gateway to be the last IP of its
            own subnet.

If everything is correct, All hosts will be able to
connect with each other.


# SW configuration:

## Ranet-SW Configuration and interfaces Fa0/1, Fa0/2 set to VLAN 10 with portfast feature.
```
Ranet-SW>
Ranet-SW>enable
Ranet-SW#configure Terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Ranet-SW(config)#vlan 10
Ranet-SW(config-vlan)#vlan 20
Ranet-SW(config-vlan)#exit
Ranet-SW(config)#interface range fastethernet 0/1-2
Ranet-SW(config-if-range)#switchport access vlan 10
Ranet-SW(config-if-range)#spanning-tree portfast
```
## interfaces Fa0/1, Fa0/2 set to VLAN 10 with portfast feature:
```
Ranet-SW(config)#interface range fastEthernet 0/3-4
Ranet-SW(config-if-range)#switchport mode access
Ranet-SW(config-if-range)#switchport access vlan 20
Ranet-SW(config-if-range)#spanning-tree portfast
```
## Enabling trunking:
```
Ranet-SW#configure terminal
Ranet-SW(config)#interface gigabitEthernet 0/1
Ranet-SW(config-if)#switchport mode trunk
Ranet-SW(config-if)#exit
Ranet-SW(config)#interface gigabitEthernet 0/2
Ranet-SW(config-if)#switchport mode trunk
Ranet-SW(config-if)#end
Ranet-SW#
Ranet-SW#copy running-config startup-config
```
# GW Configuration:
```
Ranet-GW>
Ranet-GW>enable
Ranet-GW#configure terminal
Ranet-GW(config)#interface fastEthernet 0/0
Ranet-GW(config-if)#no shutdown
Ranet-GW(config-if)#int fa0/0.1
Ranet-GW(config-subif)#encapsulation dot1Q 10
Ranet-GW(config-subif)#ip address 192.168.0.142 255.255.255.240
Ranet-GW(config-subif)#int fa0/0.2
Ranet-GW(config-subif)#encapsulation dot1Q  20
Ranet-GW(config-subif)#ip address 192.168.0.158 255.255.255.240
Ranet-GW(config-subif)#end
Ranet-GW#show ip route
Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
       i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
       * - candidate default, U - per-user static route, o - ODR
       P - periodic downloaded static route

Gateway of last resort is not set

     192.168.0.0/28 is subnetted, 2 subnets
C       192.168.0.128 is directly connected, FastEthernet0/0.1
C       192.168.0.144 is directly connected, FastEthernet0/0.2

Ranet-GW#copy running-config startup-config
```
