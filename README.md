# 🖧 My Cisco Packet Tracer Lab Repository

Welcome to my Cisco networking lab repository! This is my personal collection of Packet Tracer labs covering fundamental to advanced networking concepts.

---

## 📁 Labs Included

| # | File | Description | Technologies | Devices |
|---|------|-------------|--------------|---------|
| 1 | ICMP.ARP.pkt | ARP and ICMP connectivity test | ARP, ICMP | 2x PCs, 2x 2960 switches |
| 2 | static-routing-lab.pkt | Static routing between 3 networks | Static Routing | Router0, 4x PCs, 2960 switch |
| 3 | vlan-segmentation-lab.pkt | VLAN segmentation with multiple PCs | VLAN | 50+ PCs, managed switches |
| 4 | stp-bpduguard-lab.pkt | STP, Root Bridge, BPDU Guard | STP, BPDU Guard | 3x switches |
| 5 | rstp-root-bridge-lab.pkt | RSTP root bridge and port priority | RSTP (802.1w) | Multiple switches |
| 6 | layer3-intervlan-routing-lab.pkt | Layer 3 switch inter-VLAN routing | SVI, Static Routing | L2+L3 switches, router, 8 PCs |
| 7 | router-on-a-stick-roas-lab.pkt | Router-on-a-Stick (ROAS) | VLAN, 802.1Q, Subinterfaces | L2 switch, router, 8+ PCs |

---

## 🎯 Lab Highlights

### Lab 6: Layer 3 Inter-VLAN Routing
- **VLANs:** 10, 20, 30
- **Routing:** SVI on Layer 3 switch
- **Subnetting:** /26

### Lab 7: Router-on-a-Stick (ROAS)
- **VLANs:** 10, 20, 30, 40
- **Routing:** Router subinterfaces
- **Trunk:** 802.1Q between switch and router

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

## 🛠 Requirements
- Cisco Packet Tracer 8.0 or higher

---

## 📖 How to Use
1. Clone or download this repository
2. Open any `.pkt` file in Packet Tracer
3. Explore configurations using CLI

---

## 📈 Learning Path
1. ARP/ICMP – Basic connectivity
2. Static Routing – Router fundamentals
3. VLANs – Segmentation
4. STP/RSTP – Loop prevention
5. Inter-VLAN Routing – Layer 3 switch (SVI)
6. Inter-VLAN Routing – Router-on-a-Stick (ROAS)

---

**Happy Networking!** 🚀
