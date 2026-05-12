---
hide_title: true
sidebar_label: Create Backup Repository
title: Create Backup Repository
id: backup_user_guide_07
---

# Create Backup Repository

A backup repository is used to store the backup files generated when backing up virtual machines. Currently, NAS servers using the `NFS 3` and `NFS 4` protocols are supported. Backup repositories are managed by the associated backup service. One backup service can be associated with multiple backup repositories, but one backup repository can be associated with only one backup service.

**Prerequisites**

The target path of the backup repository must grant read and write permissions to the backup service.

**Procedure**

1. Log in to **CloudTower**. On the **Backup and Disaster Recovery** page, select **Backup Repository**, and click **Create Backup Repository** to open the creation dialog.
2. Set the name and description of the backup repository.
3. Select the backup service associated with the backup repository. It is recommended to choose a backup service in the same data center as the backup repository.
4. Select the backup repository type, and configure the server address and storage folder path for the repository.

    - **Backup Repository Type**

       Select the protocol version supported by the NAS server. If both `NFS 3` and `NFS 4` are supported, `NFS 4` is recommended.

    - **Server**

       Enter the IP address of the server for the backup repository.

    - **Folder**

       Enter the target path for storing backup data. Make sure this path is an empty directory (system hidden files starting with `.` are allowed), and that it does not duplicate any existing backup repository in CloudTower. If the entered path does not exist, but its parent directory exists and has read and write permissions, the backup service will automatically create the path under the parent directory.
