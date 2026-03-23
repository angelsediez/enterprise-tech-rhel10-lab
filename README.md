# EnterpriseTech RHEL 10 Lab

A **production-style** Red Hat Enterprise Linux 10.1 homelab built with **KVM**, **QEMU**, and **libvirt**.

This repository documents a multi-VM Linux environment designed to simulate a small enterprise infrastructure and explore day-to-day system administration practices in a structured, repeatable, and well-documented way.

---

## Overview

This lab is centered around a four-node environment that represents a compact but realistic enterprise setup:

- `srv-admin`
- `srv-web`
- `srv-db`
- `srv-storage`

The goal is to build, maintain, validate, and document a RHEL-based environment that reflects real operational work across system provisioning, storage, services, networking, access control, security, troubleshooting, and persistence.

---

## Environment

- **Platform:** Red Hat Enterprise Linux 10.1
- **ISO:** `rhel-10.1-x86_64-dvd.iso`
- **Virtualization stack:** KVM + QEMU + libvirt + virt-manager
- **Topology:** Multi-VM local enterprise lab
- **Documentation style:** phase-based, validation-first, screenshot-supported

---

## What This Lab Covers

This homelab focuses on building and documenting realistic Linux administration practices, with emphasis on:

- System provisioning and baseline configuration
- Storage and filesystem management
- Service lifecycle management
- Networking and name resolution
- Firewall and access control
- SELinux-aware administration
- Scheduled tasks, logging, and operational validation
- Reproducible troubleshooting and recovery workflows
- Configuration persistence across reboots

---

## Lab Design

The environment is being built in phases so each layer can be validated and documented before moving forward. Planned areas include:

- Repository and documentation bootstrap
- Virtualization host preparation
- Virtual machine deployment
- Baseline operating system configuration
- Identity and access management
- Storage and filesystems
- Services and boot behavior
- Networking and firewall policy
- SELinux and security controls
- Logging, scheduling, and persistence
- Shared services and fault analysis
- Final environment validation

---

## Documentation Model

Each phase is expected to include:

- A phase README
- Runbooks
- Screenshots
- Validation checklists
- Troubleshooting notes
- Persistence verification after reboot

---

## Repository Structure

```text
enterprise-tech-rhel10-lab/
├── README.md
├── docs/
├── phases/
├── runbooks/
├── validation/
├── troubleshooting/
├── scripts/
├── assets/
└── notes/
```

---

## Current Status
Status: In progress  
Current phase: Bootstrap and repository setup

---

## Why This Repository Exists
This project exists as a hands-on Linux systems lab built for the sake of learning, refining, and documenting real administration work in a way that is structured, repeatable, and technically honest.

It is intended to reflect the kind of environment a Linux enthusiast and systems administrator would build to deepen practical understanding of Red Hat-based infrastructure.

---

## Author
Angel Diez
