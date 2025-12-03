# Chapter 4: Methodology

## Research Design

This project uses applied research methodology, implementing networking concepts in Cisco Packet Tracer to solve IndianSupport.com's communication needs. The approach follows systematic phases: planning, design, configuration, testing, and documentation.

## Project Development Phases

The development of the IndianSupport.com network followed a structured approach divided into several phases:

### Phase 1: Planning and Requirements Analysis

**Requirements Identified:**
- Main branch: 8 departments, 40 computers, 16 phones
- Branch 1 & 2: 3 departments each, 6 computers, 3 phones each
- Services: IP telephony, DHCP, DNS, web, email, dual ISP connectivity
- Equipment: 8 routers, 13 switches, 1 server

### Phase 2: Network Design

**Topology Design:**
- Main branch: Hierarchical design with redundant core routers and multilayer switches
- Branches: Simplified single-router design
- ISP networks: Dual-provider connectivity for redundancy

**IP Addressing:**
- Internal: 192.168.0.0/16 (VLAN numbers match network addresses)
- WAN: 10.0.0.0/8 (/30 subnets for point-to-point links)
- Pattern: VLAN 10 → 192.168.10.0/24, VLAN 20 → 192.168.20.0/24

### Phase 3: Device Configuration

Configuration followed bottom-up approach:

**Step 1: Access Switches**
- Created VLANs for assigned departments
- Configured access ports with data/voice VLANs
- Enabled port security (3 devices max, sticky MAC, restrict mode)
- Configured trunk ports to multilayer switches

**Step 2: Multilayer Switches**
- Created all 17 VLANs on both switches
- Configured trunk ports to routers and access switches
- Configured LACP EtherChannel between MLS switches (Fa0/23-24)

**Step 3: Core Routers (Router-Test-1 & Router-Test-2)**
- Configured 16 sub-interfaces with HSRP (priority 110 vs 100)
- Created DHCP pools for all VLANs (data pools include DNS, voice pools include Option 150)
- Configured OSPF (router IDs 1.1.1.1 and 2.2.2.2, all networks in area 0)
- Configured EIGRP AS 100 on WAN interfaces
- Enabled bidirectional route redistribution
- Configured telephony service (24 phones, numbers 3001-3072)
- Created dial peers for inter-site calling

**Step 4: Branch Routers**
- Branch1-R1: 6 VLANs, OSPF+EIGRP, 3 phones (1001, 1010, 1020)
- Branch2-R1: 6 VLANs, OSPF+EIGRP, 3 phones (2001, 2010, 2020)
- Configured dial peers to reach main branch and other branch

**Step 5: ISP Routers**
- Configured serial interfaces with appropriate IP addressing
- Enabled EIGRP AS 100 on all interfaces

**Step 6: Server (192.168.150.8)**
- DNS: Added A records for all services and gateways
- HTTP: Enabled web service with custom homepage
- Email: Created SMTP/POP3 accounts for all departments

### Phase 4: Testing and Verification

**Connectivity Tests:**
- Layer 2: Verified MAC learning, VLAN creation, trunk operation, EtherChannel status ✓
- Layer 3: Ping tests within VLANs, between VLANs, between sites ✓
- All connectivity tests passed ✓

**HSRP Tests:**
- Verified active/standby status (show standby)
- Tested failover by shutting down Router-Test-1 interface
- Failover occurred in ~5 seconds with no packet loss ✓
- Verified failback when Router-Test-1 returned ✓

**Routing Tests:**
- OSPF: All internal routes present, neighbors established ✓
- EIGRP: WAN routes learned, ISP neighbors up ✓
- Route redistribution working bidirectionally ✓
- Traceroute confirmed expected paths through ISPs ✓

**DHCP Tests:**
- PCs received correct addresses with proper gateway and DNS ✓
- Phones received voice VLAN addresses with Option 150 ✓

**Telephony Tests:**
- All 22 phones registered successfully ✓
- Intra-department calls: Working ✓
- Inter-department calls: Working ✓
- Inter-site calls: Working ✓
- Call quality: Clear with no delays ✓

**Server Services Tests:**
- DNS: Name resolution working from all locations ✓
- Web: Accessible via IP and DNS name from all sites ✓
- Email: Messages sent and received between departments ✓

**Security Tests:**
- Port security blocked unauthorized devices ✓
- VLANs properly isolated traffic ✓

### Phase 5: Documentation

- Saved all device configurations
- Created IP addressing and VLAN tables
- Exported network diagrams
- Documented test results with screenshots
- Wrote complete research paper

## Challenges and Solutions

**Challenge 1 - HSRP Complexity:** Managing identical configurations across 16 sub-interfaces on two routers. *Solution:* Used configuration templates and verified each interface systematically.

**Challenge 2 - Route Redistribution:** Routes not sharing between OSPF and EIGRP initially. *Solution:* Added proper redistribution commands with metrics in both directions.

**Challenge 3 - Dial Peers:** Inter-site calls failing. *Solution:* Verified IP addresses in dial peers and confirmed EIGRP route advertisement.

**Challenge 4 - DHCP Option 150:** Phones not registering automatically. *Solution:* Added Option 150 to all voice VLAN DHCP pools.

**Challenge 5 - Port Security:** Initial "shutdown" mode too restrictive. *Solution:* Changed to "restrict" mode.

**Challenge 6 - EtherChannel:** Port-channel wouldn't form due to protocol mismatch. *Solution:* Configured both sides for LACP active mode.

## Validation

All project requirements were successfully met: 8 departments in main branch ✓, 2 routers with HSRP ✓, 2 MLSs with EtherChannel ✓, 7 access switches ✓, OSPF routing ✓, Branch offices configured ✓, ISP connectivity with EIGRP ✓, IP telephony functional ✓, VLANs and security implemented ✓, Centralized services operational ✓.
