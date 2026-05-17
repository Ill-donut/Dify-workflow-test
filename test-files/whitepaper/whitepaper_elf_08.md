---
title: Job types
sidebar_label: Job types
hide_title: true
id: whitepaper_elf_08
---

# Job types

## Resource type

The resource type manages tasks by describing resource states and processing them in a state-machine-like manner to reach the target state. Its core concept is resource state assurance: regardless of the current state, the system guarantees that after the current resource description is submitted, the result will be consistent with what was submitted.

![ELF-4.8.1.png](../assets/elf-white-paper/image15.png)

Advantages:

- Non-operational descriptions avoid errors caused by state inconsistency.
- Friendly to frontend entry points; input is simple and the frontend does not need to analyze behavior.
- Can complete a series of complex transaction-like tasks.

## One-time task type

One-time tasks are typically used for tasks that are time-consuming yet well-defined and straightforward, such as attaching a disk or removing a host.

## Scheduled task type

Scheduled tasks are triggered periodically by Job Center Scheduler, and are used to handle tasks that need to run in a continuous loop, such as alert checks and the virtual machine HA function.

The overall scheduled task process has two main parts:

- Job Center Scheduler periodic trigger

    Scheduled tasks are triggered by Job Center Scheduler, which is deployed only on a fixed set of three or five nodes. As long as one node's service is healthy, scheduled tasks will execute normally. Multi-node deployment provides more robust disaster recovery.

    ![ELF-4.8.3.png](../assets/elf-white-paper/image14.png)

- Execution of well-defined tasks

    Unlike resource-type tasks, scheduled tasks have no state-machine-like setup. Therefore, when a scheduled task is submitted, the task to be executed and the required details must be specified upfront.
