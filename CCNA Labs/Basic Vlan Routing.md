# Basic VLAN Routing

![](https://github.com/Adel-Ahmed777/CCNA-200-301/blob/main/CCNA%20Labs/Lab%20Images/Basic%20Vlan%20Routing.jpg?raw=true)

## Activities:

> Configure VTP
- Configure all switckes to be part of the FCL domain.
- Configure SW1 as the VTP server
- Configure SW2,3 as VTP clients.

> Configure VLAN Trunks
- Configure SW1 Fa0/1,2 as trunks
- Configure SW2 Fa0/23,24 as trunks
- Configure SW3 Fa0/23,24 as trunks

> Configure VLANs
- Using SW1 configure VLAN-10 and name it Dept-A
- Using SW1 configure VLAN-20 and name it Dept-B
- Using SW1 configure VLAN-99 and name it Management

> Assign Interfaces to VLANs
- Configure SW2 interfaces Fa1,2 to VLAN-10
- Configure SW3 interfaces Fa1,2 to VLAN-20

> Assign IP Addresses
- Assign the VLAN-99 interface of SW1,2,3 with 192.168.99.1, 2, 3
- Assign PC-0 and PC-1 to the 192.168.10.X network segment as shown in the network digram
- Assign PC-0 and PC-1 to the default gateway 192.168.10.1 network segment as shown in the network digram
- Assign PC-2 and PC-3 to the 192.168.20.X network segment as shown in the network digram
- Assign PC-2 and PC-3 to the default gateway 192.168.20.1 network segment as shown in the network digram

> Configure Spanning Tree Protocol
- Configure SW1 to be the root bridge for all VLANs
- Note that the connection between SW1 and SW2, 3 are active
- Note that the connection between SW2 and SW3 are not active they are in blocking mode.

> Verify Connectivity
- from PC-0 ping PC-1
- frpm PC-2 ping PC-3
- from PC-0 ping PC-3 Note the pings are not successful because PC-4 is in a different VLAN


## Configure VTP
- Configure all switckes to be part of the FCL domain.
- Switch  1
```
SW1>enable
SW1#configure terminal
SW1(config)#no ip domain-lookup
SW1(config)#vtp domain FCL
SW1(config)#end
SW1# copy running-config startup-config
```

- Switch 2
```
SW2>enable
SW2#configure terminal
SW2(config)#no ip domain-lookup
SW2(config)#vtp domain FCL
Changing VTP domain name from NULL to FCL
SW2(config)#end
SW2#copy running-config startup-config
```

- Switch 3
```
SW3>enable
SW3#configure terminal
SW3(config)#no ip domain-lookup
SW3(config)#vtp domain FCL
SW3(config)#end
SW3#copy running-config startup-config
```

- Configure SW1 as the VTP server
```
SW1#enable
SW1#configure terminal
SW1(config)#vtp mode server
```

- Configure SW2,3 as VTP clients.
- Switch 2
```
SW2#configure terminal
SW2(config)#vtp mode client
```

- Switch 3
```
SW3#configure terminal
SW3(config)#vtp mode client
```

## Configure VLAN Trunks
- Configure SW1 Fa0/1,2 as trunks
```
SW1#configure terminal
SW1(config)#interface fastethernet 0/1
SW1(config-if)#switchport mode trunk
SW1(config-if)#no shutdown
SW1(config-if)#
SW1(config-if)#end
SW1(config)#interface fastEthernet 0/2
SW1(config-if)#switchport mode trunk
SW1(config-if)#no shutdown
SW1#copy running-config startup-config
```

- Configure SW2 Fa0/23,24 as trunks
```
SW2#configure terminal
SW2(config)#interface fastEthernet 0/23
SW2(config-if)#switchport mode trunk
SW2(config-if)#no shutdown
SW2(config-if)#exit
SW2(config)#interface fastEthernet 0/24
SW2(config-if)#switchport mode trunk
SW2(config-if)#no shutdown
SW2(config-if)#end
SW2#copy running-config startup-config
```

- Configure SW3 Fa0/23,24 as trunks
```
SW3#configure terminal
SW3(config)#interface fastEthernet 0/23
SW3(config-if)#switchport mode trunk
SW3(config-if)#no shutdown
SW3(config-if)#
SW3(config-if)#exit
SW3(config)#interface fastEthernet 0/24
SW3(config-if)#switchport mode trunk
SW3(config-if)#no shutdown
SW3(config-if)#end
SW3#copy running-config startup-config
```
## Configure VLANs
- Using SW1 configure VLAN-10 and name it Dept-A
- Using SW1 configure VLAN-20 and name it Dept-B
- Using SW1 configure VLAN-99 and name it Management

```
SW1#configure terminal
SW1(config)#vlan 10
SW1(config-vlan)#name Dept-A
SW1(config-vlan)#exit
SW1(config)#vlan 20
SW1(config-vlan)#name Dept-B
SW1(config-vlan)#exit
SW1(config)#vlan 99
SW1(config-vlan)#name Management
SW1(config-vlan)#end
SW1#copy running-config startup-config
```

## Assign Interfaces to VLANs
- Configure SW2 interfaces Fa1,2 to VLAN-10
- Configure SW3 interfaces Fa1,2 to VLAN-20

- Switch 2
```
SW2#configure terminal
SW2(config)#interface fastEthernet 0/1
SW2(config-if)#switchport access vlan 10
SW2(config-if)#exit
SW2(config)#interface fastEthernet 0/2
SW2(config-if)#switchport access vlan 10
SW2(config-if)#end
SW2#
```

- Switch 3
```
SW3#configure terminal
SW3(config)#interface fastEthernet 0/1
SW3(config-if)#switchport access vlan 20
SW3(config-if)#exit
SW3(config)#interface fastEthernet 0/2
SW3(config-if)#switchport access vlan 20
SW3(config-if)#end
```

## Assign IP Addresses
- Assign the VLAN-99 interface of SW1,2,3 with 192.168.99.1, 2, 3

Sw1
```
SW1#configure  terminal
SW1(config)#interface vlan 99
SW1(config-if)#ip address 192.168.99.1 255.255.255.0
SW1(config-if)#no shu
SW1(config-if)#no shutdown
SW1(config-if)#end
SW1#copy running-config startup-config
```

Sw2
```
SW2#configure terminal
SW2(config)#interface vlan 99
SW2(config-if)#ip address 192.168.99.2 255.255.255.0
SW2(config-if)#no shutdown
SW2#copy running-config startup-config
```

Sw3
```
SW3#configure terminal
SW3(config)#interface vlan 99
SW3(config-if)#ip address 192.168.99.3 255.255.255.0
SW3(config-if)#no shutdown
SW3#copy running-config startup-config
```



## Configure Spanning Tree Protocol
- Configure SW1 to be the root bridge for all VLANs
```
SW1#configure terminal
SW1(config)#spanning-tree vlan 10 root primary
SW1(config)#spanning-tree vlan 20 root primary
SW1(config)#spanning-tree vlan 99 root primary
SW1(config)#end
SW1#copy running-config startup-config
```
