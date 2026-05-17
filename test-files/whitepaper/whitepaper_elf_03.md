---
title: Job Center
sidebar_label: Job Center
hide_title: true
id: whitepaper_elf_03
---

# Job Center

![](../assets/elf-white-paper/image5.png)

The diagram above illustrates the relationship between Job Center and the key components it interacts with. In SMTX OS virtual machine service, objects such as virtual machines, virtual volumes, VM snapshots, virtual volume snapshots, and VM templates are defined as "resources" and stored in MongoDB. Resources have states; state transitions are performed by executing certain operations, which are referred to as Follower tasks. Job Center generates Follower tasks by analyzing a resource's current state and target state, which is defined as a Leader task. Each Job typically contains a collection of resources, which may consist of one or more of the resource types described above. In addition, Job Center supports periodically triggered Jobs that may not contain a resource collection; after being processed by the Leader, they are also split into Follower tasks—for example, periodic node information collection.

MongoDB is deployed in ELF in a master/secondary replica set configuration, typically on 3 or 5 nodes as needed. Job Center uses MongoDB as the task queue to route Job-related tasks to target nodes for execution. Job and task statuses are also stored in MongoDB. Job Center tracks task statuses to determine when to terminate a task (timeout) and whether to resubmit a task, ensuring that each task is executed at least once. Task reentrancy is guaranteed by the task implementation itself.

Job Center consists of two components: Job Center Worker and Job Center Scheduler.
