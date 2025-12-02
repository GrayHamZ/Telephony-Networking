enable
configure terminal

host SW-Branch1-1

! VLANs for Department I
vlan 10
name DATA_DEPT_I
exit
vlan 20
name VOICE_DEPT_I
exit

! VLANs for Department J
vlan 30
name DATA_DEPT_J
exit
vlan 40
name VOICE_DEPT_J
exit

! VLANs for Department K (for trunk)
vlan 50
name DATA_DEPT_K
exit
vlan 60
name VOICE_DEPT_K
exit

vlan 99
name NATIVE_VLAN
exit

! Access ports for IP Phones and PCs (Department I)
interface range fastEthernet 0/1 - 10
switchport mode access
switchport access vlan 10
switchport voice vlan 20
spanning-tree portfast
no shutdown
exit

! Trunk to Router
interface gigabitEthernet 0/1
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,50,60,99
no shutdown
exit

interface range fastEthernet 0/23 - 24
 default interface fastEthernet 0/23
 default interface fastEthernet 0/24
 
interface range fastEthernet 0/23 - 24
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,60,99
 channel-protocol lacp
 channel-group 1 mode active
 no shutdown
 exit

interface port-channel 1
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,60,99
 no shutdown
 exit

write