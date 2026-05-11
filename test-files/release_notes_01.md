---
title: What's in this release
author: SmartX documentation team
hide_title: true
id: release_notes_01
sidebar_label: What's in this release
---

# What's in this release

## What's new

### Virtualization

- Supports enabling Boost mode in SMTX OS (ELF) active-active clusters.
- Allows editing and displaying the IPv6 address and gateway information for VLAN NICs and SR-IOV passthrough NICs on virtual machines.
- Supports configuring a QoS policy for virtual machine CPU resources.
- Automatically enables NUMA memory binding for virtual machines with CPU exclusive enabled.
- Supports mounting CCP devices provided by the Hygon HCT feature on virtual machines.
- Supports automatically configuring a maximum of 4 virtual disk multi-queues for virtual machines on Intel x86_64 and Kunpeng AArch64 platforms to improve virtual machine performance. <!-- http://jira.smartx.com/browse/ELF-6344 -->

### Block storage

- Supports encrypting virtual volume data at rest using third-party Key Management Services (KMS).
- Displays the storage overprovisioning ratio.

### Networking

- Provides port connectivity test with alerts for abnormal ports.
- Automatically detects IP conflicts when creating or editing virtual machine IP addresses.
- Supports customizing access control for host-specific ports and configuring IP allowlists to allow access to these ports.

### Operations and management

- Allows removing hosts and converting the host role on CloudTower.
- Supports SR-IOV passthrough and PCI passthrough for Netswift NICs.

### Kernel

- Supports virtual PTP hardware clock in clusters with the AArch64 architecture to ensure time synchronization between virtual machines and hosts where they reside. <!-- http://jira.smartx.com/browse/SMTXOS-292 -->
- Supports SSSRAID controller cards. <!-- http://jira.smartx.com/browse/SMTXOS-328 -->
- Supports Netswift 10GbE NICs of the txgbe series. <!-- http://jira.smartx.com/browse/SMTXOS-290 -->
- Supports Phytium S5000C CPUs. <!-- http://jira.smartx.com/browse/SMTXOS-258 -->

## Improvements

### Virtualization

- Optimizes virtual machine hot migration by improving migration speed and reducing performance impact during the migration process.
- Improves virtual machine HA behavior in the following ways:
  - Monitors the virtual machine operating system booting status during virtual machine rebuild or status recovery, and triggers reboot if the booting fails.
  - When SMTX OS is installed on a dedicated physical disk, the host HA behavior is adjusted to reboot when the file system encounters read-only exceptions.<!-- http://jira.smartx.com/browse/ELF-7154 -->

### Block storage

- Optimizes the granularity of snapshot COW (Copy-on-Write) to reduce the physical capacity used by volume snapshots.
- Improves read and write performance for non-contiguous I/O for cold data.
- Optimizes the data allocation policy to prevent performance fluctuations when the volume size occupies 30% - 50% of the node write cache capacity.
- Updates the data migration alert to be disabled by default to avoid frequent triggers that might disturb users.
- Adjusts the bandwidth limits for data recovery and migration to prevent I/O blockage,  and optimizes data recovery for better adaptation to diﬀerent hardware conditions to achieve more stable operations.
- Adds pre-upgrade checks to prevent long data recovery time caused by excessive write cache usage, thus avoiding prolonged upgrade duration.
- When data becomes inaccessible due to data loss caused by continuous physical disk or node failures, the temporary replica feature will automatically initiate data recovery.
- Optimizes the data placement policy for data movements between nodes or between performance and capacity tiers to improve cache hit rates in reading hotspot areas.
- Shortens I/O interruption when updating storage service configuration during host maintenance or performing cluster upgrades, ensuring that I/O fluctuation perceived by virtual machines is less than 1 second in most scenarios.

### Operations and management

