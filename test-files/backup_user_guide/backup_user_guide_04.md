---
hide_title: true
sidebar_label: Planning license unit allocation
title: Planning license unit allocation
id: backup_user_guide_04
---

# Planning license unit allocation

The software license for SMTX Backup & Disaster Recovery is shared by the backup service and the replication service. License units are consumed based on the type of protected object and the function used, as follows:

- **Virtual machines in SMTX OS (ELF) clusters**

  - Backup: Backing up one virtual machine consumes 1 license unit.

  - Asynchronous replication: Asynchronously replicating one virtual machine consumes 2 license units.

  - Synchronous replication: Synchronously replicating one virtual machine consumes 4 license units.

- **Volumes in SMTX ZBS block storage clusters**: Asynchronously replicating 1 TiB of storage volume consumes 2 license units.

Therefore, you need to plan the allocation of license units in advance based on actual business needs by considering the required services, the number of virtual machines and volumes to be protected, and the potential business expansion.
