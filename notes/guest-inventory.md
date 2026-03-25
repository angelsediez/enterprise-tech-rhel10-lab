# 📊 Guest Inventory - RHEL 10 Lab

## 🎯 Purpose
This file tracks the guest virtual machines used in the **EnterpriseTech RHEL 10 lab**. It provides a quick operational overview of resource allocation, status, and validation across the infrastructure.

---

## 💻 Host Context
The following environment settings apply to the virtualization host where these guests reside:

| Component | Specification |
| :--- | :--- |
| **Host Platform** | Fedora Linux 43 (KDE Plasma Desktop Edition) |
| **Hypervisor Stack** | KVM + QEMU + libvirt + virt-manager |
| **Libvirt Connection** | `qemu:///system` |
| **Storage Pool** | `enterprise-tech-images` |
| **Internal Network** | `lab-int` |
| **Guest OS Target** | Red Hat Enterprise Linux 10.1 |
| **ISO Path** | `/var/lib/libvirt/boot/rhel-10.1-x86_64-dvd.iso` |

---

## 📑 Guest Inventory Table

| Guest | Role | vCPU | RAM | Disk | Firmware | Status | Validation | Screenshots |
| :--- | :--- | :---: | :---: | :---: | :---: | :--- | :--- | :--- |
| `srv-admin` | Administration and management node | 2 | 4096 | 60G qcow2 | UEFI / OVMF | ⚪ Pending | ⚪ Pending | ⚪ Pending |
| `srv-web` | Web service node | 2 | 4096 | 60G qcow2 | UEFI / OVMF | ⚪ Pending | ⚪ Pending | ⚪ Pending |
| `srv-db` | Database service node | 2 | 4096 | 60G qcow2 | UEFI / OVMF | ⚪ Pending | ⚪ Pending | ⚪ Pending |
| `srv-storage` | Shared storage and NFS/autofs support node | 2 | 4096 | 60G qcow2 | UEFI / OVMF | ⚪ Pending | ⚪ Pending | ⚪ Pending |

> [!NOTE]
> All disks are stored in the `enterprise-tech-images` pool. 

---

## 🚦 Status Definitions

### Install Status
* `Pending`: Resource planned but not yet created.
* `In progress`: Currently being installed or configured.
* `Installed`: OS installation completed successfully.
* `Rebuild required`: Existing guest needs to be destroyed and re-deployed.

### Validation Status
* `Pending`: No validation performed yet.
* `Partially validated`: Basic connectivity or services confirmed.
* `Validated`: Fully operational according to runbook specs.
* `Validation failed`: Issues found during post-install checks.

---

## 📓 Per-Guest Notes

### 🛠️ `srv-admin`
* Reference installation model for the entire lab.
* **Current Focus:** Phase 02 deployment.
* *Requirement:* Must be 100% validated before proceeding with other nodes to ensure the deployment pattern is solid.

### 🌐 `srv-web`
* Intended for hosting web services in later phases.
* Will replicate the `srv-admin` base configuration.

### 🗄️ `srv-db`
* Target for database engines and data persistence exercises.
* Initial deployment remains a standard minimal/server install.

### 💾 `srv-storage`
* Core node for NFS, shared volumes, and `autofs` workflows.
* *Scalability:* May require secondary virtual disks in future phases.

---

## 🔄 Tracking & Maintenance
Update this file whenever one of the following events occurs:
1.  A guest is defined or created in `libvirt`.
2.  Hardware resources (RAM/vCPU/Disk) are modified.
3.  Installation or validation phases are completed.
4.  Screenshots are captured and stored in the assets folder.

---

## 🚩 Current Phase Alignment
* **Phase 00:** Repository Bootstrap ✅
* **Phase 01:** Virtualization Host Ready ✅
* **Phase 02:** First Guest Deployment 🚧

**Priority Guest:** `srv-admin`
Remaining guests remain in `Pending` state until the first installation pattern is successfully validated.
