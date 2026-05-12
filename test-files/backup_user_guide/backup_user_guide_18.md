---
hide_title: true
sidebar_label: Viewing restore points
title: Viewing restore points
id: backup_user_guide_18
---

# Viewing restore points

In the left sidebar of the **Backup & DR** page in CloudTower, click **Backup plan**. Select a backup plan and click its name to enter the details page. You can view all virtual machines included in the backup plan and the restore points for each virtual machine.

| **Field**              | **Description**                                                                                                                                                                                                                                        | **Example**                         |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------- |
| Restore point          | The name of the restore point is the time it was created.                                                                                                                                                                              | "2022-06-20 13:45" |
| Backup type            | The backup type when the restore point was created.                                                                                                                                                                                    | "Full Backup"                       |
| Total backup file size | The size of backup files corresponding to the restore point.                                                                                                                                                                           | "10 MiB"                            |
| Backup valid capacity  | The sum of the backup valid capacity of all virtual volumes of the virtual machine. The valid capacity refers to the size of backup files before compression.                                                          | "15 MiB"                            |
| Consistency type       | The consistency type of the snapshot corresponding to the restore point. It can be crash consistent or file-system consistent.                                                                                         | "File-system consistent"            |
| Compression ratio      | When compression is enabled in the backup plan, data transferred to the backup repository is compressed before being stored as backup files. <br/> Compression ratio = Backup Valid Capacity / Total Backup File Size. | "1.5"               |
| Execution type         | The execution type of the backup plan. It can be automatic execution based on the backup schedule or manual execution.                                                                                                 | "Automatic"                         |
