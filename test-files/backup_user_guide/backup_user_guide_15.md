---
hide_title: true
sidebar_label: Edit Backup Plan
title: Edit Backup Plan
id: backup_user_guide_15
---

# Edit Backup Plan

In the **Backup Plans** list, select the backup plan you want to edit and click **...**. You can choose **Edit Basic Information**, **Edit Backup Schedule**, or **Edit Retention Policy**, then make changes in the corresponding pop-up page.

- **Edit Basic Information**

  <table>
  <thead>
    <tr>
      <th>Configuration Item</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Name/Description</td>
      <td>Edit the name and description of the backup plan.</td>
    </tr>
    <tr>
      <td>File System Consistency</td>
      <td><p>Choose whether to enable file system consistency. After it is enabled, for running virtual machines with VM tools installed, the system will silence or freeze the file system to ensure that all disk I/O has completed when the snapshot is captured and that the data is in a recoverable, consistent state, thereby achieving file system-consistent backups; other virtual machines will be backed up with crash consistency, and the snapshot will not contain in-memory data from the VM file system. If this is not enabled, all virtual machines will be backed up with crash consistency, and the related snapshots will not contain in-memory data from the VM file system.</p>
      <p><strong>Note</strong>: Virtual machines will be temporarily unavailable while file system-consistent snapshots are being created.</p></td>
    </tr>
    <tr>
      <td>Compression</td>
      <td>Choose whether to compress backup data. The change takes effect the next time the backup plan runs.</td>
    </tr>
    <tr>
    <td>Virtual Machines Added to the Backup Plan</td>
    <td>Select virtual machines to add to or remove from the backup. The change takes effect the next time the backup plan runs.
      <ul>
    <li>If a virtual machine is added, the first backup after addition is a full backup.</li>
    <li>If a virtual machine is removed, you must choose whether to delete its recovery points at the same time. If a recovery point currently has related backup or recovery tasks, that recovery point cannot be deleted. If you choose to keep the recovery points, restoring the virtual machine from the retained recovery points is still supported.</li>
      </ul>
    </td>
    </tr>
  </tbody>
  </table>

  >**Note**:
  >
  >If a virtual machine in the backup plan has been deleted, moved to the recycle bin, converted to a virtual machine template, migrated across clusters, or if the cluster it belongs to has been removed, it can no longer be backed up. To prevent such virtual machines from continuing to consume license units, remove them from the backup plan through Edit Basic Information.

- **Edit Backup Schedule**

  <table>
  <thead>
    <tr>
      <th>Configuration Item</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Backup Cycle</td>
      <td>After modifying the backup cycle, you must also modify the full backup cycle. The changes take effect starting from the next time the backup plan runs.</td>
    </tr>
    <tr>
      <td>Full Backup Cycle</td>
      <td>The change takes effect starting from the next time the backup plan runs.</td>
    </tr>
    <tr>
      <td>Backup Window</td>
      <td>The change takes effect starting from the next time the backup plan runs.</td>
    </tr>
  </tbody>
  </table>

- **Edit Retention Policy**

  <table>
  <thead>
    <tr>
      <th>Configuration Item</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Recovery Point Retention Policy</td>
      <td>The change takes effect immediately after it is saved. If you reduce the recovery point retention time or the number of retained recovery points, recovery points that exceed the retention policy will be deleted.</td>
    </tr>
  </tbody>
  </table>
