enable
configure terminal

vlan 10
name DATA_VLAN
vlan 20
name VOICE_VLAN
vlan 99
name NATIVE_VLAN
exit

interface range fastEthernet 0/1 - 10
switchport mode access
switchport access vlan 10
switchport voice vlan 20
spanning-tree portfast
exit

interface gigabitEthernet 0/1
switchport mode trunk
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,99

interface range fastEthernet 0/23 - 24
 default interface fastEthernet 0/23
 default interface fastEthernet 0/24
 
interface range fastEthernet 0/23 - 24
 channel-protocol lacp
 channel-group 1 mode active
 no shutdown
 exit

interface port-channel 1
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,99
 no shutdown
 exit

write