---
hide_title: true
sidebar_label: Planning backup plans
title: Planning backup plans
id: backup_user_guide_02
---

# Planning backup plans

Backup services use backup plans to manage backup policies. A backup plan defines backup services, backup objects, backup repositories, backup schedules, and restore point retention policies. Before creating a backup plan, you need to consider the following aspects:

- **Backup object**

  Each backup plan can include one or more virtual machines that share the same backup policy. Therefore, it is recommended to categorize virtual machines based on different data protection requirements and group virtual machines that share the same backup schedule, backup window, and retention policy into the same backup plan. This avoids redundant configurations and improves operation and management efficiency.

- **Backup type**

  Backup types include full backup and incremental backup. A full backup will be performed during the initial backup. You can combine full backup and incremental backup to create a backup policy that best meets your actual needs.

  - Full backup: Makes a full copy of all data of the virtual machine when the backup is performed.

  - Incremental backup: Backs up all data that has changed since the last backup, whether it was a full or incremental backup.

- **Backup schedule**

  By setting a backup schedule, the backup service can automatically perform periodic backups for virtual machines. You can set the appropriate data backup interval based on the RPO (Recovery Point Objective) target of your business system. The minimum RPO supported by the backup is 15 minutes. You can choose an appropriate backup schedule based on your business requirements to ensure timely data backup and recovery capability.

- **Restore point retention policy**

  After executing a backup plan, the backup service creates a restore point for each virtual machine in the backup plan. Restore points contain all virtual machine data at the time of backup, which can be used to restore virtual machines to the state at the point in time when needed.

  The restore point retention policy can be defined to specify the number of restore points to be retained and the time range. When backup data does not need to be retained long-term, you can configure the restore point retention policy to control the number of restore points in the backup repository.
