---
title: Job Resource Group
sidebar_label: Job Resource Group
hide_title: true
id: whitepaper_elf_10
---

# Job Resource Group

Job Resource Group is a feature that serves resource-type Jobs. It groups resources within a single Job so that dependencies can be handled and DAGs can be built in isolation for each group. Group assignments must be specified when submitting the Job. If there are multiple groups, each group has its own DAG; because there are no dependencies between groups, they can be executed in parallel. This feature is currently used in batch operations, such as creating virtual machines from a VM template in batches.

![ELF-4.10.png](../assets/elf-white-paper/image12.png)

<!-- order:5 -->
