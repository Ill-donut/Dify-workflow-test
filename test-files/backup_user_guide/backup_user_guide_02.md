---
hide_title: true
sidebar_label: Backup Plan Planning
title: Backup Plan Planning
id: backup_user_guide_02
---

# Backup Plan Planning

The backup service uses backup plans to manage backup policies. A backup plan defines the backup service, backup objects, backup repository, backup cycle, and recovery point retention policy. Before creating a backup plan, plan it from the following aspects:

- **Backup objects**

  Each backup plan can include one or more virtual machines that share the same backup policy. Therefore, it is recommended to classify virtual machines according to different data protection requirements, and place virtual machines with the same backup cycle, backup window, and retention policy in the same backup plan. This avoids repeatedly defining the same backup policy and improves operations and management efficiency.

- **Backup type**

  Backup types include full backup and incremental backup, and a full backup is performed for the first backup. You can combine full backup and incremental backup to create the backup policy that best meets actual requirements.

    - Full backup: Makes a complete copy of all data on the virtual machine at the time the backup is performed.

    - Incremental backup: Backs up all changed data based on the previous backup (full backup or incremental backup).

- **Backup cycle**

  By setting a backup cycle, the backup service can automatically perform periodic backups of virtual machines. You can correctly set the data backup interval according to the RPO (Recovery Point Objective) target of the business system. The minimum supported RPO for backups is 15 minutes, so you can choose an appropriate backup cycle based on business requirements to ensure timely data backup and recovery capability.

- **Recovery point retention policy**

  After each backup plan is executed, the backup service creates a recovery point for each virtual machine in the backup plan. The recovery point contains all virtual machine data at the backup time. When needed, you can restore the virtual machine to the state at the backup time through the recovery point.

  The recovery point retention policy can define the number of recovery points to retain or a time range. When backup data does not need to be kept for a long time, you can use the recovery point retention policy to control the number of recovery points in the backup repository.
