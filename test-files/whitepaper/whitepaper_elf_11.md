---
title: Supported Components and Features
sidebar_label: Supported Components and Features
hide_title: true
id: whitepaper_elf_11
---

# Supported Components and Features

## Virtual Machine

A virtual machine is the core of the entire ELF and provides customers with virtual computing services. ELF is based on KVM, with libvirt used as an auxiliary component to implement virtual machine creation and management. In addition, to ensure that virtual machines can obtain cluster capabilities such as high reliability and high availability, features such as virtual machine HA, virtual machine migration, and virtual machine automatic scheduling have been added.

The main features provided by virtual machines are:

- (Batch) create

- (Batch) power on

- (Batch) shut down

- (Batch) force shut down

- (Batch) restart

- (Batch) force restart

- (Batch) pause

- (Batch) resume

- (Batch) migrate

- (Batch) delete

- Clone

## Virtual Machine Automatic Scheduling

Virtual machine automatic scheduling is an important part of virtual machines. Its purpose is to automatically schedule the creation or startup of virtual machines according to cluster usage, so as to balance the distribution of virtual machines within the cluster.

In ELF, the VM Scheduler implements the scheduling algorithm and works with Job Center to complete automatic virtual machine scheduling. VM Scheduler is deployed on 3 or 5 nodes as needed. Only one node's VM Scheduler is in Active state, while the others are in Standby state. The VM Scheduler in Active state switches along with the ZBS-Meta Leader and is always on the same node as the ZBS-Meta Leader. In addition, VM Scheduler uses MongoDB to store node resource data during calculation. When it is unavailable, functions related to allocating resources for virtual machines are unavailable, typically including virtual machine creation, power on, and migration.

VM Scheduler filters nodes based on a filter chain, then calculates weights for nodes that meet scheduling requirements, and finally selects the optimal node as the target node for virtual machine scheduling. The process is shown in the following figure:

![](../assets/elf-white-paper/image7.png)

The filter chain consists of multiple filters and identifies available hosts. Its main functions are:

1. Filter out nodes that do not meet the hard physical requirements of the virtual machine

   Nodes that are not suitable are filtered out through some hard criteria, such as whether the node is alive, network environment configuration, CPU compatibility, whether the total amount of virtual machine memory allocated on a single node does not exceed physical memory, and whether host maintenance mode is enabled.

2. Filter out nodes that do not meet policy requirements according to virtual machine placement group rules

   - A virtual machine placement group policy is a set of policies that define where virtual machines can be placed. Once enabled, it becomes a mandatory policy. Its priority is higher than the two principles above. Currently, ELF placement group rules include the following three types:

     - Must place / must not place on the selected host: In an active-active environment, when this type of policy and high availability are enabled, it is recommended to select at least one host in each of the two availability zones. Otherwise, business continuity may be interrupted. If the selected hosts here are all in the preferred availability zone, then when the entire preferred availability zone is unavailable, high availability is constrained by the "must" requirement and cannot automatically migrate the virtual machine to a host in the secondary availability zone.

     - Prefer to place / not place on the selected host: In an active-active environment, when this type of policy and high availability are enabled, it is not recommended to select hosts in the secondary availability zone, so that virtual machines will preferentially migrate to hosts in the preferred availability zone. Even if the entire preferred availability zone becomes unavailable, because this is a "prefer" policy rather than a "must" policy, the system will still automatically migrate virtual machines to the secondary availability zone, ensuring business continuity.

     - Prefer / must place on the same / different host: The two types above define the placement relationship between virtual machines and hosts, while this type defines the placement relationship between virtual machines and virtual machines.

   - In an active-active cluster, placement groups also support availability zone placement policies, but within the same placement group rule, only one of "virtual machine-host policy" or availability zone can be selected; both cannot be set at the same time. Currently, ELF placement groups support the following availability zone rules:

     - Must place on the preferred / secondary availability zone
     - Prefer to place on the preferred / secondary availability zone

3. In an active-active environment, when no availability zone placement group policy is configured, preferred availability zone nodes are selected first

    If there are available nodes in the preferred availability zone, they are selected first. Only when there are no available nodes in the preferred availability zone are nodes in the secondary availability zone selected.

4. Select nodes that support enabling CPU exclusivity for virtual machines according to the scheduling scenario

    - If the scheduling scenario is a scheduling request initiated by the user, such as power-on or live migration, the scheduler will select nodes whose number of exclusive CPUs supports enabling CPU exclusivity for virtual machines.

    - If the scheduling scenario is virtual machine HA, the scheduler will first try to select nodes whose number of exclusive CPUs supports enabling CPU exclusivity for virtual machines. If no nodes meet this condition, the scheduler will not filter nodes, and CPU exclusivity will not be enabled after the virtual machine is rebuilt.

