---
hide_title: true
sidebar_label: Manually performing a backup plan
title: Manually performing a backup plan
id: backup_user_guide_12
---

# Manually performing a backup plan

A created backup plan runs automatically according to the specified backup schedule by default, but it can also be executed manually.

**Prerequisite**

The backup plan has no ongoing manual jobs.

**Procedure**

1. In the left sidebar of the **Backup & DR** page in CloudTower, select **Backup plan**. In the list, select the target backup plan to perform manually. Click **...** on the right side of the list or the backup plan details page and select **Perform manually**.

2. Select the backup type in the pop-up **Manually perform backup plan** dialog box.

   - If any virtual machine in the backup plan does not have manually generated restore points, only full backup is supported.
   - If all virtual machines in the backup plan have manually generated restore points, you can choose either full backup or incremental backup.

3. Click **Perform manually** to initiate the manual execution of the backup plan and automatically create a backup job for each associated virtual machine. If needed, you can stop the backup job in the CloudTower task center.
