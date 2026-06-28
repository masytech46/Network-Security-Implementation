DATSECURE Enterprise Network Security Implementation
Overview

DATSECURE Enterprise Network Security Implementation is a Cisco Packet Tracer project designed to simulate a secure departmental network infrastructure. The project demonstrates how network segmentation, routing, Access Control Lists (ACLs), and server access controls can be used to secure organizational resources while maintaining necessary communication between departments.

The network consists of three departments:

Administration
Sales
Human Resources (HR)

Each department operates on its own subnet and is connected through a centralized router that enforces security policies.

Project Objectives
Design a scalable enterprise network architecture.
Implement subnetting and IP addressing.
Configure inter-network communication.
Enforce security policies using ACLs.
Deploy an internal HTTP server.
Restrict server access based on departmental requirements.
Validate connectivity and security through testing

Network Topology

Physical Components
| Device            | Quantity | Purpose                     |
| ----------------- | -------- | --------------------------- |
| Cisco Router      | 1        | Routing and ACL Enforcement |
| Cisco 2960 Switch | 3        | Department Connectivity     |
| PCs               | 6        | End User Workstations       |
| Server            | 1        | Internal HTTP Service       |

Network Architecture

                    DATSECURE ROUTER
                   /       |       \
                  /        |        \
                 /         |         \
          Admin LAN   Sales LAN    HR LAN
        192.168.10.0 192.168.20.0 192.168.30.0
             /24          /24          /24

IP Addressing Plan

Network Addressing Scheme

| Department | Network Address | Subnet Mask   | Default Gateway |
| ---------- | --------------- | ------------- | --------------- |
| Admin      | 192.168.10.0/24 | 255.255.255.0 | 192.168.10.1    |
| Sales      | 192.168.20.0/24 | 255.255.255.0 | 192.168.20.1    |
| HR         | 192.168.30.0/24 | 255.255.255.0 | 192.168.30.1    |

Host Address Allocation

Administration Department

| Device           | IP Address    |
| ---------------- | ------------- |
| Router Interface | 192.168.10.1  |
| Admin-PC1        | 192.168.10.2  |
| Admin-PC2        | 192.168.10.3  |
| DATSECURE Server | 192.168.10.10 |

Sales Department

| Device           | IP Address   |
| ---------------- | ------------ |
| Router Interface | 192.168.20.1 |
| Sales-PC1        | 192.168.20.2 |
| Sales-PC2        | 192.168.20.3 |

Human Resources Department

| Device           | IP Address   |
| ---------------- | ------------ |
| Router Interface | 192.168.30.1 |
| HR-PC1           | 192.168.30.2 |
| HR-PC2           | 192.168.30.3 |

Network Design
Core Layer

The DATSECURE Router acts as the core device and is responsible for:

Inter-network routing
ACL enforcement
Default gateway services
Traffic management
Access Layer

Three Cisco 2960 switches provide connectivity for:

Administration Department
Sales Department
Human Resources Department
End Devices
2 Administrative PCs
2 Sales PCs
2 HR PCs
1 Internal Web Server

Device Configuration

Router Interfaces

| Interface          | IP Address   | Purpose       |
| ------------------ | ------------ | ------------- |
| GigabitEthernet0/0 | 192.168.10.1 | Admin Gateway |
| GigabitEthernet0/1 | 192.168.20.1 | Sales Gateway |
| GigabitEthernet0/2 | 192.168.30.1 | HR Gateway    |

Router Functions
Routes traffic between departments.
Acts as the default gateway.
Enforces ACL security policies.
Controls access to internal services.
Switch Functions
MAC Address Learning
Frame Forwarding
Broadcast Containment
User Connectivity
Routing and Switching
Routing Method

The network uses Directly Connected Routing.

Since all networks are directly connected to the router, no dynamic routing protocol such as OSPF or EIGRP is required.

Connected Routes

192.168.10.0/24 → Admin Network
192.168.20.0/24 → Sales Network
192.168.30.0/24 → HR Network

Switching Protocol

The Cisco 2960 switches operate at Layer 2 and utilize Spanning Tree Protocol (STP) for:

Loop Prevention
Network Stability
Redundancy Support
Security Implementation
Security Objectives
Protect internal resources.
Restrict unauthorized access.
Enforce departmental security policies.
Secure server communications.
Access Control Policy
Administration Department

Permissions

Access Sales Network
Access HR Network
Access Internal Server

Access Level: Full Access

Sales Department

Permissions

Access Admin Network
Access Internal Server

Restrictions

Cannot Access HR Network

Access Level: Limited Access

Human Resources Department

Restrictions

Cannot Access Admin Network
Cannot Access Sales Network
Cannot Access Internal Server

Access Level: Highly Restricted

Access Control Lists (ACLs)

ACLs are implemented on the router to enforce security requirements.

ACL Rules
Permit Admin traffic.
Permit Sales access to approved resources.
Deny HR access to internal resources.
Restrict HTTP access based on department.

Example ACL Configuration

access-list 100 permit ip 192.168.10.0 0.0.0.255 any

access-list 100 permit tcp 192.168.20.0 0.0.0.255 host 192.168.10.10 eq 80

access-list 100 deny ip 192.168.30.0 0.0.0.255 host 192.168.10.10

access-list 100 deny ip 192.168.30.0 0.0.0.255 192.168.10.0 0.0.0.255

access-list 100 deny ip 192.168.30.0 0.0.0.255 192.168.20.0 0.0.0.255

Server Implementation

DATSECURE Web Server

| Parameter  | Value         |
| ---------- | ------------- |
| IP Address | 192.168.10.10 |
| Network    | Admin         |
| Service    | HTTP          |

Purpose

The server hosts internal web resources accessible only to authorized departments.

Access Rules

| Department | HTTP Access |
| ---------- | ----------- |
| Admin      | Allowed     |
| Sales      | Allowed     |
| HR         | Denied      |

Testing and Verification
Phase 1: Basic Connectivity Testing
Ping Admin-PC2 from Admin-PC1.
Ping Sales-PC2 from Sales-PC1.
Ping HR-PC2 from HR-PC1.

Expected Result: Successful communication within each department.

Phase 2: Inter-Department Connectivity
Ping Sales-PC1 from Admin-PC1.
Ping Admin-PC1 from Sales-PC1.
Attempt to ping HR-PC1 from Sales-PC1.
Attempt to ping Admin-PC1 from HR-PC1.

Expected Results

Admin ↔ Sales: Allowed
Sales → HR: Blocked
HR → Admin: Blocked
Phase 3: Server Access Verification
Open http://192.168.10.10 from Admin-PC1.
Open http://192.168.10.10 from Sales-PC1.
Open http://192.168.10.10 from HR-PC1.

Expected Results
Admin: Access Granted
Sales: Access Granted
HR: Access Denied

Results

Successful Outcomes

Inter-department routing operational.
ACL enforcement operational.
Server accessible to authorized departments.
Unauthorized access successfully blocked.
Network segmentation functioning correctly.
End-to-end connectivity verified.

Technologies Used

Cisco Packet Tracer
Cisco Router
Cisco Catalyst 2960 Switches
IPv4 Addressing
Access Control Lists (ACLs)
HTTP Server
ICMP
ARP
Spanning Tree Protocol (STP)


Conclusion

The DATSECURE Enterprise Network Security Implementation project demonstrates a secure and scalable enterprise network using Cisco Packet Tracer. Through subnet segmentation, centralized routing, ACL-based security controls, and managed server access, the project successfully meets both technical and business requirements while providing a strong foundation for future network expansion and security enhancements.
