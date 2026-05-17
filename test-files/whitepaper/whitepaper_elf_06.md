---
title: Job task dependency
sidebar_label: Job task dependency
hide_title: true
id: whitepaper_elf_06
---

# Job task dependency

After tasks are split, they form an unordered set. The Leader then builds a directed acyclic graph (DAG) based on their dependencies to determine the execution order. For example, in the diagram below, starting a virtual machine depends on creating it, and creating the virtual machine depends on creating the disk.

![ELF-4.5.png](../assets/elf-white-paper/image13.png)
