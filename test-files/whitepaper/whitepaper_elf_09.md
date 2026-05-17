---
title: Job Queue
sidebar_label: Job Queue
hide_title: true
id: whitepaper_elf_09
---

# Job Queue

Job Queue is the queue implementation for Job. As long as a specific flag is included when submitting a Job, Jobs with the same flag will be executed sequentially according to the order in which they were submitted. Job Queue plays an important role in recovery after congestion blocking and in controlling resource preemption. Tasks that currently use this feature include virtual machine HA, Job Recovery, and scheduled snapshots.
