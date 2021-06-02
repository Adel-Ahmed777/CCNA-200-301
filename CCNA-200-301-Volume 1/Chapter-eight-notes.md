# How to create a VLAN, name it and assign it to an interface

**Configuration steps**
```
enable
configure terminal
vlan [vlan id]
name [add name]
exit

interface [port type] [add port number]
switchport access vlan [add vlan id]
switchport mode access

exit
end
```
> To assign multiple interfaces to a specific VLAN, Type **interface range fastethernet [add range id]**  .
Example **interface range fastEthernet 0/11 -12**

# How to configure VLAN trunking between two switches

> For trunking you can use the following command options based on the deisred trunking option:
>
> **switchport mode trunk**
>
> **switchport mode dynamic desirable**
>
> **switchport mode dynamic auto**

**VLAN trunking configuration steps**
```
SW1>enable
SW1#configure terminal
SW1(config)#interface [port type] [add port number]
SW1(config-if)#switchport mode trunk
SW1(config-if)#end
```



# How to confgure data and voice VLAN

**Steps**
1. Create the voice and data VLANS in the global configuration mode
   1. **vlan** *add id*
   2. **name** *add name*
   3. <ins>[Repeat the above steps depending on the number of VLANS needed]</ins>
2. Configure the data VLAN same way you configure an access VLAN
   1. **interface** *type number*
   2. **switchport access vlan** *add VLAN number*
   3. **switchport mode access**
3. Configure the voice
   1. **switchport voice vlan** *id-number*
