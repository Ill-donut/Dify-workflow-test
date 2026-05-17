---
title: Job Resource Group
sidebar_label: Job Resource Group
hide_title: true
id: whitepaper_elf_10
---

# Job Resource Group

Job Resource Group serves resource-type Jobs by grouping resources within the same Job, so that operations are isolated when handling dependencies and constructing a directed acyclic graph. The grouping relationship must be specified when submitting the Job. If there are multiple groups, there are multiple directed acyclic graphs, because there are no dependencies between the graphs, so they can be executed in parallel. Currently, this feature is used in batch processing, for example, batch creation of virtual machines from a virtual machine template.

![ELF-4.10.png](../assets/elf-white-paper/image12.png)

<!-- order:5 -->
