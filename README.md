# 🖧 Cisco Packet Tracer Lab Repository

> 📚 A structured, hands-on collection of Cisco networking labs and protocol deep-dives — built while preparing for **CCNA (200-301)**
> From basic ARP/ICMP to advanced OSPF + HSRP redundancy, plus written Transport Layer analysis with packet-level breakdowns.

<div align="center">

![Cisco](https://img.shields.io/badge/Cisco-Packet%20Tracer-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)
![CCNA](https://img.shields.io/badge/CCNA-200--301-00873E?style=for-the-badge&logo=cisco&logoColor=white)
![Labs](https://img.shields.io/badge/Total%20Labs-13-FF6B35?style=for-the-badge)
![Docs](https://img.shields.io/badge/Protocol%20Docs-1-7C3AED?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Actively%20Preparing-red?style=for-the-badge)

</div>

---

## 🧭 Quick Navigation

- [All Labs](#-all-labs)
- [Documentation & Protocol Deep-Dives](#-documentation--protocol-deep-dives)
- [Lab Highlights](#-lab-highlights)
- [Routing Protocol Comparison](#-routing-protocol-comparison)
- [Learning Path](#-learning-path)
- [Master Verification Commands](#-master-verification-commands)

> 💡 On mobile, tables and code blocks scroll horizontally — swipe sideways if a row looks cut off.

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
| `11` | `ospf-dual-router-isp-lab.pkt` | OSPF Dual Router + ISP Link | OSPF, Loopback, Default Route | Cisco 2911, CGR1240 |
| `12` | `ospf-multirouter-serial-wan.pkt` | OSPF Multi-Router Serial WAN | OSPF, Serial Links, /29 Wildcard | 2911, 3x CGR1240, 2x PC |
| `13` | `ospf-HSRP.pkt` | OSPF + HSRP Gateway Redundancy ⭐ | OSPF, HSRP, Virtual IP, Mesh Switches | 3x ISR4331, 4x Switch, 2x PC |

</div>

---

## 📘 Documentation & Protocol Deep-Dives

> Written analysis and packet-level study to complement the hands-on labs above.

<div align="center">

| # | 🗂️ File | 📋 Topic | 🔧 Focus |
|:---:|--------|----------|----------|
| `D1` | `Transport_Layer_Documentation.pdf` | Transport Layer Analysis: TCP vs. UDP Deep Dive | 3-Way Handshake, Flow Control, Port Multiplexing, Wireshark Trace Analysis |

</div>

<details>
<summary>📦 <b>Doc 1 — Transport Layer Analysis: TCP vs. UDP Deep Dive ⭐ LATEST</b></summary>

### 🎯 Key Focus Areas

| Area | What's Covered |
|------|-----------------|
| **Session Multiplexing** | Port allocation structures — Well-Known, Registered, and Ephemeral ranges |
| **TCP State Transitions** | 3-Way Handshake (`SYN` → `SYN-ACK` → `ACK`) and teardown (`FIN` sequences) with correlated Seq/Ack numbers |
| **Flow Control** | Dynamic window sizing to protect receiver buffer space |
| **Application Mapping** | Cross-reference table mapping enterprise services to their Layer 4 transport and port |

📥 [Download full PDF Documentation](./Transport_Layer_Documentation.pdf)

---

### 🔢 Port Allocation Ranges

| Range | Span | Purpose |
|-------|------|---------|
| **Well-Known** | 0 – 1023 | Reserved for standard services (HTTP, SSH, DNS, etc.) |
| **Registered** | 1024 – 49151 | Assigned to vendor/user applications |
| **Ephemeral** | 49152 – 65535 | Temporary client-side ports for outbound sessions |

---

### ⚖️ TCP vs. UDP — Core Comparison

| Feature | TCP | UDP |
|---------|-----|-----|
| Connection Type | Connection-oriented | Connectionless |
| Reliability | Guaranteed (ACKs, retransmission) | Best-effort |
| Ordering | In-order delivery | No guarantee |
| Handshake | 3-Way (SYN, SYN-ACK, ACK) | None |
| Flow Control | Yes (window sizing) | No |
| Header Overhead | 20 bytes | 8 bytes |
| Typical Use | HTTP/S, SSH, FTP, Email | DNS, DHCP, Streaming, VoIP, SNMP |

---

### 🛠️ Analyzed Protocols & Port Metrics

| Transport | Service | Port(s) |
|-----------|---------|---------|
| **TCP** | HTTP | 80 |
| **TCP** | HTTPS | 443 |
| **TCP** | SSH | 22 |
| **TCP** | SMTP | 25 |
| **TCP** | FTP | 20 / 21 |
| **UDP** | DHCP | 67 / 68 |
| **UDP** | TFTP | 69 |
| **UDP** | Syslog | 514 |
| **UDP** | SNMP | 161 / 162 |
| **Dual-Mode** | DNS | 53 |

---

### 🔁 TCP Connection Lifecycle

**3-Way Handshake (Establishment)**
```
Client                          Server
  |------ SYN (Seq=10) -------->|
  |<-- SYN-ACK (Seq=50,Ack=11)--|
  |------ ACK (Ack=51) -------->|
        Connection Established
```

**4-Way Teardown (Termination)**
```
Client                          Server
  |------ FIN ------------------>|
  |<----- ACK ---------------------|
  |<----- FIN ----------------------|
  |------ ACK ------------------>|
        Connection Closed
```

---

### 🔍 Sample Wireshark Trace Breakdown

```text
No.  Source          Destination     Protocol  Info
1    192.168.1.50    10.0.0.80       TCP       500 → 80 [SYN] Seq=10 Win=64240 Len=0
2    10.0.0.80       192.168.1.50    TCP       80 → 500 [SYN, ACK] Seq=50 Ack=11 Win=65535 Len=0
3    192.168.1.50    10.0.0.80       TCP       500 → 80 [ACK] Seq=11 Ack=51 Win=64240 Len=0
```

**Reading the trace:**
- Packet 1 — Client (port 500) initiates with `SYN`, Seq=10
- Packet 2 — Server responds `SYN-ACK`, Ack=11 (Seq+1), starts its own Seq=50
- Packet 3 — Client completes handshake with `ACK`, Ack=51 → session open for data transfer

---

### 📊 Flow Control — Window Sizing

| Concept | Explanation |
|---------|-------------|
| **Receive Window (Win)** | Advertised buffer space on the receiving host |
| **Dynamic Adjustment** | Window shrinks/grows based on receiver processing speed |
| **Zero Window** | Buffer full — sender pauses until window reopens |
| **Why It Matters** | Prevents buffer overflow and unnecessary retransmissions |

</details>

---

## 🎯 Lab Highlights

<details>
<summary>📦 <b>Lab 13 — OSPF + HSRP Gateway Redundancy</b></summary>

### 🗺️ Topology

```
        [PC0]                    [PC1]
          |                        |
       Fa0/1                    Fa0/1
      Switch0 ─────────────── Switch1
      Gig0/1  Gig0/2      Gig0/2  Gig0/1
        |                            |
        |                            |
      Gig0/1                      Fa0/1
      Switch2 ─────────────── Switch3
      Fa0/1   Gig0/2      Fa0/2   Gig0/2
        |                            |
      Fa0/2                       Gig0/1
        |                            |
   Gig0/0/0                     Gig0/0/0
   Router0(ISR4331)          Router3(ISR4331)
   HSRP Active                HSRP Standby
   192.168.1.1                192.168.1.5
        |                            |
   Gig0/0/1                     Gig0/0/1
   10.0.2.0/30                10.0.3.0/30
        \                           /
         \                         /
          ──── Router2(ISR4331) ───
                  (WAN Hub)
```

**HSRP Virtual IP: `192.168.1.254`** ← PCs use this as their default gateway

---

### 🔢 IP Addressing & Wildcard Masks

| Interface / Link | IP Address | Subnet | Wildcard Mask |
|-----------------|-----------|--------|---------------|
| Router0 Gig0/0/0 (LAN) | 192.168.1.1/24 | /24 | **0.0.0.255** |
| Router3 Gig0/0/0 (LAN) | 192.168.1.5/24 | /24 | **0.0.0.255** |
| HSRP Virtual IP | 192.168.1.254/24 | /24 | **0.0.0.255** |
| Router0 ↔ Router2 | 10.0.2.0/30 | /30 | **0.0.0.3** |
| Router3 ↔ Router2 | 10.0.3.0/30 | /30 | **0.0.0.3** |
| PC0 / PC1 LAN | 192.168.1.0/24 | /24 | **0.0.0.255** |

> 💡 **Wildcard Formula:** `255.255.255.255 − Subnet Mask`

---

### 🔁 HSRP — What & Why

| Feature | Explanation |
|---------|-------------|
| **Virtual IP** | `192.168.1.254` — PCs use this as gateway, never changes |
| **Active Router** | Router0 — forwards all traffic normally |
| **Standby Router** | Router3 — monitors Active, takes over if it fails |
| **Failover** | If Router0 goes down, Router3 becomes Active in seconds |
| **Transparent to PCs** | PCs never need to change their default gateway |
| **Protocol** | Cisco proprietary (CCNA exam topic) |

---

### ⚙️ Configuration

#### Router0 — HSRP Active + OSPF
```bash
conf t
interface GigabitEthernet0/0/0
 ip address 192.168.1.1 255.255.255.0
 ! HSRP Configuration
 standby 1 ip 192.168.1.254       ! Virtual IP — shared gateway for PCs
 standby 1 priority 110           ! Higher priority = Active router
 standby 1 preempt                ! Reclaim Active role after recovery
 no shutdown

interface GigabitEthernet0/0/1
 ip address 10.0.2.1 255.255.255.252
 no shutdown

router ospf 1
 network 192.168.1.0 0.0.0.255 area 0
 network 10.0.2.0 0.0.0.3 area 0
end
wr
```

#### Router3 — HSRP Standby + OSPF
```bash
conf t
interface GigabitEthernet0/0/0
 ip address 192.168.1.5 255.255.255.0
 ! HSRP Configuration
 standby 1 ip 192.168.1.254       ! Same Virtual IP as Router0
 standby 1 priority 90            ! Lower priority = Standby router
 standby 1 preempt
 no shutdown

interface GigabitEthernet0/0/1
 ip address 10.0.3.1 255.255.255.252
 no shutdown

router ospf 1
 network 192.168.1.0 0.0.0.255 area 0
 network 10.0.3.0 0.0.0.3 area 0
end
wr
```

#### PC Default Gateway
```
PC0 Default Gateway: 192.168.1.254  ← HSRP Virtual IP
PC1 Default Gateway: 192.168.1.254  ← HSRP Virtual IP
```

---

### 🧪 Verification Commands & Results

```bash
! Verify HSRP status
Router0# show standby brief
Interface  Grp  Pri  P  State   Active        Standby       VirtualIP
Gi0/0/0    1    110  P  Active  local         192.168.1.5   192.168.1.254

Router3# show standby brief
Interface  Grp  Pri  P  State    Active        Standby  VirtualIP
Gi0/0/0    1    90   P  Standby  192.168.1.1   local    192.168.1.254

! Verify OSPF neighbors
Router0# show ip ospf neighbor
Neighbor ID   State   Interface
[Router2 ID]  FULL    GigabitEthernet0/0/1
```

### PDU Simulation Results
| Source | Destination | Type | Status |
|--------|-------------|------|--------|
| PC0 | Router2 | ICMP | ✅ Successful |
| PC1 | Router2 | ICMP | ✅ Successful |
| PC1 | Router2 | ICMP | ✅ Successful |

---

### 📊 HSRP vs Other FHRP Protocols

| Feature | HSRP | VRRP | GLBP |
|---------|------|------|------|
| Vendor | Cisco only | Open standard | Cisco only |
| Virtual IP | Separate from real IPs | Can use router's IP | Separate |
| Load Balancing | ❌ Active/Standby only | ❌ | ✅ Yes |
| Preempt | Manual config | Auto | Auto |
| CCNA Exam | ✅ Yes | ✅ Yes | ✅ Yes |

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
| Works with HSRP | ✅ | ✅ | ✅ | ✅ |

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
│  ✅  Lab 11  →  OSPF Dual Router + ISP Link                           │
│  ✅  Lab 12  →  OSPF Multi-Router Serial WAN                          │
│  ✅  Lab 13  →  OSPF + HSRP Gateway Redundancy                        │
│  ✅  Doc 01  →  Transport Layer: TCP vs UDP Deep Dive  ◄ YOU ARE HERE │
│  ⏳  Next    →  ACLs · NAT/PAT · DHCP · WAN                           │
└──────────────────────────────────────────────────────────────────────┘
```

---

## 🧪 Master Verification Commands

```bash
# HSRP
show standby brief               # HSRP Active/Standby state + Virtual IP
show standby                     # Full HSRP details

# OSPF
show ip ospf neighbor            # Neighbor adjacency & FULL state
show ip route ospf               # OSPF-learned routes only
show ip ospf database            # Full LSDB
show ip protocols                # OSPF process & Router ID

# General
show ip route                    # Full routing table
show ip interface brief          # All interfaces + status
ping [ip]                        # Test reachability
traceroute [ip]                  # Trace path hop by hop
```

---

## 🛠️ Requirements

- Cisco Packet Tracer **8.0 or higher**
- Wireshark (for verifying TCP/UDP packet-level concepts)

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
