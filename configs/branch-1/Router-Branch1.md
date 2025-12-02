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

interface gigabitEthernet 0/0
no shutdown
exit

interface gigabitEthernet 0/0.10
encapsulation dot1Q 10
ip address 192.168.170.1 255.255.255.0
exit

interface gigabitEthernet 0/0.20
encapsulation dot1Q 20
ip address 192.168.180.1 255.255.255.0
exit

interface gigabitEthernet 0/0.99
encapsulation dot1Q 99 native
ip address 192.168.199.1 255.255.255.0
exit

ip dhcp excluded-address 192.168.170.1
ip dhcp excluded-address 192.168.180.1

ip dhcp pool DATA_POOL
network 192.168.170.0 255.255.255.0
default-router 192.168.170.1
dns-server 192.168.150.8
exit

ip dhcp pool VOICE_POOL
network 192.168.180.0 255.255.255.0
default-router 192.168.180.1
option 150 ip 192.168.180.1
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
max-ephones 5
max-dn 5
ip source-address 192.168.180.1 port 2000
auto assign 1 to 5
exit
ephone-dn 1
number 1001
ephone-dn 2
number 1002
ephone-dn 3
number 1003

end
write