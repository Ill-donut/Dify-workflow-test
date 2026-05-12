---
hide_title: true
sidebar_label: Restoring a virtual machine from a restore point
title: Restoring a virtual machine from a restore point
id: backup_user_guide_17
---

# Restoring a virtual machine from a restore point

Each time a backup plan is executed, a restore point is created for each virtual machine in the backup plan. You can restore a virtual machine from its restore point.

Virtual machines can be restored either by restoring the virtual machine in place or rebuilding the virtual machine.

- **Restore the virtual machine in place**

  Refers to restoring the virtual volume data of the source virtual machine to the state when the restore point was created without changing the configuration of the source virtual machine. Note that the restored virtual machine will replace the source virtual machine. Proceed with caution.

  > **Note**:
  >
  > In any of the following scenarios, you cannot restore the virtual machine in place:
  >
  > - The source virtual machine is in the `Suspended`, `Updating`, or `Unknown` state.
  > - The source virtual machine has been deleted, moved to the recycle bin, migrated to another cluster, or converted into a virtual machine template.
  > - The source virtual machine has added, removed, or expanded its virtual volumes after the restore point was generated.
  > - The cluster in which the source virtual machine resides has been removed from CloudTower.

- **Rebuild the virtual machine**

  Refers to creating a new virtual machine using a restore point while retaining the source virtual machine. The configuration and virtual volume data of the rebuilt virtual machine are the same as those of the source virtual machine at the time the restore point was generated.

**Precaution**

When restoring a virtual machine, if the target cluster uses an expired Trial license, the restoration will fail.

**Procedure**

1. In the left sidebar of the **Backup & DR** page in CloudTower, click **Backup plan**. Select a backup plan and click its name to enter the details page.

2. Select the virtual machine to restore. Click its name to choose a restore point based on the backup time.

3. Click **Restore**. In the pop-up **Restore virtual machine** dialog box, select the restore mode and enter configuration information as needed.

   - **Restore VM in place**

     Restores the virtual volume data of the source virtual machine to the state when the restore point was created without changing the configuration of the source virtual machine.

     > **Information**:
     >
     > If the virtual machine you want to restore in place is in the `running` state, it will be shut down before the restoration.

   - **Rebuild VM**

     Creates a new virtual machine using a restore point while retaining the source virtual machine. The configuration and virtual volume data of the rebuilt virtual machine are the same as those of the source virtual machine at the time the restore point was generated.

     - **Configure the basic information for the rebuilt virtual machine**

       | Parameter | Description                                                                                                                                                                                                                                                                              |
       | -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
       | Target cluster             | Select the target cluster to rebuild the virtual machine. You can select a SMTX OS (ELF) cluster with the same CPU architecture as the cluster of the source virtual machine.                                                         |
       | Target host                | Select the target host to rebuild the virtual machine. You can choose a specific host in the target cluster. The default is **Automatically place VM on proper host**.                                                                   |
       | New VM name                | Enter a name for the rebuilt virtual machine. Make sure that its name is different from other virtual machines in the target cluster. The default is the name of the source virtual machine at the time the restore point was generated. |

       > **Information**:
       >
       > If you select another cluster to create the virtual machine other than the cluster of the source virtual machine, ensure that the storage network of the backup service is connected to the storage network of the target cluster.

     - **Configure the storage policy for the rebuilt virtual machine**

       Select a storage policy for the rebuilt virtual machine. You can choose to keep it the same as the source virtual machine or customize a new storage policy.

       > **Information**:
       >
       > If the source virtual machine uses an erasure coding storage policy but the target cluster does not meet the prerequisite for erasure coding, the rebuilt virtual machine will not be able to use the same storage policy as the source virtual machine. In this case, you need to customize a storage policy for the rebuilt virtual machine.

     - **Configure the network mapping**

       When rebuilding a virtual machine, to ensure service continuity, you need to configure a VM network mapping for the rebuilt virtual machine.

       - If the target cluster is associated with a VPC network, the mapped network can be set to either VPC or VLAN.
       - If the target cluster does not support the VPC feature or is not associated with a VPC network, the mapped network can only be set to VLAN. In this case, if the source uses a VLAN network, it is recommended to select the same type (Access or Trunk) of VLAN network for the rebuilt virtual machine.

4. Choose whether to enable **Automatic start after restore**. This option is enabled by default.

5. Click **Restore** to start the restore job. If needed, you can stop the restore job in the CloudTower task center.
