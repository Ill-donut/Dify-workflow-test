---
title: Virtual machine service architecture
sidebar_label: Virtual machine service architecture
hide_title: true
id: whitepaper_elf_02
---

# Virtual machine service architecture

![](../assets/elf-white-paper/architecture.png)

## RESTful API Service

RESTful API Service is the entry point for all HTTP APIs. It consists of a group of independent services that provide API access for the web console management interface, as well as some command-line entry services. The APIs provided cover not only ELF but also other services such as ZBS and monitoring data.

The service is built on coroutines for high performance, supporting hundreds of concurrent requests. In terms of extensibility, modules can be loaded into the server as plugins.

The service is deployed on every node; you only need to access any single node. A failure on any individual node does not affect the entry points on other nodes. Each node's entry point is functionally identical and stateless, so calling the API service on any node returns the same result.

## VNC Proxy Service

VNC Proxy Service is the component that provides web console access to the VNC interface of virtual machines. It is deployed on all nodes. The service communicates over the management network and acts as a proxy—accessing the VNC Proxy Service on any node allows you to reach the VNC of any virtual machine on that node.

## VM Scheduler

VM Scheduler schedules virtual machines according to placement policies and automatic scheduling rules. It is deployed on the master node. Across all nodes, exactly one VM Scheduler instance is in the **Active** state and switches together with the ZBS-Meta Leader, while all others remain in the **Standby** state.

For more details, see the [Virtual machine auto-scheduling](whitepaper_elf_11.md#virtual-machine-auto-scheduling) section.

## DHCP Service

DHCP Service provides DHCP configuration for virtual machine networks and responds to DHCP requests from virtual machines. It is deployed on the master node. Across all nodes, exactly one DHCP Service instance is in the **Active** state and switches together with the ZBS-Meta Leader, while all others remain in the **Standby** state.

## VMTools Agent

VMTools Agent is deployed and runs on every node. It enables communication between the host and the VMTools service deployed inside virtual machines via VirtIO Serial. Its main functions include but are not limited to:

- Periodically collecting static Guest OS information from virtual machines and persisting it to MongoDB.
- Providing a gRPC interface to query virtual machine Guest OS performance data, and supporting configuration of virtual machine network settings, usernames, and passwords.
- Providing a file system quiescing interface to support file-system consistent snapshots of virtual machines.

## Job Center Worker

Job Center Worker (JC Worker) is a component of Job Center, deployed on every node to execute various asynchronous tasks. JC Worker instances have no primary or secondary distinction; all are in the **Active** state. Each node's JC Worker can spawn up to 100 concurrent execution units, each corresponding to either a Leader task or a Follower task.

Job Center uses MongoDB as the task queue to form a JC Worker cluster. After a Job is submitted to Job Center, it is routed via MongoDB to an available node, where the node's JC Worker processes it. A Job starts with a Leader task, which is then split into multiple Follower tasks; each Follower task is submitted back to Job Center as an asynchronous task for execution. A Follower task can specify a target node, in which case Job Center dispatches it to that node; otherwise, it randomly selects a relatively idle node based on cluster load.

For more details, see the [Job Center Worker](whitepaper_elf_04.md) section.

## Job Center Scheduler

Job Center Scheduler (JC Scheduler) is another component of Job Center, deployed on the master node to submit scheduled Jobs to the Job Center Worker. JC Scheduler instances have no primary or secondary distinction; all are in the **Active** state. As long as one JC Scheduler is functioning normally in the cluster, scheduled Jobs across the cluster will work correctly.

Currently, the main scheduled Jobs include:

- SMTX OS virtual machine state synchronization and recovery
- Job Center high availability
- Periodic collection and cleanup tasks

For more details, see the [Job Center Scheduler](whitepaper_elf_05.md) section.

## VM Monitor

VM Monitor is a lightweight monitoring service deployed on every node. It monitors storage and network to support the high availability (HA) feature. Across all nodes, exactly one VM Monitor instance serves as the Leader and switches together with the ZBS-Meta Leader, while the others run as Followers. Regardless of whether an instance is a Leader or Follower, when it detects that both storage and network are unavailable, it shuts down any running virtual machines on that node to prevent duplicate virtual machines from appearing after HA is triggered on the healthy cluster. Additionally, the VM Monitor acting as Leader is responsible for updating each node's status in MongoDB to trigger HA on healthy nodes.

HA is triggered when any of the following conditions are met:

- The ZBS service over NFS is unavailable for more than 90 seconds, and the Job Center heartbeat check over MongoDB is unavailable for more than 90 seconds
- The host file system enters read-only state

For more details, see the [Virtual machine high availability](whitepaper_elf_14.md) section.

<!-- order:3 -->
