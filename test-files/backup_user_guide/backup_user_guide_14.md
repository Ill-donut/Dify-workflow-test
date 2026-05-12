---
hide_title: true
sidebar_label: Viewing backup plans
title: Viewing backup plans
id: backup_user_guide_14
---

# Viewing backup plans

In the left sidebar of the **Backup & DR** page in CloudTower, select **Backup plan** to view all existing backup plans.

| **Field**                     | **Description**                                                                                                  | **Example**                         |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| Name                          | The name of the backup plan.                                                                     | "bk_plan"      |
| Description                   | The description of the backup plan.                                                              | "description"                       |
| Status                        | Whether the backup plan is executed by schedule.                                             | "In effect", "Suspended"            |
| Backup repository             | The backup repository where backup files are stored.                                             | "nfs_repo"     |
| Backup service                | The backup service that executes the backup plan.                                                | "bk_service"   |
| Last execution result         | The result of the most recent execution of the backup plan.                                      | "All success"                       |
| Last execution time           | The date and time of the most recent execution of the backup plan.                               | "2022-10-01 12:00" |
| Next auto execution time      | The date and time of the next automatic execution of the backup plan.                            | "2022-10-02 12:00" |
| Backup objects                | The number of backup objects in the backup plan.                                                 | "10"                                |
| Total backup file size        | The total size of backup files from all restore points of all backup objects in the backup plan. | "100 GiB"                           |
| Backup valid capacity         | The total backup valid capacity of all restore points of all backup objects in the backup plan.  | "150 GiB"                           |
| File-system consistency       | Whether `file-system consistency` is enabled.                                                    | "Enabled"                           |
| Compression                   | Whether compression is enabled.                                                                  | "Enabled"                           |
| Backup file compression ratio | The ratio of the backup valid capacity to the total backup file size.                            | "1.5"               |

Click the name of a backup plan to enter its details page. You can view its basic information, backup schedule, backup time, execution records, VM restore points, and events related to the backup.

- **Basic information**

  Displays the backup service name, backup repository name, file-system consistency status, compression status, backup file compression ratio, backup valid capacity, and total backup file size.

- **Backup schedule**

  Displays the backup schedule, full backup schedule, backup window, and restore point retention policy of the backup plan.

- **Backup time**

  Displays the last execution time and result triggered either manually or automatically, as well as the next automatic execution time.

- **Execution records**

  Displays the execution status of the backup plan, with different colors representing different statuses.

  - Green indicates that the backup plan was executed on that day and all backup jobs were successful.

  - Red indicates that the backup plan was executed on that day, but one or more backup jobs failed. Hover over the indicator to view the failure time and the number of virtual machines with failed backup jobs.

  - Blue indicates that the backup plan will be executed as scheduled on that day. Hover over the indicator to view the scheduled execution time.

  - Gray indicates that there is no scheduled backup plan for that day.

- **VM restore point**

  Displays all virtual machines in the backup plan and all restore points for each virtual machine.

- **Events**

  Displays user events and system events related to the backup plan.
