# DATSECURE Enterprise Network Security Implementation

A secure enterprise network designed and implemented in **Cisco Packet Tracer** to demonstrate network segmentation, routing, access control, and secure resource sharing across multiple departments.

---

## Project Overview

The **DATSECURE Enterprise Network Security Implementation** project simulates a real-world business environment where different departments require secure communication while maintaining controlled access to sensitive resources.

The network is divided into three departments:

* Administration
* Sales
* Human Resources (HR)

Each department operates on its own subnet and connects through a centralized router that manages routing and security policies.

The project demonstrates key networking concepts such as:

* IPv4 Addressing and Subnetting
* Inter-Network Routing
* Access Control Lists (ACLs)
* Network Segmentation
* HTTP Server Deployment
* Network Security Enforcement

---

## Project Objectives

The main goals of this project are to:

* Design a scalable enterprise network.
* Implement logical network segmentation.
* Configure secure communication between departments.
* Restrict unauthorized access using ACLs.
* Deploy an internal web server.
* Control access to shared resources.
* Validate connectivity through testing and verification.

---

## Network Topology

### Network Devices

| Device            | Quantity | Purpose                          |
| ----------------- | -------- | -------------------------------- |
| Cisco Router      | 1        | Routing and Security Enforcement |
| Cisco 2960 Switch | 3        | Department Connectivity          |
| PCs               | 6        | End-User Devices                 |
| Server            | 1        | Internal Web Service             |

### Department Structure

```text
                    DATSECURE ROUTER
                   /       |       \
                  /        |        \
                 /         |         \
          Admin LAN   Sales LAN    HR LAN
        192.168.10.0 192.168.20.0 192.168.30.0
             /24          /24          /24
```

---

## IP Addressing Scheme

### Network Information

| Department | Network Address | Subnet Mask   | Default Gateway |
| ---------- | --------------- | ------------- | --------------- |
| Admin      | 192.168.10.0/24 | 255.255.255.0 | 192.168.10.1    |
| Sales      | 192.168.20.0/24 | 255.255.255.0 | 192.168.20.1    |
| HR         | 192.168.30.0/24 | 255.255.255.0 | 192.168.30.1    |

### Host Allocation

#### Administration Department

| Device           | IP Address    |
| ---------------- | ------------- |
| Router Interface | 192.168.10.1  |
| Admin-PC1        | 192.168.10.2  |
| Admin-PC2        | 192.168.10.3  |
| DATSECURE Server | 192.168.10.10 |

#### Sales Department

| Device           | IP Address   |
| ---------------- | ------------ |
| Router Interface | 192.168.20.1 |
| Sales-PC1        | 192.168.20.2 |
| Sales-PC2        | 192.168.20.3 |

#### Human Resources Department

| Device           | IP Address   |
| ---------------- | ------------ |
| Router Interface | 192.168.30.1 |
| HR-PC1           | 192.168.30.2 |
| HR-PC2           | 192.168.30.3 |

---

## Network Design

### Core Layer

The **DATSECURE Router** serves as the central routing device and is responsible for:

* Inter-network routing
* ACL enforcement
* Default gateway services
* Traffic management

### Access Layer

Three Cisco 2960 switches provide connectivity for:

* Administration Department
* Sales Department
* Human Resources Department

### End Devices

The network includes:

* 2 Administrative PCs
* 2 Sales PCs
* 2 HR PCs
* 1 Internal HTTP Server

---

## Router Configuration

### Interface Assignments

| Interface          | IP Address   | Purpose       |
| ------------------ | ------------ | ------------- |
| GigabitEthernet0/0 | 192.168.10.1 | Admin Gateway |
| GigabitEthernet0/1 | 192.168.20.1 | Sales Gateway |
| GigabitEthernet0/2 | 192.168.30.1 | HR Gateway    |

### Router Responsibilities

* Routes traffic between networks.
* Provides default gateway services.
* Applies security policies.
* Controls access to internal resources.

---

## Switching Operations

The Cisco 2960 switches operate at **Layer 2** and perform:

* MAC address learning
* Frame forwarding
* Broadcast containment
* User connectivity

### Spanning Tree Protocol (STP)

