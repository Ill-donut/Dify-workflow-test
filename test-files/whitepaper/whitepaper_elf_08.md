---
title: Job Type
sidebar_label: Job Type
hide_title: true
id: whitepaper_elf_08
---

# Job Type

## Resource Type

A resource type is a task that reaches a desired state by describing the state of a resource and handling it in a manner similar to a state machine. Its core idea is resource state assurance. In other words, no matter what the current state is, the system will ensure that after the current resource description is submitted, the resulting state is consistent with what was submitted.

![ELF-4.8.1.png](../assets/elf-white-paper/image15.png)

Advantages:

- Non-operation-based description, avoiding errors caused by inconsistent states.

- Friendly to frontend entry points, simple input, and no need for frontend behavior analysis.

- Can complete a series of complex transactional-like tasks.

## One-time Task Type

One-time tasks are usually used for tasks that take a relatively long time but are clearly simple, such as mounting disks and removing hosts.

## Scheduled Task Type

Scheduled tasks are timed tasks triggered by Job Center Scheduler and are used to handle tasks that need to loop continuously, such as alarm checks and virtual machine HA features.

The overall scheduled task process mainly consists of two parts:

- Timed triggering by Job Center Scheduler

    Scheduled tasks are triggered by Job Center Scheduler deployed on only three or five fixed nodes. As long as one node service is functioning normally, scheduled tasks can be executed normally. Multi-node deployment is used for better disaster recovery.

    ![ELF-4.8.3.png](../assets/elf-white-paper/image14.png)

- Execute a specific task

    Scheduled tasks do not have a state machine-like setup like resource types, so when submitting a scheduled task, you need to enter the task to be executed and the required details.
