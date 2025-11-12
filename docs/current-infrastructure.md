# 💾 Current Infrastructure (As-Is State)

This document provides a detailed inventory of the homelab environment prior to the IaC migration project. This "as-is" state is defined by a monolithic architecture where a single server manages both storage and all virtualized application services.

---

## 💻 1. Hardware Inventory

The entire environment currently runs on a single physical machine.

### Server: The Monolith

| Component | Make/Model/Details | Notes |
| :--- | :--- | :--- |
| **Chassis** | [Specify Chassis Model] | E.g., Fractal Design Define R5 |
| **CPU** | [Specify CPU Model] | E.g., Intel Core i7-8700 |
| **RAM** | [Total RAM Capacity and Type] | E.g., 64GB DDR4 ECC |
| **Motherboard** | [Specify Motherboard Model] | |
| **NIC(s)** | [Specify NIC Card(s) and Speed] | E.g., Integrated 1x 1GbE |

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
| **Router/Gateway** | [Specify Router Model] | The main point of egress/ingress for `sirhexx.com` services. |
| **Switch** | [Specify Switch Model] | E.g., Unmanaged 8-Port Switch |
| **Primary Subnet** | [Specify IP Range] | E.g., `192.168.1.0/24` |
| **Server IP** | [Specify Static IP] | Primary management and service IP. |
| **DNS/DHCP** | [Specify Device/Service] | E.g., Router provides DHCP, services use 8.8.8.8. |

---

## 💻 3. Software and Services

All application services are hosted directly within the TrueNAS Scale application library (using K3s/Kubernetes under the hood).

### Operating System

* **Primary OS:** TrueNAS SCALE (Core Version: [Specify Version])
* **Virtualization:** K3s/Kubernetes managed via TrueNAS Apps GUI.

### Core Services Inventory

| Service Name | Application/Container Name | Purpose | Current Access URL |
| :--- | :--- | :--- | :--- |
| **Media Server** | **Jellyfin** | Video streaming and media management. | `jellyfin.sirhexx.com` |
| **DNS/Ad-Blocking** | [Specify Application] | E.g., Pi-hole or AdGuard Home. | `dns.sirhexx.com` |
| **Download Management** | [Specify Application] | E.g., qBittorrent, Transmission. | |
| **Monitoring** | [Specify Application] | E.g., Prometheus/Grafana stack. | |
| **VPN Access** | [Specify Application] | E.g., WireGuard or OpenVPN. | |
| **[Add Other Services]** | | | |

### Configuration Management Status

* **Configuration Source:** Manual setup via TrueNAS Web GUI.
* **Code Repository:** None for current infrastructure configuration.
* **Desired Future State:** 100% IaC managed via Terraform/Ansible.