After unsuitable nodes are filtered out, if more than one node remains, scoring and sorting are performed using the following algorithm based on whether the current virtual machine is in the **running** state:

- When the virtual machine is in the **running** state:

  - CPU score = (total vCPUs of virtual machines in the **running** state on the host + number of vCPUs required by the current virtual machine) / (total allocated vCPUs in the cluster + number of vCPUs required by the current virtual machine)

  - Memory score = (total memory of virtual machines in the **running** state on the host + memory required by the current virtual machine) / total physical memory of the node

  - Host score = (CPU score + Memory score) / 2

- When the virtual machine is in the **shut down** state:

   - CPU score = (total vCPUs of all virtual machines on the host + number of vCPUs required by the current virtual machine) / total logical CPU count of the physical node

   - Memory score = (total memory of all virtual machines on the host + memory required by the current virtual machine) / total physical memory of the node

   - Host score = (CPU score + Memory score) / 2


The node with the lowest host score has the highest weight and will ultimately be selected as the target scheduling node.

The host scoring algorithm described above aims to evenly distribute resources. In batch scheduling scenarios, when cluster memory resources are tight, it may cause some virtual machines to fail scheduling. This algorithm is not suitable for VM HA recovery scenarios. In VM HA recovery, restoring more virtual machines is more important than balancing resources, so in batch scheduling scenarios the virtual machine scheduler will use a different scheduling order, combined with an algorithm that allocates resources compactly: the less available memory a host has, the higher its weight. If using the compact resource allocation algorithm can successfully schedule more virtual machines, that algorithm will be chosen.

## Virtual Machine Snapshot

A virtual machine snapshot is a backup of virtual volumes and virtual machine configuration information. Virtual machines and virtual machine snapshots are independent entities and do not depend on each other.

Each virtual machine snapshot contains the following information:

- Snapshots of all virtual volumes

- Virtual machine configuration information, such as vCPU, memory, disk boot order, network configuration, and so on

In addition, virtual machine snapshots support the following features:

- Snapshot rollback

- Rebuild a virtual machine from a snapshot

## Virtual Machine Template

A virtual machine template is similar to a virtual machine snapshot in that it is also a backup of virtual volumes and virtual machine configuration. However, unlike snapshots, templates can be used to mass-produce new virtual machines after they are created, and virtual machines cannot be rolled back from a template. In addition, the virtual volume snapshots under a virtual machine snapshot are developed based on the snapshot feature of ZBS, while the virtual volume templates under a virtual machine template are handled through the cloning method controlled by the SMTX OS virtual machine service. Virtual machine templates and virtual machines are independent entities and do not depend on each other. Each virtual volume under a virtual machine template is a new volume cloned from ZBS, but this special virtual volume is not displayed or used in ELF.

Each virtual machine template contains the following information:

- A new virtual volume cloned from all virtual volumes under the source virtual machine

- Virtual machine configuration information, such as vCPU, memory, disk boot order, network configuration, and so on

Features supported by virtual machine templates:

- Create a template from a shut down virtual machine

- Batch create virtual machines from a template

## Virtual Volume

Based on ZBS, ELF uses the iSCSI capabilities of ZBS to build virtual volumes for virtual machines. The advantages of ZBS give virtual volumes features such as high performance and high availability.

When ELF uses the storage capabilities of ZBS, a virtual volume corresponds to an iSCSI LUN. ELF helps users use ZBS more conveniently, so some ZBS concepts, such as iSCSI Target, are hidden in ELF and do not need to be exposed. Users only need to create a virtual volume and set the corresponding storage policy, and ELF will handle all underlying interactions and associations with ZBS.

## Virtual Volume Snapshot

Virtual volume snapshots are handled based on ZBS volume snapshots. The iSCSI LUN used by ELF virtual volumes belongs to a ZBS volume, so as long as a snapshot is taken of the ZBS volume, a snapshot of the iSCSI LUN can be created.

## ISO Image

ISO images are built based on the iSCSI service of ZBS. Each uploaded ISO image is saved to an iSCSI LUN and then mounted to a virtual machine for use through CDROM.

Currently, the only supported way to create images is browser upload. The browser automatically splits the file and uploads it in chunks.


<!-- order:6 -->
