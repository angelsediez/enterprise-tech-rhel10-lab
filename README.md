<div align="center">

# 🖥️ EnterpriseTech RHEL 10 Lab

### A production-style Red Hat Enterprise Linux 10.1 homelab built with KVM, QEMU, and libvirt

![Platform](https://img.shields.io/badge/Platform-RHEL%2010.1-red)
![Host](https://img.shields.io/badge/Host-Fedora%2043-blue)
![Virtualization](https://img.shields.io/badge/Virtualization-KVM%20%2B%20QEMU%20%2B%20libvirt-6f42c1)
![Status](https://img.shields.io/badge/Status-In%20Progress-brightgreen)
![Docs](https://img.shields.io/badge/Documentation-Phase--based-orange)

</div>

---

## 📌 Overview
This repository documents a **multi-VM Red Hat Enterprise Linux 10.1 homelab** designed to simulate a compact enterprise environment. It explores real-world Linux systems administration in a structured, repeatable, and well-documented way.

The lab is organized into **execution phases**, supported by professional runbooks, validation checklists, and technical evidence.

---

## 🏗️ Lab Nodes
The infrastructure consists of four core virtual machines:

| Hostname | Role |
| :--- | :--- |
| `srv-admin` | Administration and management node |
| `srv-web` | Web service node |
| `srv-db` | Database service node |
| `srv-storage` | Shared storage and NFS/autofs support node |

---

## 🎯 What This Lab Covers
This homelab focuses on practical, production-ready workflows:
* 🖥️ **Provisioning:** Baseline configuration and reproducible deployments.
* 📦 **Software:** Package management and internal repository usage.
* 👤 **Identity:** SSH hardening, permissions, and user lifecycle.
* 💾 **Storage:** Filesystems, LVM, and mount persistence.
* ⚙️ **Systemd:** Service management and boot behavior.
* 🌐 **Networking:** Hostname resolution and Firewalld policy.
* 🔐 **Security:** SELinux-aware administration.
* 📝 **Ops:** Logging, scheduling, and operational validation.
* 🧰 **Recovery:** Reproducible troubleshooting workflows.

---

## 🧱 Environment Context

| Item | Value |
| :--- | :--- |
| **Guest Platform** | Red Hat Enterprise Linux 10.1 (`rhel10.1`) |
| **Host Platform** | Fedora Linux 43 (KDE Plasma Desktop Edition) |
| **Virtualization** | KVM + QEMU + libvirt + virt-manager |
| **Lab Style** | Multi-VM local enterprise simulation |
| **ISO Path** | `/var/lib/libvirt/boot/rhel-10.1-x86_64-dvd.iso` |

---

## 🗺️ Project Structure

```text
enterprise-tech-rhel10-lab/
├── README.md               # Main landing page
├── assets/                 # Images, diagrams, and screenshots
├── docs/                   # General design and architecture
├── notes/                  # Host notes and technical references
├── phases/                 # Execution documentation by phase
├── runbooks/               # Step-by-step operational procedures
├── scripts/                # Helper scripts for validation
├── troubleshooting/        # Failure logs and recovery workflows
└── validation/             # Verification steps and checklists
```

### 📚 Repository Layout
* **docs/** — General design and lab-level documentation.
* **phases/** — Execution and documentation grouped by phase.
* **runbooks/** — Step-by-step operational procedures.
* **validation/** — Checks and verification steps.
* **troubleshooting/** — Failures, root causes, and recovery.
* **assets/** — Images, diagrams, and screenshots.

---

## 🚀 Progress by Phase

- [x] **Phase 00** — Bootstrap and repository setup ✅
- [x] **Phase 01** — Virtualization host preparation ✅
- [x] **Phase 02** — First RHEL 10.1 guest deployment ✅
- [ ] **Phase 03** — Shell, files, and local documentation ⚪
- [ ] **Phase 04** — Identity, SSH, and permissions ⚪
- [ ] **Phase 05** — Software and scripting ⚪
- [ ] **Phase 06** — Running systems and service management ⚪
- [ ] **Phase 07** — Local storage and filesystems ⚪
- [ ] **Phase 08** — Networking and firewall ⚪
- [ ] **Phase 09** — NFS and autofs ⚪
- [ ] **Phase 10** — SELinux and troubleshooting ⚪
- [ ] **Phase 11** — Final integrated validation ⚪

---

## 🖼️ Snapshot Gallery

### 🖥️ Host Setup (Phase 01)
**Fedora 43 host identity**
![Host Identity](https://github.com/angelsediez/enterprise-tech-rhel10-lab/raw/main/assets/screenshots/phase-01/P01-01-fedora43-host-release.png)

**KVM capability confirmed**
![KVM Capability](https://github.com/angelsediez/enterprise-tech-rhel10-lab/raw/main/assets/screenshots/phase-01/P01-02-kvm-capability-and-dev-kvm.png)

### 🚀 Guest Deployment (Phase 02)
**RHEL 10.1 installation workflow**
![Installation Workflow](https://github.com/angelsediez/enterprise-tech-rhel10-lab/raw/main/assets/screenshots/phase-02/P02-04-anaconda-installation-summary-srv-admin.png)

**First guest validated**
![Guest Validated](https://github.com/angelsediez/enterprise-tech-rhel10-lab/raw/main/assets/screenshots/phase-02/P02-07a-srv-admin-os-and-hostname-validation.png)

---

## ✅ Current Status

> [!IMPORTANT]
> **Status:** In Progress  
> **Completed Phases:** 00, 01, 02  
> **Validated Guest:** `srv-admin`  
> **Next Milestone:** Phase 03 — Shell, files, and local documentation

---

## 🧠 Design Philosophy
This project is built as a hands-on Linux systems lab emphasizing:
* **Repeatability:** Workflows must be easy to replicate.
* **Operational Clarity:** Clear separation between host and guest tasks.
* **Clean Documentation:** Validation-first approach with visual evidence.
* **Realistic Workflows:** Mimicking small, structured enterprise environments.

---

## 🔗 Key Files
* `runbooks/rhel10-install.md` — Main guest installation guide.
* `notes/guest-inventory.md` — Current state of all lab VMs.
* `phases/02-rhel10-install/README.md` — Detailed Phase 02 report.
* `docs/architecture.md` — High-level lab design.

---

## 👤 Author
**Angel Diez**
