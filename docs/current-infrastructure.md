# 💾 Current Infrastructure (As-Is State)

This document provides a detailed inventory of the homelab environment prior to the IaC migration project. This "as-is" state is defined by a monolithic architecture where a single server manages both storage and all virtualized application services.

---

## 💻 1. Hardware Inventory

The entire environment currently runs on a single physical machine.

### Server: The Monolith

| Component | Make/Model/Details | Notes |
| :--- | :--- | :--- |
| **Chassis** | Dell R710 | Dell Poweredge R710 |
| **CPU** | Intel X5650 | Intel(R) Xeon(R) CPU X5650 @2.67GHz |
| **RAM** | 94Gi DDR3 | 94Gi DDR3 |
| **Motherboard** | Dell 0YDJK3 | Dell 0YDJK3 Ver. A02 |
| **NIC(s)** | Broadcom NetXtreme II BCM5709  | 4x Gigabit Ethernet Cards: eno1, eno2, eno3, eno4 

### Storage Configuration (ZFS)

| Component | Quantity | Capacity (per drive) | Total Pool Capacity | Pool Name | Role |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OS Drive** | 1 | [Specify Capacity] | N/A | Boot-Pool | TrueNAS Scale OS |
| **Data Drives** | [Number of Drives] | [Capacity per Drive] | [Total Raw/Usable Capacity] | Data-Pool | Application Data, Media Storage |
| **Cache/Log** | [Specify Drive Type/Quantity] | [Specify Capacity] | N/A | N/A | If using L2ARC/SLOG |

---

## 🌐 2. Network Configuration

The current setup utilizes a flat network without VLAN segmentation, relying on the primary server for service access.

| Component | Make/Model | Notes |
| :--- | :--- | :--- |
| **Router/Gateway** | Netgear RS400 | The main point of egress/ingress for `sirhexx.com` services |
| **Primary Switch** | TP-Link T1600G-28PS | 24-Port Gigabit Smart PoE+ Switch with 4 SFP Slots |
| **Secondary Switches** | TP-Link TL-SG1005D | 5-Port Gigabit Desktop Switch |
| **Primary Subnet** | `192.168.1.1/16` |  |
| **Server IP** | `192.168.1.5` | Primary management and service IP. |
| **DNS/DHCP** | Provided Through Gateway  | Router provides DHCP and DNS using 1.1.1.1 |

---

## 💻 3. Software and Services

All application services are hosted directly within the TrueNAS Scale application library (using K3s/Kubernetes under the hood).

### Operating System

* **Primary OS:** TrueNAS SCALE (Core Version: TrueNAS-24.10.2.3)
* **Virtualization:** K3s/Kubernetes managed via TrueNAS Apps GUI.

### Core Services Inventory

| Service Name | Application/Container Name | Purpose | Local IP Address | Current Access URL |
| :--- | :--- | :--- | :--- |
| **Media Server** | **Jellyfin** | Video streaming and media management. | `http://192.168.1.5:30013`  | `https://watch.sirhexx.com` |
| **DNS/Ad-Blocking** | [Specify Application] | E.g., Pi-hole or AdGuard Home. | `dns.sirhexx.com` |
| **Download Management** | [Specify Application] | E.g., qBittorrent, Transmission. | |
| **Monitoring** | [Specify Application] | E.g., Prometheus/Grafana stack. | |
| **VPN Access** | [Specify Application] | E.g., WireGuard or OpenVPN. | |
| **[Add Other Services]** | | | |

### Configuration Management Status

* **Configuration Source:** Manual setup via TrueNAS Web GUI.
* **Code Repository:** None for current infrastructure configuration.
* **Desired Future State:** 100% IaC managed via Terraform/Ansible.
