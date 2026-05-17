---
title: Supported components and features
sidebar_label: Supported components and features
hide_title: true
id: whitepaper_elf_11
---

# Supported components and features

## Virtual machine

Virtual machines are the core of ELF, providing virtual computing services to users. ELF uses KVM as the foundation, with libvirt assisting in virtual machine construction and management. To ensure virtual machines benefit from high reliability, high availability, and other cluster features, virtual machine HA, migration, and auto-scheduling capabilities are also included.

The main features provided for virtual machines include:

- Create (in batches)
- Start (in batches)
- Shut down (in batches)
- Force shut down (in batches)
- Restart (in batches)
- Force restart (in batches)
- Suspend (in batches)
- Resume (in batches)
- Migrate (in batches)
- Delete (in batches)
- Clone

## Virtual machine auto-scheduling

Virtual machine auto-scheduling is an important component of virtual machine management. Its purpose is to automatically schedule the creation or startup of virtual machines based on cluster usage, to achieve a balanced distribution of virtual machines within the cluster.

In ELF, VM Scheduler implements the scheduling algorithm in conjunction with Job Center to complete virtual machine auto-scheduling. VM Scheduler is deployed on 3 or 5 nodes as needed, with exactly one instance in the **Active** state; it switches together with the ZBS-Meta Leader, always residing on the same node as the ZBS-Meta Leader. VM Scheduler also uses MongoDB to store node resource data under processing. When VM Scheduler is unavailable, all resource-allocation functions for virtual machines, such as creation, start, and migration, become unavailable.

VM Scheduler uses a filter chain to screen nodes, then calculates a score for each eligible node, and finally selects the optimal node as the scheduling target. The process is shown in the diagram below:

![](../assets/elf-white-paper/image7.png)

The filter chain consists of multiple filters that screen available hosts. The main filtering functions are:

1. Filter out nodes that do not meet the hard physical requirements of the virtual machine

   Nodes are filtered out based on hard criteria such as: whether the node is alive, network environment configuration, CPU compatibility, whether the total memory allocated to virtual machines on a single node exceeds physical memory, and whether host maintenance mode is enabled.

2. Filter out nodes that do not satisfy VM placement group policy requirements

   A VM placement group policy is a set of rules governing where virtual machines are placed. Once enabled, it becomes a mandatory policy with higher priority than the criteria above. ELF currently supports three types of placement group policies:

   - Must be placed/not placed on selected hosts: In an active-active environment, when this policy and HA are both enabled, it is recommended to select at least one host in each availability zone. Otherwise, business continuity may be interrupted. If all selected hosts are in the primary availability zone and the entire primary availability zone becomes unavailable, HA cannot automatically migrate virtual machines to hosts in the secondary availability zone due to the "must" constraint.
   - Prioritized to be placed/not placed on selected hosts: In an active-active environment, when this policy and HA are both enabled, it is not recommended to select hosts in the secondary availability zone, so that virtual machines preferentially migrate to hosts in the primary availability zone. Even if the entire primary availability zone becomes unavailable, because this is a "preferred" rather than "must" policy, the system will still automatically migrate virtual machines to the secondary availability zone, ensuring business continuity.
   - Prioritized/must be placed on the same/different hosts: While the above two types govern the placement relationship between virtual machines and hosts, this type governs the placement relationship between virtual machines and other virtual machines.

   In an active-active cluster, you can also configure availability zone placement policies. However, for a single VM-host placement group policy, you can only select either `host` or `availability zone` for hosting the virtual machines, not both simultaneously. ELF currently supports the following availability zone placement rules:

   - Member virtual machines must be placed in the primary or secondary availability zone
   - Member virtual machines are prioritized to be placed in the primary or secondary availability zone

3. In an active-active environment, when no availability zone placement group policy is configured, nodes in the primary availability zone are prioritized

   If available nodes exist in the primary availability zone, they are prioritized. Nodes in the secondary availability zone are selected only when no available nodes exist in the primary availability zone.

