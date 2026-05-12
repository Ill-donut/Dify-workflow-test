---
hide_title: true
sidebar_label: Deleting a backup plan
title: Deleting a backup plan
id: backup_user_guide_16
---

# Deleting a backup plan

1. In the left sidebar of the **Backup & DR** page in CloudTower, select **Backup plan**. In the list, select the target backup plan to delete. Click **...** on the right side of the list or its details page and select **Delete**.

2. In the pop-up **Delete backup plan** dialog box, choose whether to delete the restore points of all virtual machines in the backup plan when you delete the backup plan.

   - If the restore points to be deleted are associated with backup or restore jobs in progress, selecting **Remove restore points** is not allowed.
   - If you choose to **Keep restore points**, the corresponding backup files will continue to be stored in the backup repository.

3. Click **Delete**.
