# 🗺️ Project Scope Definition: Homelab IaC Migration

This document defines the scope of the "Homelab-IaC-Migration-Project." It establishes the project boundaries, identifies key deliverables, and structures the overall effort into manageable phases (Sub-Projects).

## 🎯 Master Project Goal

To transition the current monolithic homelab (single TrueNAS Scale server hosting all services) to a modern, decoupled architecture featuring dedicated Compute (Proxmox VE) and Storage (TrueNAS Scale) servers, with all infrastructure and application deployment managed via **Infrastructure as Code (IaC)**.

## ✅ Master Project Acceptance Criteria (The "Done" State)

The project will be considered successful and complete when the following conditions are met:

1.  **Infrastructure Decoupled:** Proxmox VE is fully operational on the dedicated compute server, and TrueNAS Scale is configured solely for storage on the original server.
2.  **Core Services Migrated:** All essential current applications (e.g., **Jellyfin**, DNS, monitoring) are redeployed successfully on the new Proxmox platform (as VMs or containers).
3.  **IaC Maturity Achieved:** The entire process—from provisioning a new VM/Container to deploying an application—can be executed reliably and repeatedly using the **Terraform** and **Ansible** source code in the `src/` directory.
4.  **Documentation Complete:** All sections of the `docs/` folder, including functional guides and the IaC strategy, are fully populated and accurate.

---

## 🏗️ Project Breakdown: Sub-Projects

The master project is divided into four distinct and sequential Sub-Projects. Each sub-project has its own focused scope, specific deliverables, and defined completion criteria.

### Sub-Project 1: Infrastructure Design & Documentation (The Blueprint)

* **Scope:** Define the "Future State" architecture, establish the IP addressing scheme, and document the "Current State" infrastructure. This sub-project focuses purely on planning and documentation.
* **Key Deliverables:**
    * **`docs/current-infrastructure.md`**: Complete inventory of current hardware, networking, and software.
    * **`docs/functional-docs/network-diagrams/ip-scheme.csv`**: Defined IP schema for new VLANs and services (e.g., Management, Servers, IoT).
    * **`docs/iac-strategy.md`**: High-level design document for using Terraform, Ansible, and scripting together.
* **Acceptance Criteria:** All initial documentation files are created, reviewed, and finalized.

### Sub-Project 2: Core Infrastructure Provisioning (The Foundation)

* **Scope:** Set up the physical and virtual networking layers, install Proxmox VE and TrueNAS Scale, and establish the IaC baseline needed for provisioning.
* **Key Deliverables:**
    * **New Server Setup:** Proxmox VE installed, configured for remote management, and integrated with GitHub (for version control).
    * **TrueNAS Setup:** TrueNAS Scale reset to a storage-only role, ZFS pools configured, and necessary network shares created (NFS/SMB).
    * **Terraform Initial Code:** Working Terraform files (`src/terraform/`) to provision a basic test VM and/or LXC container on Proxmox.
* **Acceptance Criteria:** A "Hello World" VM can be provisioned and destroyed solely using the Terraform code. TrueNAS shares are accessible from the Proxmox environment.

### Sub-Project 3: Configuration Management & Application Deployment (The Automation)

* **Scope:** Develop the Ansible playbooks and roles required to configure the operating systems within the provisioned VMs/Containers and deploy core applications.
* **Key Deliverables:**
    * **Ansible Playbooks:** Complete Ansible inventory and playbooks (`src/ansible/`) for post-OS installation tasks (user accounts, SSH keys, network configs).
    * **Application Deployment Playbooks:** Playbooks to deploy one or two critical, complex services (e.g., the new container stack for **Jellyfin**/Arr apps).
    * **Automation Scripts:** Python/Bash scripts (`src/scripts/`) for orchestration (e.g., running Terraform then Ansible in sequence).
* **Acceptance Criteria:** A newly provisioned VM can be automatically configured and have a sample application deployed to it by executing a single script or Ansible playbook.

### Sub-Project 4: Migration, Review, and Portfolio Generation (The Polish)

* **Scope:** The actual cutover of services, final system hardening, and creation of the public-facing portfolio assets.
* **Key Deliverables:**
    * **Service Cutover:** All essential legacy services are fully disabled on the old TrueNAS setup and running stably on the new Proxmox setup.
    * **Security Hardening:** Implementation of final firewall rules, network segmentation, and system-level security best practices.
    * **Blog Posts/Documentation:** The functional guides are polished, and the blog post series is written (documenting the journey for the portfolio).
* **Acceptance Criteria:** The old infrastructure is powered down (or re-purposed), the new services are stable for one week, and the public-facing documentation/blog series is ready for publication.

---

## 🚫 Out of Scope

The following items are explicitly **excluded** from the scope of this Master Project:

* Physical relocation or cabling beyond connecting the two core servers and necessary switches.
* Migration of non-essential, legacy applications that are no longer required.
* Any non-IaC-managed configuration (i.e., manual GUI changes to Proxmox or TrueNAS will be re-coded into Terraform/Ansible).
* Deep-dive configuration of Kubernetes (K3s/K8s) if used; the scope only covers the provisioning of the underlying cluster nodes via IaC.