- Provides an option for host maintenance mode to ignore specified VM placement group rules and avoid rule conflicts.
- Adds alerts for host system partition read-only errors.  <!-- http://jira.smartx.com/browse/OCTO-1509 -->
- Frees up unnecessary management network ports used by services running on a host.
- Unifies container engines on a host to `containerd`. <!-- http://jira.smartx.com/browse/TUNA-6974 -->
- Tests and alerts management IP connectivity issues for witness nodes in active-active clusters.<!-- http://jira.smartx.com/browse/TUNA-6847 -->
- Collects monitoring data for witness node traﬃc in active-active clusters. <!-- http://jira.smartx.com/browse/TUNA-7242 -->
- Tests NTP server connectivity during cluster deployment. <!-- http://jira.smartx.com/browse/TUNA-7242 -->
- Optimizes the port status detection frequency to update the port status display within 15 seconds on CloudTower.<!-- http://jira.smartx.com/browse/TUNA-6952 -->
- Adds new memory error alerts. <!-- http://jira.smartx.com/browse/OCTO-1468 -->
- Adjusts the Trial and Subscription license expiration policies for SMTX OS clusters. After expiration, existing resources and enabled features will remain functional, and I/O will be unaﬀected, but new virtual machines or resources cannot be created.

## Resolved issues

### Virtualization

- The `elf-vm-monitor` service might fail to start due to an initialization error in host high availability configuration under rare circumstances. The issue has been resolved in this release. <!-- http://jira.smartx.com/browse/ELF-7178 --> <!-- http://jira.smartx.com/browse/ELF-7181 -->
- In clusters with Boost mode enabled, double-write issues might occur after a virtual machine was rebuilt via HA due to host failures. The issue has been resolved in this release. <!-- http://jira.smartx.com/browse/ELF-7136 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=6003 -->
- After ejecting the SMTX VMTools ISO image from the virtual machine operating system and performing a hot migration, the configuration of that virtual machine might not be edited while the virtual machine is in the `Running` state. The issue has been resolved in this release. <!-- http://jira.smartx.com/browse/ELF-7102 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=5883 -->
- The temporary files from failed virtual machine export tasks were not properly cleaned up, which might lead to unexpected storage usage. The issue has been resolved in this release. <!-- http://jira.smartx.com/browse/ELF-7084 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=5885 -->
- Editing virtual machine IP configurations via SMTX VMTools might cause unintended IP configuration changes. The issue has been resolved in this release.<!-- http://jira.smartx.com/browse/ELF-7009 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=5817 -->
- When rolling back a virtual machine using snapshots, the rollback might fail due to a mismatch between the UUID of the snapshot and the virtual volume mounted on the virtual machine with the same path. The issue has been resolved in this release.<!-- http://jira.smartx.com/browse/ELF-6967 -->
- The extended cluster storage unavailability (e.g., due to expired licenses) could lead to HA abnormalities. The issue has been resolved in this release. <!-- http://jira.smartx.com/browse/ELF-6950 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=5668 -->
- The memory usage for Windows virtual machines with SMTX VMTools installed might incorrectly display as 100%. The issue has been resolved in this release. <!-- http://jira.smartx.com/browse/ELF-6935 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=2608 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=4897 -->
- When installing SMTX VMTools on virtual machines with the RHEL operating system, service conflicts might cause the installation to fail. The issue has been resolved in this release. <!-- http://jira.smartx.com/browse/ELF-6923 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=5593 -->
- The average latency data in virtual machine storage resource monitoring was inaccurate. The issue has been resolved in this release.<!-- http://jira.smartx.com/browse/ELF-6905 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=5637 -->
- Exporting a virtual machine might fail because the virtual machine name contained special characters. The issue has been resolved in this release. <!-- http://jira.smartx.com/browse/ELF-6886 -->
- The failed virtual machine scheduling caused unexpected host memory usage due to the delay in clearing failed scheduling caches. The issue has been resolved in this release.<!-- http://jira.smartx.com/browse/ELF-6733 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=5125 -->
- In clusters with Boost mode enabled, the disks using the IDE bus were not protected by disk lock. The issue has been resolved in this release. <!-- http://jira.smartx.com/browse/ELF-6723 -->
- There might be conflicts between the default network segment of the system service and system networks or VM networks. The issue has been resolved in this release. <!-- http://jira.smartx.com/browse/ELF-6646 -->
- After initializing a virtual machine with Debian or Ubuntu operating system with cloud-init, the virtual machine IP acquired via SMTX VMTools might be wrong. The issue has been resolved in this release. <!-- http://jira.smartx.com/browse/ELF-6609 -->
- When migrating virtual machines in batches, selecting `Automatically place VM on proper host` might result in certain virtual machines being migrated back to their original hosts. The issue has been resolved in this release. <!-- http://jira.smartx.com/browse/ELF-6545 -->
- Virtual machines with E1000 NICs had a low probability of experiencing network interruptions. The issue has been resolved in this release. <!-- http://jira.smartx.com/browse/ELF-6451 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=3922 -->
- The disk with the IDE bus type on a Windows virtual machine might cause virtual machine crashes. The issue has been resolved in this release.<!-- http://jira.smartx.com/browse/ELF-5997 -->
- Creating file-system consistent snapshots under specific file system partition mount orders could cause the virtual machine to become unresponsive. The issue has been resolved in this release.<!-- http://jira.smartx.com/browse/ELF-5862 --> <!-- https://cs.smartx.com/knowledgebase/detail?id=3155 -->
- Rebooting or forcibly rebooting a virtual machine might prevent its ISO file mounted via CD-ROM from being ejected properly. The issue has been resolved in this release. <!-- http://jira.smartx.com/browse/ELF-2554 -->
- For clusters running the openEuler operating system with the Intel x86_64 architecture, the virtual machine CPU compatibility could not be set to IceLake due to a kernel issue. The issue has been resolved in this release. <!-- http://jira.smartx.com/browse/SMTXOS-294 -->

