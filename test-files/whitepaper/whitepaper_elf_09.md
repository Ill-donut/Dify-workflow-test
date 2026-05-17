---
title: Job Queue
sidebar_label: Job Queue
hide_title: true
id: whitepaper_elf_09
---

# Job Queue

Job Queue is a queue implementation for Jobs. When a Job is submitted with a specific flag, all Jobs sharing the same flag are executed sequentially in the order they were submitted. Job Queue plays an important role in recovering from congestion and controlling resource contention. Tasks that currently use this feature include virtual machine HA, Job Recovery, and scheduled snapshots.
