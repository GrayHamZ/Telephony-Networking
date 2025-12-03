# Chapter 1: Introduction

## Background of the Study

IP telephony allows businesses to make phone calls over the internet instead of traditional phone lines. This project creates a complete network system for IndianSupport.com that enables voice and data communication across multiple locations.

IndianSupport.com operates from a main branch (3-story building with 8 departments) and two smaller branch offices (each with 3 departments). The network needs to support both computers and IP phones while ensuring reliable connectivity between all locations.

## Problem Statement

IndianSupport.com faces several challenges in establishing a reliable multi-site communication network:

1. Enabling seamless communication between departments and branches
2. Ensuring network reliability even if equipment fails
3. Securing company data from unauthorized access
4. Providing internet connectivity through multiple providers
5. Supporting both data and voice services on a single infrastructure

## Objectives of the Study

**General Objective:** Design and implement a functional IP telephony network connecting all IndianSupport.com departments and branches.

**Specific Objectives:**
1. Implement VLANs to separate data and voice traffic
2. Configure HSRP for router redundancy
3. Set up OSPF routing in the main branch
4. Connect branches through ISP networks using EIGRP
5. Enable IP phone calling between all locations
6. Implement security features including port security
7. Deploy centralized DNS, web, and email services

## Scope and Limitations

**Scope:**
- Main branch: 8 departments, 40 computers, 16 IP phones
- Branch 1 & 2: 3 departments each, 6 computers, 3 IP phones per branch
- Routers, multilayer switches, and access switches configuration
- IP telephony, DNS, web, and email services
- Dual ISP connectivity (PLDT and GLOBE)

**Limitations:**
- Implemented in Cisco Packet Tracer (simulation, not physical hardware)
- Basic security only (no advanced firewalls)
- Internal email system only
- Focus on functionality over performance optimization

## Significance of the Study

This project demonstrates practical application of enterprise networking concepts including VLANs, HSRP, OSPF, EIGRP, and IP telephony. It provides IndianSupport.com with a reliable, redundant communication infrastructure and serves as a reference for similar networking implementations. The design follows industry best practices for redundancy, security, and scalability.
