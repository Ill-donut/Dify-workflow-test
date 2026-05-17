---
title: Virtual Machine Service Architecture
sidebar_label: Virtual Machine Service Architecture
hide_title: true
id: whitepaper_elf_02
---

# Virtual Machine Service Architecture

![](../assets/elf-white-paper/architecture.png)

## RESTful API Service

RESTful API Service is the entry point for all HTTP APIs. It consists of a set of independent services used to provide API services for the Web console management interface, as well as some command-line entry services. The provided API services are not limited to ELF, but also include APIs for ZBS, monitoring data, and more.

In terms of performance, the service is developed based on coroutines and can provide hundreds of concurrent connections to meet high-performance requirements. In terms of extensibility, modules can be loaded into the server in the form of plugins for use.

The service is deployed on every node, and users only need to access any one of the nodes. A failure on a single node will not affect the entry service of other nodes. The entry function on each node is identical and stateless. The results returned by calling the API service on any node are the same.

## VNC Proxy Service

VNC Proxy Service is a component that provides access to the virtual machine VNC interface service for the Web console management interface, and it is deployed on all nodes. The service communicates through the management network and provides Proxy services. By accessing the VNC Proxy service on any node, you can access the VNC of any virtual machine on that node.

## VM Scheduler

VM Scheduler is used to schedule virtual machines according to placement policies and automatic scheduling rules. It is deployed on the master node. There is exactly 1 active VM Scheduler on each node, and it switches along with the ZBS-Meta Leader; the others remain in Standby state.

For more details, see the [Virtual Machine Automatic Scheduling](whitepaper_elf_11.md#virtual-machine-automatic-scheduling) section.

## DHCP Service

DHCP Service is used to provide DHCP services for virtual machine networking and respond to virtual machine DHCP requests. It is deployed on the master node. There is exactly 1 DHCP Service in Active state on each node, and it switches along with the ZBS-Meta Leader; the others remain in Standby state.

## VM VMTools Agent

VM VMTools Agent is deployed and runs on every node. It supports communication between the host machine and the VMTools service deployed inside virtual machines through VirtIO Serial. Its main functions include but are not limited to:

- Periodically collect static information from the virtual machine Guest OS and persist it to the MongoDB database
- Provide gRPC interfaces to query Guest OS-related performance data of virtual machines, and support configuring virtual machine network, username, password, and so on
- Provide interfaces for silent file systems to support consistent snapshots of virtual machine file systems

## Job Center Worker

Job Center Worker, abbreviated as JC Worker, is a component of Job Center. It is deployed on every node and used to execute various asynchronous tasks. JC Workers on all nodes have no master-slave distinction and are all in Active state. JC Worker on each node can generate up to 100 concurrent execution units. Each execution unit can correspond to a Leader task or a Follower task.

Job Center uses MongoDB as the task queue to form a JC Worker cluster. After a Job is submitted to Job Center, it is routed through MongoDB to any available node and processed by the JC Worker on that node: the Job starts with a Leader task, then is split into multiple Follower tasks, and each Follower task is submitted back to Job Center as an asynchronous task for execution. A Follower task can specify a target node, in which case Job Center distributes the task to the specified target node. Otherwise, it randomly selects a relatively idle node as the target node based on cluster load.

For more details, see the [Job Center Worker](whitepaper_elf_04.md) section.

## Job Center Scheduler

Job Center Scheduler, abbreviated as JC Scheduler, is another component of Job Center. It is deployed on the master node and used to submit scheduled Jobs to Job Center Worker. JC Schedulers on all nodes have no master-slave distinction and are all in Active state. As long as one JC Scheduler in the cluster is running normally, scheduled Job execution in the cluster can be guaranteed.

Currently, the scheduled Jobs mainly include:

- SMTX OS virtual machine state synchronization and recovery
- Job Center high availability
- Scheduled collection and cleanup tasks

For more details, see the [Job Center Scheduler](whitepaper_elf_05.md) section.

## VM Monitor

VM Monitor is a lightweight monitoring service deployed on each node, used to monitor storage and network to support High Availability (HA) functionality. There is exactly 1 Leader VM Monitor on each node, which switches along with the ZBS-Meta Leader, while the others run as Follower. Regardless of whether it is Leader or Follower, when both storage and network are detected as unavailable, it will shut down the virtual machines running on that node to prevent duplicate virtual machines from being triggered after HA is activated in a healthy cluster. In addition, the VM Monitor acting as Leader is also responsible for updating the status of each node to MongoDB so that HA can be triggered on healthy nodes.

HA is triggered when any of the following conditions is met:

- The NFS-based ZBS service is unavailable for more than 90 seconds, and the MongoDB-based Job Center heartbeat check is unavailable for more than 90 seconds

- The host file system enters read-only mode

For more details, see the [Virtual Machine High Availability](whitepaper_elf_14.md) section.

<!-- order:3 -->
