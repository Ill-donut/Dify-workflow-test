---
title: Job Center Scheduler
sidebar_label: Job Center Scheduler
hide_title: true
id: whitepaper_elf_05
---

# Job Center Scheduler

Job Center Scheduler, abbreviated as JC Scheduler, is deployed to 3 or 5 nodes as needed and is used only to submit Jobs to Job Center. The JC Scheduler instances on each node have no master-slave distinction and are all in the Active state. In each scheduled Job cycle, the JC Scheduler instances on all nodes submit Jobs to Job Center, but only one JC Scheduler succeeds in submitting; the others give up because they lose the competition. This process is guaranteed by MongoDB atomic operations. Therefore, as long as one JC Scheduler in the cluster is functioning normally, the entire cluster's scheduled Job processing can be ensured.
