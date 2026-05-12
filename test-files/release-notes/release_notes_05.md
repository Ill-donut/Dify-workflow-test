---
title: Function support (for the AArch64 architecture)
author: SmartX documentation team
hide_title: true
id: release_notes_05
sidebar_label: Function support (for the AArch64 architecture)
---

# Function support (for the AArch64 architecture)

The following functions related to virtual machine services are not available if SMTX OS is deployed on the `Kunpeng AArch64` or `Phytium AArch64` architecture:

- E1000 NIC
- Cirrus, VGA, and QXL graphics cards
- BIOS firmware mode
- CPU compatibility configuration
- vGPU

The following functions are also not available if SMTX OS is deployed on the `Phytium AArch64` architecture:

- RDMA
- GPU passthrough
- PCI passthrough NIC
- SR-IOV passthrough NIC
- Encryption controller