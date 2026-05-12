---
hide_title: true
sidebar_label: View Backup Plans
title: View Backup Plans
id: backup_user_guide_14
---

# View Backup Plans

On the **Backup** page, select **Backup Plans** to view all current backup plans.

  | Field | Description | Example |
  | ----| ---- | ----|
  | Name | The name of the backup plan. | """bk_plan""" |
  | Description | The description of the backup plan. | """description""" |
  | Status | The active state of the backup plan's automatic execution cycle. | """Active"""; """Paused""" |
  | Backup Repository | The backup repository that stores backup files. | """nfs_repo""" |
  | Backup Service | The backup service that executes the backup plan. | """bk_service""" |
  | Most Recent Execution Result | The result of the most recent execution of the backup plan. | """All succeeded""" |
  | Most Recent Execution Time | The date and time of the most recent execution of the backup plan. | """2022-10-01 12:00""" |
  | Next Automatic Execution Time | The date and time of the next automatic execution of the backup plan. | """2022-10-02 12:00""" |
  | Number of Backup Objects | The number of backup objects included in the backup plan. | """10""" |
  | Total Backup File Capacity | The sum of the backup file sizes of all restore points for all backup objects in the backup plan. | """100 GiB""" |
  | Backup Effective Capacity | The sum of the effective backup capacity of all restore points for all backup objects in the backup plan. | """150 GiB""" |
  | File System Consistency | Whether file system consistency has been enabled.     | "Yes"|
  | Compression | Whether compression has been enabled.                     |"Yes"|
  | Backup File Compression Ratio | Backup effective capacity / total backup file capacity. | """1.5""" |

Click a backup plan name to go to the backup plan details page, where you can view the current backup plan's basic information, backup cycle, backup time, execution records, virtual machine restore points, and related backup events.

  - **Basic Information**

    Displays the backup service name, backup repository name, whether file system consistency is enabled, whether compression is enabled, the backup file compression ratio, backup effective capacity, and total backup file capacity.

  - **Backup Cycle**

    Displays the backup plan's backup cycle, full backup cycle, backup window, and restore point retention policy.

  - **Backup Time**

    Displays the backup plan's next automatic execution time, most recent execution time (including manual and automatic executions), and most recent execution result (including manual and automatic executions).

  - **Execution Records**

    Displays the execution status of the current backup plan. Different colors indicate different states.

    - Green indicates that the backup plan was executed today and all backup tasks succeeded.

    - Red indicates that the backup plan was executed today and some backup tasks failed. Hover over the item to view the time when the backup plan execution failed and the number of VMs whose backups failed.

    - Blue indicates that there is a backup plan scheduled to run today but it has not yet been executed. Hover over the item to view the time when the backup plan will be executed.

    - Gray indicates that there is no backup plan scheduled to run today.

  - **VM Restore Points**

    Displays all VMs included in the current backup plan and all restore points for each VM.

  - **Events**

    Displays user events and system events related to the current backup plan.
