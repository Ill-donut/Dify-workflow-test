---
hide_title: true
sidebar_label: Editing a backup plan
title: Editing a backup plan
id: backup_user_guide_15
---

# Editing a backup plan

In the **Backup plan** list, select the target backup plan to edit. Click **...** and choose **Edit basic information**, **Edit backup schedule and window**, or **Edit retention policy** accordingly to edit the target backup plan in the pop-up dialog box.

- **Edit basic information**

  <table>
  <thead>
    <tr>
      <th>Parameter</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Name/Description</td>
      <td>Edit the name and description of the backup plan.</td>
    </tr>
    <tr>
      <td>File-system consistency</td>
      <td><p>Choose whether to enable file-system consistency. When enabled, for virtual machines with VMTools installed and running, a quiesced or frozen file system is used to ensure that all disk I/O operations are completed and the data is in a restorable and consistent state during snapshot capture, thereby achieving a file-system consistent backup. For other virtual machines, crash-consistent backups are performed, and memory data is not included in snapshots. When disabled, all virtual machines will perform crash-consistent backups, and related snapshots will not include memory data of the virtual machine file system. </p>
      <p><strong>Note</strong>: The virtual machine will be temporarily unavailable while creating a file system consistency snapshot. </p></td>
    </tr>
    <tr>
      <td>Compression</td>
      <td>Choose whether to compress backup data. The change will take effect the next time the backup plan is executed. </td>
    </tr>
    <tr>
    <td>Virtual machines added to the backup plan</td>
    <td>Choose virtual machines to add to or remove from the backup plan. The change will take effect the next time the backup plan is executed. 
      <ul>
    <li>If you add a virtual machine to the backup plan, the first backup will be a full backup. </li>
    <li>If you remove a virtual machine from the backup plan, you need to choose whether to delete the restore points for the virtual machine as well. A restore point cannot be deleted if it is associated with any ongoing backup or restore job. If you choose to retain the restore points, you can restore the virtual machine from them. </li>
      </ul>
    </td>
    </tr>
  </tbody>
  </table>

  > **Information**:
  >
  > If a virtual machine in the backup plan has been deleted, moved to the recycle bin, converted into a virtual machine template, migrated to another cluster, or if its associated cluster has been removed from CloudTower, the virtual machine cannot be backed up. To prevent such virtual machines from consuming license units, remove them from the backup plan by editing the basic information of the plan.

- **Edit backup schedule and window**

  <table>
  <thead>
    <tr>
      <th>Parameter</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Backup schedule</td>
      <td>After modifying the backup schedule, you need to modify the full backup schedule as well. The changes will take effect the next time the backup plan is executed. </td> 
    </tr>
    <tr>
      <td>Full backup schedule</td>
      <td>The change will take effect the next time the backup plan is executed. </td> 
    </tr>
    <tr>
      <td>Backup window</td>
      <td>The change will take effect the next time the backup plan is executed. </td>
    </tr>
  </tbody>
  </table>

- **Edit retention policy**

  <table>
  <thead>
    <tr>
      <th>Parameter</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Retention policy</td>
      <td>The change will take effect immediately. If you shorten the retention period or reduce the number of restore points, any restore points exceeding the limit of the retention policy will be deleted. </td> 
    </tr>
  </tbody>
  </table>


