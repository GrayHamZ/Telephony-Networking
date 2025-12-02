enable
configure terminal
hostname Main-R1

! Interface to PLDT-R2 (Serial)
interface serial 0/0/0
ip address 10.3.3.2 255.255.255.252
no shutdown
exit

! Internal LAN Interface
interface gigabitEthernet 0/0
ip address 172.16.0.1 255.255.255.0
no shutdown
exit

! OSPF Configuration for internal networks
router ospf 1
router-id 4.4.4.4
network 172.16.0.0 0.0.0.255 area 0
exit

! EIGRP Configuration for ISP connectivity
router eigrp 100
network 10.3.3.0 0.0.0.3
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

end
write