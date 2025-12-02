# TechCorp Solutions - IP Telephony Configuration Guide

## Project Overview
This documentation contains all configuration files for the TechCorp Solutions IP Telephony Network deployment across Main Branch, Branch 1, Branch 2, and ISP networks.

---

## File Structure
```
Telephony Documentation/
├── Instructions.md                    # Original project requirements
├── topology-overview.md               # Network architecture and design
├── master-addressing-table.md         # Complete IP addressing scheme
├── device-inventory.md                # Device models and port allocations
├── README.md                          # This file
├── CONFIG-INDEX.md                    # Quick reference for all configs
└── configs/
    ├── main-branch/
    │   ├── routers/
    │   │   ├── Router-Main-1.txt
    │   │   └── Router-Main-2.txt
    │   ├── multilayer-switches/
    │   │   ├── MLS-Core-1.txt
    │   │   └── MLS-Core-2.txt
    │   └── access-switches/
    │       ├── SW-Floor1-1.txt
    │       ├── SW-Floor1-2.txt
    │       ├── SW-Floor2-1.txt
    │       ├── SW-Floor2-2.txt
    │       ├── SW-Floor3-1.txt
    │       ├── SW-Floor3-2.txt
    │       └── SW-Floor3-3.txt
    ├── branch-1/
    │   ├── Router-Branch1.txt
    │   ├── SW-Branch1-1.txt
    │   └── SW-Branch1-2.txt
    ├── branch-2/
    │   ├── Router-Branch2.txt
    │   ├── SW-Branch2-1.txt
    │   └── SW-Branch2-2.txt
    ├── isp-pldt/
    │   ├── ISP-PLDT-R1.txt
    │   └── ISP-PLDT-R2.txt
    └── isp-globe/
        ├── ISP-GLOBE-R1.txt
        └── ISP-GLOBE-R2.txt
```

---

## Quick Start Guide

### Step 1: Review Documentation
1. **topology-overview.md** - Understand the network architecture
2. **master-addressing-table.md** - Review all IP addresses and VLANs
3. **device-inventory.md** - Check device models and port usage

### Step 2: Build the Topology in Packet Tracer
1. Add all devices according to `device-inventory.md`
2. Connect devices following the physical connections map
3. Label all devices with proper hostnames

### Step 3: Apply Configurations
1. Copy configurations from the respective `.txt` files
2. Paste directly into device CLI in Packet Tracer
3. Verify with `show running-config`

### Step 4: Configure End Devices
- **PCs**: Set to DHCP (automatically obtain IP)
- **IP Phones**: Power on and they will auto-register
- **Servers**: Configure static IPs per master-addressing-table.md

### Step 5: Verification
Run these commands to verify configuration:

#### On Routers:
```
show ip interface brief
show ip route
show ip ospf neighbor          (Main Branch)
show ip bgp summary            (Main Branch & ISP)
show ip eigrp neighbors        (ISP only)
```

#### On Multilayer Switches:
```
show ip interface brief
show vlan brief
show spanning-tree summary
show standby brief
show ip route
show ip ospf neighbor
```

#### On Access Switches:
```
show vlan brief
show interface status
show spanning-tree summary
show port-security interface [interface]
show ip dhcp snooping
```

#### For IP Telephony:
```
show telephony-service
show ephone summary
show ephone-dn summary
```

---

## Configuration Highlights

### Security Features Implemented
✅ **Port Security** - MAC address limits on all access ports  
✅ **DHCP Snooping** - Prevents rogue DHCP servers  
✅ **Dynamic ARP Inspection** - Prevents ARP spoofing  
✅ **BPDU Guard** - Protects against spanning tree attacks  
✅ **Root Guard** - Prevents unauthorized root bridges  
✅ **SSH v2** - Secure remote access  
✅ **Password Encryption** - All passwords encrypted  

### Redundancy Features
✅ **Dual Routers** - ISP redundancy at Main Branch  
✅ **Dual Core Switches** - MLS redundancy with HSRP  
✅ **EtherChannel** - Link aggregation between cores  
✅ **Dual Uplinks** - Each access switch has 2 uplinks  
✅ **OSPF** - Dynamic routing for failover  
✅ **Rapid PVST+** - Fast spanning tree convergence  

### VoIP Features
✅ **Voice VLANs** - Separate VLANs for voice traffic  
✅ **QoS** - Priority queuing for voice packets  
✅ **PoE** - Power over Ethernet for IP phones  
✅ **Call Manager** - Centralized telephony service  
✅ **Auto-registration** - Phones automatically register  
✅ **TFTP Server** - For phone configuration files  

---

## Default Credentials

### All Devices
- **Enable Secret**: cisco123
- **Console Password**: console123
- **VTY Password**: vty123
- **SSH Username**: admin
- **SSH Password**: admin123

### VTP Domain (Main Branch)
- **Domain**: TECHCORP
- **Password**: techcorp123

