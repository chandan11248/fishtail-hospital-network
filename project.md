# FISHTAIL HOSPITAL NETWORK — COMPLETE PROJECT INFORMATION
# CT 654 Computer Networks | IOE Pulchowk Campus | April 2026
# Student: Chandan Kumar Shah | Roll No: 080BCT023
================================================================================


## 1. PROJECT OVERVIEW

**Project Title:** Network Design and Implementation for Fishtail Hospital  
**Course:** CT 654 — Computer Networks  
**Institution:** Institute of Engineering, Pulchowk Campus, Tribhuvan University  
**Tool Used:** Cisco Packet Tracer 8.x  
**IP Block Assigned:** 172.16.0.0/22 (Total: 1024 addresses)  
**Scenario:** Multi-department hospital network with ISP connectivity


---


## 2. REQUIREMENTS MET (Checklist)

| Requirement                                          | Status | Detail                          |
|------------------------------------------------------|--------|---------------------------------|
| Minimum 10 routers                                   | ✓      | 10 routers (ISP-R1 + Chandan1–9)|
| At least 3 transit routers                           | ✓      | Chandan4, Chandan5, Chandan8    |
| ISP router + connection                              | ✓      | ISP-R1 with 203.0.113.0/24      |
| At least 9 LANs with 6 different subnet sizes        | ✓      | 9 LANs + 9 P2P links, 6 sizes   |
| OSPF multi-area (minimum 3 areas)                    | ✓      | Area 0, Area 1, Area 2          |
| Minimum 7 VLANs                                      | ✓      | VLAN 10, 20, 30, 40, 50, 60, 70 |
| At least 2 VLANs spanning 3+ switches                | ✓      | VLAN 10 and VLAN 20 (SW3/SW4/SW5)|
| Minimum 3 DNS servers                                | ✓      | DNS1, DNS2, ISP-DNS             |
| Minimum 2 Web servers                                | ✓      | WebServer1, WebServer2          |
| Minimum 3 DHCP servers                               | ✓      | DHCP1, DHCP2, DHCP3             |
| Router security (passwords + telnet)                 | ✓      | All 9 routers configured        |
| Router naming convention                             | ✓      | Chandan1–Chandan9               |
| VLSM addressing                                      | ✓      | 6 different prefix lengths used |
| Interface labeling in Packet Tracer                  | ✓      | All IPs labeled in topology     |


---


## 3. DEVICE INVENTORY

| Device       | Model          | Quantity | Role                      |
|--------------|----------------|----------|---------------------------|
| Routers      | Cisco 2911     | 10       | ISP-R1 + Chandan1–9       |
| Switches     | Cisco 2960-24TT| 5        | SW1, SW2, SW3, SW4, SW5   |
| Servers      | Server-PT      | 8        | DNS, DHCP, Web, ISP       |
| Workstations | PC-PT          | 5        | Admin, OPD, Ward, ICU     |
| **TOTAL**    |                | **28**   |                           |


---


## 4. NETWORK TOPOLOGY STRUCTURE

```
                          [ISP-DNS: 203.0.113.10]
                                   |
                          ISP-R1 [172.16.0.1]
                                   |  (GigabitEthernet)
                          Chandan1 [172.16.0.2]  ← Core Router / ASBR
                         /         |          \
               (Serial)           (Serial)    (GigE)
             Chandan2           Chandan3*     Chandan4
          (Admin GW)          (Ward F1/ABR)  (Transit)
               |                   |              |
           Chandan6            Chandan7        Chandan5
          (OPD GW)           (Ward F2)        (Transit)
               |                   |              |
              SW2                 SW4          Chandan8*
           (OPD LAN)          (VLANs)          (ABR)
                                   |              |
                                  SW3          Chandan9
                                (VLANs)     (Server/ICU)
                                                  |
                              SW1               SW5
                           (Admin LAN)      (VLANs)
```
*ABR = Area Border Router (connects two OSPF areas)


---


## 5. OSPF MULTI-AREA ROUTING

### Area Assignment

