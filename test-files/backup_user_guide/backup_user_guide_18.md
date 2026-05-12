---
hide_title: true
sidebar_label: View Recovery Points
title: View Recovery Points
id: backup_user_guide_18
---
# View Recovery Points

Log in to **CloudTower**. In the **Backup and Disaster Recovery** page, click **Backup Plans**, select a backup plan, and click the backup plan name to enter the backup plan details page. You can then view all virtual machines included in the current backup plan and the recovery points already created for each virtual machine.

  | Field | Description | Example |
  | ----| ----| ----|
  | Recovery Point | Recovery points are named by the time they were created. | """2022-06-20 13:45"""|
  | Backup Type | The backup type corresponding to the recovery point when it was created. | """Full Backup"""|
  | Backup File Size | The size of the backup file corresponding to the recovery point. | """10 MiB""" |
  | Backup Effective Capacity | The sum of the effective capacity of all virtual volumes of the virtual machine. Effective capacity is the capacity size before the backup file is compressed. | """15 MiB""" |
  | Consistency Type | The consistency type of the snapshot corresponding to the recovery point, including crash-consistent and file system-consistent.         |  """File System Consistency"""           |
  | Compression Ratio | When compression is enabled for the backup plan, the data transferred to the backup repository is compressed and then stored as a backup file.<br/> Compression ratio = backup effective capacity / backup file size. | """1.5"""|
  | Execution Type | The execution type of the backup plan, including automatic execution according to the configured backup schedule and manual execution. | """Automatic Execution""" |
