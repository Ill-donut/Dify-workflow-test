---
hide_title: true
sidebar_label: Creating a backup repository
title: Creating a backup repository
id: backup_user_guide_07
---

# Creating a backup repository

The backup repository is used to store backup files generated when backing up virtual machines. It currently supports NAS servers that use the `NFS 3` and `NFS 4` protocols. A backup repository is managed by the associated backup service. A backup service can be associated with multiple backup repositories, but a backup repository can only be associated with one backup service.

**Prerequisite**

Ensure that the backup service has permissions to read from and write into the backup repository.

**Procedure**

1. In the left sidebar of the **Backup & DR** page in CloudTower, select **Backup repository** and click **+ Create backup repository**.
2. Enter the name and description of the backup repository.
3. Select the backup service to associate with the backup repository. It is recommended to choose a backup service located in the same data center as the backup repository.
4. Select the backup repository type and configure the server address and folder path of the repository.

   - **Backup repository type**

     Select the protocol version supported by the NAS server. If both `NFS 3` and `NFS 4` are supported, it is recommended to choose `NFS 4`.

   - **Server address**

     Enter the IP address of the backup repository server.

   - **Folder**

     Enter the destination path for storing backup data. Ensure that the path is an empty directory (system hidden files whose filenames start with `.` are allowed). The path must not overlap any existing backup repository path in CloudTower. If the specified path does not exist when its parent directory exists and has read and write permissions, the backup service will automatically create the path under the parent directory.