| OSPF Area        | Routers Included              | Type          |
|------------------|-------------------------------|---------------|
| Area 0 (Backbone)| Chandan1, Chandan3, Chandan4, Chandan5, Chandan8 | Transit/Core |
| Area 1           | Chandan2, Chandan3, Chandan6, Chandan7           | Admin/OPD/Ward |
| Area 2           | Chandan8, Chandan9                               | ICU/Server Room |

### ABR (Area Border Routers)
- **Chandan3** — sits on boundary of Area 0 and Area 1
- **Chandan8** — sits on boundary of Area 0 and Area 2

### ASBR (Autonomous System Boundary Router)
- **Chandan1** — redistributes static default route from ISP into OSPF (ISP connectivity)

### Routing Logic
- All inter-area routes learned via OSPF (marked `O IA` in routing table)
- Default route (0.0.0.0/0) from ISP-R1 → Chandan1 → redistributed into OSPF
- ISP-R1 itself uses a static summary route: `ip route 172.16.0.0 255.255.252.0 172.16.0.2`


---


## 6. IP ADDRESSING — COMPLETE TABLE

### 6a. Point-to-Point Links (all /30 — 2 usable hosts each)

| Link                      | Network         | Router A IP     | Router B IP     |
|---------------------------|-----------------|-----------------|-----------------|
| ISP-R1 ↔ Chandan1         | 172.16.0.0/30   | 172.16.0.1      | 172.16.0.2      |
| Chandan1 ↔ Chandan2       | 172.16.0.4/30   | 172.16.0.5      | 172.16.0.6      |
| Chandan1 ↔ Chandan3       | 172.16.0.8/30   | 172.16.0.9      | 172.16.0.10     |
| Chandan1 ↔ Chandan4       | 172.16.0.12/30  | 172.16.0.13     | 172.16.0.14     |
| Chandan4 ↔ Chandan5       | 172.16.0.16/30  | 172.16.0.17     | 172.16.0.18     |
| Chandan2 ↔ Chandan6       | 172.16.0.20/30  | 172.16.0.21     | 172.16.0.22     |
| Chandan3 ↔ Chandan7       | 172.16.0.24/30  | 172.16.0.25     | 172.16.0.26     |
| Chandan5 ↔ Chandan8       | 172.16.0.28/30  | 172.16.0.29     | 172.16.0.30     |
| Chandan8 ↔ Chandan9       | 172.16.0.32/30  | 172.16.0.33     | 172.16.0.34     |

**DCE side** (provides clock rate 64000): Chandan1 (both serials), Chandan2 S0/0/1, Chandan3 S0/0/1, Chandan4 S0/0/0, Chandan5 S0/0/1, Chandan8 S0/0/1

### 6b. LAN Subnets (VLSM — 6 different subnet sizes)

| Department          | VLAN | Subnet            | Gateway       | Hosts | Prefix |
|---------------------|------|-------------------|---------------|-------|--------|
| Administration      | —    | 172.16.1.0/24     | 172.16.1.1    | 254   | /24    |
| OPD                 | —    | 172.16.2.0/25     | 172.16.2.1    | 126   | /25    |
| General Ward        | 10   | 172.16.3.0/26     | 172.16.3.1    | 62    | /26    |
| Private Ward        | 20   | 172.16.3.64/27    | 172.16.3.65   | 30    | /27    |
| Maternity Ward      | 30   | 172.16.3.96/27    | 172.16.3.97   | 30    | /27    |
| Server Room         | 40   | 172.16.3.128/28   | 172.16.3.129  | 14    | /28    |
| Laboratory          | 60   | 172.16.3.144/28   | 172.16.3.145  | 14    | /28    |
| ICU / Emergency     | 50   | 172.16.3.160/27   | 172.16.3.161  | 30    | /27    |
| Pharmacy            | 70   | 172.16.3.192/29   | 172.16.3.193  | 6     | /29    |
| ISP Public Network  | —    | 203.0.113.0/24    | 203.0.113.1   | 254   | /24    |

**6 prefix lengths used:** /24, /25, /26, /27, /28, /29 ✓

### 6c. Address Utilization Summary

| Category              | Addresses Used |
|-----------------------|---------------|
| P2P links (9 × /30)   | 36            |
| Admin LAN (/24)       | 254           |
| OPD LAN (/25)         | 126           |
| VLAN subnets combined | 196           |
| Total used            | ~612          |
| Reserved for expansion| ~412          |
| Total block (172.16.0.0/22) | 1024   |


