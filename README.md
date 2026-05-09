# 🖧 Cisco Packet Tracer Lab Repository

> 📚 A structured, hands-on collection of Cisco networking labs — built while preparing for **CCNA (200-301)**
> From basic ARP/ICMP to real hardware OSPF on Cisco 2911 & CGR1240 routers.

![Cisco](https://img.shields.io/badge/Cisco-Packet%20Tracer-blue?style=for-the-badge&logo=cisco)
![CCNA](https://img.shields.io/badge/Certification-CCNA%20200--301-green?style=for-the-badge)
![Labs](https://img.shields.io/badge/Labs-11%20and%20Growing-orange?style=for-the-badge)
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
| `11` | `ospf-dual-router-isp-lab.pkt` | OSPF Dual Router + ISP Link — Cisco 2911 & CGR1240 ⭐ | OSPF, Loopback, Default Route, ISP Link | Cisco 2911, CGR1240 |

</div>

---

## 🎯 Lab Highlights

<details>
<summary>📦 <b>Lab 10 — Advanced OSPF: Loopback · Passive Interface · Type-5 LSA</b></summary>

```
        [Router0 ID:9.9.9.9]
       /          \
  Gig0/1          Gig0/0
10.0.12.0/30   10.0.13.0/30
     |                |
[Router1]         [Router2]
     \                /
          [Router3 ID:3.3.3.3]
              |
           [Switch]──[PC0] 192.168.4.0/24
```

| Concept | Command | Purpose |
|---------|---------|---------|
| Loopback | `interface Loopback0` | Stable Router ID — never goes down |
| Passive Interface | `passive-interface Gig0/2` | Advertise LAN without sending Hello packets |
| Default Route | `default-information originate` | Inject 0.0.0.0/0 as Type-5 LSA |

</details>

<details>
<summary>📦 <b>Lab 11 — REAL HARDWARE OSPF: Cisco 2911 & CGR1240 ⭐ LATEST</b></summary>

### 🏭 Cisco 2911 Used

| Device | Model | IOS Version | Router ID |
|--------|-------|-------------|-----------|
| Main Router | Cisco 2911/K9 | 15.1(4)M5 | 1.1.1.1 |
| Neighbor | Cisco CGR1240/K9 | 15.4(2)CG | 5.5.5.5 |

---

### 🗺️ Topology

```
          [ISP]
            | 203.118.10.2/30
            |
     ┌──────┴──────┐
     │  Cisco 2911  │  Router ID: 1.1.1.1
     │  Hostname:   │  Loopback: 1.1.1.1/32
     │   Router     │
     └──┬───────┬───┘
        │       │
   Gig0/0    Gig0/1
10.0.20.1  10.0.10.1
   /30         /30
        │       │
        │    (unused)
   ┌────┴────┐
   │CGR1240  │  Router ID: 5.5.5.5
   │         │  Loopback: 5.5.5.5/32
   └─────────┘
  Fa2/4: 10.0.20.2/30
  Fa2/3: 10.0.30.1/30
```

---

### 🔢 IP Addressing & Wildcard Masks

| Interface | IP Address | Subnet | Wildcard Mask | Connected To |
|-----------|-----------|--------|---------------|--------------|
| 2911 Loopback0 | 1.1.1.1/32 | /32 | **0.0.0.0** | — (Router ID) |
| 2911 Gig0/0 | 10.0.20.1/30 | /30 | **0.0.0.3** | CGR1240 Fa2/4 |
| 2911 Gig0/1 | 10.0.10.1/30 | /30 | **0.0.0.3** | Unused |
| 2911 Gig0/2 | 203.118.10.1/30 | /30 | **0.0.0.3** | ISP |
| CGR1240 Loopback0 | 5.5.5.5/32 | /32 | **0.0.0.0** | — (Router ID) |
| CGR1240 Fa2/4 | 10.0.20.2/30 | /30 | **0.0.0.3** | 2911 Gig0/0 |
| CGR1240 Fa2/3 | 10.0.30.1/30 | /30 | **0.0.0.3** | — |

> 💡 **Wildcard Formula:** `255.255.255.255 − Subnet Mask`
> /32 → `255.255.255.255 − 255.255.255.255` = **0.0.0.0** (exact host match)
> /30 → `255.255.255.255 − 255.255.255.252` = **0.0.0.3**

---

### ⚙️ Full Configuration

#### Cisco 2911 (Main Router)
```bash
enable
configure terminal
hostname Router

! Loopback — stable Router ID
interface loopback 0
 ip address 1.1.1.1 255.255.255.255

! LAN/WAN interfaces
interface gigabitethernet 0/0
 ip address 10.0.20.1 255.255.255.252
 no shutdown

interface gigabitethernet 0/1
 ip address 10.0.10.1 255.255.255.252
 no shutdown

interface gigabitethernet 0/2
 ip address 203.118.10.1 255.255.255.252
 no shutdown

! Static default route to ISP
ip route 0.0.0.0 0.0.0.0 203.118.10.2

! OSPF configuration
router ospf 1
 router-id 1.1.1.1
 auto-cost reference-bandwidth 10000    ! Tune for Gigabit links
 network 10.0.10.0 0.0.0.3 area 0
 network 10.0.20.0 0.0.0.3 area 0
 default-information originate          ! Advertise default route as Type-5 LSA
end
wr
```

#### Cisco CGR1240 (Neighbor Router)
```bash
enable
configure terminal

! CRITICAL — must enable IP routing on CGR series!
ip routing

! Loopback — stable Router ID
interface loopback 0
 ip address 5.5.5.5 255.255.255.255

! Interfaces
interface fastethernet 2/4
 ip address 10.0.20.2 255.255.255.252
 no shutdown

interface fastethernet 2/3
 ip address 10.0.30.1 255.255.255.252
 no shutdown

! OSPF configuration
router ospf 1
 router-id 5.5.5.5
 network 10.0.20.0 0.0.0.3 area 0
end
wr
```

---

### ✅ OSPF Neighbor Verification

```bash
Router# show ip ospf neighbor

Neighbor ID   Pri   State       Dead Time   Interface
5.5.5.5        1    FULL/BDR    00:00:37    GigabitEthernet0/0
```

> **FULL** = Perfect adjacency ✅
> **BDR** = CGR1240 is Backup Designated Router on this segment

---

### 📊 OSPF Adjacency States (Reference)

| State | Meaning |
|-------|---------|
| DOWN | No Hello received yet |
| INIT | Hello received, not yet bidirectional |
| 2-WAY | Both routers see each other |
| EXSTART | Preparing to exchange database |
| EXCHANGE | Actively sharing LSAs |
| LOADING | Processing received LSAs |
| **FULL** | ✅ Fully adjacent — desired state |

---

### 🐛 Issues Found & Fixed

| # | Problem | Symptom | Fix |
|---|---------|---------|-----|
| 1 | IP routing disabled on CGR1240 | No OSPF adjacency | `ip routing` command |
| 2 | Wrong Router ID | Old ID stuck after change | `clear ip ospf process` |
| 3 | Interface name typo | `% Invalid input detected` | Use full name e.g. `gigabitethernet 0/0` |
| 4 | No default route propagation | Neighbors had no internet path | `default-information originate` |

---

### 💡 Key Lessons from Cisco 2911

```
1. ip routing          → Must enable on CGR/ISR series routers explicitly
2. clear ip ospf process → Required after changing router-id
3. auto-cost reference-bandwidth 10000 → Tune for modern Gigabit links
4. default-information originate → Only works if a default route already exists
5. Full interface names → Real IOS is strict: "gigabitethernet" not "g0/0"
```

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
| Router ID | ❌ | ✅ | ✅ | ❌ |
| Loopback Support | ❌ | ✅ | ✅ | ❌ |
| Cisco 2911 Ready | ✅ | ✅ | ✅ | ✅ |

</div>

---

## 📈 Learning Path

```
┌──────────────────────────────────────────────────────────────────┐
│                     CCNA LEARNING JOURNEY                         │
├──────────────────────────────────────────────────────────────────┤
│  ✅  Lab 01  →  ARP & ICMP                                        │
│  ✅  Lab 02  →  Static Routing                                    │
│  ✅  Lab 03  →  VLANs & Trunking                                  │
│  ✅  Lab 04  →  STP & BPDU Guard                                  │
│  ✅  Lab 05  →  RSTP                                              │
│  ✅  Lab 06  →  Inter-VLAN L3 Switch (SVI)                        │
│  ✅  Lab 07  →  Router-on-a-Stick (ROAS)                          │
│  ✅  Lab 08  →  OSPF + Floating Static                            │
│  ✅  Lab 09  →  EIGRP Partial Mesh + Wildcard Masks               │
│  ✅  Lab 10  →  Advanced OSPF: Loopback · Passive · LSA Type-5    │
│  🔄  Lab 11  →  REAL HARDWARE OSPF: Cisco 2911 + CGR1240  ◄ HERE │
│  ⏳  Next    →  ACLs · NAT/PAT · DHCP · WAN                       │
└──────────────────────────────────────────────────────────────────┘
```

---

## 🧪 Master Verification Commands

```bash
# OSPF
show ip ospf neighbor            # Neighbor adjacency & FULL state
show ip route ospf               # OSPF-learned routes only
show ip ospf database            # Full LSDB — see all LSA types
show ip ospf interface brief     # OSPF-enabled interfaces
show ip protocols                # OSPF process details & Router ID
clear ip ospf process            # Reset OSPF (use after router-id change)

# EIGRP
show ip eigrp neighbors          # EIGRP neighbor table
show ip route eigrp              # EIGRP routes only

# General
show ip route                    # Full routing table
show ip interface brief          # All interfaces + status
ping [ip]                        # Test reachability
traceroute [ip]                  # Trace path hop by hop
```

---

## 🛠️ Requirements

- Cisco Packet Tracer **8.0+** for simulation labs
- **Cisco 2911:** Cisco 2911, Cisco CGR1240 (for Lab 11)

---

## 👤 About

> 🎓 **M Hamza Siddique** — Currently preparing for Cisco CCNA 200-301
> 💡 Practicing on both **Packet Tracer** and **real Cisco hardware**
> 🔗 [LinkedIn](https://www.linkedin.com/in/hamza-malik-791ba8301/) · [GitHub](https://github.com/hamzamalik97)

---

<div align="center">

**Happy Networking! 🚀**

*"The expert in anything was once a beginner."*

⭐ Star this repo if it helped you!

</div>
