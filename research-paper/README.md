# IndianSupport.com IP Telephony Network - Research Paper

## Complete Documentation for NET 2 Final Project

**Company:** IndianSupport.com  
**Project Type:** IP Telephony Network Implementation  
**Date:** December 2025  
**Software Used:** Cisco Packet Tracer

---

## Document Structure

This research paper contains the following chapters:

1. **Chapter 1: Introduction**
   - Background of the Study
   - Problem Statement
   - Objectives of the Study
   - Scope and Limitations
   - Significance of the Study

2. **Chapter 2: Related Literature**
   - Overview of IP Telephony
   - Virtual Local Area Networks (VLANs)
   - Routing Protocols (OSPF and EIGRP)
   - Network Redundancy (HSRP and EtherChannel)
   - Network Security
   - DHCP and Centralized Services
   - Best Practices in Network Design

3. **Chapter 3: Technical Background**
   - Network Design Overview
   - IP Addressing Scheme
   - VLAN Configuration
   - Routing Configuration
   - HSRP Implementation
   - DHCP Configuration
   - IP Telephony Configuration
   - Switch Configuration
   - Server Configuration
   - Security Features

4. **Chapter 4: Methodology**
   - Research Design
   - Project Development Phases
   - Device Configuration Process
   - Testing and Verification
   - Challenges and Solutions
   - Validation of Design

5. **Chapter 5: Discussion and Implementation**
   - Main Branch Implementation
   - Branch Office Implementation
   - ISP Network Implementation
   - Inter-Site Telephony
   - Security Implementation
   - Performance Considerations
   - Troubleshooting Insights
   - Lessons Learned

6. **Chapter 6: Conclusion and Recommendations**
   - Summary of the Project
   - Key Achievements
   - Conclusions
   - Recommendations for Enhancement
   - Future Enhancements
   - Real-World Applicability

7. **References**
   - Academic and professional references in APA format

8. **Appendices**
   - IP Addressing Tables
   - VLAN Assignment Tables
   - Phone Number Directory
   - Device Inventory
   - Configuration Commands
   - Troubleshooting Commands
   - Network Diagrams
   - Project Timeline
   - Acronyms and Abbreviations

---

## Project Overview

IndianSupport.com operates from three locations:
- **Main Branch:** 3-story building with 8 departments (A-H)
- **Branch 1:** 1-story building with 3 departments (I-K), connected via PLDT ISP
- **Branch 2:** 1-story building with 3 departments (L-N), connected via GLOBE ISP

### Equipment Summary
- 4 Main Routers (2 at main branch, 1 per branch)
- 4 ISP Routers (2 for PLDT, 2 for GLOBE)
- 2 Multilayer Switches (main branch)
- 11 Access Switches (7 at main branch, 2 per branch)
- 52 Computers total
- 22 IP Phones total
- 1 Centralized Server (DNS, Web, Email)

### Key Technologies Implemented
- VLANs for traffic separation
- HSRP for router redundancy
- OSPF for internal routing
- EIGRP for ISP connectivity
- IP Telephony with inter-site calling
- DHCP for automatic configuration
- Port Security for access control
- EtherChannel for link redundancy

---

## How to Use This Documentation

### For Reviewing the Project
1. Start with **Chapter 1** to understand the project objectives
2. Review **Chapter 3** for technical details of the implementation
3. Check **Chapter 5** for discussion of how everything works together
4. Refer to **Appendices** for specific details like IP addresses and phone numbers

### For Implementing a Similar Network
1. Study **Chapter 2** to understand the technologies involved
2. Follow the process described in **Chapter 4** for systematic implementation
3. Use configuration examples from **Appendix E**
4. Reference troubleshooting commands in **Appendix F**

### For Understanding Network Design
1. Review **Chapter 3** for the network architecture
2. Study **Chapter 5** to understand design decisions
3. Read **Chapter 6** for best practices and recommendations

---

## Configuration Files

All device configurations referenced in this paper are available in the project repository:

**Main Branch:**
- Router-Test-1.txt
- Router-Test-2.txt
- MLS-Test-1.txt, MLS-Test-2.txt
- SW-Test-1.txt through SW-Test-7.txt
- Server-Setup-Instructions.md

**Branches:**
- Router-Branch1.md, Router-Branch2.md
- Switch configurations for both branches

**ISPs:**
- ISP-PLDT-R1.md, ISP-PLDT-R2.md
- ISP-GLOBE-R1.txt, ISP-GLOBE-R2.txt

**Network Topologies:**
- MainBranch.pkt
- Branch1.pkt, Branch2.pkt
- PLDT ISP.pkt, GLOBE ISP.pkt
- test.pkt (complete integrated network)

---

## Contact Information

**Project Author:** [Your Name]  
**Course:** NET 2  
**Institution:** [Your School Name]  
**Date Completed:** December 2025

---

## Acknowledgments

This project was completed as the final requirement for NET 2. Special thanks to:
- The course instructor for guidance and requirements
- Cisco Systems for Packet Tracer software
- Online networking communities for technical references
- Classmates for collaboration and support

---

## APA Formatting Note

This research paper follows the American Psychological Association (APA) 7th edition formatting standards as required by the project guidelines. All references are properly cited, and the document structure follows academic research paper conventions with modifications to make the content more accessible and practical for a networking project.

---

## Version History

**Version 1.0** - December 2025
- Initial complete documentation
- All 6 chapters completed
- Appendices with comprehensive reference material
- Configuration files documented
- Testing results included

---

*This document is part of the Final Project for NET 2: IP Telephony Documentation*

*Company: IndianSupport.com*  
*Project: IP Telephony Network with HSRP, OSPF, EIGRP, and Multi-Site Connectivity*
