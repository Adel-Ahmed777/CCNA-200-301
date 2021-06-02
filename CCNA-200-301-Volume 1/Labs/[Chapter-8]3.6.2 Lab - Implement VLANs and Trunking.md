# 3.6.2 Lab - Implement VLANs and Trunking
![](https://raw.githubusercontent.com/Adel-Ahmed777/CCNA-200-301/main/CCNA-200-301-Volume%201/screenshots-vol1/3.6.2_Lab.jpg?token=AMOEUHPRD3SKNPRC2H4LVILAX5CN4)

>## Part 1: Build the Network and Configure Basic Device Settings.

>Step 2: Configure basic settings for each switch.
  
**a.	Console into the switch and enable privileged EXEC mode.**

**b. Assign a device name to the switch.**  
S1
```
Switch>enable
Switch#configure terminal
Switch(config)#hostname S1
```
S2
```
Switch>enable
Switch#configure terminal
Switch(config)#hostname S2
```
**c. Disable DNS lookup**

S1
```
S1(config)#no ip domain lookup
```
S2
```
S2(config)#no ip domain lookup
```
**d.	Assign class as the privileged EXEC encrypted password.**

S1
```
S1(config)#enable secret class
```
S2
```
S2(config)#enable secret class
```
**e.	Assign cisco as the console password and enable login.**

**f.	Assign cisco as the VTY password and enable login.**

S1
```
S1(config)#line console 0
S1(config-line)#password cisco
S1(config-line)#login
S1(config-line)#exit
S1(config)#line vty 0 15
S1(config-line)#password cisco
S1(config-line)#login
S1(config-line)#exit
```
S2
```
S2(config)#line console 0
S2(config-line)#password cisco
S2(config-line)#login
S2(config-line)#exit
S2(config)#line vty 0 15
S2(config-line)#password cisco
S2(config-line)#login
S2(config-line)#exit
```
**g.	Encrypt the plaintext passwords.**

S1
```
S1(config)#service password-encryption
```
S2
```
S2(config)#service password-encryption
```
**h.	Create a banner that warns anyone accessing the device that unauthorized access is prohibited**

S1
```
S1(config)#banner motd "unauthorized access is prohibited"
```
S2
```
S2(config)#banner motd "unauthorized access is prohibited"
```
**i.	Copy the running configuration to the startup configuration.**

S1
```
S1#copy running-config startup-config
```
S2
```
S2#copy running-config startup-config
```

> Step 3: Configure PC hosts.

Add the configuration manually as per the addressing table.

>## Part 2: Create VLANs and Assign Switch Ports

> Step 1: Create VLANs on both switches.

**a.	Create and name the required VLANs on each switch from the table above.**

S1
```
S1#configure terminal
S1(config)#vlan 10
S1(config-vlan)#name Management
S1(config-vlan)#vlan 20
S1(config-vlan)#name Sales
S1(config-vlan)#vlan 30
S1(config-vlan)#name Operations
S1(config-vlan)#vlan 999
S1(config-vlan)#name ParkingLot
S1(config-vlan)#vlan 1000
S1(config-vlan)#name Native
S1(config-vlan)#
```
S2
```
S2#configure terminal
S2(config)#vlan 10
S2(config-vlan)#name Management
S2(config-vlan)#vlan 20
S2(config-vlan)#name Sales
S2(config-vlan)#vlan 30
S2(config-vlan)#name Operations
S2(config-vlan)#vlan 999
S2(config-vlan)#name ParkingLot
S2(config-vlan)#vlan 1000
S2(config-vlan)#name Native
S2(config-vlan)#
```
**b.	Configure the management interface on each switch using the IP address information in the Addressing Table.**

S1
```
S1(config)#interface vlan 10
S1(config-if)#ip address 192.168.10.11 255.255.255.0
S1(config-if)#exit
S1(config)#interface vlan 20
S1(config-if)#ip address 192.168.20.11 255.255.255.0
S1(config-if)#exit
S1(config)#interface vlan 30
S1(config-if)#ip address 192.168.30.11 255.255.255.0
S1(config-if)#exit
```
S2
```
S2(config)#interface vlan 10
S2(config-if)#ip address 192.168.10.12 255.255.255.0
S2(config-if)#exit
```
**c.	Assign all unused ports on the switch to the ParkingLot VLAN, configure them for static access mode, and administratively deactivate them.**

As per the topology, the unused ports on switch one are from 0/2 to 0/5, 0/7 to 0/24 and the two gigabitEthernet ports 0/1 and 0/2.
S1
```
S1(config)#interface range fastEthernet 0/2-5, fastEthernet 0/7-24, gigabitEthernet 0/1-2
S1(config-if-range)#switchport mode access
S1(config-if-range)#switchport access vlan 999
S1(config-if-range)#shutdown
```
As per the topology, the unused ports on switch two are from 0/2 to 0/17, 0/19 to 0/24 and the two gigabitEthernet ports 0/1 and 0/2.
S2
```
S2(config)#interface range fastEthernet 0/2-17, fastEthernet 0/19-24, gigabitEthernet 0/1-2
S2(config-if-range)#switchport mode access
S2(config-if-range)#switchport access vlan 999
S2(config-if-range)#shutdown
```

> Step 2: Assign VLANs to the correct switch interfaces.

**a.	Assign used ports to the appropriate VLAN (specified in the VLAN table above) and configure them for static access mode.**

S1
```
S1(config)#interface fastEthernet 0/6
S1(config-if)#switchport mode access
S1(config-if)#switchport access vlan 20
```
S2
```
S2(config)#interface fastEthernet 0/18
S2(config-if)#switchport mode access
S2(config-if)#switchport access vlan 30
```
**b.	Verify that the VLANs are assigned to the correct interfaces.**

for both switches, enter the following command for verification:**#show vlan brief**

> ## Part 3: Configure an 802.1Q Trunk Between the Switches

> Step 1: Manually configure trunk interface F0/1.
 
**a.	Change the switchport mode on interface F0/1 to force trunking. Make sure to do this on both switches**

S1
```
S1#configure terminal
S1(config)#interface fastEthernet 0/1
S1(config-if)#switchport mode trunk
```
S2
```
S2#configure terminal
S2(config)#interface fastEthernet 0/1
S2(config-if)#switchport mode trunk
```
**b.	Set the native VLAN to 1000 on both switches**

S1
```
S1#configure terminal
S1(config)#interface fastEthernet 0/1
S1(config-if)#switchport trunk native vlan 1000
```
S2
```
S2#configure terminal
S2(config)#interface fastEthernet 0/1
S2(config-if)#switchport trunk native vlan 1000
```
**c.	As another part of trunk configuration, specify that only VLANs 10, 20, 30, and 1000 are allowed to cross the trunk.**

S1
```
S1#configure terminal
S1(config)#interface fastEthernet 0/1
S1(config-if)#switchport trunk allowed vlan remove 1
S1(config-if)#switchport trunk allowed vlan remove 999
S1(config-if)#^Z
```
S2
```
S2#configure terminal
S2(config)#interface fastEthernet 0/1
S2(config-if)#switchport trunk allowed vlan remove 1
S2(config-if)#switchport trunk allowed vlan remove 999
S2(config-if)#^Z
```

> Step 2: Verify connectivity.

Follwoing the above steps PC-A should be able to ping S1 VLAN 20 **successfully** as per the following screenshot:

![](https://raw.githubusercontent.com/Adel-Ahmed777/CCNA-200-301/main/CCNA-200-301-Volume%201/screenshots-vol1/3.6.2%20Lab%20-Part_3_step_2.jpg?token=AMOEUHISP365SBJK3FWWZ53AX5AWG)

Finally, Were the pings from PC-B to S2 successful?

Answer: No. Becasue they are in different VLANS.

The Ping was not successful as per the following screenshot:

![](https://raw.githubusercontent.com/Adel-Ahmed777/CCNA-200-301/main/CCNA-200-301-Volume%201/screenshots-vol1/3.6.2%20Lab%20-Part_3_step_2_2.jpg?token=AMOEUHKSVVHXSBWAX52DWPTAX5BQO)
