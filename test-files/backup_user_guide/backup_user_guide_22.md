---
hide_title: true
sidebar_label: Set Backup Cycle and Time Window
title: Set Backup Cycle and Time Window
id: backup_user_guide_22
---

# Set Backup Cycle and Time Window

Set the cycle for automatic backup plan execution, including setting the backup cycle, specifying the full backup cycle, and setting the backup window.

1. **Set Backup Cycle**

    <table>
    <thead>
    <tr>
      <th>Execution Type</th>
      <th>Default Cycle</th>
      <th>Supported Cycle Settings</th>
      <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
      <td>Minute
      </td>
      <td>15 minutes
      </td>
      <td>15 ~ 59 minutes
      </td>
      <td rowspan="2" >The system starts counting from 00:00 every day and executes backup tasks according to the configured time cycle.
      </td>
    </tr>
    <tr>
      <td>Hour
      </td>
      <td>1 hour
      </td>
      <td>1 ~ 23 hours
      </td>
    </tr>
    <tr>
      <td>Day
      </td>
      <td>1 day
      </td>
      <td>1 ~ 30 days
      </td>
      <td>You need to set one or more execution times for the selected day. The minimum interval between two execution times is 15 minutes.
      </td>
    </tr>
    <tr>
      <td>Week
      </td>
      <td>Every Monday
      </td>
      <td>Monday ~ Sunday
      </td>
      <td>You can choose to execute on one or more days of the week, and need to set one or more execution times for the selected day. The minimum interval between two execution times is 15 minutes.
      </td>
    </tr>
    </tbody>
    </table>

     >**Note**:
     >
     >At the automatic execution time of the backup cycle, if the previous automatic task has not finished, this execution will be skipped.

2. **Set Full Backup Cycle**

    Specify the execution time for full backups among all backup execution times. Unspecified time points will perform incremental backups.

    - When the backup cycle is set to execute by **minute**, **hour**, or **day**, the full backup cycle can be set to execute by **day**, **week**, or **month**. After configuration, within the full backup execution cycle, you need to select one from all backup execution times as the full backup execution time.
    - When the backup cycle is set to execute by **week**, the full backup can be set to **week** or **month**. After configuration, within the full backup execution cycle, you need to select one from all backup execution times as the full backup execution time.

3. **Set Backup Window**

    Choose whether to enable **Allow backup tasks to run only within the backup window**, which is disabled by default. After enabling:

    - The interval between the start and end of the backup window must be at least 15 minutes.
    - The execution time configured in the backup cycle must fall within the time range of the backup window. If the execution time is the same as the backup window end time, the backup task will not be initiated.
    - Backup tasks that are not completed within the time window will be stopped by default after the backup window ends, and the corresponding virtual machine snapshots and backup files will be deleted. If you do not want to stop such backup tasks, select **If the backup cannot be completed within the time window, continue to complete the current backup**.
