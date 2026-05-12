---
hide_title: true
sidebar_label: Viewing backup overview
title: Viewing backup overview
id: backup_user_guide_20
---

# Viewing backup overview

In the left sidebar of the **Backup & DR** page in CloudTower, select **Overview** and you can view information including the overall status of protected virtual machines, execution records of backup plans, the status of backup plans, backup repository capacity usage, and the health status of backup services.

- **Protected resources**

  Navigate to the **Virtual machine** tab to view the numbers of protected and unprotected virtual machines and the proportion of protected virtual machines to the total number of virtual machines in all SMTX OS (ELF) clusters managed by CloudTower.

- **Execution records**

  Navigate to the **Virtual machine** tab to view the execution status of all backup and replication plans for all virtual machines. Green indicates successful jobs, while red indicates failed jobs.

- **Backup plan**

  Displays the total number of backup plans, the number of backup plans in effect, and the number of suspended backup plans.

- **Backup file compression ratio**

  Displays the overall compression ratio, which only counts the compression of successfully generated restore points in backup plans with compression enabled. The compression ratio is calculated by dividing the backup valid capacity by the total backup file size.

  - Backup valid capacity: The sum of the valid capacity of all successfully generated restore points in backup plans with compression enabled. Valid capacity refers to the size of backup files before compression.

  - Total backup file size: The size of stored backup files corresponding to restore points that were successfully generated in all backup plans with compression enabled.

- **Backup repository capacity**

  Displays the total capacity, capacity usage, used capacity, and available capacity of all backup repositories.

- **Capacity usage**

  Displays the capacity usage of all backup repositories.

- **Backup service**

  Displays information about all backup services, including the service name, version, status, the number of associated SMTX OS clusters, the number of backup repositories, and the number of backup plans. The status can be one of the following: `Deploying`, `Upgrade available`, `Upgrading`, `Uninstalling`, and `Abnormal`. If no status is displayed, it indicates a normal state.
