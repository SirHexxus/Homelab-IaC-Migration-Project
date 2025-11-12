# ⚙️ Proxmox VE Setup Guide (Compute Server)

This guide documents the manual steps required to install and initially configure the Proxmox Virtual Environment (PVE) compute server. These steps establish the **baseline foundation** before the Infrastructure as Code (IaC) process takes over.

---

## 1. 💾 Installation and Initial OS Setup

### 1.1. Prepare Installation Media
* Download the latest Proxmox VE ISO image from the official website.
* Use a tool (e.g., Ventoy, Rufus, balenaEtcher) to create a bootable USB drive.

### 1.2. Execute Installation
* Boot the new compute server from the USB drive.
* Select the graphical install option.
* **Disk Configuration:** Dedicate the entire OS drive (or volume) to the PVE installation.
* **Network Configuration:** Assign a static IP address for the **Management VLAN/Subnet** as defined in `docs/functional-docs/network-diagrams/ip-scheme.csv`.
    * **IP Address:** [Placeholder for Management IP]
    * **Hostname:** `pve01.sirhexx.com` (or similar)
* Complete the installation and reboot the server.

---

## 2. 🔑 Post-Installation OS Hardening

These steps ensure the server is secure and ready for remote management via SSH.

### 2.1. Update and Upgrade
Execute the following commands via SSH or console:
```bash
# Update package lists and upgrade existing packages
apt update && apt full-upgrade -y
```

### 2.2. Configure SSH Access
* **Disable Root SSH Login (Optional but Recommended):** Create a standard admin user and use `sudo` instead of logging in directly as root.
* **Install Public Key:** Ensure your personal SSH public key is added to the authorized keys for the primary administrative user for secure, password-less login.

---

## 3. 🌐 Network and Storage Configuration Baseline

This section prepares Proxmox to interact with your physical network and the TrueNAS storage server.

### 3.1. Configure Network Bridges
* Define the Linux bridges (`vmbrX`) within the Proxmox UI or `/etc/network/interfaces` to map to your physical NICs and intended VLANs (as defined in the IaC Strategy).
* **Required Bridge:** Create the primary bridge for the Management Network.
* **VLAN Tagging:** If using an 802.1Q capable switch, configure the appropriate VLAN tags on the Proxmox side.

### 3.2. Add TrueNAS Storage
* **Storage Type:** Select **NFS** or **SMB** based on the shares exported from TrueNAS Scale.
* **Add Share:** Use the Proxmox Web GUI to add the storage location.
    * **ID:** `truenas-data` (or similar)
    * **Server:** [TrueNAS Management IP]
    * **Share Path:** [/mnt/Data-Pool/projections/VMs]
    * **Content:** Select **Disk image** and **Container template**.

---

## 4. ☁️ IaC Enablement: Cloud-Init and API

These are the final steps that bridge the manual setup with the automated IaC process.

### 4.1. Create a Cloud-Init Template
* **Download OS Image:** Download a basic Cloud-Init compatible OS image (e.g., Ubuntu 22.04 LTS `cloudimg`) and import it into Proxmox.
* **Create Template VM:** Convert the imported image into a VM, configure basic hardware settings (RAM, CPU), and mark it as a **Template**.
    * *This template will be cloned by Terraform.*

### 4.2. Generate Proxmox API Token
* **Purpose:** The Terraform provider requires an API token to communicate with and provision resources on Proxmox.
* **Steps:**
    1.  Create a dedicated **user** (e.g., `terraform-user`).
    2.  Create an **API Token** for that user.
* **Security Note:** The generated token (Key ID and Secret) **must** be securely stored (e.g., encrypted via Ansible Vault) and used only by Terraform.

---

## 5. ➡️ Next Step

The Proxmox server is now ready for Sub-Project 2: Core Infrastructure Provisioning. The next step is to write the Terraform code (`src/terraform/`) using the generated API token to provision the first resources.
