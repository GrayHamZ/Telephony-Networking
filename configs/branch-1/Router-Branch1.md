! Prerequisiste for telephony

enable
configure terminal
license boot module c2900 technology-package uck9
! ENTER YES AFTER

end
write
reload

! main config

enable
configure terminal
hostname Branch1-R1

ip domain-name indiansupport.com
crypto key generate rsa general-keys modulus 1024
username admin secret cisco
line vty 0 4
login local
transport input ssh
exit

ipv6 unicast-routing

interface gigabitEthernet 0/0
no shutdown
exit

! Sub-interfaces for Department I
interface gigabitEthernet 0/0.10
encapsulation dot1Q 10
ip address 192.168.170.1 255.255.255.0
ipv6 address 2001:db8:ACAD:170::1/64
ipv6 enable
exit

interface gigabitEthernet 0/0.20
encapsulation dot1Q 20
ip address 192.168.180.1 255.255.255.0
ipv6 address 2001:db8:ACAD:180::1/64
ipv6 enable
exit

! Sub-interfaces for Department J
interface gigabitEthernet 0/0.30
encapsulation dot1Q 30
ip address 192.168.190.1 255.255.255.0
ipv6 address 2001:db8:ACAD:190::1/64
ipv6 enable
exit

interface gigabitEthernet 0/0.40
encapsulation dot1Q 40
ip address 192.168.200.1 255.255.255.0
ipv6 address 2001:db8:ACAD:200::1/64
ipv6 enable
exit

! Sub-interfaces for Department K
interface gigabitEthernet 0/0.50
encapsulation dot1Q 50
ip address 192.168.210.1 255.255.255.0
ipv6 address 2001:db8:ACAD:210::1/64
ipv6 enable
exit

interface gigabitEthernet 0/0.60
encapsulation dot1Q 60
ip address 192.168.220.1 255.255.255.0
ipv6 address 2001:db8:ACAD:220::1/64
ipv6 enable
exit

! Management VLAN
interface gigabitEthernet 0/0.99
encapsulation dot1Q 99 native
ip address 192.168.199.1 255.255.255.0
ipv6 address 2001:db8:ACAD:199::1/64
ipv6 enable
exit

ip dhcp excluded-address 192.168.170.1
ip dhcp excluded-address 192.168.180.1
ip dhcp excluded-address 192.168.190.1
ip dhcp excluded-address 192.168.200.1
ip dhcp excluded-address 192.168.210.1
ip dhcp excluded-address 192.168.220.1

! DHCP Pool for Department I - Data
ip dhcp pool DATA_POOL_DEPT_I
network 192.168.170.0 255.255.255.0
default-router 192.168.170.1
dns-server 192.168.150.8
exit

! DHCP Pool for Department I - Voice
ip dhcp pool VOICE_POOL_DEPT_I
network 192.168.180.0 255.255.255.0
default-router 192.168.180.1
option 150 ip 192.168.180.1
exit

! DHCP Pool for Department J - Data
ip dhcp pool DATA_POOL_DEPT_J
network 192.168.190.0 255.255.255.0
default-router 192.168.190.1
dns-server 192.168.150.8
exit

! DHCP Pool for Department J - Voice
ip dhcp pool VOICE_POOL_DEPT_J
network 192.168.200.0 255.255.255.0
default-router 192.168.200.1
option 150 ip 192.168.200.1
exit

! DHCP Pool for Department K - Data
ip dhcp pool DATA_POOL_DEPT_K
network 192.168.210.0 255.255.255.0
default-router 192.168.210.1
dns-server 192.168.150.8
exit

! DHCP Pool for Department K - Voice
ip dhcp pool VOICE_POOL_DEPT_K
network 192.168.220.0 255.255.255.0
default-router 192.168.220.1
option 150 ip 192.168.220.1
exit

! WAN Interface to ISP PLDT-R1 (Serial)
interface serial 0/0/0
ip address 10.1.1.1 255.255.255.252
clock rate 64000
no shutdown
exit

! OSPF Configuration for internal networks
router ospf 1
router-id 1.1.1.1
network 192.168.170.0 0.0.0.255 area 0
network 192.168.180.0 0.0.0.255 area 0
network 192.168.190.0 0.0.0.255 area 0
network 192.168.200.0 0.0.0.255 area 0
network 192.168.210.0 0.0.0.255 area 0
network 192.168.220.0 0.0.0.255 area 0
network 192.168.199.0 0.0.0.255 area 0
exit

! EIGRP Configuration for ISP connectivity
router eigrp 100
network 10.1.1.0 0.0.0.3
no auto-summary
exit

! Redistribute OSPF into EIGRP (advertise internal networks to ISP)
router eigrp 100
redistribute ospf 1 metric 10000 100 255 1 1500
exit

! Redistribute EIGRP into OSPF (learn remote networks from ISP)
router ospf 1
redistribute eigrp 100 subnets
exit

telephony-service
max-ephones 3
max-dn 3
ip source-address 192.168.180.1 port 2000
auto assign 1 to 3
exit

! Phone Directory Number - Department I
ephone-dn 1
number 1001
exit

! Phone Directory Number - Department J
ephone-dn 2
number 1010
exit

! Phone Directory Number - Department K
ephone-dn 3
number 1020
exit

! Dial-peer to Test network (phone numbers 3xxx)
dial-peer voice 1 voip
destination-pattern 3...
session target ipv4:192.168.20.2
exit

! Dial-peer to Branch-2 (phone numbers 2xxx)
dial-peer voice 2 voip
destination-pattern 2...
session target ipv4:192.168.240.1
exit

end
write