# DATSECURE Enterprise Network Security Implementation

![Cisco Packet Tracer](https://img.shields.io/badge/Platform-Cisco%20Packet%20Tracer-blue)
![Network Security](https://img.shields.io/badge/Focus-Network%20Security-green)
![Status](https://img.shields.io/badge/Status-Completed-success)

## Executive Summary

The **DATSECURE Enterprise Network Security Implementation** project is a secure and scalable enterprise network designed and implemented using **Cisco Packet Tracer**. The solution demonstrates industry-standard networking principles, including network segmentation, routing, access control, and secure resource sharing across multiple departments.

The network architecture was developed to support organizational security requirements by separating users into distinct departmental networks while maintaining controlled communication through centralized routing and Access Control Lists (ACLs).

The implementation showcases practical skills in:

* Enterprise Network Design
* IPv4 Addressing and Subnetting
* Router and Switch Configuration
* Access Control List (ACL) Deployment
* Inter-VLAN/Inter-Network Routing
* Network Security Enforcement
* Server Deployment and Access Management

---

# Project Overview

## Business Scenario

Organizations often require multiple departments to share infrastructure resources while ensuring that sensitive information remains protected from unauthorized access.

DATSECURE addresses these challenges by implementing a segmented network architecture for:

* Administration Department
* Sales Department
* Human Resources (HR) Department

Each department operates independently within its own subnet while controlled communication is enforced through security policies configured on the core routing device.

---

## Project Objectives

The primary objectives of this project include:

* Design a secure enterprise network infrastructure.
* Implement structured IPv4 addressing.
* Configure routing between departmental networks.
* Deploy centralized security policies using ACLs.
* Restrict unauthorized access to sensitive resources.
* Implement an internal web server.
* Verify network functionality through testing and validation.

---

# Network Architecture

## Network Topology

The network follows a hierarchical enterprise design model consisting of a Core Layer and an Access Layer.

```text id="c4r0b9"
                           DATSECURE ROUTER
                     (Core Routing & Security Layer)
                                     |
      ----------------------------------------------------------------
      |                              |                               |
      |                              |                               |
  Admin Switch                  Sales Switch                    HR Switch
      |                              |                               |
  ----------                    ----------                     ----------
  |        |                    |        |                     |        |
Admin1  Admin2              Sales1   Sales2                HR1      HR2
     |
DATSECURE Server
```

---

## Network Components

| Device                     | Quantity | Function                         |
| -------------------------- | -------- | -------------------------------- |
| Cisco Router               | 1        | Routing and Security Enforcement |
| Cisco Catalyst 2960 Switch | 3        | Department Connectivity          |
| End User PCs               | 6        | User Access                      |
| HTTP Server                | 1        | Internal Web Services            |

---

# IP Addressing Plan

## Network Addressing Scheme

| Department      | Network Address | Subnet Mask   | Default Gateway |
| --------------- | --------------- | ------------- | --------------- |
| Administration  | 192.168.10.0/24 | 255.255.255.0 | 192.168.10.1    |
| Sales           | 192.168.20.0/24 | 255.255.255.0 | 192.168.20.1    |
| Human Resources | 192.168.30.0/24 | 255.255.255.0 | 192.168.30.1    |

---

## Host Allocation

### Administration Network

| Device           | IP Address    |
| ---------------- | ------------- |
| Router Interface | 192.168.10.1  |
| Admin-PC1        | 192.168.10.2  |
| Admin-PC2        | 192.168.10.3  |
| DATSECURE Server | 192.168.10.10 |

### Sales Network

| Device           | IP Address   |
| ---------------- | ------------ |
| Router Interface | 192.168.20.1 |
| Sales-PC1        | 192.168.20.2 |
| Sales-PC2        | 192.168.20.3 |

### Human Resources Network

| Device           | IP Address   |
| ---------------- | ------------ |
| Router Interface | 192.168.30.1 |
| HR-PC1           | 192.168.30.2 |
| HR-PC2           | 192.168.30.3 |

---

# Network Design Methodology

## Core Layer

The **DATSECURE Router** serves as the central routing and security device responsible for:

* Inter-network communication
* Packet forwarding
* ACL enforcement
* Gateway services
* Security policy implementation

### Core Responsibilities

* Route traffic between departments.
* Restrict unauthorized communications.
* Protect internal resources.
* Control server accessibility.

---

## Access Layer

The Access Layer consists of three Cisco Catalyst 2960 switches.

### Functions

* User connectivity
* Frame forwarding
* MAC address learning
* Broadcast management
* Layer 2 switching

---

# Routing Implementation

## Routing Strategy

The project utilizes **Directly Connected Routing**.

Because each subnet is directly attached to the router, there is no requirement for dynamic routing protocols such as:

* OSPF
* EIGRP
* RIP

### Connected Routes

```text id="r5x9gk"
192.168.10.0/24 → Administration Network
192.168.20.0/24 → Sales Network
192.168.30.0/24 → Human Resources Network
```

---

# Switching Technology

## Cisco Catalyst 2960 Switching

The switches operate at **OSI Layer 2** and perform:

* MAC Address Learning
* Frame Switching
* Broadcast Control
* Traffic Segmentation

### Spanning Tree Protocol (STP)

The network leverages **STP** to provide:

* Loop Prevention
* Network Stability
* Fault Tolerance
* Redundancy Protection

---

# Security Architecture

## Security Objectives

The network was designed around four key security principles:

1. Segmentation
2. Least Privilege Access
3. Resource Protection
4. Controlled Communication

---

## Access Control Policy

### Administration Department

#### Permissions

* Access Sales Network
* Access HR Network
* Access Internal Server

#### Access Level

**Full Administrative Access**

---

### Sales Department

#### Permissions

* Access Administration Network
* Access Internal Web Server

#### Restrictions

* No access to HR resources

#### Access Level

**Restricted Business Access**

---

### Human Resources Department

#### Restrictions

* No access to Administration resources
* No access to Sales resources
* No access to Internal Server

#### Access Level

**Highly Restricted**

---

# Access Control List (ACL) Implementation

ACLs were deployed to enforce organizational security policies and control traffic flow between departments.

## Security Rules

### Permitted Traffic

* Administration → All Networks
* Sales → Administration
* Sales → HTTP Server

### Denied Traffic

* Sales → HR
* HR → Administration
* HR → Sales
* HR → Internal Server

---

## Sample ACL Configuration

```cisco
access-list 100 permit ip 192.168.10.0 0.0.0.255 any

access-list 100 permit tcp 192.168.20.0 0.0.0.255 host 192.168.10.10 eq 80

access-list 100 deny ip 192.168.30.0 0.0.0.255 host 192.168.10.10

access-list 100 deny ip 192.168.30.0 0.0.0.255 192.168.10.0 0.0.0.255

access-list 100 deny ip 192.168.30.0 0.0.0.255 192.168.20.0 0.0.0.255
```

---

# Server Deployment

## DATSECURE Internal Web Server

The project includes an internal HTTP server used to simulate centralized business services.

| Parameter  | Value            |
| ---------- | ---------------- |
| Hostname   | DATSECURE Server |
| IP Address | 192.168.10.10    |
| Service    | HTTP             |
| Department | Administration   |

---

## Server Access Matrix

| Department      | Access Status |
| --------------- | ------------- |
| Administration  | Authorized    |
| Sales           | Authorized    |
| Human Resources | Denied        |

---

# Testing and Validation

Comprehensive testing was performed to validate functionality and security requirements.

## Connectivity Testing

### Internal Department Testing

```bash
ping 192.168.10.3
ping 192.168.20.3
ping 192.168.30.3
```

### Expected Result

* Successful connectivity within each department.

---

## Inter-Network Testing

### Successful Communication

```bash
ping 192.168.20.2
ping 192.168.10.2
```

### Expected Result

* Communication succeeds according to ACL policy.

---

## Access Restriction Testing

```bash
ping 192.168.30.2
```

### Expected Result

* Traffic blocked where policy restrictions apply.

---

## Server Access Validation

### Browser Test

```text
http://192.168.10.10
```

### Expected Results

| Department     | Result         |
| -------------- | -------------- |
| Administration | Access Granted |
| Sales          | Access Granted |
| HR             | Access Denied  |

---

# Results

The project successfully met all functional and security objectives.

## Key Achievements

* Successful network segmentation
* Secure inter-network routing
* ACL policy enforcement
* Controlled resource accessibility
* Protected internal services
* Verified end-to-end communication

---

# Technologies Used

* Cisco Packet Tracer
* Cisco Router
* Cisco Catalyst 2960 Switches
* IPv4 Addressing
* Access Control Lists (ACLs)
* HTTP Services
* ICMP
* ARP
* Spanning Tree Protocol (STP)

---

# Conclusion

The **DATSECURE Enterprise Network Security Implementation** project demonstrates the successful design and deployment of a secure enterprise network using Cisco Packet Tracer. Through effective network segmentation, structured IP addressing, centralized routing, ACL-based security controls, and controlled server access, the solution meets both operational and security requirements.

This project highlights practical enterprise networking skills and serves as a strong foundation for implementing larger, more advanced network infrastructures in real-world environments.
