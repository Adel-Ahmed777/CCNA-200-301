# Securing user mode and privileged mode with simple passwords:

> ##  How to configure a password before entering enable mode:
```
enable
configure terminal
enable secret [password value]
exit
```

> ##  How to configure console password:
```
enable
configure terminal
line console 0
password [password value]
login
exit
```

> ## How to configure the telnet (vty) password:
```
enable
configure terminal
line vty 0 15
password [password value]
login
exit
```
# Securing user mode access with local usernames and passwords:

> ## How to add usernames with their password:
*Note: you can add as many users as you want*
```
enable
configure terminal
username [name of user] secret [password value]
```

> ## How to configure the console to use locally configured username/password pairs:
```
enable
configure terminal
line console 0
login local
no password
```
**login local :** This command prompts the console to ask the user for both the username and password. **no password :** This command is optional to remove any existing simple shared passwords.

> ## How to configure Telnet (vty) to use locally configured username/password pairs:
```
enable
configure terminal
line vty 0 15
login local
no password
```
**login local :** This command prompts the console to ask the user for both the username and password. **no password :** This command is optional to remove any existing simple shared passwords.

# Securing remote access with secure shell:
> ## How to secure remote access with secure shell:
```
enable
configure terminal
hostname [enter host name]
ip domain-name [example.com]
crypto key generate rsa
```
Next, the following question will appear:
**Note :**
Choose a key modulus size that is between 360 to 2048. A key > 512 will take some time.
```
How many bits in the modulus [512]:
```
The following command is optional. it can be used to only allow SSHv2 connections.
```
ip ssh version 2
```
Next, configure the vty lines for local username support, just like with Telnet.
```
line vty 0 15
login local
exit
```
Finally, Define the local usernames, just like with Telnet.
```
username [name of user] secret [password value]
username [name of user] secret [password value]
^Z
```

> ## How to configure a cisco switch to support SSH using local usernames:
```
enable
configure terminal
hostname [enter host name]
ip domain-name [example.com]
crypto key generate rsa
```
Next, the following question will appear:
**Note :**
Choose a key modulus size that is between 360 to 2048. A key > 512 will take some time.
```
How many bits in the modulus [512]:
```
The following command is optional. it can be used to only allow SSHv2 connections.
```
ip ssh version 2
```
The following command is optional. Vty can be configured with the desired settings to approve SSH and whether to also allow Telnet:
```
line vty 0 15
transport input [choose desired option]
```
>> options for the transpost input command are:
```
transport input all or transport input telnet ssh [Support both Telnet and SSH]
transport input none [Support neither]
transport input telnet [Support only Telnet]
transport input ssh [Support only SSH]
```

> ## How to configure IPv4 on a Switch:
```
enable
configure terminal
interface vlan 1
ip address [add ip address and SNM]
no shutdown
exit [to get out of vlan configuration mode]
ip default-gateway [add ip address for the default gateway]
```

> ## How to configure a switch to learn its IP address with DHCP:
```
enable
configure terminal
interface vlan 1
ip address dhcp
no shutdown
^z
```
