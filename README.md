# 🖧 Cisco Packet Tracer Lab Repository

> 📚 A structured, hands-on collection of Cisco networking labs and protocol deep-dives — built while preparing for **CCNA (200-301)**
> From basic ARP/ICMP to OSPF, HSRP, Standard & Extended ACLs, Transport Layer analysis with packet-level breakdowns.

<div align="center">

![Cisco](https://img.shields.io/badge/Cisco-Packet%20Tracer-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)
![CCNA](https://img.shields.io/badge/CCNA-200--301-00873E?style=for-the-badge&logo=cisco&logoColor=white)
![Labs](https://img.shields.io/badge/Total%20Labs-16-FF6B35?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Actively%20Preparing-red?style=for-the-badge)

</div>

---

## 🧭 Quick Navigation

- [All Labs](#-all-labs)
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
| `13` | `ospf-HSRP.pkt` | OSPF + HSRP Gateway Redundancy | OSPF, HSRP, Virtual IP, Mesh Switches | 3x ISR4331, 4x Switch, 2x PC |
| `14` | `Transport_Layer_Documentation.pdf` | Transport Layer Analysis: TCP vs. UDP Deep Dive | TCP/UDP, 3-Way Handshake, Flow Control, Wireshark Trace | Written Protocol Analysis |
| `15` | `standard-acl-lab.pkt` | Standard ACLs — Traffic Filtering & Security | Standard ACL, Wildcard Mask, `ip access-group` | 2x 2911 Router, 4x Switch, 4x PC, 2x Server |
| `16` | `extended-acl-server-dept-lab.pkt` | Extended ACLs — Server Protection & Department Isolation ⭐ | Extended ACL, Named ACL, TCP/UDP Port Matching, Sequence Numbers | 2x 2911 Router, 4x Switch, 4x PC, 2x Server |

</div>

---

## 🎯 Lab Highlights

<details>
<summary>📦 <b>Lab 14 — Transport Layer Analysis: TCP vs. UDP Deep Dive</b></summary>

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

<details>
<summary>📦 <b>Lab 15 — Standard ACLs: Traffic Filtering & Security</b></summary>

### 🗺️ Topology

```
  [PC1 172.16.1.1]  [PC0 172.16.1.2]
         |                  |
       Fa0/1             Fa0/2
          \               /
           Switch1 (Fa0/1)
                 |
           Gig0/0 (172.16.1.3/24)
              Router1 (2911)
           Gig0/1 (172.16.2.3/24)
           Gig0/2 (203.0.113.1/30)  ── WAN ──  Gig0/0 (203.0.113.2/30)
                                                   Router2 (2911)
                                               Gig0/1 (192.168.1.1/24)
                                               Fa0/1  (192.168.2.1/24)
           Switch0 (Fa0/1)                    Switch2 (Fa0/1)   Switch3 (Fa0/1)
         Fa0/2    Fa0/3                         Fa0/2               Fa0/2
          |         |                             |                   |
  [PC2 172.16.2.1] [PC3 172.16.2.2]    [Server0 192.168.1.100]  [Server1 192.168.2.100]
```

---

### 📋 Lab Requirements

| # | Requirement | ACL Used | Applied On |
|---|-------------|----------|------------|
| 1 | Only PC1 (`172.16.1.1`) and PC0 (`172.16.1.2`) can access `192.168.1.0/24` | ACL 5 | Router2 Gig0/1 `out` |
| 2 | `172.16.2.0/24` cannot access `192.168.2.0/24` | ACL 10 | Router2 Fa0/1 `out` |
| 3 | `172.16.1.0/24` cannot access `172.16.2.0/24` | ACL 5 | Router1 Gig0/1 `out` |
| 4 | `172.16.2.0/24` cannot access `172.16.1.0/24` | ACL 10 | Router1 Gig0/0 `out` |

> 💡 **Standard ACL Rule:** Place standard ACLs as **close to the destination** as possible — they filter by source IP only, so placing them near the source would block traffic to all destinations.

---

### 🔢 IP Addressing Table

| Device | Interface | IP Address | Subnet |
|--------|-----------|------------|--------|
| PC1 | Fa0 | 172.16.1.1 | /24 |
| PC0 | Fa0 | 172.16.1.2 | /24 |
| PC2 | Fa0 | 172.16.2.1 | /24 |
| PC3 | Fa0 | 172.16.2.2 | /24 |
| Server0 | Fa0 | 192.168.1.100 | /24 |
| Server1 | Fa0 | 192.168.2.100 | /24 |
| Router1 Gig0/0 | — | 172.16.1.3 | /24 |
| Router1 Gig0/1 | — | 172.16.2.3 | /24 |
| Router1 Gig0/2 | — | 203.0.113.1 | /30 |
| Router2 Gig0/0 | — | 203.0.113.2 | /30 |
| Router2 Gig0/1 | — | 192.168.1.1 | /24 |
| Router2 Fa0/1 | — | 192.168.2.1 | /24 |

---

### ⚙️ ACL Configuration

#### Standard ACL 5 — Permit only PC1 & PC0, deny all others
```bash
Router(config)#access-list 5 deny host 172.16.1.1
Router(config)#access-list 5 deny host 172.16.2.1
Router(config)#access-list 5 permit any
```
> Denies PC1 (`172.16.1.1`) and PC2 (`172.16.2.1`) explicitly, permits all other hosts.

#### Standard ACL 10 — Block entire 172.16.2.0/24 subnet
```bash
Router(config)#access-list 10 deny 172.16.2.0 0.0.0.255
Router(config)#access-list 10 permit any
```
> Denies all traffic sourced from `172.16.2.0/24`, permits everything else.

#### Applying ACLs to Interfaces
```bash
! Block 172.16.2.0/24 from reaching 192.168.2.0/24
Router(config)#interface GigabitEthernet0/1
Router(config-if)#ip access-group 10 out

! Apply ACL 5 to restrict access to 192.168.1.0/24
Router(config)#interface GigabitEthernet0/1
Router(config-if)#ip access-group 5 out
```

---

### 🧪 Verification Commands & Output

```bash
! View all configured ACLs and match counters
Router# show ip access-lists

Standard IP access list 5
    10 deny host 172.16.1.1 (1 match(es))
    20 deny host 172.16.2.1
    30 permit any (3 match(es))

Standard IP access list 10
    10 deny 172.16.2.0 0.0.0.255 (1 match(es))
    20 permit any (1 match(es))

! Verify ACL applied to interface
Router# show ip interface GigabitEthernet0/1
  Outgoing access list is 10
```

> 💡 The `(match(es))` counter increments every time a packet hits that ACE — useful for confirming the ACL is actually being evaluated.

---

### 📊 Standard vs Extended ACL — Key Differences

| Feature | Standard ACL | Extended ACL |
|---------|-------------|--------------|
| Filters by | Source IP only | Source IP, Dest IP, Port, Protocol |
| ACL Number Range | 1 – 99 | 100 – 199 |
| Placement Rule | Close to **destination** | Close to **source** |
| Granularity | Low | High |
| CCNA Exam | ✅ Yes | ✅ Yes |

</details>

---

<details>
<summary>📦 <b>Lab 16 — Extended ACLs: Server Protection & Department Isolation ⭐ LATEST</b></summary>

### 🗺️ Topology

```
  [PC1 172.16.1.1]  [PC0 172.16.1.2]
         |                  |
       Fa0/1             Fa0/2
          \               /
           Switch1 (Fa0/1)
                 |
           Gig0/0 (172.16.1.x/24)
              Router0 (2911)
           Gig0/2 (WAN) ──── Router2 (2911)
                                 |            \
                           Gig0/1 (192.168.1.1)  Fa0/1 (192.168.2.1)
                           Switch2              Switch3
                             |                    |
                        [Server0 192.168.1.100]  [Server1 192.168.2.100]
```

---

### 📋 Task Breakdown

| Task | Objective | ACL Name | Applied On |
|------|-----------|----------|------------|
| **1** | Allow only HTTP/HTTPS from `172.16.2.0/24` + ICMP from any to Server0. Block all other traffic to Server0. | `To-server0` (Extended) | Router2 `Gig0/0` **in** |
| **2** | Block `172.16.1.0/24` from reaching `172.16.2.0/24`. Allow internet access. | `TO-172.16.2.0` (Extended) | Router0 `Gig0/2` **in** |
| **3** | Block specific host PC0 (`172.16.1.1`) from reaching Server1 (`192.168.2.100`) only. | Injected at sequence **line 5** of `TO-172.16.2.0` | Same interface |

> 💡 **Extended ACL Rule:** Place extended ACLs as **close to the source** as possible — they can filter by source IP, destination IP, protocol, and port, so early placement saves bandwidth.

---

### ⚙️ Configuration

#### Task 1 — Router2: Named Extended ACL (Server0 Protection)
```bash
ip access-list extended To-server0
 permit tcp 172.16.2.0 0.0.0.255 host 192.168.1.100 eq www
 permit tcp 172.16.2.0 0.0.0.255 host 192.168.1.100 eq 443
 permit icmp any host 192.168.1.100
 deny ip any host 192.168.1.100
 permit ip any any

interface GigabitEthernet0/0
 ip access-group To-server0 in
```

#### Task 2 — Router0: Department Isolation (LAN1 → LAN2 blocked)
```bash
ip access-list extended TO-172.16.2.0
 deny ip 172.16.1.0 0.0.0.255 172.16.2.0 0.0.0.255
 permit ip any any

interface GigabitEthernet0/2
 ip access-group TO-172.16.2.0 in
```

#### Task 3 — Inject Host Rule at Sequence Line 5 (PC0 → Server1 blocked)
```bash
! Inject specific host rule ABOVE the subnet rule without rewriting the ACL
ip access-list extended TO-172.16.2.0
 5 deny ip host 172.16.1.1 host 192.168.2.100
```

#### Final Consolidated ACL on Router0
```bash
Extended IP access list TO-172.16.2.0
 5 deny ip host 172.16.1.1 host 192.168.2.100
 10 deny ip 172.16.1.0 0.0.0.255 172.16.2.0 0.0.0.255
 20 permit ip any any
```

---

### 🔑 Key Concepts Applied

| Concept | Explanation |
|---------|-------------|
| **One ACL per interface/direction** | Combined Tasks 2 & 3 into one ACL to avoid overwriting — strict IOS rule |
| **Extended placement near source** | Applied on Router0 `Gig0/2` inbound to drop packets before they enter the WAN |
| **Sequence number injection** | Added host-specific rule at line 5 to slot above the broader subnet deny at line 10 — no need to delete and rewrite |
| **`host` keyword** | Equivalent to `0.0.0.0` wildcard mask — targets a single IP precisely without accidentally matching a subnet |
| **Top-to-bottom processing** | Most specific rule first (line 5: single host), then broader (line 10: subnet), then global permit (line 20) |

---

### 🧪 Verification Commands

```bash
! View ACL with match counters
Router# show ip access-lists

Extended IP access list To-server0
    10 permit tcp 172.16.2.0 0.0.0.255 host 192.168.1.100 eq www
    20 permit tcp 172.16.2.0 0.0.0.255 host 192.168.1.100 eq 443
    30 permit icmp any host 192.168.1.100
    40 deny ip any host 192.168.1.100
    50 permit ip any any

Extended IP access list TO-172.16.2.0
    5  deny ip host 172.16.1.1 host 192.168.2.100
    10 deny ip 172.16.1.0 0.0.0.255 172.16.2.0 0.0.0.255
    20 permit ip any any

! Verify ACL applied to interface
Router# show ip interface GigabitEthernet0/0
  Inbound access list is To-server0

Router# show ip interface GigabitEthernet0/2
  Inbound access list is TO-172.16.2.0
```

---

### 📊 Standard vs Extended ACL — Full Comparison

| Feature | Standard ACL | Extended ACL |
|---------|-------------|--------------|
| ACL Number Range | 1 – 99 | 100 – 199 |
| Named ACL | ✅ | ✅ |
| Filter by Source IP | ✅ | ✅ |
| Filter by Dest IP | ❌ | ✅ |
| Filter by Port/Protocol | ❌ | ✅ (TCP, UDP, ICMP, etc.) |
| Placement | Near **destination** | Near **source** |
| Granularity | Low | High |
| Sequence Injection | ✅ | ✅ |
| CCNA Exam | ✅ | ✅ |

</details>

---

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
│  ✅  Lab 14  →  Transport Layer: TCP vs UDP Deep Dive                  │
│  ✅  Lab 15  →  Standard ACLs: Traffic Filtering & Security           │
│  ✅  Lab 16  →  Extended ACLs: Server Protection & Dept Isolation ◄ YOU ARE HERE │
│  ⏳  Next    →  NAT/PAT · DHCP · DNS · WAN                            │
└──────────────────────────────────────────────────────────────────────┘
```

---

## 🧪 Master Verification Commands

```bash
# ACL
show ip access-lists              # All ACLs with match counters
show ip interface [int]           # Shows inbound/outbound ACL on interface
show running-config | include access  # Quick ACL config grep

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
