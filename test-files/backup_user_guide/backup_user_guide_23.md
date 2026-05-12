---
hide_title: true
sidebar_label: Configuring the retention policy
title: Configuring the retention policy
id: backup_user_guide_23
---

# Configuring the retention policy

Configure the retention policy for restore points. The retention policy only applies to the automatically created restore points. Manually created restore points are retained permanently.

  <table>
  <thead>
    <tr>
    <th>Parameter</th>
    <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
    <td>Keep by time</td>
    <td>Keep the restore points created during the last <code>n</code> days.
    </td>
    </tr>
    <tr>
    <td>Keep by quantity</td>
    <td>Keep the last <code>n</code> restore points. </td>
    </tr>
    <tr>
    <td>Keep permanently</td>
    <td>Keep the restore points permanently. </td>
    </tr>
  </tbody>
  </table>

> **Information**:
>
> The backup service uses a combination of full backup and incremental backup. After a full backup is performed, each subsequent incremental backup is performed based on the previous backup. Restoring a virtual machine requires the full backup restore point and all associated incremental backup restore points. Therefore, to ensure successful virtual machine recovery, the backup service retains restore points for both full backup and incremental backup, even if the restore points exceed the specified limit of the retention policy. When the next full backup restore point and its associated incremental backup restore points meet the retention policy, the previous full backup restore point and the associated incremental backup restore points will be deleted.
>
> For example, a backup service performs a full backup at 00:00 every day and an incremental backup every hour. The configured restore point retention policy is set to retain the most recent 7 restore points. At 05:00 on the current day, all 30 restore points generated from 00:00 of the previous day to 05:00 of the current day are retained. After 06:00, all restore points generated on the previous day will be deleted, and the restore points generated from 00:00 of the current day onward will be retained, ensuring that the most recent 7 restore points are retained.
