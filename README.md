# Fishtail Hospital Network Design

[![Cisco Packet Tracer](https://img.shields.io/badge/Tool-Cisco%20Packet%20Tracer%208.x-blue)](https://www.netacad.com/courses/packet-tracer)
[![Course](https://img.shields.io/badge/Course-CT%20654%20Computer%20Networks-green)](https://ioe.edu.np)
[![Institution](https://img.shields.io/badge/Institution-IOE%20Pulchowk%20Campus-red)](https://pcampus.edu.np)

## 📋 Project Overview

A comprehensive enterprise network design and implementation for **Fishtail Hospital** using Cisco Packet Tracer. This project demonstrates advanced networking concepts including multi-area OSPF routing, VLAN segmentation, VLSM addressing, and network services configuration.

**Student:** Chandan Kumar Shah  
**Roll No:** 080BCT023  
**Course:** CT 654 — Computer Networks  
**Institution:** Institute of Engineering, Pulchowk Campus, Tribhuvan University  
**Date:** April 2026

## 🏗️ Network Architecture

```
                      [ISP-DNS: 203.0.113.10]
                               |
                      ISP-R1 [172.16.0.1]
                               |
                      Chandan1 [ASBR/Core]
                     /         |          \
                Chandan2    Chandan3*    Chandan4
              (Admin GW)   (Ward/ABR)   (Transit)
                   |           |            |
               Chandan6    Chandan7     Chandan5
              (OPD GW)    (Ward F2)    (Transit)
                   |           |            |
                  SW2         SW4       Chandan8*
               (OPD LAN)   (VLANs)       (ABR)
                              |            |
                             SW3       Chandan9
                          (VLANs)    (Server/ICU)
                                          |
                  SW1                    SW5
               (Admin)                (VLANs)
```

## ✅ Requirements Implemented

| Requirement | Status | Details |
|-------------|--------|---------|
| Minimum 10 routers | ✅ | 10 routers (ISP-R1 + Chandan1–9) |
| At least 3 transit routers | ✅ | Chandan4, Chandan5, Chandan8 |
| ISP router + connection | ✅ | ISP-R1 with 203.0.113.0/24 |
| 9+ LANs with 6 different subnet sizes | ✅ | 9 LANs + 9 P2P links, 6 sizes |
| OSPF multi-area (3+ areas) | ✅ | Area 0, Area 1, Area 2 |
| Minimum 7 VLANs | ✅ | VLAN 10, 20, 30, 40, 50, 60, 70 |
| 2+ VLANs spanning 3+ switches | ✅ | VLAN 10 and VLAN 20 |
| Minimum 3 DNS servers | ✅ | DNS1, DNS2, ISP-DNS |
| Minimum 2 Web servers | ✅ | WebServer1, WebServer2 |
| Minimum 3 DHCP servers | ✅ | DHCP1, DHCP2, DHCP3 |
| Router security | ✅ | Passwords + telnet on all routers |
| VLSM addressing | ✅ | 6 different prefix lengths |

## 📊 Network Statistics

| Metric | Value |
|--------|-------|
| Total Devices | 28 |
| Routers | 10 |
| Switches | 5 |
| Servers | 8 |
| Workstations | 5 |
| OSPF Areas | 3 |
| VLANs | 7 |
| IP Block | 172.16.0.0/22 (1024 addresses) |

## 🌐 IP Addressing Scheme (VLSM)

| Department | VLAN | Subnet | Gateway | Prefix |
|------------|------|--------|---------|--------|
| Administration | — | 172.16.1.0/24 | 172.16.1.1 | /24 |
| OPD | — | 172.16.2.0/25 | 172.16.2.1 | /25 |
| General Ward | 10 | 172.16.3.0/26 | 172.16.3.1 | /26 |
| Private Ward | 20 | 172.16.3.64/27 | 172.16.3.65 | /27 |
| Maternity Ward | 30 | 172.16.3.96/27 | 172.16.3.97 | /27 |
| Server Room | 40 | 172.16.3.128/28 | 172.16.3.129 | /28 |
| Laboratory | 60 | 172.16.3.144/28 | 172.16.3.145 | /28 |
| ICU / Emergency | 50 | 172.16.3.160/27 | 172.16.3.161 | /27 |
| Pharmacy | 70 | 172.16.3.192/29 | 172.16.3.193 | /29 |

## 🔧 Technologies Used

- **Routing Protocol:** OSPF Multi-Area (Area 0, 1, 2)
- **VLAN Routing:** Router-on-a-Stick (802.1Q)
- **IP Addressing:** VLSM with 6 prefix lengths
- **Network Services:** DNS, DHCP, Web Servers
- **Security:** Console/VTY passwords, Enable secret

## 📁 Repository Contents

| File | Description |
|------|-------------|
| `final_project.pkt` | Cisco Packet Tracer project file |
| `project.md` | Complete project documentation |
| `report.tex` | LaTeX report for submission |
| `topology.png` | Network topology diagram |
| `emblem.png` | Institution emblem |

## 🚀 How to Use

1. Download and install [Cisco Packet Tracer 8.x](https://www.netacad.com/courses/packet-tracer)
2. Open `final_project.pkt` in Packet Tracer
3. Explore the network topology and configurations
4. Test connectivity using the simulation mode

## 🧪 Connectivity Tests

All tests verified from PC-Admin1 (172.16.1.10):

- ✅ Gateway reachability (172.16.1.1)
- ✅ Cross-area OSPF routing (172.16.2.10)
- ✅ Cross-VLAN communication (172.16.3.10)
- ✅ ISP connectivity (203.0.113.10)
- ✅ DNS resolution (hospital.local → 172.16.2.3)

## 📜 License

This project is submitted as coursework for CT 654 Computer Networks at IOE Pulchowk Campus.

---

**Author:** Chandan Kumar Shah (080BCT023)  
**Course Instructor:** CT 654 Computer Networks Faculty  
**Institution:** Institute of Engineering, Pulchowk Campus
