---
title: Job Center Worker
sidebar_label: Job Center Worker
hide_title: true
id: whitepaper_elf_04
---

# Job Center Worker

Job Center Worker (JC Worker) is deployed on all nodes with no primary or secondary distinction; all instances are in the **Active** state. Structurally, JC Worker consists of three components: Leader, Follower, and Splitter. In terms of Job execution, JC Worker acts as the actual executor of tasks in two roles: Leader and Follower. Each JC Worker can switch between the two roles, but within a single task execution cycle, it can only be either a Leader or a Follower.

## Leader

The first JC Worker to handle a Job is called the Leader. It executes the Leader task, which is responsible for splitting the Job, building a topology structure, and dispatching subtasks. When a Job is submitted to Job Center, it starts with a Leader task. The Leader uses the Splitter to split the Job into a set of subtasks (Follower tasks), builds a topology for them, and dispatches them. When all subtasks are complete, the last subtask is resubmitted to the Leader, which then updates the Job result based on all subtask results. The relationship is described as follows:

![](../assets/elf-white-paper/image10.png)

Job Center does not allow multiple Jobs to operate on the same resource simultaneously, as concurrent operations on a resource could corrupt it and cause data inconsistency. To prevent this, the Leader is also responsible for locking the resources included in a Job, and releasing them after the Job completes. When the Leader begins processing a Job, it marks each included resource one by one. If any resource is already marked by another Job, the Leader abandons the current Job, updates its status to failed, and stops processing. Only when all included resources are successfully marked does task splitting proceed. As a result, operations on the same resource in Job Center are serialized, and concurrently submitting Jobs that include a large number of resources may create a performance bottleneck at the resource locking stage.

## Follower

The JC Worker that actually executes a Job's subtasks is called a Follower. In the implementation, each Follower task corresponds to a function that does one simple thing. The completion status and time of each Follower task are recorded to minimize the impact of machine failures and improve the success rate of task recovery. For example, creating, starting, and shutting down virtual machines are each separate Follower tasks. Follower tasks may have dependencies; when a Follower task completes, downstream tasks are submitted according to the topology built by the Leader, until all Follower tasks are complete.

## Splitter

Splitter is the component used by the Leader during execution. It is responsible for splitting a Job into one or more Follower tasks. A Job typically contains a collection of resources, and resources are designed as stateful objects. Resources can undergo valid transitions between states; these transitions are decomposed into a series of operation steps, which are described as Follower tasks. The validity of state transitions (note: not all states can transition to each other) and the transition steps are predefined and mapped to Follower tasks, forming a state transition graph. Each type of resource in Job Center has a corresponding Splitter—for example, virtual machines have a KvmVMSplitter, which is responsible for splitting a Job into Follower tasks at runtime according to the state transition graph. Suppose a virtual machine is currently in the **Shutdown** state, and a Job is submitted to bring it to the **Running** state. According to the virtual machine state transition graph, transitioning from **Shutdown** to **Running** requires a power-on operation, so the Splitter generates a Follower task for powering on the virtual machine.

![ELF-4.8.1.png](../assets/elf-white-paper/image15.png)

In addition, Job Center supports periodically triggered Jobs that may not contain a resource collection, such as periodic node information collection. These Jobs are handled by a specific Splitter, which splits the Job into Follower tasks by analyzing the data attached to the Job.
