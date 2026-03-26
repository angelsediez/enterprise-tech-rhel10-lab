# 🚀 Phase 02 - RHEL 10.1 Guest Deployment

## 🎯 Objective
Deploy the first RHEL 10.1 guest virtual machine on the Fedora 43 virtualization host and establish the installation pattern that will later be reused for the remaining lab nodes.

This phase focuses on guest creation, installation, first boot validation, and host-side verification.

---

## 🔍 Scope

### **Included in this phase:**
* Preparing the guest installation workflow.
* Using the stable RHEL 10.1 ISO path on the host.
* Creating the first guest VM (`srv-admin`).
* Utilizing the existing libvirt storage pool and internal lab network.
* Completing the base RHEL 10.1 installation.
* Validating the guest from both host and guest perspectives.
* Documenting screenshots and inventory data.

### **Excluded (Later Phases):**
* Advanced guest configuration (User policy, SSH hardening).
* Package workflows and application deployment.
* SELinux tuning and Firewalld rules.
* NFS/autofs setup.

---

## 💻 Host Context
The deployment is performed on the following environment:

| Component | Specification |
| :--- | :--- |
| **Host OS** | Fedora Linux 43 (KDE Plasma Desktop Edition) |
| **Hypervisor Stack** | KVM + QEMU + libvirt + virt-manager |
| **Libvirt Connection** | `qemu:///system` |
| **Storage Pool** | `enterprise-tech-images` |
| **Internal Lab Network** | `lab-int` |
| **Guest Target** | Red Hat Enterprise Linux 10.1 |
| **ISO Path** | `/var/lib/libvirt/boot/rhel-10.1-x86_64-dvd.iso` |

---

## 🛠️ Guest Deployment Strategy
This phase uses `srv-admin` as the reference model. The workflow follows this sequence:

1.  **Install** `srv-admin` using the standard runbook.
2.  **Validate** that the VM is healthy and reachable.
3.  **Document** the workflow to ensure reproducibility.
4.  **Reuse** the validated pattern for `srv-web`, `srv-db`, and `srv-storage` as each guest is deployed.

---

## 📐 Guest Design Decisions

### **Core Configuration**
* **Initial Guest:** `srv-admin`
* **Firmware Model:** UEFI / OVMF
* **Network Model:** `lab-int` (Internal libvirt network)
* **Storage Model:** `enterprise-tech-images` (Pool-based storage)

### **Installation Methodology**
* **Method:** `virt-install` via terminal on Fedora 43.
* **Flow:** Graphical install flow completed through the VM console.
* **Focus:** Clean base install with a reproducible VM definition.

---

## ✅ Work Completed
* Confirmed host-side ISO stability and `rhel10.1` availability in `osinfo`.
* Validated storage pool (`enterprise-tech-images`) and network (`lab-int`).
* Created `srv-admin.qcow2` guest disk.
* Launched and completed the RHEL 10.1 installation for `srv-admin`.
* Configured hostname and guest identity during installation.
* Created initial admin user (`jdoe`) and enabled root account.
* Performed multi-point validation (Internal guest checks & Host-side `virsh` checks).
* Enabled VM **autostart** for `srv-admin`.
* Repeated the validated deployment pattern for `srv-web`.
* Launched and completed the RHEL 10.1 installation for `srv-web`.
* Validated `srv-web` from both guest-side and host-side.
* Enabled VM **autostart** for `srv-web`.
* Repeated the validated deployment pattern for `srv-db`.
* Launched and completed the RHEL 10.1 installation for `srv-db`.
* Validated `srv-db` from both guest-side and host-side.
* Enabled VM **autostart** for `srv-db`.

---

## 📑 Guest Inventory Status

| Guest | Planned Role | Status |
| :--- | :--- | :--- |
| `srv-admin` | Administration and management node | ✅ Installed and Validated |
| `srv-web` | Web service node | ✅ Installed and Validated |
| `srv-db` | Database service node | ✅ Installed and Validated |
| `srv-storage` | Shared storage and support node | ⚪ Pending |

---

## 🧪 Validation Results
The following milestones were successfully verified:
* **ISO/OS Info:** ISO reachable and `rhel10.1` recognized.
* **VM Presence:** Guest exists in libvirt and boots successfully.
* **Connectivity:** Attached to `lab-int` with DHCP active.
* **Identity:** Guest hostnames were correctly set during installation and validated after first boot.
* **Stability:** Host-side validation confirms active interface and IP.
* **Persistence:** Autostart enabled and confirmed.
* **Pattern Reuse:** `srv-web` now follows the same validated deployment pattern as `srv-admin`.
* **Second Guest Validation:** `srv-web` was validated from both guest-side and host-side.
* **Second Guest Persistence:** Autostart enabled and confirmed for `srv-web`.
* **Third Guest Reuse:** `srv-db` now follows the same validated deployment pattern used for `srv-admin` and `srv-web`.
* **Third Guest Validation:** `srv-db` was validated from both guest-side and host-side.
* **Third Guest Persistence:** Autostart enabled and confirmed for `srv-db`.

---

## 📸 Screenshots
Captured evidence is stored in `assets/screenshots/phase-02/`:

**srv-admin Core Evidence:**
* `P02-01-iso-pool-network-ready.png`
* `P02-02-srv-admin-volume-created.png`
* `P02-03-virt-install-srv-admin.png`
* `P02-04-anaconda-installation-summary-srv-admin.png`
* `P02-05-anaconda-installation-destination-srv-admin.png`
* `P02-06-anaconda-network-hostname-srv-admin.png`
* `P02-08-srv-admin-host-side-validation.png`

**srv-admin Additional Detail:**
* `P02-04b-anaconda-software-selection-srv-admin.png`
* `P02-07a-srv-admin-os-and-hostname-validation.png`
* `P02-07b-srv-admin-network-target-storage-validation.png`
* `P02-06b-anaconda-root-account-srv-admin.png`

**srv-web Core Evidence:**
* `P02-09-virt-install-srv-web.png`
* `P02-11-anaconda-network-hostname-srv-web.png`
* `P02-14-srv-web-first-boot-validation.png`
* `P02-15-srv-web-host-side-validation.png`

**srv-web Additional Detail:**
* `P02-10-anaconda-installation-destination-srv-web.png`
* `P02-12-anaconda-installation-summary-srv-web.png`
* `P02-13-installation-complete-srv-web.png`

**srv-db Core Evidence:**
* `P02-17-anaconda-installation-destination-srv-db.png`
* `P02-18-anaconda-network-hostname-srv-db.png`
* `P02-19-anaconda-installation-summary-srv-db.png`
* `P02-20-installation-complete-srv-db.png`
* `P02-21-srv-db-first-boot-validation.png`
* `P02-22-srv-db-host-side-validation.png`

**srv-db Additional Detail:**
* `P02-19b-anaconda-software-selection-srv-db.png`
* `P02-19c-anaconda-root-account-srv-db.png`
* `P02-19d-anaconda-user-creation-srv-db.png`
* `P02-22b-srv-db-autostart-and-dominfo.png`

---

## 📂 Related Files
* `runbooks/rhel10-install.md`
* `notes/guest-inventory.md`
* `phases/01-virtualization-host/README.md`
* `phases/01-virtualization-host/lab-int.xml`

---

## 🏁 Outcome
Phase 02 has now produced three working RHEL 10.1 guests (`srv-admin`, `srv-web`, and `srv-db`). The lab now has a validated installation workflow and a solid deployment pattern for the remaining node.
