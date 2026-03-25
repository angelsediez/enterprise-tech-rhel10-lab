# Phase 02 - RHEL 10.1 Guest Deployment

## Objective

Deploy the first RHEL 10.1 guest virtual machine on the Fedora 43 virtualization host and establish the installation pattern that will later be reused for the remaining lab nodes.

This phase focuses on guest creation and installation only.

---

## Scope

This phase covers:

- preparing the guest installation workflow
- using the stable RHEL 10.1 ISO path on the host
- creating the first guest VM (`srv-admin`)
- using the existing libvirt storage pool and internal lab network
- completing the base RHEL 10.1 installation
- validating the guest from both the host and guest side
- documenting screenshots and inventory data

This phase does **not** cover advanced guest configuration such as:
- user policy
- SSH hardening
- package workflows beyond installation basics
- SELinux tuning
- firewalld rules
- NFS/autofs
- application deployment

Those belong to later phases.

---

## Host Context

- Host OS: `Fedora Linux 43 (KDE Plasma Desktop Edition)`
- Hypervisor stack: `KVM + QEMU + libvirt + virt-manager`
- libvirt connection: `qemu:///system`
- Storage pool: `enterprise-tech-images`
- Internal lab network: `lab-int`
- Guest target platform: `Red Hat Enterprise Linux 10.1`
- ISO path: `/var/lib/libvirt/boot/rhel-10.1-x86_64-dvd.iso`

---

## Guest Deployment Strategy

This phase uses `srv-admin` as the first guest and installation model.

The idea is:

1. install `srv-admin`
2. validate that the VM is healthy
3. document the installation workflow
4. reuse the same pattern later for:
   - `srv-web`
   - `srv-db`
   - `srv-storage`

---

## Guest Design Decisions

### Initial guest selected
- `srv-admin`

### Firmware model
- UEFI / OVMF

### Network model
- libvirt internal network: `lab-int`

### Storage model
- libvirt storage pool: `enterprise-tech-images`

### Guest installation method
- `virt-install` on the Fedora 43 host
- graphical install flow completed through the VM console / viewer

### Installation focus
- clean base install
- reproducible VM definition
- basic readiness validation after first boot

---

## Work Completed

- confirmed that the host-side ISO path is stable
- confirmed that `rhel10.1` is available in `osinfo`
- prepared the first guest deployment workflow
- created and installed `srv-admin`
- attached the guest to the `lab-int` network
- used the `enterprise-tech-images` storage pool
- completed the base RHEL 10.1 installation
- validated guest visibility from the host
- validated first boot behavior

> Update this section as real work is completed.

---

## Expected Guest Inventory

This phase begins the guest inventory for the lab.

Initial target nodes:

| Guest | Planned Role | Status |
|---|---|---|
| `srv-admin` | Administration and management node | In progress |
| `srv-web` | Web service node | Pending |
| `srv-db` | Database service node | Pending |
| `srv-storage` | Shared storage and support node | Pending |

Update the status column as the phase progresses.

---

## Validation Goals

At the end of this phase, the following should be true:

- the RHEL 10.1 ISO is reachable from the host
- `virt-install` can use `rhel10.1`
- the `srv-admin` guest exists in libvirt
- the guest boots successfully
- the guest is attached to `lab-int`
- the guest disk exists in `enterprise-tech-images`
- the guest is visible through `virsh`
- the guest receives network connectivity appropriate for this phase
- screenshots and guest inventory are documented

---

## Screenshots

Store all screenshots in:

`assets/screenshots/phase-02/`

Suggested captures:

- host preflight with ISO + pool + network ready
- `virt-install` command and launch
- RHEL boot menu / installer start
- Anaconda installation summary
- installation destination
- network and hostname screen
- first boot validation inside `srv-admin`
- host-side validation with `virsh`

> Replace this section later with the real screenshot filenames.

---

## Related Files

- `runbooks/rhel10-install.md`
- `notes/guest-inventory.md`
- `phases/01-virtualization-host/README.md`
- `phases/01-virtualization-host/lab-int.xml`

---

## Outcome

Once this phase is completed successfully, the lab will have its first installed RHEL 10.1 guest (`srv-admin`) and a reusable installation pattern for the remaining nodes.

The next step after this phase is to continue with post-install baseline work in later phases.
