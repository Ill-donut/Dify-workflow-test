---
hide_title: true
sidebar_label: Configuring the backup schedule and backup window
title: Configuring the backup schedule and backup window
id: backup_user_guide_22
---

# Configuring the backup schedule and backup window

Configure the policy for automatic execution of the backup plan, including the backup schedule, full backup schedule, and backup window.

1. **Configure the backup schedule**

    <table>
    <thead>
    <tr>
      <th>Execution type</th>
      <th>Default value</th>
      <th>Supported range</th>
      <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
      <td>Minute
      </td>
      <td>15 minutes
      </td>
      <td>15 to 59 minutes
      </td>
      <td rowspan="2" >The system will start timing at 00:00 each day and perform backup jobs according to the specified schedule.
      </td>
    </tr>
    <tr>
      <td>Hour
      </td>
      <td>1 hour
      </td>
      <td>1 to 23 hours
      </td>
    </tr>
    <tr>
      <td>Day
      </td>
      <td>1 day
      </td>
      <td>1 to 30 days
      </td>
      <td>Set one or more execution times with a minimum interval of 15 minutes between two execution times. 
      </td>
    </tr>
    <tr>
      <td>Week
      </td>
      <td>Every Monday
      </td>
      <td>Monday to Sunday
      </td>
      <td>You can choose one or more days of the week for execution. Set one or more execution times for each chosen day. The minimum interval between two execution times is 15 minutes.
      </td>
    </tr>
    </tbody>
    </table>

   > **Information**:
   >
   > If a previous automatic backup job has not been completed by the next scheduled time, the backup service will skip the new automatic execution.

2. **Configure the full backup schedule**

   Specify full backup execution times from all scheduled backup execution times. Incremental backups will be performed for time points not specified for full backups.

   - If the backup schedule is set to run by **minute**, **hour**, or **day**, the full backup schedule can be configured to execute by **day**, **week**, or **month**. Once set, you need to select one of the scheduled backup times within the full backup schedule as the execution time for the full backup.
   - If the backup schedule is set to run by **week**, the full backup schedule can be configured to execute by **week** or **month**. Once set, you need to select one of the scheduled backup times within the full backup schedule as the execution time for the full backup.

3. **Configure the backup window**

   Choose whether to enable **Perform only within window**. The option is disabled by default. Once enabled, consider the following:

   - The minimum duration for the backup window is 15 minutes.

   - The scheduled execution time must be within the time range of the backup window. If the scheduled backup time coincides with the end time of the backup window, the backup job will not be performed.

   - If a backup job exceeds the backup window, the backup service will automatically stop it and delete the corresponding virtual machine snapshots and backup files. To prevent such backup jobs from being stopped, select **Continue backup until finished even if beyond this window**.
