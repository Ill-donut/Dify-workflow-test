---
hide_title: true
sidebar_label: Restore Backup Repository
title: Restore Backup Repository
id: backup_user_guide_24
---
# Restore Backup Repository

When the backup service becomes abnormal and cannot be recovered, or when you redeploy the backup service in a new environment, you can use the **Restore Backup Repository** feature to let a new backup service take over the original backup repository, use the existing data and metadata in the repository, and quickly rebuild backup plans and associate historical restore points.

**Applicable Scenarios**

Restore Backup Repository is suitable for the following scenarios:

- Backup service failure: the backup service VM cannot be recovered due to hardware failure, data corruption, or other reasons, and a new backup service needs to be deployed.

- CloudTower failure: CloudTower fails and needs to be redeployed, while the original backup management functions also need to be restored.

**Prerequisites**

- The backup service VM previously associated with the backup repository to be restored has been shut down or is unavailable, to avoid data conflicts caused by multiple backup services accessing the same repository at the same time;

- The new backup service has been deployed and its service status is normal;

- The version of the original backup service associated with the backup repository must be 2.3.0 or later, and the version of the newly associated backup service must not be lower than the original backup service version;

- The backup network of the new backup service must be able to access the backup repository to be restored.

**Procedure**

1. Log in to **CloudTower**. On the **Backup and Disaster Recovery** page, select **Backup Repositories**, click **...** in the upper-right corner of the page, and choose **Restore Backup Repository**.

2. In the pop-up window, enter the name and description of the restored repository. The name and description are customizable and can be different from the original name and description.

3. Select the backup service to be newly associated with the repository. The version must be no lower than 2.3.0 and no lower than the version of the originally associated backup service.

4. Select the backup repository type, and enter the server address and storage folder path of the repository.

    - **Backup repository type**

       Select the NFS protocol version used by the repository (`NFS 3` or `NFS 4`). You can choose based on the current environment; it does not need to be consistent with the original configuration.

    - **Server**

       Enter the IP address of the server for the backup repository. It **must be exactly the same as the original repository address**.

    - **Folder**

       Enter the target path for storing backup data. It **must be exactly the same as the original repository path**.

5. Click **Restore** to start the restore operation.

After the restoration is complete, you can go to the **Backup Plans** page to view the restored backup plans.