4. Select nodes that support CPU pinning for the virtual machine, based on the scheduling scenario

   - If the scheduling scenario is user-initiated (for example, power-on or hot migration), the scheduler selects nodes whose available exclusive CPU count supports CPU pinning for the virtual machine.
   - If the scheduling scenario is virtual machine HA, the scheduler preferentially selects nodes whose available exclusive CPU count supports CPU pinning. If no such nodes exist, the scheduler does not filter out nodes, and CPU pinning will not be enabled after the virtual machine is rebuilt.

After filtering, if more than one node remains, the nodes are scored and ranked using the following algorithm based on whether the virtual machine is currently in the **Running** state:

- When the virtual machine is in the **Running** state:

  - CPU score = (Total vCPUs of **Running** virtual machines on the host + vCPUs required by the current virtual machine) / (Total vCPUs allocated across the cluster + vCPUs required by the current virtual machine)

  - Memory score = (Total memory of **Running** virtual machines on the host + Memory required by the current virtual machine) / Total physical memory of the node

  - Host score = (CPU score + Memory score) / 2

- When the virtual machine is in the **Shutdown** state:

   - CPU score = (Total vCPUs of all virtual machines on the host + vCPUs required by the current virtual machine) / Total logical CPUs of the physical node

   - Memory score = (Total memory of all virtual machines on the host + Memory required by the current virtual machine) / Total physical memory of the node

   - Host score = (CPU score + Memory score) / 2

The node with the lowest host score has the highest weight and is ultimately selected as the scheduling target.

The preceding host scoring algorithm aims to distribute resources evenly. In batch scheduling scenarios, this may cause some virtual machines to fail to be scheduled when cluster memory resources are tight. This algorithm is not suitable for VM HA recovery scenarios, where recovering more virtual machines takes priority over resource balance. Therefore, in batch scheduling scenarios, the VM scheduler uses a different scheduling order combined with a compact resource allocation algorithm, where nodes with less available memory are assigned higher weights. If the compact resource allocation algorithm can successfully schedule more virtual machines, it will be selected.

## VM snapshot

A VM snapshot is a backup of virtual volume states and virtual machine configuration. Virtual machines and VM snapshots are independent of each other and do not depend on one another.

Each VM snapshot includes the following:

- Snapshots of all virtual volumes
- Virtual machine configuration, such as vCPU, memory, disk boot order, and network configuration

In addition, VM snapshots support the following operations:

- Snapshot rollback
- Rebuild virtual machine from snapshot

## VM template

A VM template is similar to a VM snapshot in that it also backs up virtual volume states and virtual machine configuration. However, unlike a snapshot, a template can be used to create new virtual machines in batches after it is created, and rollback is not supported. Additionally, the virtual volume snapshots in a VM snapshot are implemented using ZBS snapshot features, whereas the virtual volume templates in a VM template are handled through the clone mechanism controlled by the SMTX OS virtual machine service. Virtual machines and VM templates are independent of each other and do not depend on one another. Each virtual volume under a VM template is a new volume cloned by ZBS; this special virtual volume is not displayed or used within ELF.

Each VM template includes the following:

- A new virtual volume cloned from each virtual volume of the source virtual machine
- Virtual machine configuration, such as vCPU, memory, disk boot order, and network configuration

Supported operations for VM templates:

- Create a template from a shut-down virtual machine
- Create virtual machines in batches from a template

## Virtual volume

Built on top of ZBS, ELF uses ZBS's iSCSI feature to create virtual volumes for virtual machines. The advantages of ZBS give virtual volumes high performance and high availability.

When using ZBS storage features in ELF, each virtual volume corresponds to one iSCSI LUN. ELF helps users interact with ZBS more conveniently, so some ZBS concepts, such as iSCSI target, are hidden in ELF and do not need to be perceived. You only need to create a virtual volume and set the corresponding storage policy; ELF handles all underlying interactions and associations with ZBS.

## Virtual volume snapshot

Virtual volume snapshots are based on ZBS volume snapshots. The iSCSI LUN used by an ELF virtual volume belongs to a ZBS volume, so taking a snapshot of the ZBS volume completes the snapshot creation for the iSCSI LUN.

## ISO image

ISO images are built on ZBS's iSCSI service. Each uploaded ISO image is saved to an iSCSI LUN and mounted to virtual machines for use as a CD-ROM.

Currently, the only supported method for creating images is browser upload. The browser automatically splits the file and uploads it in chunks.

<!-- order:6 -->
