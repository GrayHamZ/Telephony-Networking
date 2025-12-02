# Network Device Inventory

## Router Specifications

### Branch Routers

#### Router-Branch1
- **Model**: Cisco 2911
- **Modules**: 
  - 2x HWIC-2T (Serial WAN Interface Cards)
- **Interfaces**:
  - **GigabitEthernet Ports**:
    - `Gi0/0` - Router-on-a-stick for VLANs (Data, Voice, Native)
    - `Gi0/1` - Available
    - `Gi0/2` - Available
  - **Serial Ports** (via HWIC-2T modules):
    - `Se0/0/0` - WAN connection to ISP-PLDT-R1 (10.1.1.1/30)
    - `Se0/0/1` - Available
    - `Se0/1/0` - Available
    - `Se0/1/1` - Available

---

### ISP PLDT Routers

#### ISP-PLDT-R1
- **Model**: Cisco 2911
- **Modules**: 
  - 2x HWIC-2T (Serial WAN Interface Cards)
- **Interfaces**:
  - **GigabitEthernet Ports**:
    - `Gi0/0` - Available
    - `Gi0/1` - Available
    - `Gi0/2` - Available
  - **Serial Ports** (via HWIC-2T modules):
    - `Se0/0/0` - WAN connection to Branch1 (10.1.1.2/30)
    - `Se0/0/1` - WAN connection to PLDT-R2 (10.2.2.1/30) - DCE (clock rate)
    - `Se0/1/0` - Available
    - `Se0/1/1` - Available

#### ISP-PLDT-R2
- **Model**: Cisco 2911
- **Modules**: 
  - 2x HWIC-2T (Serial WAN Interface Cards)
- **Interfaces**:
  - **GigabitEthernet Ports**:
    - `Gi0/0` - Available
    - `Gi0/1` - Available
    - `Gi0/2` - Available
  - **Serial Ports** (via HWIC-2T modules):
    - `Se0/0/0` - WAN connection to PLDT-R1 (10.2.2.2/30)
    - `Se0/0/1` - WAN connection to Main-R1 (10.3.3.1/30) - DCE (clock rate)
    - `Se0/1/0` - Available
    - `Se0/1/1` - Available

---

### Main Branch Routers

#### Router-Main-1
- **Model**: Cisco 2911
- **Modules**: 
  - 2x HWIC-2T (Serial WAN Interface Cards)
- **Interfaces**:
  - **GigabitEthernet Ports**:
    - `Gi0/0` - Internal LAN (172.16.0.1/24)
    - `Gi0/1` - Available
    - `Gi0/2` - Available
  - **Serial Ports** (via HWIC-2T modules):
    - `Se0/0/0` - WAN connection to PLDT-R2 (10.3.3.2/30)
    - `Se0/0/1` - Available
    - `Se0/1/0` - Available
    - `Se0/1/1` - Available

---

## Network Topology Summary

```
Branch1-R1 (OSPF Area 0)
    |
    | Se0/0/0 - 10.1.1.0/30
    |
ISP-PLDT-R1 (OSPF ↔ EIGRP Redistribution)
    |
    | Se0/0/1 - 10.2.2.0/30
    |
ISP-PLDT-R2 (EIGRP ↔ OSPF Redistribution)
    |
    | Se0/0/1 - 10.3.3.0/30
    |
Main-R1 (OSPF Area 0)
```

---

## Routing Protocols

- **Branch1-R1**: OSPF Area 0 (Router-ID: 1.1.1.1)
- **ISP-PLDT-R1**: OSPF Area 0 + EIGRP 100 with bidirectional redistribution (Router-ID: 2.2.2.2)
- **ISP-PLDT-R2**: EIGRP 100 + OSPF Area 0 with bidirectional redistribution (Router-ID: 3.3.3.3)
- **Main-R1**: OSPF Area 0 (Router-ID: 1.1.1.1)

---

## Notes

- All serial WAN connections use /30 subnets for point-to-point links
- Clock rate configured on DCE side of serial connections (PLDT routers)
- HWIC-2T modules provide 2 serial ports each (4 total per router with 2 modules)
- Gigabit Ethernet ports used for LAN connections and inter-switch trunking
