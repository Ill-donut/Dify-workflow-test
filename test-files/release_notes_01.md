---
title: Release Update Notes
author: SmartX Documentation Team
hide_title: true
id: release_notes_01
sidebar_label: Release Update Notes
---

# Release Update Notes

## New

### Virtualization

- Supports enabling Boost mode in SMTX OS (ELF) active-active clusters.
- Supports editing and displaying IPv6 address and gateway information for VM VLAN NICs and SR-IOV passthrough NICs.
- Supports setting QoS policies for VM CPU resources.
- Supports automatically enabling NUMA memory binding when CPU exclusivity is enabled for a VM.
- Supports attaching CCP devices provided by the Hygon HCT feature to VMs.
- VMs on Intel x86_64 and Kunpeng AArch64 platforms support automatic configuration of up to 4 virtual disk multi-queues to improve VM performance. <!-- http://jira.smartx.com/browse/ELF-6344 -->

### Block Storage

- Supports using a third-party key management service to encrypt virtual volume data at rest.
- Supports displaying the storage over-provisioning ratio.

### Network

- Supports network port connectivity detection and provides alerts for abnormal network ports.
- Supports automatic IP conflict checks when a VM IP address is created or edited.
- Supports custom access control for specific host ports and configuring an IP whitelist that is allowed to access these ports.

### Operations and Maintenance Management

- Supports removing hosts and converting host roles through CloudTower.
- Supports SR-IOV passthrough and PCI passthrough for Wangxun NICs.

### Kernel

- Supports using a virtual PTP hardware clock in AArch64 architecture clusters to ensure time synchronization between VMs and their hosts.<!-- http://jira.smartx.com/browse/SMTXOS-292 -->
- Supports SSSRAID controller cards.<!-- http://jira.smartx.com/browse/SMTXOS-328 -->
- Supports Wangxun 10 GbE NICs (txgbe series).<!-- http://jira.smartx.com/browse/SMTXOS-290 -->
- Supports Phytium S5000C series CPUs.<!-- http://jira.smartx.com/browse/SMTXOS-258 -->

## Improvements

### Virtualization

- Optimizes VM live migration to increase migration speed and reduce the impact on VM performance during migration.
- Optimizes VM HA behavior:
  - Monitors the VM operating system startup status when rebuilding a VM or restoring VM status, and triggers a VM restart when startup fails.
  - When the SMTX OS operating system is installed on an independent physical disk, the HA behavior when a host file system in the cluster becomes read-only is adjusted to restarting the host.<!-- http://jira.smartx.com/browse/ELF-7154 -->

### Block Storage

- Optimizes the granularity of snapshot COW to reduce the physical capacity occupied by volume snapshots.
- Optimizes read/write performance for non-contiguous I/O of cold data.
- Optimizes the data allocation policy to avoid performance fluctuations when a volume has a large capacity, occupying 30% to 50% of a node's write cache capacity.
- Changes the data migration alert to be disabled by default to avoid frequent triggers that disturb users.
- Adjusts throttling policies for data recovery and migration to avoid service I/O blocking caused by data recovery and migration. It also optimizes the adaptability of data recovery to different hardware conditions, making operation more stable.
- Adds checks to upgrade prechecks to prevent excessively high write cache capacity usage from causing long data recovery time and to avoid excessively long upgrade time.
- When data loss caused by consecutive physical disk or node exceptions makes data inaccessible, the system uses the temporary replica function to automatically attempt data repair.
- Optimizes the data placement policy when data flows between nodes or between the performance tier and capacity tier, improving cache hit rates for read-hot data areas.
- Optimizes the I/O interruption time during storage service configuration adjustment or cluster upgrade while a host is in maintenance mode, so that in most scenarios the I/O fluctuation perceived by VMs is less than 1 second.

### Operations and Maintenance Management

