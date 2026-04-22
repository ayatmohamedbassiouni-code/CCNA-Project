# Cisco Packet Tracer Network Project 🌐

A comprehensive enterprise network simulation built in Cisco Packet Tracer, covering multi-area routing, switching, VLANs, redundancy, security, and NAT configurations.

---

## Network Topology Overview

The topology is divided into multiple interconnected segments including a WAN core, a multilayer switched LAN, a DHCP/routing zone, and a secure access layer — all simulated using routers, multilayer switches, and access switches.

---

## Devices Used

| Device     | Model            | Role                                      |
|------------|------------------|-------------------------------------------|
| R1         | Router           | Core WAN router                           |
| R2         | Router           | DHCP server router (VLAN 100 & VLAN 400)  |
| R3 / PAT   | Router           | PAT (NAT Overload) gateway                |
| DSW1       | 3560 Multilayer  | PVST VLAN 100 Root / VTP Server           |
| DSW2       | 3560 Multilayer  | PVST VLAN 200 Root / VTP Client           |
| MLS5       | 3560 Multilayer  | Inter-VLAN Routing                        |
| ASW3       | 2960 Switch      | VTP Client / BPDUGuard + PortFast         |
| ASW4       | 2960 Switch      | VTP Client                                |
| Switch3    | 2960-24TT        | Access layer switch                       |
| SW6        | 2960 Switch      | SSH management / Port Security            |
| SW7        | 2960 Switch      | Access layer (VLAN 500)                   |
| SW8        | 2960 Switch      | Access layer (192.168.70.0/24)            |

---

## WAN Links

| Link              | Subnet         | Connected Devices  |
|-------------------|----------------|--------------------|
| R1 ↔ DSW1         | 10.10.10.0/30  | Gig0/0 — Gig0/1    |
| R1 ↔ R2           | 20.20.20.0/30  | Se0/0/1 — Se0/0/0  |
| R1 ↔ R2           | 30.30.30.0/30  | Secondary WAN link |
| R2 ↔ R3 (PAT)     | 40.40.40.0/30  | Se0/1/0            |
| R2 ↔ MLS5         | 50.50.50.0/30  | Gig0/1 — Gig0/0    |

---

## VLANs Configured

| VLAN | Subnet              | Description                   |
|------|---------------------|-------------------------------|
| 100  | 192.168.100.0/24    | PVST Root: DSW1               |
| 200  | 192.168.200.0/24    | PVST Root: DSW2               |
| 300  | 192.168.30.0/24     | Routed via MLS5               |
| 400  | 192.168.40.0/24     | DHCP from R2 / Port Security  |
| 500  | 192.168.50.0/24     | SW6 & SW7 access layer        |
| 600  | 192.168.60.0/24     | DHCP Snooping / DAI zone      |
| —    | 192.168.70.0/24     | SW8 access segment (PAT side) |

---

## Features & Technologies Implemented

### Switching
- **VTP (VLAN Trunking Protocol)** — DSW1 as VTP Server; DSW2, ASW3, ASW4 as VTP Clients
- **PVST (Per-VLAN Spanning Tree)** — DSW1 is root for VLAN 100; DSW2 is root for VLAN 200
- **BPDUGuard + PortFast** — Configured on ASW3 access ports
- **Inter-VLAN Routing** — Configured on MLS5 (Layer 3 switching)

### Routing & WAN
- **Static / Dynamic Routing** — Between R1, R2, R3 over serial WAN links
- **PAT (NAT Overload)** — Configured on R3 (PAT router) on Se0/0/1 toward the internet

### DHCP
- **DHCP for VLAN 100** — Served from R2
- **DHCP for VLAN 400** — Served from R2
- **DHCP Snooping** — Enabled on SW6 segment

### Security
- **Port Security — Restrict** mode on SW6 (VLAN 500 / host2)
- **Port Security — Protect** mode on SW6 (VLAN 600 / PC1 & Server1)
- **Port Security — Shutdown** mode on Switch3 (VLAN 400 segment)
- **DAI (Dynamic ARP Inspection)** — Enabled on VLAN 600 segment
- **SSH Remote Management** — Configured on SW6

---

## Tools Used

- Cisco Packet Tracer

---

## How to Open

1. Download and install [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer)
2. Clone this repository or download the `.pkt` file
3. Open `Projectttcs46.pkt` in Packet Tracer
4. Explore the topology and verify configurations via CLI on each device

---

## License

This project is open-source and available under the [MIT License](LICENSE).
