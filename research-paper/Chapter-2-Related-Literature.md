# Chapter 2: Related Literature

## IP Telephony

IP telephony (VoIP) transmits voice calls over data networks instead of traditional phone lines. Voice is converted into data packets, transmitted across the network, and converted back to audio at the destination. This technology is cost-effective because it uses a single network infrastructure for both voice and data, reducing equipment and maintenance costs.

## Virtual Local Area Networks (VLANs)

VLANs divide one physical network into multiple logical networks, improving organization and security. For IP telephony, separate VLANs for voice and data traffic provide:
- Better voice quality (voice traffic isn't affected by data traffic)
- Improved security (voice and data networks are isolated)
- Easier troubleshooting (issues can be traced to specific VLANs)

The industry standard uses 802.1Q protocol for VLAN tagging, allowing network devices to identify which VLAN packets belong to.

## Routing Protocols

**OSPF (Open Shortest Path First):** A link-state protocol where routers share connection information to build a complete network map. OSPF is ideal for internal networks because it quickly adapts to changes, works with multi-vendor equipment, and uses bandwidth efficiently.

**EIGRP (Enhanced Interior Gateway Routing Protocol):** Cisco's hybrid protocol combining features from different routing types. EIGRP is used for ISP connections due to its fast convergence, efficient bandwidth usage, and automatic route summarization.

## Network Redundancy

**HSRP (Hot Standby Router Protocol):** Provides router redundancy through active/standby configuration. If the active router fails, the standby router takes over automatically within seconds, ensuring continuous network availability without user intervention.

**EtherChannel:** Bundles multiple physical links into one logical connection, providing increased bandwidth and redundancy. If one link fails, traffic continues on remaining links while load balancing distributes traffic across all active connections.

## Network Security

**Port Security:** Controls which devices can connect to switch ports by learning MAC addresses and blocking unauthorized devices. This prevents rogue devices from accessing the network.

**VLAN Segmentation:** Isolates traffic between departments, containing security breaches and enabling different security policies per VLAN.

## DHCP and Network Services

**DHCP:** Automatically assigns IP addresses and network configuration to devices. For IP phones, DHCP Option 150 tells phones where to find the call processing server, enabling automatic phone configuration.

**DNS:** Translates friendly names (like "server.local") to IP addresses, making networks easier to use and manage.

**Email Services:** Internal email systems use SMTP for sending and POP3/IMAP for receiving messages.

## Best Practices

Industry-standard network design practices include:
1. Plan thoroughly before implementation
2. Use structured IP addressing schemes
3. Document all configurations
4. Implement redundancy for critical systems
5. Build security from the start
6. Test all features thoroughly
7. Design for future growth
