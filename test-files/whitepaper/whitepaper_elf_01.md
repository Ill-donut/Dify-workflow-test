---
title: Overview
sidebar_label: Overview
hide_title: true
id: whitepaper_elf_01
---

# Overview

ELF is a virtualization computing platform developed by SmartX based on Kernel-based Virtual Machine (KVM). It integrates with ZBS, the distributed block storage service designed and developed by SmartX, to deliver a complete hyper-converged virtualization solution. Throughout this document, ELF refers to the KVM-based virtual machine service computing platform, and ZBS refers to SmartX's proprietary distributed block storage service.

ELF addresses common virtualization computing requirements such as virtual machine management and VLAN network management. ELF is easy to operate and maintain, as unnecessary low-frequency features have been removed, which significantly reduces the system's learning curve and operational overhead. You can manage the hyper-converged virtualization platform through a simple web interface. In addition, because the underlying storage is powered by ZBS, virtual machines running on the ELF platform deliver excellent I/O performance with high data reliability and availability.

- Fully distributed architecture

    The management platform has no single point of failure, unlike vCenter.

- Simple and intuitive Web UI

    Built on open-source KVM, the platform meets the requirements of most virtualization scenarios.

- Virtual machine high availability

    When a physical server fails, the virtual machines on it are automatically migrated to healthy physical servers, ensuring business continuity.

- VLAN network support

    Supports Layer 2 VLAN network isolation with simple configuration and maintenance, covering most network use cases.
