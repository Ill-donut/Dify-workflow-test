---
hide_title: true
sidebar_label: Restoring a backup repository
title: Restoring a backup repository
id: backup_user_guide_24
---
# Restoring a backup repository

If the backup service is in the `Abnormal` state and cannot be recovered, or if you have deployed the backup service in a new environment, you can use the **Restore backup repository** feature to let the new backup service take over the previous backup repository, quickly rebuild backup plans and associate historical restore points with the existing data and metadata in the repository.

**Scenario**

Restoring a backup repository applies to the following scenarios:

- Backup service failure: The backup service virtual machine cannot be recovered due to hardware failure, data corruption, or other reasons, thus requiring a new backup service to be deployed.

- CloudTower failure: CloudTower needs to be redeployed due to failure, while the previous backup management capabilities also need to be restored.

**Prerequisite**

- The backup service virtual machine previously associated with the backup repository to be restored is either in the `Shutdown` state or is unavailable. Otherwise, data conflicts may occur if multiple backup services access the same repository simultaneously.

- The new backup service has been deployed and is running properly.

- The version of the previous backup service associated with the backup repository must be 2.3.0 or later, and the version of the newly associated backup service must not be earlier than that of the previous backup service. 

- The backup network of the new backup service must be able to access the backup repository to be restored.

**Procedure**

1. In the left sidebar of the **Backup & DR** page in CloudTower, select **Backup repository**. Click **...** on the upper-right corner of the page and select **Restore backup repository**.

2. In the pop-up dialog box, enter the name and description of the restored repository. They can be customized and differ from the original ones.

3. Select a backup service to be associated with the restored repository. You need to select a backup service of version 2.3.0 or later, which must not be earlier than the previously associated backup service.

4. Select the backup repository type, and enter the server address and the path of the folder to mount the restored repository accordingly.

    - **Backup repository type**

      Select the NFS protocol version used by the repository (`NFS 3` or `NFS 4`). You can choose either based on the current environment. It does not need to be consistent with the previous configuration.

    - **Server**

      Enter the IP address of the backup repository server. **It must be exactly identical to the previous repository server address**.

    - **Folder**

      Enter the target path for storing backup data. **It must be exactly identical to the previous repository path**.

5. Click **Restore** to start the restore operation.

After the backup repository restore is complete, you can navigate to the **Backup plan** page to view the restored backup plans.
