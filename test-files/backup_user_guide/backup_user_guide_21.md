---
hide_title: true
sidebar_label: Configuring the basic information
title: Configuring the basic information
id: backup_user_guide_21
---

# Configuring the basic information

1. Enter the name and description of the backup plan.

2. Select a backup service as well as a backup repository for the backup plan and choose whether to enable file-system consistency and compression accordingly.

   <table>
    <tbody><tr>
      <th>Parameter</th>
      <th>Description</th>
    </tr>
    <tr>
      <td>Backup service</td>
      <td>Select a backup service. It is recommended to select a backup service located in the same data center as the virtual machines to be backed up.</td>
    </tr>
    <tr>
      <td>Backup repository</td>
      <td>Select a backup repository. Only backup repositories associated with the backup service can be selected.</td>
    </tr>
    <tr>
      <td>File-system consistency</td>
      <td><p>Enabled by default. For virtual machines with VMTools installed and running, a quiesced or frozen file system is used to ensure that all disk I/O operations are completed and the data is in a restorable and consistent state during snapshot capture, thereby achieving a file-system consistent backup. For other virtual machines, crash-consistent backups are performed, and file system memory data is not included in snapshots. When disabled, all virtual machines will perform crash-consistent backups, and related snapshots will not include memory data of the virtual machine file system. </p>
      <p><strong>Note</strong>: The virtual machine will be temporarily unavailable while creating a file system consistency snapshot. </p>
      </td>
    </tr>
    <tr>
      <td>Compression</td>
      <td>Choose whether to enable backup data compression, which is enabled by default. The virtual volume data transferred to the backup repository will be compressed before being stored as backup files. </td>
    </tr>
   </tbody></table>

3. Select one or more virtual machines for the backup plan. You can filter virtual machines by name, cluster name, label name, or label value.

   > **Information**:
   >
   > - The following virtual machines are not supported for backup:
   >   - Virtual machines with shared virtual volumes mounted.
   >   - Virtual machines with no virtual volumes mounted.
   >   - Virtual machines that run system services, such as Everoute Controller virtual machines, CloudTower virtual machines, backup service virtual machines, replication service virtual machines, observability virtual machines, advanced monitoring virtual machines, and security virtual machines (SVM).
   >   - Virtual machines that serve as SKS workload cluster nodes.
   >   - Container registry virtual machines.
   >   - Virtual machines in the `Updating` or `Unknown` state.
   >   - Virtual machines in a cluster disconnected from CloudTower.
   >   - Virtual machines in a cluster with an expired Trial license.
   >   - Test virtual machines and replica virtual machines created by the replication service.
   > - For virtual machines included in a backup plan, when a cross-cluster cold migration or staged migration is performed without retaining the source virtual machine:
   >   - If the target cluster of the migration is associated with the current backup service, the backup plan will continue to protect the migrated virtual machine.
   >   - If the target cluster of the migration is not associated with the current backup service, the migrated virtual machine will be removed from the backup plan after migration.
   >   - For virtual machines migrated through cold migration or staged migration to clusters running SMTX OS (ELF) 5.x.x earlier than version 5.1.3 or to clusters running SMTX OS (ELF) 6.0.x, they will be removed from the backup plan after migration.
   > - For virtual machines included in a backup plan, if a cross-cluster cold migration or staged migration is performed with the source virtual machine retained, the backup plan will continue to protect the source virtual machine rather than the migrated virtual machine.