- Optimizes how host maintenance mode handles VM placement group rule conflicts and provides an option to ignore rules.
- Adds an alert item for host system partitions becoming read-only. <!-- http://jira.smartx.com/browse/OCTO-1509 -->
- Reduces unnecessary ports occupied on the management network by services running on hosts.
- Unifies the container engine on hosts to containerd.<!-- http://jira.smartx.com/browse/TUNA-6974 -->
- Adds detection and alerts for management IP connectivity of witness nodes in active-active clusters.<!-- http://jira.smartx.com/browse/TUNA-6847 -->
- Adds collection of monitoring data related to witness node network traffic in active-active clusters.<!-- http://jira.smartx.com/browse/TUNA-7242 -->
- Supports detecting NTP server connectivity during cluster deployment.<!-- http://jira.smartx.com/browse/TUNA-7242 -->
- Optimizes the network port status detection interval. CloudTower displays network port status changes within 15 seconds.<!-- http://jira.smartx.com/browse/TUNA-6952 -->
- Adds new memory error alerts.<!-- http://jira.smartx.com/browse/OCTO-1468 -->
- Adjusts the trial and subscription license expiration policy for SMTX OS clusters. After a subscription or trial license expires, created resources and enabled functions can still be used normally and I/O is not interrupted, but VMs or other resources cannot be created.

## Fixed Issues

### Virtualization

- Fixed the issue where, in very rare cases, abnormal initialization of host high availability configuration information might cause the `elf-vm-monitor` service to fail to start.<!-- http://jira.smartx.com/browse/ELF-7178 --> <!-- http://jira.smartx.com/browse/ELF-7181 -->
- Fixed the issue where, in clusters with Boost mode enabled, double writes might occur after a VM was rebuilt by HA due to a host exception.<!-- http://jira.smartx.com/browse/ELF-7136 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=6003 -->
- Fixed the issue where, after the SMTX VM Tools ISO was ejected inside the VM operating system, performing live migration might cause the VM to become uneditable while running.<!-- http://jira.smartx.com/browse/ELF-7102 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=5883 -->
- Fixed the issue where, after VM export failed, temporary files created during the export task might not be reclaimed, causing unexpected storage resource usage.<!-- http://jira.smartx.com/browse/ELF-7084 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=5885 -->
- Fixed the issue where, after editing VM IP configuration by using SMTX VM Tools, unexpected changes to the VM IP configuration might occur.<!-- http://jira.smartx.com/browse/ELF-7009 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=5817 -->
- Fixed the issue where, when rolling back a VM from a snapshot, rollback might fail because the UUID of the snapshot did not match that of the virtual volume mounted to the VM at the same path.<!-- http://jira.smartx.com/browse/ELF-6967 -->
- Fixed the issue where long-term unavailability of cluster storage, for example due to cluster license expiration, might cause abnormal HA behavior.<!-- http://jira.smartx.com/browse/ELF-6950 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=5668 -->
- Fixed the issue where memory usage of Windows VMs with SMTX VM Tools installed might be incorrectly displayed as 100%.<!-- http://jira.smartx.com/browse/ELF-6935 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=2608 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=4897 -->
- Fixed the issue where VMs running the RHEL operating system might fail to install SMTX VM Tools because of service conflicts.<!-- http://jira.smartx.com/browse/ELF-6923 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=5593 -->
- Fixed the issue where average latency data in VM storage resource monitoring was inaccurate.<!-- http://jira.smartx.com/browse/ELF-6905 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=5637 -->
- Fixed the issue where exporting a VM might fail because the VM name contained special characters.<!-- http://jira.smartx.com/browse/ELF-6886 -->
- Fixed the issue where, after VM scheduling failed, the abnormal scheduling cache was not cleared within the expected time, which might cause unexpected host memory usage.<!-- http://jira.smartx.com/browse/ELF-6733 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=5125 -->
- Fixed the issue where disks using the IDE bus in clusters with Boost mode enabled were not protected by disk locks.<!-- http://jira.smartx.com/browse/ELF-6723 -->
- Fixed the issue where the default network segment of system services might conflict with system networks or VM networks.<!-- http://jira.smartx.com/browse/ELF-6646 -->
- Fixed the issue where, after VMs running Debian or Ubuntu were initialized by using cloud-init, the VM IP information collected through SMTX VM Tools might be incorrect.<!-- http://jira.smartx.com/browse/ELF-6609 -->
- Fixed the issue where, during batch VM migration, selecting automatic scheduling to a suitable host might cause some VMs to still be migrated back to the original host.<!-- http://jira.smartx.com/browse/ELF-6545 -->
- Fixed the issue where VMs using E1000-mode NICs might have a low-probability network interruption.<!-- http://jira.smartx.com/browse/ELF-6451 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=3922 -->
- Fixed the issue where Windows VMs using disks whose bus type was IDE might crash.<!-- http://jira.smartx.com/browse/ELF-5997 -->
- Fixed the issue where, under a specific file system partition mount order, creating a file-system-consistent snapshot for a VM might cause the VM to become unresponsive.<!-- http://jira.smartx.com/browse/ELF-5862 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=3155 -->
- Fixed the issue where restarting or forcibly restarting a VM might cause the ISO mounted to the VM through CD-ROM to fail to eject normally.<!-- http://jira.smartx.com/browse/ELF-2554 -->
- Fixed the issue where, due to a kernel issue, VM CPU compatibility could not be set to IceLake in Intel x86_64 architecture clusters running the openEuler operating system.<!-- http://jira.smartx.com/browse/SMTXOS-294 -->

