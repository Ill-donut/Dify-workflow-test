---
title: Job Center Scheduler
sidebar_label: Job Center Scheduler
hide_title: true
id: whitepaper_elf_05
---

# Job Center Scheduler

Job Center Scheduler (JC Scheduler) is deployed on 3 or 5 nodes as needed, and is used solely to submit Jobs to Job Center. JC Scheduler instances have no primary or secondary distinction; they are all in the **Active** state. In each scheduled Job cycle, every node's JC Scheduler submits a Job to Job Center, but only one submission succeeds; the others fail due to contention and give up. This process is guaranteed by MongoDB's atomic operations. Therefore, as long as one JC Scheduler is functioning normally in the cluster, scheduled Jobs across the entire cluster will work correctly.
