# LAB 4-9: Dynamic Host Configuration Protocol (DHCP)

## 1. Enable and set IP address on LAN interface to be the first IP of the subnet 10.0.0.128/28

Through console connection, enter terminal
```
Ranet-GW>
Ranet-GW>
Ranet-GW>enable
Ranet-GW#
Ranet-GW#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Ranet-GW(config)#interface fastEthernet 0/0
Ranet-GW(config-if)#no shutdown

Ranet-GW(config-if)#
%LINK-5-CHANGED: Interface FastEthernet0/0, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/0, changed state to up

Ranet-GW(config-if)#ip address 10.0.0.129 255.255.255.240
Ranet-GW(config-if)#exit
```

## 2. Enable and set IP address on serial interface to be the last IP of the subnet 77.8.210.0/30
```
Ranet-GW(config)#interface serial 0/0/0
Ranet-GW(config-if)#ip address 77.8.210.2 255.255.255.252
Ranet-GW(config-if)#no shutdown
%LINK-5-CHANGED: Interface Serial0/0/0, changed state to up
Ranet-GW(config-if)#exit
```
## 3. Set the default route to let the connection out to the internet.
```
Ranet-GW(config)#ip route 0.0.0.0 0.0.0.0 serial 0/0/0
```
## 4. Configure to let this router translate between the addresses in this LAN and the addresses ISP gave us (19.5.39.129 - 19.5.39.130) [Remark: use ACL no.1 and pool named "Ranet" only!]

```
Ranet-GW(config)#access-list 1 permit 10.0.0.128 0.0.0.15
Ranet-GW(config)#ip nat pool Ranet 19.5.39.129 19.5.39.130 netmask 255.255.255.252
Ranet-GW(config)#ip nat inside source list 1 pool Ranet overload
Ranet-GW(config-if)#ip nat inside
Ranet-GW(config-if)#exit
Ranet-GW(config)#interface serial 0/0/0
Ranet-GW(config-if)#ip nat outside
Ranet-GW(config-if)#exit
```
## 5. Configure to let this router do as DHCP server for the hosts in LAN. You have to supply all information that is necessary for hosts to connect to the internet, and do not forget to exclude addresses of the gateway and the switch. [  Remark: use pool named "Ranet" also!]
```
Ranet-GW(config)#ip dhcp pool Ranet
Ranet-GW(dhcp-config)#default-router 10.0.0.129
Ranet-GW(dhcp-config)#dns-server 77.8.209.5
Ranet-GW(dhcp-config)#network 10.0.0.128 255.255.255.240
Ranet-GW(dhcp-config)#%DHCPD-4-PING_CONFLICT: DHCP address conflict:  server pinged 10.0.0.129.
Ranet-GW(dhcp-config)#exit
Ranet-GW(config)#ip dhcp excluded-address 10.0.0.129 10.0.0.130
Ranet-GW(config)#end
Ranet-GW#
%SYS-5-CONFIG_I: Configured from console by console
Ranet-GW#
```