### Block storage

- The I/O aggregation service could cause write I/O requests to fail to return in rare cases. The issue has been resolved in this release.
- When `zbs-taskd` failed to connect to ZooKeeper due to network issues, the main thread could become blocked, rendering `zbs-taskd` unable to provide services. The issue has been resolved in this release.
- The calculation of exclusive physical capacity for consistency snapshot groups was inaccurate. The issue has been resolved in this release.
- When creating a snapshot during I/O operations, the data had an extremely low probability to be inconsistent. The issue has been resolved in this release.
- In iSCSI mode, executing the `blkdiscard` command concurrently with `iSCSI rescan` could lead to errors. The issue has been resolved in this release.
- Sending small packets to the RPC server at specific intervals during vulnerability scans could cause high I/O latency. The issue has been resolved in this release.
- After creating a snapshot for a pinned volume, the data might fail to remain pinned in the cache. The issue has been resolved in this release.
- When only certain nodes in a cluster had reserved cache for pinned volumes, the volume data could not be balanced properly. The issue has been resolved in this release.
- High latency on the physical disk hosting the cache partition could result in long-tail delays. The issue has been resolved in this release.
- Data in VM template volumes could migrate repeatedly between nodes. The issue has been resolved in this release.
- Upgrades from SMTX OS 4.0.x could occasionally fail due to errors in space calculation. The issue has been resolved in this release.
- After 6 hours of continuous initial I/O activity, virtual volumes could experience a one-time performance fluctuation due to localization awareness. The issue has been resolved in this release.
- A small amount of UNMAP I/O data generated during virtual machine cross-cluster hot migration was not synchronized to the target cluster timely. The issue has been resolved in this release.

### Networking