⚠️ **IMPORTANT**: Change these passwords in production environments!

---

## Common IP Addresses to Remember

| Service | IP Address |
|---------|------------|
| MLS-Core-1 Management | 10.0.1.10 |
| MLS-Core-2 Management | 10.0.1.11 |
| Web Server | 10.0.200.10 |
| Email Server | 10.0.200.11 |
| DNS Server | 10.0.200.12 |
| DHCP Server | 10.0.200.13 |
| TFTP Server | 10.0.200.14 |
| Call Manager | 10.0.200.15 |

---

## VLAN Summary

### Main Branch
- **VLAN 10**: HR (10.0.10.0/24)
- **VLAN 11**: Finance (10.0.11.0/24)
- **VLAN 20**: IT (10.0.20.0/24)
- **VLAN 21**: Sales (10.0.21.0/24)
- **VLAN 22**: Marketing (10.0.22.0/24)
- **VLAN 30**: Operations (10.0.30.0/24)
- **VLAN 31**: Customer Service (10.0.31.0/24)
- **VLAN 32**: Executive (10.0.32.0/24)
- **VLAN 100**: Voice (10.0.100.0/23)
- **VLAN 200**: Servers (10.0.200.0/24)

### Branch 1
- **VLAN 41-43**: Office Data (192.168.10-12.0/24)
- **VLAN 101**: Voice (192.168.100.0/24)

### Branch 2
- **VLAN 51-53**: Office Data (192.168.20-22.0/24)
- **VLAN 102**: Voice (192.168.101.0/24)

---

## Routing Protocol Configuration

### OSPF (Main Branch)
- **Process ID**: 1
- **Area**: 0 (Backbone)
- **Router IDs**:
  - Router-Main-1: 1.1.1.1
  - Router-Main-2: 2.2.2.2
  - MLS-Core-1: 3.3.3.3
  - MLS-Core-2: 4.4.4.4

### EIGRP (ISP Networks)
- **PLDT AS**: 100
- **GLOBE AS**: 200

### BGP (Internet Connectivity)
- **TechCorp AS**: 65001
- **PLDT AS**: 65100
- **GLOBE AS**: 65200

---

## Troubleshooting Tips

### No Connectivity Issues
1. Check cable connections in Packet Tracer
2. Verify interfaces are up: `show ip interface brief`
3. Check VLAN assignments: `show vlan brief`
4. Verify routing: `show ip route`
5. Test gateway: `ping [default-gateway]`

### IP Phone Not Working
1. Verify PoE is enabled on switch port
2. Check voice VLAN configuration
3. Verify DHCP pool for voice VLAN
4. Check telephony-service configuration
5. Verify option 150 in DHCP (TFTP server)

### Inter-VLAN Routing Issues
1. Check SVI interfaces are up on MLS
2. Verify `ip routing` is enabled
3. Check HSRP status: `show standby brief`
4. Verify trunk links: `show interface trunk`

### OSPF Not Working
1. Check network statements match interface IPs
2. Verify area 0 configuration
3. Check for passive interfaces where needed
4. Verify router IDs: `show ip ospf`

### Spanning Tree Issues
1. Check root bridge priority
2. Verify portfast on access ports
3. Check for blocked ports: `show spanning-tree`
4. Verify BPDU guard is working

---

## Testing Checklist

- [ ] All devices powered on and accessible
- [ ] All interfaces showing "up/up"
- [ ] VLANs created and assigned correctly
- [ ] Trunk links operational
- [ ] OSPF neighbors established
- [ ] HSRP active/standby roles correct
- [ ] DHCP pools distributing addresses
- [ ] Inter-VLAN routing functional
- [ ] Internet access from all sites
- [ ] IP phones registered and making calls
- [ ] Port security working
- [ ] SSH access functional
- [ ] Redundancy failover tested

---

## Support Information

### Project Details
- **Company**: TechCorp Solutions
- **Project Type**: IP Telephony Network
- **Date**: December 2025
- **Simulation Tool**: Cisco Packet Tracer

### Documentation References
- See `topology-overview.md` for network diagrams
- See `master-addressing-table.md` for all IP addresses
- See `device-inventory.md` for hardware specifications
- See `CONFIG-INDEX.md` for configuration quick reference

---

## Notes for Implementation

1. **Configure in order**: Start with core (MLS), then distribution (routers), then access (switches)
2. **Test incrementally**: Verify each layer before moving to the next
3. **Save configurations**: Use `write memory` or `copy run start` after each device
4. **Document changes**: Keep track of any modifications made during deployment
5. **Backup configs**: Save all running-configs before making changes

---

## Version History
- **v1.0** - Initial configuration deployment (December 2025)

---

*This documentation is designed for use with Cisco Packet Tracer for educational purposes.*
#   T e l e p h o n y - N e t w o r k i n g  
 