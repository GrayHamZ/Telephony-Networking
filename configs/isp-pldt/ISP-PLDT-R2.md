enable
configure terminal
hostname ISP-PLDT-R2

! Interface to PLDT-R1 (Serial)
interface serial 0/0/0
ip address 10.2.2.2 255.255.255.252
no shutdown
exit

! Interface to Main-R1 (Serial)
interface serial 0/0/1
ip address 10.3.3.1 255.255.255.252
clock rate 64000
no shutdown
exit

! EIGRP Configuration
router eigrp 100
network 10.2.2.0 0.0.0.3
network 10.3.3.0 0.0.0.3
no auto-summary
exit

end
write