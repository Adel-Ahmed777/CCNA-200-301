# Lab 4 port security
## Activities:
> 1. Configure port security on interface Fa 0/1 of the switch with the following settings :
- Port security enabled
- Mode : restrict
- Allowed mac addresses : 3
- Dynamic mac address learning.

> 2. Configure port security on interface Fa 0/2 of the switch with the following settings :
- Port security enabled
- Mode : shutdown
- Allowed mac addresses : 3
- Dynamic mac address learning.

> 3. Configure port security on interface Fa 0/3 of the switch with the following settings :
- Port security enabled
- Mode : protect
- Static mac address entry : 00E0.A3CE.3236

> 4. From LAPTOP 1 :
- Try to ping 192.168.1.2 and 192.168.1.3. It should work.
- Try to ping 192.168.1.4 and 192.168.1.5. It should work.

> 5. Connect ROGUE laptop to the hub.
- Try to ping 192.168.1.1. It should work.
- Try to ping 192.168.1.4. It should fail.


## 1. Configure port security on interface Fa 0/1 of the switch with the following settings :
- Port security enabled
- Mode : restrict
- Allowed mac addresses : 3
- Dynamic mac address learning.

```
Switch>enable
Switch#configure terminal
Switch(config)#interface fastethernet 0/1
Switch(config-if)# no shutdown
Switch(config-if)#switchport mode access
Switch(config-if)#switchport port-security
Switch(config-if)#switchport port-security maximum 3
Switch(config-if)#switchport port-security mac-address sticky
Switch(config-if)#switchport port-security violation restrict
```

## 2. Configure port security on interface Fa 0/2 of the switch with the following settings :
- Port security enabled
- Mode : shutdown
- Allowed mac addresses : 3
- Dynamic mac address learning.

```
Switch#configure terminal
Switch(config)#interface fastEthernet 0/2
Switch(config-if)# no shutdown
Switch(config-if)#switchport mode access
Switch(config-if)#switchport voice vlan 20
Switch(config-if)#switchport port-security
Switch(config-if)#switchport port-security maximum 3
Switch(config-if)#switchport port-security mac-address sticky
Switch(config-if)#switchport port-security violation shutdown
```

## 3. Configure port security on interface Fa 0/3 of the switch with the following settings :
- Port security enabled
- Mode : protect
- Static mac address entry : 00E0.A3CE.3236

```
Switch#configure terminal
Switch(config)#interface fastethernet 0/3
Switch(config-if)# no shutdown
Switch(config-if)#switchport mode access
Switch(config-if)#switchport port-security
Switch(config-if)#switchport port-security violation protect
Switch(config-if)#switchport port-security mac-address 00E0.A3CE.3236
```
