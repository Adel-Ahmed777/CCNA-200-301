# Lab 3 Vlan and VTP

## Activities
>1.Configure the VTP-SERVER switch as a VTP server

>2.Connect to the  3 other switches and configure them as VTP clients.
All links between swiches must be configured as trunk lines.

>3.Configure VTP domain name as "TESTDOMAIN" and VTP password as "cisco"

>4.Configure VLAN 10 with name "STUDENTS" and VLAN 50 with name "SERVERS"

>5.Check propagation on all switches of the VTP domain.

## 1.Configure the VTP-SERVER switch as a VTP server & 3.Configure VTP domain name as "TESTDOMAIN" and VTP password as "cisco"


```
VTP-SERVER>enable
VTP-SERVER#configure terminal
VTP-SERVER(config)#no ip domain-lookup
VTP-SERVER(config)#vtp mode server
VTP-SERVER(config)#vtp domain TESTDOMAIN
VTP-SERVER(config)#vtp password cisco
VTP-SERVER(config)#end
```
## 4.Configure VLAN 10 with name "STUDENTS" and VLAN 50 with name "SERVERS"

```
VTP-SERVER#configure terminal
VTP-SERVER(config)#vlan 10
VTP-SERVER(config-vlan)#name STUDENTS
VTP-SERVER(config-vlan)#vlan 50
VTP-SERVER(config-vlan)#name SERVERS
VTP-SERVER(config-vlan)#end
VTP-SERVER#configure terminal
VTP-SERVER(config)#interface vlan 1
VTP-SERVER(config-if)#ip address 192.168.1.1 255.255.255.0
VTP-SERVER(config-if)#no shutdown
VTP-SERVER#copy running-config startup-config
```

## 2.Connect to the  3 other switches and configure them as VTP clients. All links between swiches must be configured as trunk lines. & 3.Configure VTP domain name as "TESTDOMAIN" and VTP password as "cisco"

### VTP Server Switch

```
VTP-SERVER#configure terminal
VTP-SERVER(config)#interface gigabitEthernet 0/1
VTP-SERVER(config-if)#switchport mode trunk
VTP-SERVER(config-if)#no shutdown
VTP-SERVER(config-if)#exit
VTP-SERVER(config)#interface gigabitEthernet 0/2
VTP-SERVER(config-if)#switchport mode trunk
```

### VTP client 3 switch
```
VTP-CLIENT3>enable
Password:
VTP-CLIENT3#configure terminal
VTP-CLIENT3(config)#no ip domain-lookup
VTP-CLIENT3(config)#vtp mode client
VTP-CLIENT3(config)#vtp domain TESTDOMAIN
VTP-CLIENT3(config)#vtp password cisco
VTP-CLIENT3(config)#interface gigabitEthernet 0/1
VTP-CLIENT3(config-if)#switchport mode trunk
VTP-CLIENT3(config-if)#no shutdown
VTP-CLIENT3(config-if)#exit

VTP-CLIENT3(config)#interface gigabitEthernet 0/2
VTP-CLIENT3(config-if)#switchport mode trunk
VTP-CLIENT3(config-if)#no shutdown
VTP-CLIENT3(config-if)#end

VTP-CLIENT3#configure terminal
VTP-CLIENT3(config)#interface vlan 1
VTP-CLIENT3(config-if)#ip address 192.168.1.4 255.255.255.0
VTP-CLIENT3(config-if)#no shutdown
VTP-CLIENT3(config-if)#end
VTP-CLIENT3#copy running-config startup-config
```

### VTP client 2 switch
```
VTP-CLIENT2>enable
Password:
VTP-CLIENT2#configure terminal
VTP-CLIENT2(config)#no ip domain-lookup
VTP-CLIENT2(config)#vtp mode client
VTP-CLIENT2(config)#vtp domain TESTDOMAIN
VTP-CLIENT2(config)#vtp password cisco
VTP-CLIENT2(config)#end

VTP-CLIENT2#configure terminal
VTP-CLIENT2(config)#interface gigabitEthernet 0/1
VTP-CLIENT2(config-if)#switchport mode trunk
VTP-CLIENT2(config-if)#no shutdown
VTP-CLIENT2(config-if)#exit

VTP-CLIENT2(config)#interface gigabitEthernet 0/2
VTP-CLIENT2(config-if)#switchport mode trunk
VTP-CLIENT2(config-if)#no shutdown
VTP-CLIENT2(config-if)#end
VTP-CLIENT2#
VTP-CLIENT2#configure terminal
VTP-CLIENT2(config)#interface vlan 1
VTP-CLIENT2(config-if)#ip address 192.168.1.3 255.255.255.0
VTP-CLIENT2(config-if)#no shutdown
VTP-CLIENT2(config-if)#end
VTP-CLIENT2#copy running-config startup-config
VTP-CLIENT2#


```

### VTP client 1 switch
```
VTP-CLIENT1>enable
Password:
VTP-CLIENT1#configure terminal
VTP-CLIENT1(config)#no ip domain-lookup
VTP-CLIENT1(config)#vtp mode client
VTP-CLIENT1(config)#vtp domain TESTDOMAIN
VTP-CLIENT1(config)#vtp password cisco

VTP-CLIENT1(config)#interface gigabitethernet 0/2
VTP-CLIENT1(config-if)#switchport mode trunk
VTP-CLIENT1(config-if)#no shutdown
VTP-CLIENT1(config-if)#exit

VTP-CLIENT1(config)#interface gigabitethernet 0/1
VTP-CLIENT1(config-if)#switchport mode trunk
VTP-CLIENT1(config-if)#no shutdown
VTP-CLIENT1(config-if)#end
VTP-CLIENT1#

VTP-CLIENT1#configure terminal
VTP-CLIENT1(config)#interface vlan 1
VTP-CLIENT1(config-if)#ip address 192.168.1.2 255.255.255.0
VTP-CLIENT1(config-if)#no shutdown
VTP-CLIENT1(config-if)#end
VTP-CLIENT1#copy running-config startup-config

```