---


## 7. VLAN CONFIGURATION

### VLAN Table

| VLAN ID | Name           | Subnet            | Switch Coverage       |
|---------|----------------|-------------------|-----------------------|
| 10      | General-Ward   | 172.16.3.0/26     | SW3 + SW4 + SW5 (3 switches) |
| 20      | Private-Ward   | 172.16.3.64/27    | SW3 + SW4 + SW5 (3 switches) |
| 30      | Maternity-Ward | 172.16.3.96/27    | SW4 + SW5             |
| 40      | Server-Room    | 172.16.3.128/28   | SW5                   |
| 50      | ICU-Emergency  | 172.16.3.160/27   | SW5                   |
| 60      | Laboratory     | 172.16.3.144/28   | SW4                   |
| 70      | Pharmacy       | 172.16.3.192/29   | SW3                   |

**VLAN 10 and VLAN 20 span 3 switches** (SW3 → SW4 → SW5) via 802.1Q trunk links ✓

### Trunk Links
- SW3 Gig0/2 ↔ SW4 Gig0/2 (trunk)
- SW4 Fa0/24 ↔ SW5 Fa0/24 (trunk)

### Inter-VLAN Routing Method
Router-on-a-stick using 802.1Q subinterfaces:

| Router   | Handles VLANs          | Connected Switch |
|----------|------------------------|-----------------|
| Chandan3 | VLAN 10, 20, 70        | SW3             |
| Chandan7 | VLAN 10, 20, 30, 60    | SW4             |
| Chandan9 | VLAN 10, 20, 30, 40, 50| SW5             |

### Switch Access Port Assignments

**SW1** (Admin LAN — untagged, no VLAN config needed):
- Fa0/1 → DNS1
- Fa0/2 → DHCP1
- Fa0/3 → PC-Admin1
- Gig0/1 → Chandan2 (uplink)

**SW2** (OPD LAN — untagged):
- Fa0/1 → WebServer1
- Fa0/2 → DHCP2
- Fa0/3 → PC-OPD1
- Gig0/1 → Chandan6 (uplink)

**SW3** (Ward — VLAN-tagged):
- Fa0/1 → PC-Ward1 (VLAN 10)
- Gig0/1 → Chandan3 (trunk uplink)
- Gig0/2 → SW4 (trunk)

**SW4** (Ward — VLAN-tagged):
- Fa0/1 → PC-Ward2 (VLAN 10)
- Gig0/1 → Chandan7 (trunk uplink)
- Gig0/2 → SW3 (trunk)
- Fa0/24 → SW5 (trunk)

**SW5** (Server Room / ICU — VLAN-tagged):
- Fa0/1 → DNS2 (VLAN 40)
- Fa0/2 → WebServer2 (VLAN 40)
- Fa0/3 → DHCP3 (VLAN 50)
- Fa0/4 → PC-ICU1 (VLAN 50)
- Gig0/1 → Chandan9 (trunk uplink)
- Fa0/24 → SW4 (trunk)


---


## 8. ROUTER CONFIGURATIONS (Key Commands)

### Interface IPs — Example: Chandan1
```
hostname Chandan1
interface GigabitEthernet0/0
 ip address 172.16.0.2 255.255.255.252
 no shutdown
interface GigabitEthernet0/1
 ip address 172.16.0.13 255.255.255.252
 no shutdown
interface Serial0/0/0
 ip address 172.16.0.5 255.255.255.252
 clock rate 64000
 no shutdown
interface Serial0/0/1
 ip address 172.16.0.9 255.255.255.252
 clock rate 64000
 no shutdown
ip route 0.0.0.0 0.0.0.0 172.16.0.1
```

### Router-on-a-Stick — Example: Chandan3
```
interface GigabitEthernet0/1
 no shutdown
interface GigabitEthernet0/1.10
 encapsulation dot1Q 10
 ip address 172.16.3.1 255.255.255.192
interface GigabitEthernet0/1.20
 encapsulation dot1Q 20
 ip address 172.16.3.65 255.255.255.224
interface GigabitEthernet0/1.70
 encapsulation dot1Q 70
 ip address 172.16.3.193 255.255.255.248
```

