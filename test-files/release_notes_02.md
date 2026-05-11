---
title: Installation and upgrade notes
author: SmartX documentation team
hide_title: true
id: release_notes_02
sidebar_label: Installation and upgrade notes
---

# Installation and upgrade notes

## For installation

Set the boot mode to **`UEFI`** for hosts using the `MegaRAID 9560-8i RAID` card.

## For upgrade

- When deploying SMTX OS 6.2.0 on cluster nodes, the resources required by the system (such as physical disk storage space, host CPU and memory) are diﬀerent from those of earlier versions. To ensure that the nodes have suﬃcient resources, refer to the **System resource usage** section in [_SMTX OS Configuration Specifications_](../config_specs/config_specs_01.md) for details.

- SMTX OS clusters with the `Hygon x86_64` or `Kunpeng AArch64` architecture and either of version 4.0.x or between 5.0.0 and 5.0.2 will utilize the CentOS operating system. To perform an upgrade on this type of clusters, follow the steps below:
  1. Upgrade the SMTX OS cluster to 5.0.7.
  2. Switch the operating system from CentOS to openEuler using a separately released conversion tool.
  3. Continue upgrading the SMTX OS cluster now using openEuler as the operating system from version 5.0.7 to 6.2.0.


