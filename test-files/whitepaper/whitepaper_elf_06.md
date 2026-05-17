---
title: Job Task Dependencies
sidebar_label: Job Task Dependencies
hide_title: true
id: whitepaper_elf_06
---

# Job Task Dependencies

After tasks are split out, they become a group of tasks with no ordering or sequence. Then the Leader builds a directed acyclic graph based on the dependency relationships among them to determine the execution order of the tasks. For example, in the figure below, starting a virtual machine depends on creating a virtual machine, and creating a virtual machine depends on creating a disk.

![ELF-4.5.png](../assets/elf-white-paper/image13.png)
