---
title: Job Center Worker
sidebar_label: Job Center Worker
hide_title: true
id: whitepaper_elf_04
---

# Job Center Worker

Job Center Worker, abbreviated as JC Worker, is deployed to all nodes, with no primary-secondary distinction, and all are in Active state. Structurally, the JC Worker consists of three components: Leader, Follower, and Splitter. From the perspective of the Job execution process, the JC Worker acts as the actual executor of tasks and is divided into two roles: Leader and Follower. Each JC Worker can switch between these two roles, but within a single task execution cycle it can only be either Leader or Follower.

## Leader

The first JC Worker to take over a Job is called the Leader. It executes Leader tasks and is responsible for task splitting, topology construction, and dispatching. When a Job is submitted to the Job Center, it starts with a Leader task. The Leader uses the Splitter to split the Job into tasks, generating a set of sub-tasks (that is, Follower tasks), and then constructs a topology for the sub-tasks before dispatching them. When all sub-tasks have finished executing, the last sub-task is submitted back to the Leader, which updates the Job execution result based on the execution results of all sub-tasks. The relationship is shown below:

![](../assets/elf-white-paper/image10.png)

Job Center does not allow multiple Jobs to operate on the same resource at the same time. Concurrent operations on a resource may damage the resource and cause data inconsistency. To prevent this, the Leader is also responsible for locking the resources included in the Job and releasing them after the Job execution is complete. When the Leader starts processing a Job, it marks each included resource one by one. If it finds that any resource has already been marked by another Job, it abandons the current Job, updates its status to failed, and ends processing. Only when all included resources are successfully marked will task splitting begin. Therefore, operations on the same resource in Job Center are serialized, and concurrently submitted Jobs containing a large number of resources may cause a performance bottleneck at resource locking.

## Follower

The JC Worker that actually executes Job sub-tasks is called the Follower. In implementation, each Follower task corresponds to a function, and this function does only one simple thing. The status and time when each Follower task is completed are recorded to reduce the impact of machine failures and improve the success rate of recovery tasks. For example, creating, starting, and shutting down virtual machines are all separate Follower tasks. Follower tasks may have dependencies. After a depended-on Follower task is completed, downstream tasks are submitted according to the sub-task topology constructed by the Leader until all Follower tasks are completed.

## Splitter

Splitter is a component used during Leader execution. It is responsible for splitting a Job into one or more Follower tasks. Usually a Job contains a set of resources, and resources are designed as stateful objects. Resources can legally transition between different states, and the transition process is broken down into a series of operation steps, which are described as Follower tasks. The legality of transitions between resource states (note: not all states can transition to each other) and the transition steps are predefined and mapped to Follower tasks, forming a state transition graph. Each type of resource in Job Center has a corresponding Splitter. For example, a virtual machine has a KvmVMSplitter, which is responsible for splitting the Job into Follower tasks at runtime according to the state transition graph. Suppose a virtual machine is currently in the powered-off state, and a Job is submitted with the expectation that the virtual machine will be in the running state after the Job is executed. According to the virtual machine state transition graph, moving from the powered-off state to the running state requires a power-on operation, so the Splitter generates a Follower task for powering on the virtual machine.

![ELF-4.8.1.png](../assets/elf-white-paper/image15.png)

In addition, Job Center also supports periodically triggered scheduled Jobs. Such Jobs may not contain a resource set, such as periodically collecting node information. These Jobs are handled by a specific Splitter, which analyzes the data attached to the Job and splits the Job into Follower tasks.
