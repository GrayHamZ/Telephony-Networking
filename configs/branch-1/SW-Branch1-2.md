enable
configure terminal

host SW-Branch1-2

ip domain-name indiansupport.com
crypto key generate rsa general-keys modulus 1024
username admin secret cisco
line vty 0 15
login local
transport input ssh
exit

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

! VLANs for Department K
vlan 50
name DATA_DEPT_K
exit
vlan 60
name VOICE_DEPT_K
exit

vlan 99
name NATIVE_VLAN
exit

interface vlan 99
ip address 192.168.199.3 255.255.255.0
no shutdown
exit

ip default-gateway 192.168.199.1

! Access ports for IP Phones and PCs (Department J)
interface range fastEthernet 0/1 - 10
switchport mode access
switchport access vlan 30
switchport voice vlan 40
switchport port-security
switchport port-security maximum 3
switchport port-security mac-address sticky
switchport port-security violation restrict
spanning-tree portfast
no shutdown
exit

! Access ports for IP Phones and PCs (Department K)
interface range fastEthernet 0/11 - 20
switchport mode access
switchport access vlan 50
switchport voice vlan 60
switchport port-security
switchport port-security maximum 3
switchport port-security mac-address sticky
switchport port-security violation restrict
spanning-tree portfast
no shutdown
exit

! Trunk to Router
interface gigabitEthernet 0/1
switchport mode trunk
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,50,60,99
no shutdown
exit

interface range fastEthernet 0/23 - 24
 default interface fastEthernet 0/23
 default interface fastEthernet 0/24
 
interface range fastEthernet 0/23 - 24
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