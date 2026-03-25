# RHEL 10.1 Guest Installation Runbook

## 🎯 Objective
Deploy the first RHEL 10.1 guest VM (`srv-admin`) on the Fedora 43 virtualization host using the existing libvirt storage pool, internal lab network, and stable ISO path.

This runbook documents the repeatable installation workflow that will later be reused for:
* `srv-web`
* `srv-db`
* `srv-storage`

---

## 🔍 Scope
**Included in this runbook:**
* Host-side preflight checks & ISO validation.
* Storage pool and network validation.
* Guest disk creation & `virt-install` execution.
* Base RHEL 10.1 installation flow & first boot validation.
* Host-side validation with `virsh`.

**Excluded (covered in later phases):**
* Advanced post-install configuration & SSH hardening.
* User policy & SELinux tuning.
* Firewalld policy & NFS/autofs.
* Service-specific configuration.

---

## 💻 Host & Guest Context

### Host Environment
| Component | Details |
| :--- | :--- |
| **Host OS** | Fedora Linux 43 (KDE Plasma) |
| **Hypervisor** | KVM + QEMU + libvirt + virt-manager |
| **Connection** | `qemu:///system` |
| **Storage Pool** | `enterprise-tech-images` |
| **Network** | `lab-int` |
| **ISO Path** | `/var/lib/libvirt/boot/rhel-10.1-x86_64-dvd.iso` |

### Guest Model (`srv-admin`)
| Resource | Specification |
| :--- | :--- |
| **vCPU** | 2 |
| **RAM** | 4096 MiB |
| **Disk** | 60 GiB (qcow2) |
| **Firmware** | UEFI / OVMF |
| **OS Info** | `rhel10.1` |

> [!TIP]
> Adjust guest resources later only if the workload justifies it.

---

## 🛠️ Installation Variables
Run these commands on the **Fedora 43 host** to prepare the environment:

```bash
export ISO="/var/lib/libvirt/boot/rhel-10.1-x86_64-dvd.iso"
export VM_NAME="srv-admin"
export VM_RAM="4096"
export VM_VCPUS="2"
export VM_DISK="60G"
export VM_POOL="enterprise-tech-images"
export VM_NET="lab-int"
export VM_OSINFO="rhel10.1"
```

* **Why:** Reduces typing mistakes and ensures consistency across multiple guest deployments.
* **Verification:** Run `echo "$VM_NAME" && echo "$VM_NET"` to confirm variables are set.
* **Persistence:** Temporary for the current shell session.

---

## 🚀 Installation Steps

### Step 1: Preflight Validation
```bash
ls -lh "$ISO"
virsh -c qemu:///system pool-info "$VM_POOL"
virsh -c qemu:///system net-info "$VM_NET"
virt-install --osinfo list | grep -i rhel10
```
* **Goal:** Confirm ISO existence, storage pool availability, and network status.
* **Expected Result:** ISO size visible, pool/network "active", and `rhel10.1` recognized.

### Step 2: Collision Check
```bash
virsh -c qemu:///system dominfo "$VM_NAME" || true
virsh -c qemu:///system vol-list "$VM_POOL"
```
* **Goal:** Avoid naming conflicts with existing VMs or disk volumes.

### Step 3: Create Guest Disk
```bash
virsh -c qemu:///system vol-create-as "$VM_POOL" "${VM_NAME}.qcow2" "$VM_DISK" --format qcow2
virsh -c qemu:///system vol-info --pool "$VM_POOL" "${VM_NAME}.qcow2"
```
* **Goal:** Provision a persistent 60GB virtual disk in the enterprise storage pool.

### Step 4: Launch Installation
```bash
sudo virt-install \
  --connect qemu:///system \
  --name "$VM_NAME" \
  --memory "$VM_RAM" \
  --vcpus "$VM_VCPUS" \
  --cpu host-passthrough \
  --osinfo "$VM_OSINFO" \
  --boot uefi \
  --disk vol="${VM_POOL}/${VM_NAME}.qcow2",bus=virtio \
  --network network="$VM_NET",model=virtio \
  --graphics spice \
  --video qxl \
  --cdrom "$ISO"
```
* **What it changes:** Defines the VM in libvirt and initiates the boot process.
* **Action:** If the console doesn't open, use `virt-manager` to connect manually.

---

## 📝 Anaconda Installer Guidelines
During the RHEL 10.1 installation, follow these baseline settings:

* **Hostname:** `srv-admin`
* **Installation Target:** Select the 60GB VirtIO disk.
* **Software Selection:** Keep the initial installation as simple as possible and avoid optional roles or extra software unless required for the base guest deployment.
* **Network:** Ensure it is enabled and connected to `lab-int`.
* **Security:** Set Root password and create a local admin user.

---

## 🧪 Post-Install Validation

### Host-Side Check
```bash
virsh -c qemu:///system list --all
virsh -c qemu:///system dominfo "$VM_NAME"
virsh -c qemu:///system domifaddr "$VM_NAME" || true
virsh -c qemu:///system net-dhcp-leases "$VM_NET" || true
```
* **Why:** Confirms that the VM is running, recognized by libvirt, and correctly attached to the network with a valid IP.

### Guest-Side Check
```bash
cat /etc/os-release
hostnamectl
ip -brief address
systemctl get-default
lsblk
```
* **Why:** Validates the OS identity, network visibility, boot target (e.g., multi-user), and storage structure from within.

---

### Step 8: Enable Autostart & Verify
Once validated, ensure the VM starts with the host and verify the configuration:
```bash
virsh -c qemu:///system autostart "$VM_NAME"
virsh -c qemu:///system dominfo "$VM_NAME"
```

> [!IMPORTANT]
> Enable autostart only after confirming that the installation completed successfully and the guest boots normally without depending on the installer media.

---

## 🧹 Cleanup (If things go wrong)
To reset and start over:
```bash
virsh -c qemu:///system destroy "$VM_NAME" || true
virsh -c qemu:///system undefine "$VM_NAME" --nvram || true
virsh -c qemu:///system vol-delete --pool "$VM_POOL" "${VM_NAME}.qcow2" || true
```

---

## 📸 Artifacts & Documentation
### Screenshots to Capture
Store all screenshots in `assets/screenshots/phase-02/`:
1. `P02-01-iso-pool-network-ready.png`
2. `P02-02-virt-install-srv-admin.png`
3. `P02-03-rhel10-boot-menu-srv-admin.png`
4. `P02-04-anaconda-installation-summary-srv-admin.png`
5. `P02-06-anaconda-network-hostname-srv-admin.png`
6. `P02-07-srv-admin-first-boot-validation.png`
7. `P02-08-srv-admin-host-side-validation.png`

### Files to Update
* `phases/02-rhel10-install/README.md`
* `runbooks/rhel10-install.md`
* `notes/guest-inventory.md`

---

## 🏁 Outcome
Successful completion provides a working `srv-admin` node and a validated template for `srv-web`, `srv-db`, and `srv-storage`.