STP is enabled by default and helps:

* Prevent network loops
* Improve network stability
* Support redundancy

---

## Routing Configuration

### Directly Connected Routing

This network uses **directly connected routing** because all subnets are physically connected to the router.

No dynamic routing protocol such as **OSPF** or **EIGRP** is required.

### Connected Networks

```text
192.168.10.0/24 → Administration Network
192.168.20.0/24 → Sales Network
192.168.30.0/24 → Human Resources Network
```

---

## Security Implementation

Security is a major focus of this project. Access Control Lists (ACLs) are configured on the router to enforce departmental access policies.

### Administration Department

**Permissions**

* Access Sales Network
* Access HR Network
* Access Internal Server

**Access Level:** Full Access

### Sales Department

**Permissions**

* Access Admin Network
* Access Internal Server

**Restrictions**

* Cannot access HR Network

**Access Level:** Limited Access

### Human Resources Department

**Restrictions**

* Cannot access Admin Network
* Cannot access Sales Network
* Cannot access Internal Server

**Access Level:** Highly Restricted

---

## Access Control Lists (ACLs)

ACLs are used to control traffic between departments and protect sensitive resources.

### Sample ACL Configuration

```cisco
access-list 100 permit ip 192.168.10.0 0.0.0.255 any

access-list 100 permit tcp 192.168.20.0 0.0.0.255 host 192.168.10.10 eq 80

access-list 100 deny ip 192.168.30.0 0.0.0.255 host 192.168.10.10

access-list 100 deny ip 192.168.30.0 0.0.0.255 192.168.10.0 0.0.0.255

access-list 100 deny ip 192.168.30.0 0.0.0.255 192.168.20.0 0.0.0.255
```

---

## Server Deployment

### DATSECURE Web Server

| Parameter  | Value          |
| ---------- | -------------- |
| IP Address | 192.168.10.10  |
| Network    | Administration |
| Service    | HTTP           |

### Purpose

The server hosts internal web resources that are accessible only to authorized departments.

### Access Permissions

| Department | HTTP Access |
| ---------- | ----------- |
| Admin      | Allowed     |
| Sales      | Allowed     |
| HR         | Denied      |

---

## Testing and Verification

### Phase 1: Basic Connectivity

1. Ping `Admin-PC2` from `Admin-PC1`
2. Ping `Sales-PC2` from `Sales-PC1`
3. Ping `HR-PC2` from `HR-PC1`

**Expected Result:** Successful communication within each department.

---

### Phase 2: Inter-Department Communication

1. Ping `Sales-PC1` from `Admin-PC1`
2. Ping `Admin-PC1` from `Sales-PC1`
3. Attempt to ping `HR-PC1` from `Sales-PC1`
4. Attempt to ping `Admin-PC1` from `HR-PC1`

**Expected Results**

* Admin ↔ Sales: Allowed
* Sales → HR: Blocked
* HR → Admin: Blocked

---

### Phase 3: Server Access Verification

1. Open `http://192.168.10.10` from `Admin-PC1`
2. Open `http://192.168.10.10` from `Sales-PC1`
3. Open `http://192.168.10.10` from `HR-PC1`

**Expected Results**

* Admin: Access Granted
* Sales: Access Granted
* HR: Access Denied

---

## Project Results

The project successfully achieved all intended objectives.

### Key Achievements

* Successful inter-network routing
* Effective ACL implementation
* Secure server deployment
* Controlled access to network resources
* Proper network segmentation
* Verified end-to-end connectivity

---

## Technologies Used

* Cisco Packet Tracer
* Cisco Router
* Cisco Catalyst 2960 Switches
* IPv4 Addressing
* Access Control Lists (ACLs)
* HTTP Server
* ICMP
* ARP
* Spanning Tree Protocol (STP)

---

## Conclusion

The **DATSECURE Enterprise Network Security Implementation** project demonstrates how network segmentation, routing, and access control can be combined to build a secure and scalable enterprise network.

By implementing dedicated departmental subnets, centralized routing, ACL-based security policies, and controlled server access, the network successfully meets both business and technical requirements while providing a strong foundation for future expansion.