- After modifying the cluster management IP addresses, virtual machines failed to be specified a host during the booting process. The issue has been resolved in this release. <!-- https://cs.smartx.com/knowledgebase/detail?id=4700 --> <!-- http://jira.smartx.com/browse/ER-878 -->
- When deploying a cluster or creating a new virtual distributed switch, multiple physical NICs on the host triggered frequent MAC address conflict alerts on the physical switch, as both the NIC LLDP and the internal interface communicated with the external client simultaneously. The issue has been resolved in this release. <!-- https://cs.smartx.com/knowledgebase/detail?id=5186 --> <!-- http://jira.smartx.com/browse/ER-936 -->
- After a network port was quarantined and then recovered, it failed to automatically rejoin port bonding. The issue has been resolved in this release. <!-- https://cs.smartx.com/knowledgebase/detail?id=5222 --> <!-- http://jira.smartx.com/browse/ER-942 -->

### Operations and management

- The advanced monitoring virtual machine might mistakenly trigger "The alert-sending function is in an abnormal state" alert. The issue has been resolved in this release. <!-- http://jira.smartx.com/browse/OCTO-1526 -->
- After replacing or scaling a node, the `zbs-metad` service configuration file lacked the IQN parameter. The issue has been resolved in this release. <!-- http://jira.smartx.com/browse/TUNA-7321 -->
- The `zbs-chunkd` journal partition might fail to be identified during a cluster upgrade. The issue has been resolved in this release. <!-- http://jira.smartx.com/browse/TUNA-6701 -->
- The upgrade tool unexpectedly failed to retrieve the actual CPU vendor, causing failures in uploading upgrade files or distributing them via the upgrade center. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/TUNA-5434 -->
- Duplicate entries in the configuration file caused failures in removing a host via commands. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/TUNA-7407 -->
- The node where `ZooKeeper Leader` resides could not retry role conversion via commands. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/TUNA-7092 -->
- The host CPU usage monitoring metric might experience data outage. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/TUNA-7206 -->
- A host could successfully enter maintenance mode but the task was displayed as failed. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/TUNA-6893 -->
- Abnormal SNMP requests caused the cluster to frequently trigger "Cluster alerting services do not work" alert. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/OCTO-1497 -->
- Updating the SR-IOV configuration of any Solarflare NIC on a node might mistakenly apply the changes to all remaining Solarflare NICs on that node. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/TUNA-7096 -->
- The cluster could not generate alerts properly because the advanced monitoring time lagged behind the cluster time. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/OCTO-1503 -->
- Clusters upgraded from version 3.0.11 or earlier could not display the failfast flag in RAID details. The issue has been resolved in this release.
- After enabling the active-active feature for a cluster, or rebuilding the witness node in an active-active cluster, the cluster upgrade failed. The issue has been resolved in this release.

### Kernel

- Enabling PTP on QLogic NICs caused a sudden spike in CPU usage. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/SMTXOS-284 -->
- The guest operating system clock synchronization failed when hot adding CPUs. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/SMTXOS-222 -->
- The system had a security vulnerability CVE-2019-3016. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/SMTXOS-300 -->
- PCIe devices that only supported 32-bit MSI failed to function. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/SMTXOS-306 -->
- The Hygon CPU had errata 1096. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/SMTXOS-312 -->
- Data inconsistency caused block layer I/O deadlock. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/SMTXOS-316 -->
- Resetting the capacity of the ext4 file system online might result in data corruption. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/SMTXOS-317 -->
- A potential issue might cause memory subsystem corruption. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/SMTXOS-318 -->
- The buﬀer I/O data might be inconsistent. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/SMTXOS-319 -->
- The KVM asynchronous page fault caused system deadlock. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/SMTXOS-320 -->
- A deadlock could occur in the memory allocation path. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/SMTXOS-321 -->
- Passing through NVIDIA A-series GPUs to Windows virtual machines caused the host to crash and reboot. The issue has been resolved in this release.  <!-- http://jira.smartx.com/browse/SMTXOS-323 -->
- For clusters with the AArch64 architecture, if Boost mode was enabled, the bugs in handling virtual machine page fault would cause the host to crash. The issue has been resolved in this release. <!-- http://jira.smartx.com/browse/SMTXOS-108 -->
