# 🖧 Cisco Packet Tracer Lab Repository

> 📚 A structured, hands-on collection of Cisco networking labs — built while preparing for **CCNA (200-301)**
> From basic ARP/ICMP to advanced EIGRP dynamic routing with partial mesh topologies.

![Cisco](https://img.shields.io/badge/Cisco-Packet%20Tracer-blue?style=for-the-badge&logo=cisco)
![CCNA](https://img.shields.io/badge/Certification-CCNA%20200--301-green?style=for-the-badge)
![Labs](https://img.shields.io/badge/Labs-9%20and%20Growing-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Actively%20Preparing-red?style=for-the-badge)

---

## 📁 Labs Included

| # | File | Description | Technologies | Devices |
|---|------|-------------|--------------|---------|
| 1 | `1,connectivity,ICMP,ARP.pkt` | ARP and ICMP connectivity test | ARP, ICMP | 2x PCs, 2x 2960 Switches |
| 2 | `2.router,conf.pkt` | Basic router configuration & static routing | Static Routing | Router, 4x PCs, 2960 Switch |
| 3 | `vlan-trunk-4vlans.pkt` | VLAN segmentation with trunk links | VLAN, Trunk | Multiple PCs, Managed Switches |
| 4 | `4.stp.conf.pkt` | STP, Root Bridge election, BPDU Guard | STP, BPDU Guard | 3x Switches |
| 5 | `6.rstp.hub.linktype.pkt` | RSTP root bridge and port priority | RSTP (802.1w) | Multiple Switches, Hub |
| 6 | `9.L3,switches.pkt` | Layer 3 switch inter-VLAN routing | SVI, Static Routing | L2+L3 Switches, Router, 8 PCs |
| 7 | `8.ROAS,vlan.pkt` | Router-on-a-Stick inter-VLAN routing | VLAN, 802.1Q, Subinterfaces | L2 Switch, Router, 8+ PCs |
| 8 | `static.floating.routing.pkt` | OSPF + Static + Floating Static Route | OSPF, Static Routing, Floating Static | 4x Routers, 2x PCs |
| 9 | `eigrp-partial-mesh-lab.pkt` | EIGRP dynamic routing on partial mesh | EIGRP, Wildcard Mask, /30 Links | 4x Routers, 1x Switch, 1x PC |

---

## 🎯 Lab Highlights

### Lab 8: OSPF + Static + Floating Static Route
- **Topology:** `PC0 — R0 — R1 — R2 — R3 — PC1`
- **OSPF:** Dynamic routing across all routers (Area 0)
- **Static Routing:** Manual routes as full backup
- **Floating Static:** High AD (200) backup if OSPF fails
- **Subnetting:** /30 for point-to-point links, /24 for LANs

### Lab 9: EIGRP Partial Mesh ⭐ LATEST
- **Topology:** Partial mesh — Router0 connects to Router1 & Router2; both connect to Router3
- **EIGRP AS:** 1 (all routers same Autonomous System)
- **Neighbors verified:** `show ip eigrp neighbors`
- **Routes learned:** `show ip route eigrp`
- **Wildcard Masks used:**
  - `/30` links → wildcard `0.0.0.3`
  - `/24` LAN   → wildcard `0.0.0.255`

---

## 🗺️ Lab 9 Topology

```
          [Router0]
         /         \
   Gig0/1           Gig0/0
  10.0.12.0/30    10.0.13.0/30
       |                |
  [Router1]         [Router2]
   Gig0/1            Gig0/1
  10.0.24.0/30    10.0.34.0/30
       \                /
          [Router3]
              |
          [Switch0]
              |
            [PC0]
        192.168.1.0/24
```

---

## 🔧 Lab 9 IP Addressing Plan

| Link | Network | Wildcard Mask | Subnet Mask |
|------|---------|---------------|-------------|
| Router0 ↔ Router1 | 10.0.12.0/30 | 0.0.0.3 | 255.255.255.252 |
| Router0 ↔ Router2 | 10.0.13.0/30 | 0.0.0.3 | 255.255.255.252 |
| Router1 ↔ Router3 | 10.0.24.0/30 | 0.0.0.3 | 255.255.255.252 |
| Router2 ↔ Router3 | 10.0.34.0/30 | 0.0.0.3 | 255.255.255.252 |
| Router3 LAN (PC0) | 192.168.1.0/24 | 0.0.0.255 | 255.255.255.0 |

> 💡 **Wildcard Mask = 255.255.255.255 minus Subnet Mask**
> Example: 255.255.255.255 - 255.255.255.252 = **0.0.0.3**

---

## 🔧 Lab 9 EIGRP Configuration

### All Routers — EIGRP Setup
```bash
router eigrp 1
network 10.0.12.0 0.0.0.3     ! Router0-Router1 link
network 10.0.13.0 0.0.0.3     ! Router0-Router2 link
network 10.0.24.0 0.0.0.3     ! Router1-Router3 link
network 10.0.34.0 0.0.0.3     ! Router2-Router3 link
network 192.168.1.0 0.0.0.255 ! Router3 LAN
no auto-summary
```

---

## 🧪 Lab 9 Verification — Router0 Output

### EIGRP Neighbor Table
```
Router# show ip eigrp neighbors

H   Address      Interface   Hold  Uptime    SRTT  RTO   Q Cnt  Seq Num
0   10.0.12.2    Gig0/1      12    00:17:25  40    1000  0      9
1   10.0.13.2    Gig0/0      12    00:15:14  40    1000  0      13
```

### EIGRP Routes Learned
```
Router# show ip route eigrp

D  10.0.24.0/30 [90/3072] via 10.0.12.2, GigabitEthernet0/1
D  10.0.34.0/30 [90/3072] via 10.0.13.2, GigabitEthernet0/0
```
> **D** = EIGRP route | **[90/3072]** = Admin Distance / Metric

---

## 📊 Routing Protocol Comparison

| Feature | Static | OSPF | EIGRP | Floating Static |
|---------|--------|------|-------|-----------------|
| Type | Manual | Dynamic (Link-State) | Dynamic (Hybrid) | Manual (Backup) |
| Admin Distance | 1 | 110 | 90 | 200 (custom) |
| Auto-update | ❌ | ✅ | ✅ | ❌ |
| Convergence | N/A | Medium | Fast | N/A |
| Best for | Small networks | Enterprise | Cisco networks | Redundancy |
| Wildcard Mask | ❌ Not used | ✅ Required | ✅ Required | ❌ Not used |

---

## 📊 ROAS vs Layer 3 Switch

| Feature | ROAS | Layer 3 Switch |
|---------|------|----------------|
| Device | Router | Multilayer Switch |
| Interface | Subinterfaces | SVIs |
| Speed | Slower (software) | Faster (hardware) |
| Cost | Lower | Higher |
| Best for | Small networks | Enterprise networks |

---

## 📈 Learning Path

```
1. ARP/ICMP           →  Basic connectivity & troubleshooting
2. Static Routing     →  Router fundamentals & manual routes
3. VLANs + Trunk      →  Network segmentation
4. STP/RSTP           →  Loop prevention & redundancy
5. Inter-VLAN (L3)    →  Layer 3 switch with SVI
6. Inter-VLAN (ROAS)  →  Router-on-a-Stick with 802.1Q
7. OSPF + Floating    →  Dynamic routing + backup routes
8. EIGRP              →  Hybrid routing + wildcard masks  ← YOU ARE HERE
```

---

## 🛠 Requirements

- Cisco Packet Tracer **8.0 or higher**

---

## 📖 How to Use

1. Clone or download this repository
2. Open any `.pkt` file in Cisco Packet Tracer
3. Explore configurations using the CLI
4. Use verification commands to confirm routing

---

## 🧪 Key Verification Commands

```bash
show ip route                  # Full routing table
show ip route eigrp            # EIGRP routes only
show ip eigrp neighbors        # Verify EIGRP neighbor adjacency
show ip interface brief        # Check interface status
ping 192.168.1.x               # Test end-to-end connectivity
```

---

## 👤 About

> 🎓 Currently preparing for **Cisco CCNA 200-301**
> 💡 Documenting every lab to solidify understanding and help others
> 🔗 Connect with me on [LinkedIn](https://www.linkedin.com/in/hamza-malik-791ba8301/)

---

**Happy Networking!** 🚀