### Block Storage

- Fixed the issue where, in very rare cases, the I/O aggregation service might cause write I/O to fail to return.
- Fixed the issue where, when `zbs-taskd` could not connect to ZooKeeper due to network reasons, the main thread might be blocked, causing `zbs-taskd` to be unable to provide services.
- Fixed the issue where the exclusive physical capacity value of consistency snapshot groups was inaccurate.
- Fixed the issue where creating a snapshot during I/O had an extremely low probability of causing data inconsistency.
- Fixed the issue where, in iSCSI mode, errors might occur when the `blkdiscard` command and `iSCSI rescan` were executed at the same time.
- Fixed the issue where sending small packets to the RPC server at specific intervals during vulnerability scanning might cause high I/O latency.
- Fixed the issue where, after a snapshot was created for a persistent cache volume, the data might not remain in persistent cache.
- Fixed the issue where, when only some nodes in a cluster reserved cache space for persistent cache volumes, persistent cache volume data could not be balanced normally.
- Improved long-tail latency caused by high latency on the physical disk to which the cache partition belongs.
- Fixed the issue where volumes of VM templates might repeatedly migrate data between nodes.
- Fixed the issue where cluster upgrades from SMTX OS 4.0.x might fail with low probability due to abnormal space calculation.
- Fixed the issue where, after the initial I/O of a virtual volume continued for 6 hours, one-time performance fluctuation might occur because of localization awareness.
- Fixed the issue where a small amount of UNMAP I/O generated during cross-cluster live migration was not synchronized to the target side in time.

### Network

- Fixed the issue where, after the cluster management IP was modified, a host could not be specified when a VM was powered on. <!-- https://cs.smartx.com/knowledgebase/detail?id=4700 --> <!-- http://jira.smartx.com/browse/ER-878 -->
- Fixed the issue where, when deploying a cluster or creating a new virtual distributed switch, after multiple physical network ports were associated with a host, the LLDP of the physical NIC and the internal interface communicated externally at the same time, causing frequent MAC address conflict alerts on the physical switch. <!-- https://cs.smartx.com/knowledgebase/detail?id=5186 --> <!-- http://jira.smartx.com/browse/ER-936 -->
- Fixed the issue where, after an isolated network port recovered, it could not automatically rejoin port bonding. <!-- https://cs.smartx.com/knowledgebase/detail?id=5222 --> <!-- http://jira.smartx.com/browse/ER-942 -->

### Operations and Maintenance Management

