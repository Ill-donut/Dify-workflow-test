---
title: Installation and Upgrade Notes
author: SmartX Documentation Team
hide_title: true
id: release_notes_02
sidebar_label: Installation and Upgrade Notes
---

# Installation and Upgrade Notes

## Installation

For hosts that use the `MegaRAID 9560-8i RAID` card, set the boot mode to **`UEFI`**.

## Upgrade

- When this version of SMTX OS is deployed on cluster nodes, the resources occupied by the system, including physical disk storage space and host CPU and memory, are different from those in earlier versions. Refer to the **System Resource Usage** section in [SMTX OS Configuration and Management Specifications](../config_specs/config_specs_01.md) to confirm in advance that the node resources are sufficient.

- For SMTX OS clusters deployed on Hygon x86_64 and Kunpeng AArch64 servers, if the version is 4.0.x or 5.0.0 to 5.0.2, you must follow the steps below before the upgrade can be completed.
  1. Upgrade the SMTX OS cluster from the current version to version 5.0.7 (CentOS operating system).
  2. Use the separately released conversion tool to convert the underlying operating system of the SMTX OS 5.0.7 cluster from CentOS to openEuler.
  3. Upgrade the SMTX OS 5.0.7 cluster (openEuler operating system) to this version.
