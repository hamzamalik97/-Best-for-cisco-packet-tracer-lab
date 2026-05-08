# 🖧 Cisco Packet Tracer Lab Repository

> 📚 A structured, hands-on collection of Cisco networking labs — built while preparing for **CCNA (200-301)**
> From basic ARP/ICMP to advanced OSPF with Router IDs, Loopbacks, Redistribution & Troubleshooting.

![Cisco](https://img.shields.io/badge/Cisco-Packet%20Tracer-blue?style=for-the-badge&logo=cisco)
![CCNA](https://img.shields.io/badge/Certification-CCNA%20200--301-green?style=for-the-badge)
![Labs](https://img.shields.io/badge/Labs-10%20and%20Growing-orange?style=for-the-badge)
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
| `10` | `ospf-advanced-loopback-lab.pkt` | Advanced OSPF — Router ID, Loopback, Redistribution ⭐ | OSPF, Loopback, Passive Interface, Type-5 LSA | 5x Routers, Switch, PC |

</div>

---

## 🎯 Lab Highlights

<details>
<summary>📦 <b>Lab 09 — EIGRP Partial Mesh</b></summary>

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

| Link | Network | Wildcard Mask |
|------|---------|---------------|
| R0 ↔ R1 | 10.0.12.0/30 | 0.0.0.3 |
| R0 ↔ R2 | 10.0.13.0/30 | 0.0.0.3 |
| R1 ↔ R3 | 10.0.24.0/30 | 0.0.0.3 |
| R2 ↔ R3 | 10.0.34.0/30 | 0.0.0.3 |
| R3 LAN  | 192.168.1.0/24 | 0.0.0.255 |

> 💡 **Wildcard Formula:** `255.255.255.255 − Subnet Mask = Wildcard`

</details>

<details>
<summary>📦 <b>Lab 10 — Advanced OSPF: Router ID · Loopback · Redistribution ⭐ LATEST</b></summary>

### 🗺️ Topology

```
[Router4]──ISP──[Router0 ID:9.9.9.9]──[Router1 ID:1.1.1.1]──[Router3 ID:3.3.3.3]
(203.0.113.0/30)        |                                            |
                   [Router2 ID:2.2.2.2]─────────────────────────────┘
                                                              [Switch0]
                                                                 |
                                                              [PC0]
                                                        192.168.4.0/24
```

---

### 🔢 IP Addressing & Wildcard Masks

| Link / Interface | Network | Subnet Mask | Wildcard Mask |
|-----------------|---------|-------------|---------------|
| R0 ↔ R1 | 10.0.12.0/30 | 255.255.255.252 | **0.0.0.3** |
| R0 ↔ R2 | 10.0.13.0/30 | 255.255.255.252 | **0.0.0.3** |
| R1 ↔ R3 | 10.0.24.0/30 | 255.255.255.252 | **0.0.0.3** |
| R2 ↔ R3 | 10.0.34.0/30 | 255.255.255.252 | **0.0.0.3** |
| R0 ↔ R4 (ISP) | 203.0.113.0/30 | 255.255.255.252 | **0.0.0.3** |
| R3 LAN (PC0) | 192.168.4.0/24 | 255.255.255.0 | **0.0.0.255** |
| R0 Loopback | 9.9.9.9/32 | 255.255.255.255 | **0.0.0.0** |
| R3 Loopback | 3.3.3.3/32 | 255.255.255.255 | **0.0.0.0** |

> 💡 **/32 Loopback wildcard = 0.0.0.0** — matches that exact IP only (host route)

---

### 🔁 Loopback Interface — What & Why

```bash
interface Loopback0
 ip address 9.9.9.9 255.255.255.255
```

| Feature | Explanation |
|---------|-------------|
| **Never goes down** | Unlike physical interfaces, loopbacks are always up |
| **Used as Router ID** | OSPF prefers the highest loopback IP as Router ID |
| **Stable identifier** | Even if a physical link fails, the router stays reachable |
| **Best practice** | Always configure loopbacks in production networks |

---

### 🔇 Passive Interface — What & Why

```bash
router ospf 1
 passive-interface GigabitEthernet0/2   ! LAN-facing interface
```

| Feature | Explanation |
|---------|-------------|
| **Stops Hello packets** | OSPF won't send Hello packets out that interface |
| **Still advertises** | The network is still advertised into OSPF |
| **Security** | Prevents unauthorized routers on LAN from forming adjacency |
| **Best practice** | Always use on LAN/end-user interfaces |

---

### ⚙️ OSPF Configuration

#### Router0 (Hub — redistributes default route)
```bash
conf t
interface Loopback0
 ip address 9.9.9.9 255.255.255.255

router ospf 1
 router-id 9.9.9.9
 network 10.0.12.0 0.0.0.3 area 0
 network 10.0.13.0 0.0.0.3 area 0
 network 9.9.9.9 0.0.0.0 area 0
 default-information originate          ! Redistributes 0.0.0.0 Type-5 LSA
end
```

#### Router3 (Gateway to LAN — fix for missing routes)
```bash
conf t
interface Loopback0
 ip address 3.3.3.3 255.255.255.255

router ospf 1
 router-id 3.3.3.3
 network 3.3.3.3 0.0.0.0 area 0          ! Advertise loopback
 network 192.168.4.0 0.0.0.255 area 0    ! Advertise LAN
 network 10.0.24.0 0.0.0.3 area 0
 network 10.0.34.0 0.0.0.3 area 0
 passive-interface GigabitEthernet0/2    ! LAN interface — no Hello needed
end
wr
```

---

### 🐛 Issues Found & Fixed

| # | Problem | Symptom | Fix Applied |
|---|---------|---------|-------------|
| 1 | Loopback not in OSPF | Ping to `3.3.3.3` → `U.U.U` (Unreachable) | `network 3.3.3.3 0.0.0.0 area 0` |
| 2 | LAN not advertised | PC0 unreachable from Router0 | `network 192.168.4.0 0.0.0.255 area 0` |
| 3 | Missing default route | No internet path from OSPF domain | `default-information originate` on R0 |

---

### 🧪 Verification Commands & Output

```bash
! Check OSPF neighbors
Router0# show ip ospf neighbor
Neighbor ID   State   Interface
2.2.2.2       FULL    GigabitEthernet0/0
1.1.1.1       FULL    GigabitEthernet0/1

! Check routing table
Router0# show ip route ospf
O  10.0.24.0/30 [110/2] via 10.0.12.2, GigabitEthernet0/1
O  10.0.34.0/30 [110/2] via 10.0.13.2, GigabitEthernet0/0
O  192.168.4.0/24 [110/3] via 10.0.12.2  ← appears after fix ✅
O* 0.0.0.0/0 [110/1]                      ← default route from R0 ✅

! Verify loopback reachability
Router0# ping 3.3.3.3
!!!!!                                      ← success after fix ✅
```

---

### 📊 OSPF LSA Types Reference

| LSA Type | Name | Generated By | Purpose |
|----------|------|-------------|---------|
| Type 1 | Router LSA | Every router | Describes local links |
| Type 2 | Network LSA | DR router | Describes multi-access segments |
| Type 5 | AS External LSA | ASBR (Router0) | **Default route `0.0.0.0` into OSPF** |

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
| Passive Interface | ❌ | ✅ | ✅ | ❌ |

</div>

---

## 📈 Learning Path

```
┌──────────────────────────────────────────────────────────────┐
│                   CCNA LEARNING JOURNEY                       │
├──────────────────────────────────────────────────────────────┤
│  ✅  Lab 01  →  ARP & ICMP (Layer 2/3 basics)                │
│  ✅  Lab 02  →  Static Routing (manual routes)                │
│  ✅  Lab 03  →  VLANs & Trunking (segmentation)              │
│  ✅  Lab 04  →  STP & BPDU Guard (loop prevention)           │
│  ✅  Lab 05  →  RSTP (faster convergence)                    │
│  ✅  Lab 06  →  Inter-VLAN L3 Switch (SVI)                   │
│  ✅  Lab 07  →  Router-on-a-Stick (ROAS)                     │
│  ✅  Lab 08  →  OSPF + Floating Static (redundancy)          │
│  ✅  Lab 09  →  EIGRP Partial Mesh (wildcard masks)          │
│  🔄  Lab 10  →  Advanced OSPF: Loopback · Passive · LSA Type-5  ◄ HERE │
│  ⏳  Next    →  ACLs · NAT/PAT · DHCP · WAN                  │
└──────────────────────────────────────────────────────────────┘
```

---

## 🧪 Master Command Reference

```bash
# OSPF
show ip ospf neighbor            # Neighbor adjacency & state
show ip route ospf               # OSPF-learned routes only
show ip ospf database            # Full LSDB (LSA Types)
show ip ospf interface brief     # OSPF-enabled interfaces

# EIGRP
show ip eigrp neighbors          # EIGRP neighbor table
show ip route eigrp              # EIGRP-learned routes

# General
show ip route                    # Full routing table
show ip interface brief          # Interface status summary
ping [ip]                        # Test reachability
traceroute [ip]                  # Trace path hop-by-hop
```

---

## 🛠️ Requirements

- Cisco Packet Tracer **8.0 or higher**

---

## 👤 About

> 🎓 **M Hamza Siddique** — Currently preparing for Cisco CCNA 200-301
> 💡 Documenting every lab to solidify understanding and help the community
> 🔗 [LinkedIn](https://www.linkedin.com/in/hamza-malik-791ba8301/) · [GitHub](https://github.com/hamzamalik97)

---

<div align="center">

**Happy Networking! 🚀**

*"The expert in anything was once a beginner."*

⭐ Star this repo if it helped you!

</div>
