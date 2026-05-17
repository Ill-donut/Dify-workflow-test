---
title: Overview
sidebar_label: Overview
hide_title: true
id: whitepaper_elf_01
---

# Overview

ELF is a virtualized computing platform developed by SmartX based on KVM. It can be integrated with SmartX-designed and -developed distributed block storage service (ZBS) to provide a complete hyperconverged virtualization solution. In the following text, for ease of description and understanding, ELF will be used to refer to the computing platform of the KVM-based virtual machine service, and ZBS will be used to refer to SmartX's self-developed distributed block storage service.

ELF implements the requirements of common virtualized computing scenarios, such as virtual machine management and VLAN network management. ELF is easy to operate and maintain, and removes a large number of infrequently used features, greatly reducing the learning and operations costs of the system. Users can manage the hyperconverged virtualized computing platform through simple web interactions. In addition, because the underlying storage uses ZBS, virtual machines running on the ELF platform have excellent I/O performance, as well as highly reliable and highly available data.

- Fully distributed architecture design

    The management platform does not have a single point of failure like vCenter.

- Simple and easy-to-use Web UI

    The Hypervisor is based on open source KVM and provides virtualization computing capabilities for most virtualization scenarios.

- VM high availability

    When a physical server fails, the virtual machines on it are automatically migrated to healthy physical servers to ensure high business availability.

- VLAN network support

    Supports VLAN Layer 2 network isolation, with simple configuration and operations, meeting most network usage scenarios.
