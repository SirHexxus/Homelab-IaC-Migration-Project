# ⚙️ Homelab-IaC-Migration-Project

## Project Overview

This repository documents and implements the migration of a personal homelab environment, moving from a consolidated, single-server setup (**TrueNAS Scale** only) to a more robust, decoupled, and highly available architecture featuring dedicated virtualization (**Proxmox VE**) and storage (**TrueNAS Scale**) servers.

The primary objective is to modernize the homelab by implementing **Infrastructure as Code (IaC)** principles, leveraging tools like **Terraform**, **Ansible**, and custom scripting to automate the provisioning, configuration, and deployment of virtual machines, containers, and applications. This project serves as a comprehensive demonstration of **DevOps** and **Security** best practices in a real-world infrastructure scenario, aimed at building a professional IT portfolio.

* **Project Lead:** James Stacy (@SirHexxus)
* **Domain:** sirhexx.com
* **Professional Entity:** Hexxus Web Solutions

## 🚀 Goals & Deliverables

This project is guided by the following core principles and expected deliverables:

| Category | Goal | Deliverable |
| :--- | :--- | :--- |
| **Architecture** | Decouple virtualization/compute from storage. | Dedicated **Proxmox VE** server for VMs/LXC, dedicated **TrueNAS Scale** server for ZFS storage/file shares. |
| **Automation** | Implement IaC for all core infrastructure components. | **Terraform** code for Proxmox provisioning (VMs, networks), **Ansible** playbooks for configuration management. |
| **Security** | Enforce network segmentation and least-privilege access. | Detailed network diagrams, firewall rules, and defined user/service accounts. |
| **Documentation** | Create comprehensive, professional documentation. | Functional guides (`docs/functional-docs`), project scope (`docs/project-scope.md`), and blog-post-style write-ups. |
| **Career** | Showcase advanced IT skills for career advancement. | A public, well-documented GitHub repository demonstrating System Administration and DevOps competencies. |

## 🛠️ Technology Stack (IaC Focus)

| Technology | Purpose |
| :--- | :--- |
| **Proxmox VE** | Hypervisor for hosting all VMs and LXC Containers. |
| **TrueNAS Scale** | Dedicated storage server, managing ZFS pools and network shares. |
| **Terraform** | Infrastructure provisioning (e.g., creating VMs, subnets, firewall rules). |
| **Ansible** | Configuration Management (e.g., user creation, software installation, app deployment). |
| **Bash/Python** | Custom scripting for orchestration and automation tasks. |
| **Docker/Kubernetes** | Containerization for deploying modern, resilient applications. |
| **GitHub** | Version Control and CI/CD integration. |

---

## 🗺️ Repository Structure

The following directory structure is used to organize the documentation, source code, and assets for this project.
```markdown
.
├── docs/                 # All project documentation and design artifacts
│   ├── current-infrastructure.md  # Detailed breakdown of the 'before' state
│   ├── functional-docs/  # User-focused setup guides and configuration notes
│   ├── iac-strategy.md   # Deep dive into Terraform/Ansible/Scripting implementation
│   └── project-scope.md  # Detailed definition of project boundaries and sub-projects
├── src/                  # Source code for IaC and automation
│   ├── ansible/          # Ansible playbooks, roles, and inventory
│   ├── scripts/          # Custom Bash or Python automation scripts
│   └── terraform/        # Terraform configurations for infrastructure provisioning
├── LICENSE               # Apache 2.0 License file
└── README.md             # This file
```

---

## ⚖️ License

This project is licensed under the **Apache License 2.0**. See the [LICENSE](LICENSE) file for details.
