---
hide_title: true
sidebar_label: Add Associated Cluster
title: Add Associated Cluster
id: backup_user_guide_05
---

# Add Associated Cluster

After the backup service is deployed, associate the backup service with the SMTX OS (ELF) cluster where the virtual machines to be protected are located.

- One backup service can be associated with multiple SMTX OS (ELF) clusters, and one SMTX OS (ELF) cluster can also be associated with multiple backup services.
- A backup service can only be associated with clusters whose connection status with CloudTower is `Connected`.

**Procedure**

1. Log in to CloudTower, and in the **Backup and Disaster Recovery** page, click **Settings**.
2. In the pop-up window, select a deployed backup service, and click **SMTX OS Cluster Association**.
3. Click **Edit Cluster Association**. In the operation window that appears, add one or more SMTX OS (ELF) clusters.
4. Click **Save** to complete the association between the backup service and the clusters.

After the association is complete, you can view the list of clusters associated with the backup service on the **SMTX OS Cluster Association** page.

| Parameter | Description |
| --- | --- |
| Cluster Name | The name of the cluster associated with the backup service. |
| Connection Status with CloudTower | The connection status between the cluster and CloudTower. |
| Cluster IP | The IP address used when the cluster is associated with CloudTower. |
| Data Center | The data center to which the cluster belongs in CloudTower. |
