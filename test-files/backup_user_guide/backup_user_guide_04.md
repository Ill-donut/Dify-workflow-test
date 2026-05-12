---
hide_title: true
sidebar_label: Planning License Unit Allocation
title: Planning License Unit Allocation
id: backup_user_guide_04
---
# Planning License Unit Allocation

The software license for SMTX Backup and Disaster Recovery is shared by the Backup and Replication function modules. License units are consumed according to the type of protected object and the features used, as follows:

- **SMTX OS (ELF) cluster virtual machines**

  - Backup: 1 license unit is consumed for each virtual machine backed up.

  - Asynchronous replication: 2 license units are consumed for each virtual machine asynchronously replicated.

  - Synchronous replication: 4 license units are consumed for each virtual machine synchronously replicated.

- **SMTX ZBS block storage cluster volumes**: 2 license units are consumed for each 1 TiB volume asynchronously replicated.

Please plan the allocation of license units in advance based on your actual business requirements, taking into account the function modules you need to use, the number of virtual machines and volumes to be protected, and future business expansion.
