---
hide_title: true
sidebar_label: Set Basic Information
title: Set Basic Information
id: backup_user_guide_21
---

# Set Basic Information

1. Enter the name and description of the backup plan.
2. Set the backup service and backup repository used by the backup plan, and choose whether to enable file system consistency and compression.

   <table>
    <tr>
      <th>Configuration Item</th>
      <th>Description</th>
    </tr>
    <tr>
      <td>Backup Service</td>
      <td>Select a backup service. It is recommended to choose a backup service in the same data center as the VM to be backed up.</td>
    </tr>
    <tr>
      <td>Backup Repository</td>
      <td>Select a backup repository. You can select only a backup repository associated with the backup service.</td>
    </tr>
    <tr>
      <td>File System Consistency</td>
      <td><p>Enabled by default. For running VMs with VM tools installed, the file system is quiesced or frozen to ensure that all disk I/O has completed when the snapshot is captured and that the data is in a recoverable, consistent state, thereby enabling file system-consistent backups; other VMs will be backed up with crash consistency, and the snapshot will not include in-memory data from the VM file system. After this is disabled, all VMs will be backed up with crash consistency, and the related snapshots will not include in-memory data from the VM file system.</p>
      <p><strong>Note</strong>: The VM will be temporarily unavailable while a file system-consistent snapshot is being created.</p>
      </td>
    </tr>
    <tr>
      <td>Compression</td>
      <td>Choose whether to enable backup data compression, which is enabled by default. After the VM's virtual volume data is transferred to the backup repository, it is compressed first and then stored as a backup file.</td>
    </tr>
   </table>

3. Select the VMs to include in the backup plan; you can select one or more VMs. VMs can be filtered by VM name, cluster name, tag name, and tag value.

    >**Note**:
    >
    >-  The following VMs cannot be backed up:
    >     - VMs with shared virtual volumes mounted.
    >     - VMs with no virtual volumes mounted.
    >     - VMs running system services, such as Everoute Controller VMs, CloudTower VMs, backup service VMs, replication service VMs, observability VMs, advanced monitoring VMs, security protection VMs (SVM), and so on.
    >     - SKS workload cluster node VMs.
    >     - Container image registry VMs.
    >     - VMs in the `Operation in Progress` or `Unknown` state.
    >     - VMs whose cluster has an abnormal connection to CloudTower.
    >     - VMs whose cluster uses a trial license and the license has expired.
    >     - Test VMs and replica VMs created by the replication service.
    >- For VMs already added to the backup plan, when performing cross-cluster cold migration and staged migration without retaining the source VM:
    >
    >   -  If the target cluster of the migration is associated with the current backup service, the backup plan will continue to protect the VM;
    >   - If the target cluster of the migration is not associated with the current backup service, the VM will be removed from this backup plan after migration;
    >   - For VMs migrated by cold migration or staged migration to a 5.x.x cluster lower than 5.1.3 or to a 6.0.x cluster, they will be removed from the backup plan after migration is complete.
    >- For VMs already added to the backup plan, if cross-cluster cold migration or staged migration is performed while retaining the source VM, the source VM will continue to be protected instead of the migrated VM.
