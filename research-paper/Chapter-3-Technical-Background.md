# Chapter 3: Technical Background

## Network Architecture

**Main Branch:** 2 routers (HSRP), 2 multilayer switches (EtherChannel), 7 access switches, 40 computers, 16 IP phones, 1 server

**Branch 1 (PLDT ISP):** 1 router, 2 switches, 6 computers, 3 IP phones (Departments I, J, K)

**Branch 2 (GLOBE ISP):** 1 router, 2 switches, 6 computers, 3 IP phones (Departments L, M, N)

**ISP Networks:** 4 routers (2 per ISP) using EIGRP routing

## IP Addressing Scheme

Each department has separate data and voice VLANs with matching network addresses:

**Main Branch Pattern:**
- Dept A: VLAN 10 (192.168.10.0/24) data, VLAN 20 (192.168.20.0/24) voice
- Dept B: VLAN 30 (192.168.30.0/24) data, VLAN 40 (192.168.40.0/24) voice
- Pattern continues through Dept H (VLANs 150/160)
- Management: VLAN 99 (192.168.99.0/24)

**WAN Connections:** Point-to-point /30 networks from 10.0.0.0/8 range

## VLAN Configuration

**Data VLANs:** Carry computer traffic (web, files, applications)
**Voice VLANs:** Dedicated to IP phone traffic for optimal call quality
**Native VLAN (99):** Management traffic on trunk links

Access ports support both data and voice VLANs simultaneously - phones tag their traffic while computers send untagged traffic.

## Routing Implementation

**OSPF (Main Branch):** All internal networks in Area 0, providing redundancy and fast convergence. Both routers maintain identical routing databases.

**EIGRP (ISP Connectivity):** Connects sites through PLDT and GLOBE networks. AS 100 throughout.

**Route Redistribution:** OSPF routes redistributed into EIGRP (advertise internal networks), EIGRP routes redistributed into OSPF (learn remote sites).

## HSRP Configuration

Provides active/standby router redundancy using virtual IP addresses. Router-Test-1 (priority 110) is normally active, Router-Test-2 (priority 100) is standby. Failover occurs within 3-10 seconds if active router fails. All 16 VLANs use HSRP with consistent configuration.

## DHCP Implementation

Each router has identical DHCP pools for every VLAN:
- Data VLANs: Include DNS server (192.168.150.8) and HSRP virtual gateway
- Voice VLANs: Include Option 150 pointing to telephony service
- Excluded addresses: .1 (virtual IP), .2 (Router-Test-1), .3 (Router-Test-2)

## IP Telephony System

**Telephony Service:** Runs on both routers with identical configuration
**Phone Numbers:** 3xxx (main branch), 1xxx (Branch 1), 2xxx (Branch 2)
**Dial Peers:** Route calls between sites using destination patterns (1... routes to Branch 1, 2... routes to Branch 2)

Each router supports 24 phones with automatic registration via DHCP Option 150.

## Switch Architecture

**Multilayer Switches:** Create VLANs, connect to routers via trunk, interconnect via LACP EtherChannel (200 Mbps combined bandwidth)

**Access Switches:** Configure access ports with data/voice VLANs, enable port security (max 3 devices, sticky MAC learning, restrict violation mode), use PortFast for faster port initialization

## Server Services

Server at 192.168.150.8 (VLAN 150) provides:
- **DNS:** Name resolution (server.local → 192.168.150.8)
- **HTTP/HTTPS:** Internal web hosting
- **SMTP/POP3/IMAP:** Internal email system

All DHCP pools point to this server for DNS, making services accessible from any location.

## Security Features

**Port Security:** Limits devices per port, learns MAC addresses, blocks unauthorized access
**VLAN Segmentation:** Isolates department traffic, prevents unauthorized access
**Native VLAN 99:** Unused by hosts, reduces VLAN hopping attacks
**Trunk Security:** Native VLAN on all trunks for consistent security posture
