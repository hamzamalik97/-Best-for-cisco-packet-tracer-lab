# 🖧 Cisco Packet Tracer Lab Repository

> 📚 A structured, hands-on collection of Cisco networking labs — built while preparing for **CCNA (200-301)**
> From basic ARP/ICMP to advanced multi-router OSPF with Serial WAN links, mixed hardware & ISP connectivity.

![Cisco](https://img.shields.io/badge/Cisco-Packet%20Tracer-blue?style=for-the-badge&logo=cisco)
![CCNA](https://img.shields.io/badge/Certification-CCNA%20200--301-green?style=for-the-badge)
![Labs](https://img.shields.io/badge/Labs-12%20and%20Growing-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Actively%20Preparing-red?style=for-the-badge)

---

## 📁 All Labs

<div align="center">

| # | 🗂️ File | 📋 Topic | 🔧 Technologies | 📡 Devices |
|:---:|--------|----------|----------------|-----------|
| `01` | `1,connectivity,ICMP,ARP.pkt` | ARP & ICMP Connectivity | ARP, ICMP | 2x PC, 2x Switch |
| `02` | `2.router,conf.pkt` | Static Routing | Static Routing | Router, 4x PC, Switch |
| `03` | `vlan-trunk-4vlans.pkt` | VLAN Segmentation & Trunking | VLAN, 802.1Q Trunk | Multiple PCs, Switches |
| `04` | `4.stp.conf.pkt` | STP & BPDU Guard | STP, BPDU Guard, Root Bridge | 3x Switches |
| `05` | `6.rstp.hub.linktype.pkt` | RSTP Root Bridge & Port Priority | RSTP (802.1w) | Switches, Hub |
| `06` | `9.L3,switches.pkt` | Layer 3 Inter-VLAN Routing | SVI, L3 Switch | L2+L3 Switches, 8x PC |
| `07` | `8.ROAS,vlan.pkt` | Router-on-a-Stick | VLAN, 802.1Q, Subinterfaces | Router, Switch, 8x PC |
| `08` | `static.floating.routing.pkt` | OSPF + Floating Static Backup | OSPF, Static, Floating Route | 4x Routers, 2x PC |
| `09` | `eigrp-partial-mesh-lab.pkt` | EIGRP Partial Mesh | EIGRP, Wildcard Mask, /30 | 4x Routers, Switch, PC |
| `10` | `ospf-advanced-loopback-lab.pkt` | Advanced OSPF — Loopback · Passive · Type-5 LSA | OSPF, Loopback, Passive Interface | 5x Routers, Switch, PC |
| `11` | `ospf-dual-router-isp-lab.pkt` | OSPF Dual Router + ISP Link — Cisco 2911 & CGR1240 | OSPF, Loopback, Default Route, ISP | Cisco 2911, CGR1240 |
| `12` | `ospf3.pkt` | OSPF Multi-Router Serial WAN + Mixed Hardware ⭐ | OSPF, Serial Links, Wildcard Mask, ISP | 2911, 3x CGR1240, Switch, 2x PC |

</div>

---

## 🎯 Lab Highlights

<details>
<summary>📦 <b>Lab 12 — OSPF Multi-Router Serial WAN + Mixed Hardware ⭐ LATEST</b></summary>

### 🗺️ Topology

```
[PC0]─Fa0─[Switch0]─[Router0(2911)]═══Serial WAN═══[Router1(2901)]─[Router4(CGR1240)]───[Router5(CGR1240)]
           10.0.1.0/24   Gig0/1  Se0/3/0  1192.168.12.0/30  Se0/3/0  Gig0/0  Gig2/2  203.0.113.0/30  Gig2/2
                                                                          |
                                                                       Fa0/1
                                                                          |
                                                                      [Switch2]  192.168.245.0/29
                                                                          |
                                                                       Gig0/1
                                                                          |
                                                              [Router3(CGR1240)]─Gig2/1─[Router2(CGR1240)]
                                                                   Gig2/2               Gig2/2  Gig0/1
                                                              192.168.34.0/30            10.0.2.0/24
                                                                                            |
                                                                                        [Switch1]
                                                                                            |
                                                                                          [PC1]
```

---

### 🔢 IP Addressing & Wildcard Masks

| Link / Network | Subnet | Mask | Wildcard | Connected Devices |
|----------------|--------|------|----------|-------------------|
| PC0 LAN | 10.0.1.0/24 | 255.255.255.0 | **0.0.0.255** | PC0, Switch0, Router0 Fa0/1 |
| Router0 ↔ Router1 (Serial WAN) | 1192.168.12.0/30 | 255.255.255.252 | **0.0.0.3** | Router0 Se0/3/0 ↔ Router1 Se0/3/0 |
| Router1 ↔ Router4 | 203.0.113.0/30 | 255.255.255.252 | **0.0.0.3** | Router1 Gig0/0 ↔ Router4 Gig2/2 |
| Router4 ↔ Router5 (ISP) | 203.0.113.0/30 | 255.255.255.252 | **0.0.0.3** | Router4 Gig2/2 ↔ Router5 Gig2/2 |
| Router1/Router4 shared LAN | 192.168.245.0/29 | 255.255.255.248 | **0.0.0.7** | Switch2, Router1 Fa0/1, Router4 Gig2/1 |
| Router2 ↔ Router3 | 192.168.34.0/30 | 255.255.255.252 | **0.0.0.3** | Router2 Gig2/1 ↔ Router3 Gig2/2 |
| PC1 LAN | 10.0.2.0/24 | 255.255.255.0 | **0.0.0.255** | PC1, Switch1, Router2 Gig0/1 |

> 💡 **Wildcard Formula:** `255.255.255.255 − Subnet Mask`
> /29 → `255.255.255.255 − 255.255.255.248` = **0.0.0.7** (8 hosts)
> /30 → `255.255.255.255 − 255.255.255.252` = **0.0.0.3** (4 hosts)
> /24 → `255.255.255.255 − 255.255.255.0`   = **0.0.0.255** (256 hosts)

---

### 📡 Device Summary

| Device | Model | Role | Key Interfaces |
|--------|-------|------|----------------|
| Router0 | Cisco 2911 | WAN Edge | Gig0/1 (LAN), Se0/3/0 (WAN) |
| Router1 | Cisco 2901 | WAN Hub | Se0/3/0 (WAN), Gig0/0, Fa0/1 |
| Router2 | Cisco CGR1240 | LAN Gateway | Gig0/1 (PC1 LAN), Gig2/1 |
| Router3 | Cisco CGR1240 | Transit | Gig2/2 (R2), Gig0/1 (Switch2) |
| Router4 | Cisco CGR1240 | ISP Edge | Gig2/1 (Switch2), Gig2/2 (R5) |
| Router5 | Cisco CGR1240 | ISP Simulator | Gig2/2 (R4) |

---

### ⚙️ OSPF Configuration

#### Router0 (Cisco 2911)
```bash
conf t
router ospf 1
 network 10.0.1.0 0.0.0.255 area 0       ! PC0 LAN
 network 1192.168.12.0 0.0.0.3 area 0    ! Serial WAN to Router1
end
wr
```

#### Router1 (Cisco 2901)
```bash
conf t
router ospf 1
 network 1192.168.12.0 0.0.0.3 area 0    ! Serial WAN to Router0
 network 192.168.245.0 0.0.0.7 area 0    ! Shared LAN with Router4
 network 203.0.113.0 0.0.0.3 area 0      ! Link to Router4
end
wr
```

#### Router2 (CGR1240)
```bash
conf t
router ospf 1
 network 10.0.2.0 0.0.0.255 area 0       ! PC1 LAN
 network 192.168.34.0 0.0.0.3 area 0     ! Link to Router3
end
wr
```

#### Router3 (CGR1240)
```bash
conf t
router ospf 1
 network 192.168.34.0 0.0.0.3 area 0     ! Link to Router2
 network 192.168.245.0 0.0.0.7 area 0    ! Shared LAN (Switch2)
end
wr
```

#### Router4 (CGR1240)
```bash
conf t
router ospf 1
 network 192.168.245.0 0.0.0.7 area 0    ! Shared LAN (Switch2)
 network 203.0.113.0 0.0.0.3 area 0      ! ISP link to Router5
 default-information originate            ! Advertise default route
end
wr
```

---

### 🧪 Verification

```bash
show ip ospf neighbor          ! Verify FULL adjacency on all routers
show ip route ospf             ! Confirm all OSPF routes learned
show ip route                  ! Full routing table
ping 10.0.1.2                  ! PC1 pings PC0 → Success ✅
ping 10.0.2.2                  ! PC0 pings PC1 → Success ✅
```

### PDU Simulation Results
| Source | Destination | Type | Status |
|--------|-------------|------|--------|
| PC1 | PC0 | ICMP | ✅ Successful |
| PC1 | Router4 | ICMP | ✅ Successful |
| PC1 | PC0 | ICMP | ✅ Successful |

---

### 💡 Key Concepts in This Lab

| Concept | Explanation |
|---------|-------------|
| **Serial WAN Link** | Router0 ↔ Router1 use Se0/3/0 — simulates a real ISP WAN connection |
| **Mixed Hardware** | Cisco 2911, 2901, and CGR1240 routers in same OSPF domain |
| **Shared Segment /29** | Switch2 connects Router1, Router3, Router4 — multi-access OSPF segment |
| **OSPF Cost** | Serial links have higher cost than Gigabit — OSPF prefers faster paths |
| **Dynamic Failover** | If Serial WAN fails, OSPF recalculates path automatically |
| **Wildcard /29** | `0.0.0.7` — less common, important for CCNA exam |

</details>

---

## 📊 Routing Protocol Comparison

<div align="center">

| Feature | Static | OSPF | EIGRP | Floating Static |
|:-------:|:------:|:----:|:-----:|:---------------:|
| Type | Manual | Link-State | Hybrid | Manual Backup |
| Admin Distance | 1 | 110 | 90 | 200 |
| Auto-update | ❌ | ✅ | ✅ | ❌ |
| Wildcard Mask | ❌ | ✅ | ✅ | ❌ |
| Serial WAN Support | ✅ | ✅ | ✅ | ✅ |
| Auto Failover | ❌ | ✅ | ✅ | ❌ |

</div>

---

## 📈 Learning Path

```
┌──────────────────────────────────────────────────────────────────────┐
│                      CCNA LEARNING JOURNEY                            │
├──────────────────────────────────────────────────────────────────────┤
│  ✅  Lab 01  →  ARP & ICMP                                            │
│  ✅  Lab 02  →  Static Routing                                        │
│  ✅  Lab 03  →  VLANs & Trunking                                      │
│  ✅  Lab 04  →  STP & BPDU Guard                                      │
│  ✅  Lab 05  →  RSTP                                                  │
│  ✅  Lab 06  →  Inter-VLAN L3 Switch (SVI)                            │
│  ✅  Lab 07  →  Router-on-a-Stick (ROAS)                              │
│  ✅  Lab 08  →  OSPF + Floating Static                                │
│  ✅  Lab 09  →  EIGRP Partial Mesh + Wildcard Masks                   │
│  ✅  Lab 10  →  Advanced OSPF: Loopback · Passive · LSA Type-5        │
│  ✅  Lab 11  →  OSPF Dual Router + ISP Link (Cisco 2911 + CGR1240)    │
│  🔄  Lab 12  →  OSPF Multi-Router Serial WAN + Mixed Hardware ◄ HERE  │
│  ⏳  Next    →  ACLs · NAT/PAT · DHCP · WAN                           │
└──────────────────────────────────────────────────────────────────────┘
```

---

## 🧪 Master Verification Commands

```bash
show ip ospf neighbor            # Neighbor adjacency & FULL state
show ip route ospf               # OSPF-learned routes only
show ip ospf database            # Full LSDB — all LSA types
show ip ospf interface brief     # OSPF-enabled interfaces
show ip protocols                # OSPF process details & Router ID
clear ip ospf process            # Reset OSPF (after router-id change)
show ip route                    # Full routing table
show ip interface brief          # All interfaces + status
ping [ip]                        # Test reachability
traceroute [ip]                  # Trace path hop by hop
```

---

## 🛠️ Requirements

- Cisco Packet Tracer **8.0 or higher**

---

## 👤 About

> 🎓 **M Hamza Siddique** — Currently preparing for Cisco CCNA 200-301
> 💡 Practicing on both Packet Tracer and real Cisco hardware
> 🔗 [LinkedIn](https://www.linkedin.com/in/hamza-malik-791ba8301/) · [GitHub](https://github.com/hamzamalik97)

---

<div align="center">

**Happy Networking! 🚀**

*"The expert in anything was once a beginner."*

⭐ Star this repo if it helped you!

</div>
