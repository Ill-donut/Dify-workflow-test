---
title: Job Center
sidebar_label: Job Center
hide_title: true
id: whitepaper_elf_03
---

# Job Center

![](../assets/elf-white-paper/image5.png)

The figure above shows the relationship between Job Center and the important components it interacts with. In the virtual machine service of SMTX OS, virtual machines, virtual volumes, virtual machine snapshots, virtual volume snapshots, virtual machine templates, and so on are defined as "resources" and stored in MongoDB. Resources have states, and state transitions can be performed between different states by executing certain operations. These operations are called Follower tasks. Job Center generates Follower tasks by analyzing the current state and target state of resources. This operation is also defined as a task, called a Leader task. Usually, each Job contains a set of resources, which may include one or more of the aforementioned resources. In addition, Job Center also supports periodically triggered scheduled Jobs. Such Jobs do not need to contain a resource set, but after being processed by Leader, they are also split into Follower tasks, such as scheduled collection of node information.

MongoDB is deployed in ELF as a master/secondary replica set, usually on 3 or 5 nodes depending on requirements. Job Center uses MongoDB as the task queue and routes Job-related tasks to the target nodes for execution. Job and task states are also stored in MongoDB. Job Center tracks task states to determine when to terminate a task (timeout) and whether a task needs to be resubmitted, ensuring that each task is executed at least once. Task reentrancy is guaranteed by the task itself.

Job Center consists of two components: Job Center Worker and Job Center Scheduler.
