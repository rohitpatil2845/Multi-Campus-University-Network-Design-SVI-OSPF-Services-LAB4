# 🚀 CCNA Lab 4 – Multi-Campus University Network Design (SVI + OSPF + Services)

## 📌 Overview

This lab focuses on designing a scalable university network with a main campus and a secondary campus.
The network includes VLAN segmentation, inter-VLAN routing using SVI, dynamic routing using OSPF, and centralized services like Web, FTP, and Email servers.

---

## 🧠 Problem Statement

In a university environment:

* Multiple departments exist across buildings and campuses
* Large number of users require scalable routing
* Services like web, FTP, and email must be accessible

Challenges:

* Managing multiple networks ❌
* Providing connectivity across campuses ❌
* Ensuring scalability ❌

Solution:

* VLAN segmentation
* SVI for inter-VLAN routing
* OSPF for dynamic routing
* Centralized servers

---

## 🎯 Objective

* Segment departments using VLANs
* Configure inter-VLAN routing using SVI (Layer 3 switching)
* Connect multiple campuses using routers
* Implement OSPF for dynamic routing
* Provide access to internal and external servers
* Enable DHCP for IP assignment

---

## 🌐 Network Design

### 🔹 Main Campus VLANs

| VLAN | Department | Network        |
| ---- | ---------- | -------------- |
| 10   | HR         | 192.168.1.0/24 |
| 20   | Finance    | 192.168.2.0/24 |
| 30   | Admin      | 192.168.3.0/24 |

### 🔹 Secondary Campus VLANs

| VLAN | Department | Network        |
| ---- | ---------- | -------------- |
| 40   | Business   | 192.168.4.0/24 |
| 50   | Labs       | 192.168.5.0/24 |
| 60   | IT         | 192.168.6.0/24 |

### 🔹 Inter-Campus Links

* Serial networks (e.g., 10.10.10.0/30)

---

## ⚙️ How It Works (Concept Explanation)

### 🔹 VLAN + SVI

* VLAN separates departments
* SVI (Switch Virtual Interface) provides routing at Layer 3
* Each VLAN has a gateway IP on the switch

### 🔹 OSPF

* Dynamic routing protocol
* Automatically exchanges routes between campuses
* Scalable and efficient

### 🔹 Servers

* Web server → HTTP access
* FTP server → file transfer
* Email server → communication

---

## 💻 Configuration Commands

---

### 🔹 Enable Layer 3 Switching

```id="a1b2c3"
conf t
ip routing
```

---

### 🔹 Create VLANs

```id="d4e5f6"
vlan 10
vlan 20
vlan 30
vlan 40
vlan 50
vlan 60
```

---

### 🔹 Configure SVI

```id="g7h8i9"
interface vlan 10
ip address 192.168.1.1 255.255.255.0
no shutdown

interface vlan 20
ip address 192.168.2.1 255.255.255.0
no shutdown
```

(Repeat for all VLANs)

---

### 🔹 Assign Ports

```id="j1k2l3"
interface range fa0/1 - 4
switchport mode access
switchport access vlan 10
```

---

### 🔹 OSPF Configuration

```id="m4n5o6"
router ospf 1
network 192.168.0.0 0.0.255.255 area 0
```

---

### 🔹 Router Configuration (Inter-Campus)

```id="p7q8r9"
interface serial 0/0/0
ip address 10.10.10.1 255.255.255.252
no shutdown
```

---

### 🔹 DHCP Configuration

```id="s1t2u3"
ip dhcp pool HR
network 192.168.1.0 255.255.255.0
default-router 192.168.1.1
```

---

## 🔍 Verification Commands

```id="v4w5x6"
show vlan brief
show ip interface brief
show ip route
show ip ospf neighbor
show ip dhcp binding
```

---

## 📊 Result

✅ VLAN segmentation successfully implemented
✅ Inter-VLAN communication working via SVI
✅ OSPF routing between campuses working
✅ Devices receiving IP via DHCP
✅ Access to web, FTP, and email servers working

---

## ⚠️ Issues Faced & Solution

### ❌ Issue:

* No communication between campuses

### 🔍 Cause:

* OSPF not configured correctly

### ✅ Fix:

* Corrected network statements

---

### ❌ Issue:

* VLAN routing not working

### 🔍 Cause:

* `ip routing` not enabled

### ✅ Fix:

* Enabled Layer 3 routing on switch

---

## 💡 Key Learnings

* Difference between ROAS and SVI
* Importance of dynamic routing in large networks
* Role of centralized services
* How campus networks are structured

---

## 🎯 Real-World Use Case

* University campus networks
* Corporate multi-branch networks
* Data center + branch connectivity

---

## 🚀 Conclusion

This lab demonstrates how large-scale networks are designed using VLANs, Layer 3 switching, dynamic routing, and centralized services. It reflects real-world enterprise networking scenarios.