### OSPF Configuration — Example: Chandan1
```
router ospf 1
 router-id 1.1.1.1
 network 172.16.0.0 0.0.0.3 area 0
 network 172.16.0.4 0.0.0.3 area 1
 network 172.16.0.8 0.0.0.3 area 1
 network 172.16.0.12 0.0.0.3 area 0
 default-information originate
```

### Security Configuration (applied to all Chandan1–Chandan9)
```
enable secret class
service password-encryption
line console 0
 password cisco
 login
line vty 0 4
 password network
 login
 transport input telnet
```


---


## 9. NETWORK SERVICES

### DNS Servers

| Server   | IP Address     | Location      | Role                        |
|----------|----------------|---------------|-----------------------------|
| DNS1     | 172.16.1.3     | Admin LAN/SW1 | Primary — resolves hospital.local |
| DNS2     | 172.16.3.130   | Server Room/SW5 | Backup DNS                |
| ISP-DNS  | 203.0.113.10   | ISP Network   | External / Internet DNS     |

DNS record configured: `hospital.local → 172.16.2.3 (WebServer1)`

### DHCP Servers

| Server | IP Address   | Pool Range             | Gateway       | Serves        |
|--------|--------------|------------------------|---------------|---------------|
| DHCP1  | 172.16.1.2   | 172.16.1.20 – 119      | 172.16.1.1    | Admin LAN     |
| DHCP2  | 172.16.2.2   | 172.16.2.20 – 69       | 172.16.2.1    | OPD LAN       |
| DHCP3  | 172.16.3.162 | 172.16.3.175 – 190     | 172.16.3.161  | ICU (VLAN 50) |

DHCP relay (`ip helper-address`) configured on:
- Chandan2 G0/1 → points to DHCP1 (172.16.1.2)
- Chandan6 G0/1 → points to DHCP2 (172.16.2.2)
- Chandan9 G0/1.50 → points to DHCP3 (172.16.3.162)

### Web Servers

| Server     | IP Address   | URL                | Purpose                |
|------------|--------------|--------------------|------------------------|
| WebServer1 | 172.16.2.3   | http://hospital.local | Public Hospital Portal |
| WebServer2 | 172.16.3.131 | —                  | Hospital Information System (HIS) |


---


## 10. SECURITY CONFIGURATION

Applied to all routers **Chandan1 through Chandan9**:

| Security Feature     | Value              |
|---------------------|--------------------|
| Console password     | cisco              |
| Enable secret        | class              |
| VTY (Telnet) password| network            |
| Password encryption  | service password-encryption enabled |
| Telnet access        | line vty 0 4, transport input telnet |

Telnet test: From PC-Admin1 → `telnet 172.16.1.1` → login: `network` → enable: `class`


---


## 11. END DEVICE IP ASSIGNMENTS

| Device     | IP Address      | Subnet Mask       | Gateway         | Switch/VLAN       |
|------------|-----------------|-------------------|-----------------|-------------------|
| PC-Admin1  | 172.16.1.10     | 255.255.255.0     | 172.16.1.1      | SW1 (Admin LAN)   |
| PC-OPD1    | 172.16.2.10     | 255.255.255.128   | 172.16.2.1      | SW2 (OPD LAN)     |
| PC-Ward1   | 172.16.3.10     | 255.255.255.192   | 172.16.3.1      | SW3 (VLAN 10)     |
| PC-Ward2   | 172.16.3.11     | 255.255.255.192   | 172.16.3.2      | SW4 (VLAN 10)     |
| PC-ICU1    | 172.16.3.170    | 255.255.255.224   | 172.16.3.161    | SW5 (VLAN 50)     |
| DNS1       | 172.16.1.3      | 255.255.255.0     | 172.16.1.1      | SW1               |
| DHCP1      | 172.16.1.2      | 255.255.255.0     | 172.16.1.1      | SW1               |
| WebServer1 | 172.16.2.3      | 255.255.255.128   | 172.16.2.1      | SW2               |
| DHCP2      | 172.16.2.2      | 255.255.255.128   | 172.16.2.1      | SW2               |
| DNS2       | 172.16.3.130    | 255.255.255.240   | 172.16.3.129    | SW5 (VLAN 40)     |
| WebServer2 | 172.16.3.131    | 255.255.255.240   | 172.16.3.129    | SW5 (VLAN 40)     |
| DHCP3      | 172.16.3.162    | 255.255.255.224   | 172.16.3.161    | SW5 (VLAN 50)     |
| ISP-DNS    | 203.0.113.10    | 255.255.255.0     | 203.0.113.1     | ISP-R1            |


