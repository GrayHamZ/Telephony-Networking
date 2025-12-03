# Chapter 5: Discussion and Implementation

## Main Branch Implementation

**HSRP Redundancy:** Two routers with identical configurations provide automatic failover within 5 seconds. Router-Test-1 (priority 110) is normally active while Router-Test-2 (priority 100) stands by. Testing confirmed seamless failover with no service interruption.

**Inter-VLAN Routing:** Router-on-a-stick configuration with 16 sub-interfaces handles all department traffic. Sub-interface numbers match VLAN numbers (0/0.10 for VLAN 10) for easy management.

**DHCP Design:** Router-based DHCP eliminates need for separate server while providing redundancy. All pools use HSRP virtual IPs as gateways, ensuring continuity during failover. Voice VLANs include Option 150 for automatic phone registration.

**Telephony Implementation:** Router-integrated telephony service supports 24 phones per router using logical numbering (3xxx for main branch). Auto-assign feature simplifies phone deployment.

**EtherChannel:** LACP-bonded 200 Mbps link between multilayer switches provides bandwidth and redundancy. Load balancing distributes traffic across both links.

**Access Layer:** Switches use access/voice VLAN configuration allowing phones and computers on single ports. Port security (3 device max, sticky MAC, restrict mode) and PortFast improve security and performance.

**Server Placement:** Centralized server at 192.168.150.8 provides DNS, web, and email services accessible from all locations via inter-VLAN routing.

## Branch Implementation

**Simplified Design:** Single router per branch appropriate for smaller operations. VLAN numbers reused from main branch (locally significant only) with unique IP networks.

**Telephony:** Each branch router supports 3 phones with distinct numbering (1xxx for Branch 1, 2xxx for Branch 2) clearly identifying location.

## ISP Connectivity

**Dual ISP Strategy:** PLDT and GLOBE provide path diversity, load distribution, and regional coverage. Main branch connects to both, branches connect to one each.

**EIGRP Implementation:** Efficient routing between sites with fast convergence. AS 100 used throughout for consistency.

**Route Redistribution:** Critical for multi-protocol environment. OSPF routes redistributed into EIGRP (advertise internal networks), EIGRP routes redistributed into OSPF (learn remote sites). Testing with "show ip route" confirmed proper operation.

## Inter-Site Telephony

**Dial Peer Operation:** Routing rules for calls based on number patterns. Example: destination-pattern 1... routes to 192.168.180.1 (Branch 1). Successful cross-site calling confirms all components working together: VLANs, OSPF, EIGRP, redistribution, and telephony services.

## Security Implementation

**Port Security:** Restricts devices per port, learns MAC addresses, blocks unauthorized access. "Restrict" mode blocks violations without disabling ports entirely.

**VLAN Segmentation:** Isolates department traffic, contains breaches, enables department-specific policies.

**Native VLAN 99:** Unused by hosts, reduces VLAN hopping attack surface.

## Key Lessons Learned

1. **Redundancy requires identical configuration** - Small differences cause failover issues
2. **Route redistribution is complex but essential** - Enables multi-protocol integration
3. **Logical numbering schemes simplify management** - Matching VLANs to networks aids troubleshooting
4. **Testing reveals configuration errors** - Systematic testing critical for success
5. **Documentation saves time** - Planned addressing speeds configuration
6. **Bottom-up implementation works** - Each layer verified before adding complexity
7. **Incremental changes aid troubleshooting** - One change at a time isolates issues

## Troubleshooting Examples

**Phones Not Registering:** Missing DHCP Option 150. Solution: Added option to voice VLAN pools.

**Calls Between Sites Failing:** Incomplete route redistribution. Solution: Added "redistribute eigrp 100 subnets" to OSPF.

**EtherChannel Down:** Protocol mismatch (LACP vs PAgP). Solution: Configured both sides for LACP active.

**VLANs Not Passing:** Missing from trunk allowed list. Solution: Added VLANs to trunk configuration.

## Project Success

All objectives achieved: network supports data and voice traffic ✓, VLANs implemented ✓, HSRP redundancy functional ✓, OSPF routing operational ✓, branches connected via ISPs ✓, IP phones working across sites ✓, security features enabled ✓, centralized services deployed ✓. The IndianSupport.com network is fully functional and meets all requirements.
