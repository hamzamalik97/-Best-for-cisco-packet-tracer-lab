<div align="center">

# 🌐 Cisco Packet Tracer Labs
### ▸ CCNA 200-301 Hands-On Practice Repository ◂

<img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=22&pause=1000&color=00C4FF&center=true&vCenter=true&width=600&lines=Learning+Networking+One+Lab+at+a+Time;CCNA+200-301+in+Progress...;Cisco+%7C+Routing+%7C+Switching+%7C+VLANs" alt="Typing SVG" />

<br/>

![Cisco](https://img.shields.io/badge/Cisco-Packet%20Tracer-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)
![CCNA](https://img.shields.io/badge/CCNA-200--301-00873E?style=for-the-badge&logo=cisco&logoColor=white)
![Labs](https://img.shields.io/badge/Total%20Labs-9-FF6B35?style=for-the-badge&logo=files&logoColor=white)
![Status](https://img.shields.io/badge/Status-Actively%20Preparing-red?style=for-the-badge&logo=target&logoColor=white)
![GitHub](https://img.shields.io/badge/Open%20Source-Yes-brightgreen?style=for-the-badge&logo=github&logoColor=white)

<br/>

> 💡 *"Tell me and I forget. Teach me and I remember. Involve me and I learn."* — Benjamin Franklin

</div>

---

## 👨‍💻 About This Repo

> 🎓 Currently preparing for **Cisco CCNA 200-301**
> 📁 Every lab I practice gets documented and uploaded here
> 🤝 Feel free to clone, study, and learn from these labs
> 🔗 Connect: [LinkedIn](https://www.linkedin.com/in/hamza-malik-791ba8301/) • [GitHub](https://github.com/hamzamalik97)

---

## 📊 My Progress

```
ARP / ICMP          ████████████████████  100% ✅
Static Routing      ████████████████████  100% ✅
VLANs & Trunking    ████████████████████  100% ✅
STP / RSTP          ████████████████████  100% ✅
Inter-VLAN Routing  ████████████████████  100% ✅
OSPF                ████████████████████  100% ✅
EIGRP               █████████████████░░░   85% 🔄
ACLs                ░░░░░░░░░░░░░░░░░░░░    0% ⏳
NAT / PAT           ░░░░░░░░░░░░░░░░░░░░    0% ⏳
DHCP / DNS          ░░░░░░░░░░░░░░░░░░░░    0% ⏳
```

---

## 📁 All Labs

<div align="center">

| # | 🗂️ File | 📋 Topic | 🔧 Technologies | 📡 Devices |
|:---:|--------|----------|----------------|-----------|
| `01` | `1,connectivity,ICMP,ARP.pkt` | ARP & ICMP Connectivity | ARP, ICMP, Ping | 2x PC, 2x Switch |
| `02` | `2.router,conf.pkt` | Basic Router + Static Routing | Static Routing, IP Config | Router, 4x PC, Switch |
| `03` | `vlan-trunk-4vlans.pkt` | VLAN Segmentation & Trunking | VLAN, 802.1Q Trunk | Multiple PCs, Switches |
| `04` | `4.stp.conf.pkt` | STP & BPDU Guard | STP, BPDU Guard, Root Bridge | 3x Switches |
| `05` | `6.rstp.hub.linktype.pkt` | RSTP Root Bridge & Port Priority | RSTP (802.1w), Hub | Switches, Hub |
| `06` | `9.L3,switches.pkt` | Layer 3 Inter-VLAN Routing | SVI, L3 Switch, Static Route | L2+L3 Switches, 8x PC |
| `07` | `8.ROAS,vlan.pkt` | Router-on-a-Stick | VLAN, 802.1Q, Subinterfaces | Router, Switch, 8x PC |
| `08` | `static.floating.routing.pkt` | OSPF + Floating Static Backup | OSPF, Static, Floating Route | 4x Routers, 2x PC |
| `09` | `eigrp-partial-mesh-lab.pkt` | EIGRP Partial Mesh ⭐ | EIGRP, Wildcard Mask, /30 | 4x Routers, Switch, PC |

</div>

---

## 🔬 Lab Deep Dives

<details>
<summary>📦 <b>Lab 01 — ARP & ICMP Connectivity</b></summary>

```
PC0 ──── Switch0 ──── Switch1 ──── PC1
```
- **Goal:** Verify Layer 2 ARP resolution and Layer 3 ICMP ping
- **Key Command:** `ping`, `arp -a`
- **Result:** ✅ End-to-end connectivity confirmed

</details>

<details>
<summary>📦 <b>Lab 02 — Static Routing</b></summary>

```
PC0 ── Router0 ── Router1 ── PC1
```
- **Goal:** Manually configure routes between networks
- **Key Command:** `ip route [network] [mask] [next-hop]`
- **Result:** ✅ PC0 can ping PC1 across routers

</details>

<details>
<summary>📦 <b>Lab 06 — Layer 3 Inter-VLAN Routing</b></summary>

- **VLANs:** 10, 20, 30
- **Method:** SVI (Switched Virtual Interface) on L3 switch
- **Subnetting:** /26 per VLAN
- **Key Command:** `interface vlan [id]` → `ip address`
- **Result:** ✅ All VLANs communicate through L3 switch

</details>

<details>
<summary>📦 <b>Lab 07 — Router-on-a-Stick (ROAS)</b></summary>

```
[PCs] ── Switch (trunk) ── Router (subinterfaces)
```
- **VLANs:** 10, 20, 30, 40
- **Trunk:** 802.1Q between switch and router
- **Key Command:** `encapsulation dot1q [vlan-id]`
- **Result:** ✅ All VLANs route through single router interface

</details>

<details>
<summary>📦 <b>Lab 08 — OSPF + Floating Static Route</b></summary>

```
PC0 — R0 — R1 — R2 — R3 — PC1
```
| Method | Admin Distance | Role |
|--------|---------------|------|
| OSPF | 110 | Primary dynamic routing |
| Floating Static | 200 | Backup (only if OSPF fails) |

- **Key Command:** `router ospf 1` → `network [ip] [wildcard] area 0`
- **Result:** ✅ OSPF routes traffic, static kicks in on failure

</details>

<details>
<summary>📦 <b>Lab 09 — EIGRP Partial Mesh ⭐ LATEST</b></summary>

```
        [Router0]
       /          \
  Gig0/1          Gig0/0
10.0.12.0/30   10.0.13.0/30
     |                |
[Router1]         [Router2]
     \                /
   10.0.24.0/30  10.0.34.0/30
          \      /
          [Router3]
              |
           [Switch]
              |
            [PC0]  192.168.1.0/24
```

**IP Addressing & Wildcard Masks:**

| Link | Network | Subnet Mask | Wildcard Mask |
|------|---------|-------------|---------------|
| R0 ↔ R1 | 10.0.12.0/30 | 255.255.255.252 | **0.0.0.3** |
| R0 ↔ R2 | 10.0.13.0/30 | 255.255.255.252 | **0.0.0.3** |
| R1 ↔ R3 | 10.0.24.0/30 | 255.255.255.252 | **0.0.0.3** |
| R2 ↔ R3 | 10.0.34.0/30 | 255.255.255.252 | **0.0.0.3** |
| R3 LAN | 192.168.1.0/24 | 255.255.255.0 | **0.0.0.255** |

> 💡 **Formula:** Wildcard = `255.255.255.255` − Subnet Mask

**EIGRP Config (all routers):**
```bash
router eigrp 1
 network 10.0.12.0 0.0.0.3
 network 10.0.13.0 0.0.0.3
 network 10.0.24.0 0.0.0.3
 network 10.0.34.0 0.0.0.3
 network 192.168.1.0 0.0.0.255
 no auto-summary
```

**Verification Output:**
```
Router0# show ip eigrp neighbors
H   Address      Interface   Hold  Uptime    SRTT  RTO
0   10.0.12.2    Gig0/1      12    00:17:25  40    1000
1   10.0.13.2    Gig0/0      12    00:15:14  40    1000

Router0# show ip route eigrp
D  10.0.24.0/30 [90/3072] via 10.0.12.2, GigabitEthernet0/1
D  10.0.34.0/30 [90/3072] via 10.0.13.2, GigabitEthernet0/0
```
- **Result:** ✅ EIGRP neighbors formed, routes learned, ping successful

</details>

---

## 📊 Routing Protocol Comparison

<div align="center">

| Feature | Static | OSPF | EIGRP | Floating Static |
|:-------:|:------:|:----:|:-----:|:---------------:|
| Type | Manual | Link-State | Hybrid | Manual Backup |
| Admin Distance | 1 | 110 | **90** | 200 |
| Auto-update | ❌ | ✅ | ✅ | ❌ |
| Convergence | N/A | Medium | ⚡ Fast | N/A |
| Wildcard Mask | ❌ | ✅ | ✅ | ❌ |
| Cisco Only | ❌ | ❌ | ✅ | ❌ |

</div>

---

## 🛠️ Requirements & Setup

```bash
# Software Required
Cisco Packet Tracer 8.0 or higher

# How to Use
1. Clone this repository
   git clone https://github.com/hamzamalik97/-Best-for-cisco-packet-tracer-lab.git

2. Open any .pkt file in Packet Tracer

3. Explore CLI configurations on each device

4. Run verification commands to understand the topology
```

---

## 🧪 Quick Command Reference

```bash
# Routing
show ip route                   # Full routing table
show ip route eigrp             # EIGRP routes only
show ip route ospf              # OSPF routes only
show ip ospf neighbor           # OSPF neighbor adjacency
show ip eigrp neighbors         # EIGRP neighbor adjacency

# Interfaces
show ip interface brief         # All interfaces + status
show interfaces [int]           # Detailed interface info

# VLANs & Switching
show vlan brief                 # VLAN database
show interfaces trunk           # Trunk ports
show spanning-tree              # STP topology

# Troubleshooting
ping [destination-ip]           # Test connectivity
traceroute [destination-ip]     # Trace path
```

---

## 📈 Learning Path

```
┌─────────────────────────────────────────────────────┐
│                  CCNA LEARNING JOURNEY               │
├─────────────────────────────────────────────────────┤
│  ✅  Lab 1  →  ARP & ICMP (Layer 2/3 basics)        │
│  ✅  Lab 2  →  Static Routing (manual routes)        │
│  ✅  Lab 3  →  VLANs & Trunking (segmentation)      │
│  ✅  Lab 4  →  STP & BPDU Guard (loop prevention)   │
│  ✅  Lab 5  →  RSTP (faster STP)                    │
│  ✅  Lab 6  →  Inter-VLAN L3 Switch (SVI)           │
│  ✅  Lab 7  →  Router-on-a-Stick (ROAS)             │
│  ✅  Lab 8  →  OSPF + Floating Static               │
│  🔄  Lab 9  →  EIGRP Partial Mesh  ◄ YOU ARE HERE   │
│  ⏳  Next   →  ACLs, NAT, DHCP, WAN                 │
└─────────────────────────────────────────────────────┘
```

---

<div align="center">

### ⭐ If this repo helped you, please give it a star!

[![LinkedIn](https://img.shields.io/badge/Connect%20on-LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/hamza-malik-791ba8301/)
[![GitHub](https://img.shields.io/badge/Follow%20on-GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/hamzamalik97)

**Happy Networking! 🚀**

*"The network is the computer." — John Gage, Sun Microsystems*

</div>