---


## 12. CONNECTIVITY TEST RESULTS

All tests run from PC-Admin1 (172.16.1.10):

| Test                        | Destination       | Result         | Packets Lost |
|-----------------------------|-------------------|----------------|-------------|
| Gateway reachability        | 172.16.1.1        | PASS           | 0%          |
| Cross-area (OSPF IA)        | 172.16.2.10       | PASS           | 25% (1st ARP)|
| Cross-VLAN (Ward)           | 172.16.3.10       | PASS           | 25% (1st)   |
| Cross-area to ICU           | 172.16.3.170      | PASS           | 25% (1st)   |
| To ISP (static route)       | 203.0.113.10      | PASS           | 50% (1st 2) |
| DNS resolution              | hospital.local    | PASS           | Resolved → 172.16.2.3 |

Note: First-packet loss is expected in Packet Tracer due to ARP resolution and OSPF convergence delays. After convergence, 0% loss.

OSPF verification on R1:
- Routes marked `O` = intra-area OSPF
- Routes marked `O IA` = inter-area OSPF
- Route marked `S*` = default static route to ISP


---


## 13. KEY DESIGN DECISIONS (for report discussion)

1. **Why VLSM?** The 172.16.0.0/22 block gives 1024 addresses. Different departments have vastly different sizes — Admin needs 254 hosts, Pharmacy only needs 6. VLSM prevents wastage by assigning the exact prefix needed.

2. **Why OSPF multi-area?** A single flat OSPF area would flood LSAs to every router, wasting bandwidth. Splitting into 3 areas (Area 0 backbone + 2 stub areas) contains LSA flooding within each area. Only summarized routes cross area boundaries.

3. **Why router-on-a-stick for VLANs?** Only one physical cable runs from each router to its switch, but using 802.1Q subinterfaces, multiple VLANs are carried over that one link. Each subinterface acts as a separate gateway.

4. **Why do VLAN 10 and 20 span 3 switches?** General Ward and Private Ward patients are spread across multiple floors. The same VLAN allows seamless mobility — a laptop moving from Floor 1 (SW3) to Floor 2 (SW4) or Server Room (SW5) keeps the same IP subnet.

5. **Why 3 DHCP servers?** Each major zone (Admin, OPD, ICU) has its own local DHCP server to reduce cross-network DHCP traffic. `ip helper-address` relays DHCP requests from subnets that don't have a local server.

6. **Serial vs GigabitEthernet links?** Serial links simulate WAN connections between distant building floors/wings. GigabitEthernet is used for high-speed campus backbone links (ISP-R1↔Chandan1, Chandan1↔Chandan4).


---


## 14. PROJECT STATISTICS

| Metric                     | Value      |
|---------------------------|------------|
| Total routers              | 10         |
| Transit-only routers       | 3 (Chandan4, 5, 8) |
| ABRs                       | 2 (Chandan3, Chandan8) |
| ASBR                       | 1 (Chandan1) |
| Total switches             | 5          |
| Total servers              | 8          |
| Total workstations         | 5          |
| Total devices              | 28         |
| OSPF areas                 | 3          |
| VLANs configured           | 7          |
| VLANs spanning 3 switches  | 2 (VLAN 10, 20) |
| P2P subnets (/30)          | 9          |
| LAN subnets                | 9 (+1 ISP) |
| Different prefix lengths   | 6          |
| DNS servers                | 3          |
| DHCP servers               | 3          |
| Web servers                | 2          |
| Total IP addresses in block| 1024       |
| Addresses actually used    | ~612       |

================================================================================
END OF PROJECT INFORMATION
================================================================================
