---
hide_title: true
sidebar_label: Restore a Virtual Machine from a Recovery Point
title: Restore a Virtual Machine from a Recovery Point
id: backup_user_guide_17
---

# Restore a Virtual Machine from a Recovery Point

Each time a backup plan is executed, a recovery point is created for each virtual machine included in the backup plan. You can restore a virtual machine from a recovery point.

Virtual machines support two recovery methods: in-place recovery and recreate virtual machine.

- **In-place recovery**

  In-place recovery means restoring the original virtual volume data to the same state as when the recovery point was created, without changing the original virtual machine's configuration information. In-place recovery overwrites the original virtual machine, so use it with caution.

  >**Note**:
  >
  >In the following scenarios, in-place recovery is unavailable:
  >- The original virtual machine is in the `Paused`, `Operating`, or `Unknown` state;
  >- The original virtual machine has been deleted, moved to the recycle bin, migrated to another cluster, or converted to a virtual machine template;
  >- After the recovery point was created, the original virtual machine added, deleted, or expanded any virtual volumes;
  >- The cluster where the original virtual machine resides has been removed from CloudTower.

- **Recreate virtual machine**

  Recreate virtual machine means creating a new virtual machine from the recovery point, while keeping the original virtual machine. The configuration information and virtual volume data of the recreated virtual machine are the same as those of the original virtual machine when the recovery point was created.

**Notes**

If the license type of the target cluster for recovery is a trial license and the license has expired, virtual machine recovery fails.

**Procedure**

1. Log in to **CloudTower**. On the **Backup and Disaster Recovery** page, click **Backup Plans**, select a backup plan, and click the backup plan name to enter the backup plan details page.

2. Select the virtual machine to be restored, click the virtual machine name, and choose a recovery point by time point.

3. Click **Restore**. In the **Restore Virtual Machine** dialog box, select a recovery mode and enter configuration information as needed.

     - **In-place recovery**

       Restore the original virtual volume data to the same state as when the recovery point was created. In-place recovery does not change the virtual machine's configuration information.

       >**Description**:
       >
       >During in-place recovery, if the virtual machine is running, it will be shut down first.

     - **Recreate virtual machine**

       Create a new virtual machine from the recovery point. The virtual machine's configuration information and virtual volume data are the same as those of the original virtual machine when the recovery point was created.

       - **Set basic information for the recreated virtual machine**

         |Configuration item | Description |
         | ------ | --- |
         | Target cluster | Select the target cluster for the recreated virtual machine. You can select an SMTX OS (ELF) cluster with the same CPU architecture type. |
         | Target host | Select the target host for the recreated virtual machine. You can choose a specific host in the target cluster. The default is **Automatically schedule to a suitable host**.|
         | Recreated virtual machine name | Enter the name of the recreated virtual machine. Make sure it is different from the name of any existing virtual machine in the target cluster. The default is the name of the virtual machine when the recovery point was created. |

         >**Description**:
         >
         >If the target cluster selected for the recreated virtual machine is not the same cluster as the original virtual machine, make sure the storage network of the backup service can communicate with the storage network of the target cluster.

       - **Set the storage policy for the recreated virtual machine**

          Select the storage policy for the recreated virtual machine. You can keep it the same as the original virtual machine, or customize a new storage policy.

          >**Description**:
          >
          >If the original virtual machine uses an erasure coding storage policy, but the target cluster does not meet the prerequisites for erasure coding, the storage policy for the recreated virtual machine cannot be set to remain the same as the original virtual machine. In this case, customize a storage policy for the recreated virtual machine.

       - **Set network mapping**

         When recreating a virtual machine, to ensure services continue running normally, you must configure virtual machine network mapping for the recreated virtual machine.

         - If the target cluster is already associated with a VPC network, the mapped network type can be VPC or VLAN.
         - If the target cluster does not support the VPC feature or is not associated with a VPC network, the mapped network type can only be VLAN. In this case, it is recommended to choose a virtual machine network of the same source-side VLAN type (Access or Trunk).

4. Choose whether to **Automatically power on after recovery**. This is enabled by default.

5. Click **Restore** to submit the virtual machine recovery task. After the task is created, you can stop the recovery task in the task center.