- Fixed the issue where an advanced monitoring VM might incorrectly trigger that the alert function was unavailable.<!-- http://jira.smartx.com/browse/OCTO-1526 -->
- Fixed the issue where, after node replacement or node expansion, the IQN parameter was missing from the `zbs-metad` service configuration file.<!-- http://jira.smartx.com/browse/TUNA-7321 -->
- Fixed the issue where `zbs-chunkd journal` partitions might fail to be identified during cluster upgrade.<!-- http://jira.smartx.com/browse/TUNA-6701 -->
- Fixed the issue where, because the upgrade tool unexpectedly failed to obtain the actual CPU vendor, uploading upgrade files or distributing upgrade files through the upgrade center failed. <!-- http://jira.smartx.com/browse/TUNA-5434 -->
- Fixed the issue where duplicate items in the configuration file caused host removal through the command line to fail. <!-- http://jira.smartx.com/browse/TUNA-7407 -->
- Fixed the issue where the node where `ZooKeeper Leader` was located could not retry role conversion through the command line. <!-- http://jira.smartx.com/browse/TUNA-7092 -->
- Fixed the issue where data interruption might occur in the host monitoring metric CPU usage. <!-- http://jira.smartx.com/browse/TUNA-7206 -->
- Fixed the issue where a host entered maintenance mode successfully but the task was displayed as failed. <!-- http://jira.smartx.com/browse/TUNA-6893 -->
- Fixed the issue where abnormal SNMP requests caused the cluster to frequently trigger the "cluster monitoring and alerting service cannot work normally" alert. <!-- http://jira.smartx.com/browse/OCTO-1497 -->
- Fixed the issue where updating the SR-IOV configuration of any Solarflare NIC on a node might cause the change to be applied to all other Solarflare NICs. <!-- http://jira.smartx.com/browse/TUNA-7096 -->
- Fixed the issue where the cluster could not alert normally because the time of advanced monitoring lagged behind the cluster. <!-- http://jira.smartx.com/browse/OCTO-1503 -->
- Fixed the issue where clusters upgraded from 3.0.11 and earlier could not display the failfast flag in RAID details.
- Fixed the issue where cluster upgrade failed after a cluster that had not enabled the active-active feature was converted to an active-active cluster, or after the witness node was rebuilt in an active-active cluster.

### Kernel

- Fixed the issue where CPU usage surged when the PTP feature was enabled for QLogic NICs. <!-- http://jira.smartx.com/browse/SMTXOS-284 -->
- Fixed the issue where Guest OS clock synchronization was abnormal in CPU hot-add scenarios. <!-- http://jira.smartx.com/browse/SMTXOS-222 -->
- Fixed security vulnerability CVE-2019-3016. <!-- http://jira.smartx.com/browse/SMTXOS-300 -->
- Fixed the issue where PCIe devices that supported only 32-bit MSI could not work. <!-- http://jira.smartx.com/browse/SMTXOS-306 -->
- Fixed Hygon CPU defect errata 1096. <!-- http://jira.smartx.com/browse/SMTXOS-312 -->
- Fixed the issue where data inconsistency caused block-layer I/O to hang. <!-- http://jira.smartx.com/browse/SMTXOS-316 -->
- Fixed the issue where online capacity reset of the ext4 file system might damage data. <!-- http://jira.smartx.com/browse/SMTXOS-317 -->
- Fixed the issue where the memory subsystem might be damaged. <!-- http://jira.smartx.com/browse/SMTXOS-318 -->
- Fixed the issue where buffer I/O data might be inconsistent. <!-- http://jira.smartx.com/browse/SMTXOS-319 -->
- Fixed the issue where a KVM asynchronous page fault exception caused a hang. <!-- http://jira.smartx.com/browse/SMTXOS-320 -->
- Fixed the issue where a hang might occur in the memory allocation path. <!-- http://jira.smartx.com/browse/SMTXOS-321 -->
- Fixed the issue where passing through NVIDIA A-series GPUs to Windows VMs caused the host to crash and restart. <!-- http://jira.smartx.com/browse/SMTXOS-323 -->
- Fixed a bug in VM page fault exception handling under Boost mode on the AArch64 architecture, resolving host crashes caused by the bug.<!-- http://jira.smartx.com/browse/SMTXOS-108 -->
