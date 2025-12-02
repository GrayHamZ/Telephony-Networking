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
hostname Branch2-R1

interface gigabitEthernet 0/0
no shutdown
exit

! Sub-interfaces for Department L
interface gigabitEthernet 0/0.10
encapsulation dot1Q 10
ip address 192.168.230.1 255.255.255.0
exit

interface gigabitEthernet 0/0.20
encapsulation dot1Q 20
ip address 192.168.240.1 255.255.255.0
exit

! Sub-interfaces for Department M
interface gigabitEthernet 0/0.30
encapsulation dot1Q 30
ip address 192.168.250.1 255.255.255.0
exit

interface gigabitEthernet 0/0.40
encapsulation dot1Q 40
ip address 192.168.251.1 255.255.255.0
exit

! Sub-interfaces for Department N
interface gigabitEthernet 0/0.50
encapsulation dot1Q 50
ip address 192.168.252.1 255.255.255.0
exit

interface gigabitEthernet 0/0.60
encapsulation dot1Q 60
ip address 192.168.253.1 255.255.255.0
exit

! Management VLAN
interface gigabitEthernet 0/0.99
encapsulation dot1Q 99 native
ip address 192.168.254.1 255.255.255.0
exit

ip dhcp excluded-address 192.168.230.1
ip dhcp excluded-address 192.168.240.1
ip dhcp excluded-address 192.168.250.1
ip dhcp excluded-address 192.168.251.1
ip dhcp excluded-address 192.168.252.1
ip dhcp excluded-address 192.168.253.1

! DHCP Pool for Department L - Data
ip dhcp pool DATA_POOL_DEPT_L
network 192.168.230.0 255.255.255.0
default-router 192.168.230.1
dns-server 192.168.150.8
exit

! DHCP Pool for Department L - Voice
ip dhcp pool VOICE_POOL_DEPT_L
network 192.168.240.0 255.255.255.0
default-router 192.168.240.1
option 150 ip 192.168.240.1
exit

! DHCP Pool for Department M - Data
ip dhcp pool DATA_POOL_DEPT_M
network 192.168.250.0 255.255.255.0
default-router 192.168.250.1
dns-server 192.168.150.8
exit

! DHCP Pool for Department M - Voice
ip dhcp pool VOICE_POOL_DEPT_M
network 192.168.251.0 255.255.255.0
default-router 192.168.251.1
option 150 ip 192.168.251.1
exit

! DHCP Pool for Department N - Data
ip dhcp pool DATA_POOL_DEPT_N
network 192.168.252.0 255.255.255.0
default-router 192.168.252.1
dns-server 192.168.150.8
exit

! DHCP Pool for Department N - Voice
ip dhcp pool VOICE_POOL_DEPT_N
network 192.168.253.0 255.255.255.0
default-router 192.168.253.1
option 150 ip 192.168.253.1
exit

! WAN Interface to ISP GLOBE-R1 (Serial)
interface serial 0/0/0
ip address 10.5.5.1 255.255.255.252
clock rate 64000
no shutdown
exit

! OSPF Configuration for internal networks
router ospf 1
router-id 2.2.2.2
network 192.168.230.0 0.0.0.255 area 0
network 192.168.240.0 0.0.0.255 area 0
network 192.168.250.0 0.0.0.255 area 0
network 192.168.251.0 0.0.0.255 area 0
network 192.168.252.0 0.0.0.255 area 0
network 192.168.253.0 0.0.0.255 area 0
network 192.168.254.0 0.0.0.255 area 0
exit

! EIGRP Configuration for ISP connectivity
router eigrp 100
network 10.5.5.0 0.0.0.3
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
ip source-address 192.168.240.1 port 2000
auto assign 1 to 3
exit

! Phone Directory Number - Department L
ephone-dn 1
number 2001
exit

! Phone Directory Number - Department M
ephone-dn 2
number 2010
exit

! Phone Directory Number - Department N
ephone-dn 3
number 2020
exit

end
write
