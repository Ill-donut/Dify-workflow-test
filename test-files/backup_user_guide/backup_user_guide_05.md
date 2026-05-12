---
hide_title: true
sidebar_label: Associating clusters
title: Associating clusters
id: backup_user_guide_05
---

# Associating clusters

After deploying a backup service, you need to associate it with the SMTX OS (ELF) clusters hosting the virtual machines to be protected.

- One backup service can be associated with multiple SMTX OS (ELF) clusters, and one SMTX OS (ELF) cluster can also be associated with multiple backup services.
- The backup service can only be associated with clusters whose connection status with CloudTower is `Connected`.

**Procedure**

1. In the left sidebar of the **Backup & DR** page in CloudTower, click **Settings**.
2. In the pop-up dialog box, select a deployed backup service and click **Associated cluster**.
3. Click **Edit association**. In the pop-up dialog box, add one or more SMTX OS (ELF) clusters.
4. Click **Save** to complete the association between the backup service and the cluster.

After association, you can view the list of clusters associated with the backup service on the **Associated cluster** dialog box.

| **Parameter**              | **Description**                                                                   |
| -------------------------- | --------------------------------------------------------------------------------- |
| Cluster name               | The name of the cluster associated with the backup service. |
| Connection with CloudTower | The connection status between the cluster and CloudTower. |
| Cluster IP                 | The IP address used when associating the cluster with CloudTower. |
| Data center                | The data center to which the cluster belongs in CloudTower. |
