# 🖧 Cisco Packet Tracer Lab Repository

> 📚 A structured, hands-on collection of Cisco networking labs — built while preparing for **CCNA (200-301)**
> From basic ARP/ICMP to advanced OSPF, Static Routing, and Floating Static backup routes.

![Cisco](https://img.shields.io/badge/Cisco-Packet%20Tracer-blue?style=for-the-badge&logo=cisco)
![CCNA](https://img.shields.io/badge/Certification-CCNA%20200--301-green?style=for-the-badge)
![Labs](https://img.shields.io/badge/Labs-8%20and%20Growing-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Actively%20Preparing-red?style=for-the-badge)

---

## 📁 Labs Included

| # | File | Description | Technologies | Devices |
|---|------|-------------|--------------|---------|
| 1 | `ICMP.ARP.pkt` | ARP and ICMP connectivity test | ARP, ICMP | 2x PCs, 2x 2960 Switches |
| 2 | `static-routing-lab.pkt` | Static routing between 3 networks | Static Routing | Router0, 4x PCs, 2960 Switch |
| 3 | `vlan-segmentation-lab.pkt` | VLAN segmentation with multiple PCs | VLAN | 50+ PCs, Managed Switches |
| 4 | `stp-bpduguard-lab.pkt` | STP, Root Bridge, BPDU Guard | STP, BPDU Guard | 3x Switches |
| 5 | `rstp-root-bridge-lab.pkt` | RSTP root bridge and port priority | RSTP (802.1w) | Multiple Switches |
| 6 | `layer3-intervlan-routing-lab.pkt` | Layer 3 switch inter-VLAN routing | SVI, Static Routing | L2+L3 Switches, Router, 8 PCs |
| 7 | `router-on-a-stick-roas-lab.pkt` | Router-on-a-Stick inter-VLAN routing | VLAN, 802.1Q, Subinterfaces | L2 Switch, Router, 8+ PCs |
| 8 | `ospf-static-floating-lab.pkt` | OSPF + Static + Floating Static Route | OSPF, Static Routing, Floating Static | 4x Routers, 2x PCs |

---

## 🎯 Lab Highlights

### Lab 6: Layer 3 Inter-VLAN Routing
- **VLANs:** 10, 20, 30
- **Routing:** SVI on Layer 3 Switch
- **Subnetting:** /26

### Lab 7: Router-on-a-Stick (ROAS)
- **VLANs:** 10, 20, 30, 40
- **Routing:** Router subinterfaces
- **Trunk:** 802.1Q between switch and router

### Lab 8: OSPF + Static + Floating Static Route ⭐ NEW
- **Topology:** `PC0 — R0 — R1 — R2 — R3 — PC1`
- **OSPF:** Dynamic routing across all routers (Area 0)
- **Static Routing:** Manual routes as full backup
- **Floating Static:** High AD (200) backup if OSPF fails
- **Subnetting:** /30 for point-to-point links, /24 for LANs

---

## 📊 Routing Method Comparison

| Feature | Static Routing | OSPF | Floating Static |
|---------|---------------|------|-----------------|
| Type | Manual | Dynamic | Manual (Backup) |
| Admin Distance | 1 | 110 | 200 (custom) |
| Auto-update | ❌ No | ✅ Yes | ❌ No |
| Best for | Small/stable networks | Large/dynamic networks | Redundancy/backup |
| Overhead | None | Low (Hello packets) | None |

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
1. ARP/ICMP          →  Basic connectivity & troubleshooting
2. Static Routing    →  Router fundamentals & manual routes
3. VLANs             →  Network segmentation
4. STP/RSTP          →  Loop prevention & redundancy
5. Inter-VLAN (L3)   →  Layer 3 switch with SVI
6. Inter-VLAN (ROAS) →  Router-on-a-Stick with 802.1Q
7. OSPF + Floating   →  Dynamic routing + backup routes  ← YOU ARE HERE
```

---

## 🛠 Requirements

- Cisco Packet Tracer **8.0 or higher**

---

## 📖 How to Use

1. Clone or download this repository
2. Open any `.pkt` file in Cisco Packet Tracer
3. Explore configurations using the CLI
4. Run `show ip route` and `show ip ospf neighbor` to verify

---

## 🧪 Key Verification Commands

```bash
show ip route                  # View routing table
show ip ospf neighbor          # Verify OSPF neighbors
show ip interface brief        # Check interface status
ping 192.168.10.2              # Test end-to-end connectivity
```

---

## 👤 About

> 🎓 Currently preparing for **Cisco CCNA 200-301**
> 💡 Documenting every lab to solidify understanding and help others
> 🔗 Connect with me on [LinkedIn](https://linkedin.com/in/YOUR-PROFILE)

---

**Happy Networking!** 🚀
