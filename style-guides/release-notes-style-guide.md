# Release Notes Style Guide

**Document type:** `release_notes`
**Language pair:** Simplified Chinese → English
**Scope:** Translation style rules for product release notes, covering tense, voice, sentence structure, and section-specific conventions.

---

## Rule 1 — What's New and Improvements: Use Simple Present Tense

All entries in the **What's New** and **Improvements** sections must use simple present tense. Do not use past tense or future tense.

**Correct:**
- Supports enabling Boost mode in SMTX OS (ELF) active-active clusters.
- Displays the storage overprovisioning ratio.
- Provides port connectivity test with alerts for abnormal ports.

**Incorrect:**
- Added support for enabling Boost mode in SMTX OS (ELF) active-active clusters. *(past tense — wrong)*
- Will display the storage overprovisioning ratio. *(future tense — wrong)*

---

## Rule 2 — Document Title: Use "What's in this release"

The document title must be "What's in this release" (sentence case). Do not use "Release Update Notes" or other variations.

**Correct:**
- title: What's in this release
- # What's in this release

**Incorrect:**
- title: Release Update Notes
- # Release Update Notes

---

## Rule 3 — Author Field: Use Sentence Case

The author field must use sentence case: "SmartX documentation team". Do not capitalize "Documentation Team".

**Correct:**
- author: SmartX documentation team

**Incorrect:**
- author: SmartX Documentation Team

---

## Rule 4 — Sidebar Label: Use "What's in this release"

The sidebar label must be "What's in this release" (sentence case). Do not use "Release Update Notes".

**Correct:**
- sidebar_label: What's in this release

**Incorrect:**
- sidebar_label: Release Update Notes

---

## Rule 5 — Section Headings: Use Sentence Case

All section headings (## and ### levels) must use sentence case. Capitalize only the first word and proper nouns.

**Correct:**
- ## What's new
- ## Resolved issues
- ### Block storage
- ### Networking
- ### Operations and management

**Incorrect:**
- ## New
- ## Fixed Issues
- ### Block Storage
- ### Network
- ### Operations and Maintenance Management

---

## Rule 6 — Section Subheadings: Use Sentence Case

All subheadings within sections (### level) must use sentence case. Capitalize only the first word and proper nouns.

**Correct:**
- ### Block storage
- ### Networking
- ### Operations and management

**Incorrect:**
- ### Block Storage
- ### Network
- ### Operations and Maintenance Management

---

## Rule 7 — Product Name: Use "Netswift" Instead of "Wangxun"

When referring to NICs from Netswift (formerly Wangxun), use "Netswift". Do not use "Wangxun".

**Correct:**
- Supports Netswift 10GbE NICs of the txgbe series.
- Supports SR-IOV passthrough and PCI passthrough for Netswift NICs.

**Incorrect:**
- Supports Wangxun 10 GbE NICs (txgbe series).
- Supports SR-IOV passthrough and PCI passthrough for Wangxun NICs.

---

## Rule 8 — Resolved Issues: Use Descriptive Statement + Resolution Clause

All entries in the **Resolved issues** section must follow this structure:
1. A descriptive statement explaining the issue (what could happen, under what conditions)
2. A resolution clause: "The issue has been resolved in this release."

Do not start with "Fixed the issue where...".

**Correct:**
- The `elf-vm-monitor` service might fail to start due to an initialization error in host high availability configuration under rare circumstances. The issue has been resolved in this release.
- In clusters with Boost mode enabled, double-write issues might occur after a virtual machine was rebuilt via HA due to host failures. The issue has been resolved in this release.

**Incorrect:**
- Fixed the issue where, in very rare cases, abnormal initialization of host high availability configuration information might cause the `elf-vm-monitor` service to fail to start.
- Fixed the issue where, in clusters with Boost mode enabled, double writes might occur after a VM was rebuilt by HA due to a host exception.

---

## Rule 9 — Resolved Issues Section Heading: Use "Resolved issues"

The section heading for resolved issues must be "Resolved issues" (sentence case). Do not use "Fixed Issues".

**Correct:**
- ## Resolved issues

**Incorrect:**
- ## Fixed Issues

---

## Rule 10 — What's New Section Heading: Use "What's new"

The section heading for new features must be "What's new" (sentence case). Do not use "New".

**Correct:**
- ## What's new

**Incorrect:**
- ## New

---

## Rule 11 — Networking Section Heading: Use "Networking"

When referring to the networking section, use "Networking" as the heading. Do not use "Network".

**Correct:**
- ### Networking

**Incorrect:**
- ### Network

---

## Rule 12 — Operations and Management Section Heading: Use "Operations and management"

When referring to the operations and management section, use "Operations and management" (sentence case). Do not use "Operations and Maintenance Management".

**Correct:**
- ### Operations and management

**Incorrect:**
- ### Operations and Maintenance Management

---

## Rule 13 — What's New Entries: Use Direct Simple Present Verb Forms

What's New entries should use direct simple present verb forms (e.g., "Displays", "Automatically enables", "Provides") rather than "Supports + gerund" constructions where possible.

**Correct:**
- Displays the storage overprovisioning ratio.
- Automatically enables Boost mode in SMTX OS (ELF) active-active clusters.
- Provides port connectivity test with alerts for abnormal ports.

**Incorrect:**
- Supports displaying the storage overprovisioning ratio.
- Supports automatically enabling Boost mode in SMTX OS (ELF) active-active clusters.
- Supports providing port connectivity test with alerts for abnormal ports.

---

## Rule 14 — What's New: Use Consistent Verb Choices

Use consistent and precise verbs in What's New entries. Prefer "Allows" over "Supports" when describing functionality that enables user actions. Prefer "Automatically detects" or "Tests" over "Supports detecting" or "Supports detecting and alerting".

**Correct:**
- Allows editing the configuration of existing volumes.
- Automatically detects IP conflicts.
- Tests and alerts for network port connectivity issues.

**Incorrect:**
- Supports editing the configuration of existing volumes.
- Supports automatic IP conflict checks.
- Supports network port connectivity detection and alerts.

---

## Rule 15 — What's New: Use Standard Terminology

Use standard terminology in What's New entries. Prefer "mounting" over "attaching" for storage volumes. Prefer "configuring a policy" over "setting a policy". Prefer "customizing access control" over "custom access control".

**Correct:**
- Allows mounting volumes to virtual machines.
- Supports configuring a storage policy.
- Allows customizing access control.

**Incorrect:**
- Supports attaching volumes to virtual machines.
- Supports setting a storage policy.
- Supports custom access control.

---

## Rule 16 — What's New: Use "Allows" for User-Actionable Features

Use "Allows" (or "Allows + gerund") for features that enable users to perform actions, and use "Supports" for features that provide technical capability or compatibility.

**Correct:**
- Allows editing the configuration of existing volumes.
- Allows mounting volumes to virtual machines.
- Allows removing managed object data.
- Supports Netswift 10GbE NICs of the txgbe series.
- Supports SR-IOV passthrough and PCI passthrough for Netswift NICs.

**Incorrect:**
- Supports editing the configuration of existing volumes.
- Supports mounting volumes to virtual machines.
- Supports removing managed object data.

---

## Rule 17 — What's New: Use "Improves" Instead of "Optimizes"

Use "Improves" instead of "Optimizes" in What's New entries when describing performance or behavior enhancements.

**Correct:**
- Improves virtual machine HA behavior in the following ways:
- Improves read and write performance.

**Incorrect:**
- Optimizes VM HA behavior:
- Optimizes read/write performance.

---

## Rule 18 — What's New: Use "Updates" Instead of "Changes"

Use "Updates" instead of "Changes" when describing modifications to system behavior or parameters.

**Correct:**
- Updates the data balance policy to avoid disturbing services.

**Incorrect:**
- Changes the data balance policy to avoid disturbing services.

---

## Rule 19 — What's New: Use "Shortens" Instead of "Optimizes" for Time Reduction

Use "Shortens" instead of "Optimizes" when describing time reduction or speed improvements.

**Correct:**
- Shortens the time required for updating the disk slot sequence.

**Incorrect:**
- Optimizes the time required for adjusting the disk slot sequence.

---

## Rule 20 — What's New: Use "Frees up" Instead of "Reduces" for Resource Release

Use "Frees up" instead of "Reduces" when describing the release or freeing of system resources.

**Correct:**
- Frees up unnecessary management network ports used.

**Incorrect:**
- Reduces unnecessary ports occupied.

---

## Rule 21 — What's New: Use "Collects" Instead of "Adds collection of"

Use "Collects" instead of "Adds collection of" for monitoring data collection features.

**Correct:**
- Collects monitoring data for host system partition read-only errors.

**Incorrect:**
- Adds collection of monitoring data for host system partition read-only errors.

---

## Rule 22 — What's New: Use "Tests" Instead of "Supports detecting" or "Adds detection and alerts for"

Use "Tests" instead of "Supports detecting" or "Adds detection and alerts for" when describing detection or testing features.

**Correct:**
- Tests and alerts for network port connectivity issues.
- Tests for host system partition read-only errors.

**Incorrect:**
- Supports detecting network port connectivity issues.
- Adds detection and alerts for host system partition read-only errors.

---

## Rule 23 — What's New: Add Backticks for Technical Terms

Add backticks (`) around technical terms such as software names, command names, and package names in What's New entries.

**Correct:**
- Upgrades `containerd` from v1.6.18 to v1.6.28.

**Incorrect:**
- Upgrades containerd from v1.6.18 to v1.6.28.

---

## Rule 24 — What's New: Use "Trial and Subscription" with Capitalization

When referring to trial and subscription features, use "Trial and Subscription" with initial capitalization as a proper noun.

**Correct:**
- Supports viewing existing resources and enabled features in the Trial and Subscription module.

**Incorrect:**
- Supports viewing created resources and enabled functions in the trial and subscription module.

---

## Rule 25 — What's New: Use "continuous" Instead of "consecutive" for Failures

Use "continuous" instead of "consecutive" when describing a series of failures or exceptions.

**Correct:**
- Handles continuous physical disk or node failures.

**Incorrect:**
- Handles consecutive physical disk or node exceptions.

---

## Rule 26 — What's New: Use "data movements" Instead of "data flows"

Use "data movements" instead of "data flows" when describing data transfer operations.

**Correct:**
- Reduces data movements in reading hotspot areas.

**Incorrect:**
- Reduces data flows in read-hot data areas.

---

## Rule 27 — What's New: Use "reading hotspot areas" Instead of "read-hot data areas"

Use "reading hotspot areas" instead of "read-hot data areas" when describing frequently accessed data regions.

**Correct:**
- Reduces data movements in reading hotspot areas.

**Incorrect:**
- Reduces data flows in read-hot data areas.

---

## Rule 28 — What's New: Use "virtual machine" Instead of "VM" in Descriptive Text

Use "virtual machine" instead of "VM" in descriptive text within What's New entries. Use "VM" only in code snippets or technical references.

**Correct:**
- Improves virtual machine HA behavior in the following ways:
- Allows mounting volumes to virtual machines.

**Incorrect:**
- Improves VM HA behavior in the following ways:
- Allows mounting volumes to VMs.

---

## Rule 29 — What's New: Use "booting status" Instead of "startup status"

Use "booting status" instead of "startup status" when referring to the operating system boot process.

**Correct:**
- Detects virtual machine operating system booting status.

**Incorrect:**
- Detects VM operating system startup status.

---

## Rule 30 — What's New: Use "hot migration" Instead of "live migration"

Use "hot migration" instead of "live migration" when referring to virtual machine migration.

**Correct:**
- Supports virtual machine hot migration.

**Incorrect:**
- Supports VM live migration.

---

## Rule 31 — What's New: Add "Copy-on-Write" Terminology

Use "Copy-on-Write" when describing storage snapshot or cloning technologies.

**Correct:**
- Supports Copy-on-Write (COW) snapshots.

**Incorrect:**
- Supports snapshots.

---

## Rule 32 — What's New: Use "occupies" Instead of "occupying" for Cache Capacity

Use "occupies" (simple present) instead of "occupying" (gerund) when describing cache capacity usage.

**Correct:**
- Occupies 30% - 50% of the node write cache capacity.

**Incorrect:**
- Occupying 30% to 50% of a node's write cache capacity.

---

## Rule 33 — What's New: Use "might disturb" Instead of "disturb"

Use "might disturb" instead of "disturb" when describing potential service disruption.

**Correct:**
- Updates the data balance policy to avoid disturbing services that might disturb services.

**Incorrect:**
- Updates the data balance policy to avoid disturbing services.

---

## Rule 34 — What's New: Use "updating" Instead of "adjustment"

Use "updating" instead of "adjustment" when describing modifications to system parameters or configurations.

**Correct:**
- Shortens the time required for updating the disk slot sequence.

**Incorrect:**
- Shortens the time required for adjustment of the disk slot sequence.

---

## Rule 35 — What's New: Use "alerts for" Instead of "an alert item for"

Use "alerts for" instead of "an alert item for" when describing alerting features.

**Correct:**
- Provides alerts for host system partition read-only errors.

**Incorrect:**
- Provides an alert item for host system partition read-only errors.

---

## Rule 36 — What's New: Use "S5000C" Instead of "S5000C series"

Use "S5000C" instead of "S5000C series" when referring to specific hardware models.

**Correct:**
- Supports Netswift S5000C NICs.

**Incorrect:**
- Supports Netswift S5000C series NICs.

---

## Rule 37 — What's New: Use "existing resources and enabled features" Instead of "created resources and enabled functions"

Use "existing resources and enabled features" instead of "created resources and enabled functions" when describing what users can view.

**Correct:**
- Supports viewing existing resources and enabled features in the Trial and Subscription module.

**Incorrect:**
- Supports viewing created resources and enabled functions in the trial and subscription module.

---

## Rule 38 — General Document Titles: Use Sentence Case

For all document titles in release notes (including non-What's New documents), use sentence case. Capitalize only the first word and proper nouns.

**Correct:**
- title: Installation and upgrade notes

**Incorrect:**
- title: Installation and Upgrade Notes

---

## Rule 39 — General Sidebar Labels: Use Sentence Case

For all sidebar labels in release notes (including non-What's New documents), use sentence case. Capitalize only the first word and proper nouns.

**Correct:**
- sidebar_label: Installation and upgrade notes

**Incorrect:**
- sidebar_label: Installation and Upgrade Notes

---

## Rule 40 — Section Headings in Non-What's New Documents: Use Sentence Case

For all section headings in non-What's New document types, use sentence case. Capitalize only the first word and proper nouns.

**Correct:**
- ## For installation
- ## For upgrade

**Incorrect:**
- ## Installation
- ## Upgrade

---

## Rule 41 — What's New: Use "Key Management Services (KMS)" as Standard Terminology

When referring to key management services, use "Key Management Services (KMS)" as the standard terminology. Do not use other variations.

**Correct:**
- Supports Key Management Services (KMS) for encryption key management.

**Incorrect:**
- Supports key management service for encryption key management.

---

## Rule 42 — What's New: Use "in clusters with the AArch64 architecture" Instead of "in AArch64 architecture clusters"

Use "in clusters with the AArch64 architecture" instead of "in AArch64 architecture clusters" when describing architecture-specific features.

**Correct:**
- Supports this feature in clusters with the AArch64 architecture.

**Incorrect:**
- Supports this feature in AArch64 architecture clusters.

---

## Rule 43 — What's New: Use "dedicated physical disk" Instead of "independent physical disk"

Use "dedicated physical disk" instead of "independent physical disk" when referring to disks assigned for specific purposes.

**Correct:**
- Uses a dedicated physical disk for cache.

**Incorrect:**
- Uses an independent physical disk for cache.

---

## Rule 44 — What's New: Use "prevents performance fluctuations" Instead of "avoids performance fluctuations"

Use "prevents performance fluctuations" instead of "avoids performance fluctuations" when describing features that stabilize performance.

**Correct:**
- Prevents performance fluctuations during high I/O load.

**Incorrect:**
- Avoids performance fluctuations during high I/O load.

---

## Rule 45 — What's New: Use "bandwidth limits" Instead of "throttling policies"

Use "bandwidth limits" instead of "throttling policies" when referring to bandwidth restriction mechanisms.

**Correct:**
- Configures bandwidth limits for data replication.

**Incorrect:**
- Configures throttling policies for data replication.

---

## Rule 46 — What's New: Use "pre-upgrade checks" Instead of "upgrade prechecks"

Use "pre-upgrade checks" instead of "upgrade prechecks" when referring to validation steps before an upgrade.

**Correct:**
- Runs pre-upgrade checks to verify system readiness.

**Incorrect:**
- Runs upgrade prechecks to verify system readiness.

---

## Rule 47 — What's New: Use Descriptive Phrasing for VM Placement Group Rules

When describing features that allow ignoring VM placement group rules, use phrasing that clearly explains the action and purpose, such as "to ignore specified VM placement group rules and avoid rule conflicts".

**Correct:**
- Allows configuring the system to ignore specified VM placement group rules and avoid rule conflicts.

**Incorrect:**
- Allows ignoring specified VM placement group rules.

---

## Rule 48 — What's New: Use "port status detection frequency" Instead of "network port status detection interval"

Use "port status detection frequency" instead of "network port status detection interval" when referring to how often port status is checked.

**Correct:**
- Adjusts the port status detection frequency.

**Incorrect:**
- Adjusts the network port status detection interval.

---

## Rule 49 — What's New: Use "BMC IP address" Instead of "BMC IP" in Descriptive Text

Use "BMC IP address" instead of "BMC IP" in descriptive text within What's New entries.

**Correct:**
- Detects the BMC IP address automatically.

**Incorrect:**
- Detects the BMC IP automatically.

---

## Rule 50 — What's New: Use "Supports" with Gerund for VM-as-Subject Restructuring

When restructuring sentences where the original Chinese uses a VM or platform as the subject performing an action, use a "Supports + gerund" pattern with the feature as the subject.

**Correct:**
- Supports automatically configuring a maximum of 4 virtual disk multi-queues for virtual machines on Intel x86_64 and Kunpeng AArch64 platforms to improve virtual machine performance.

**Incorrect:**
- VMs on Intel x86_64 and Kunpeng AArch64 platforms support automatic configuration of up to 4 virtual disk multi-queues to improve VM performance.

---

## Rule 51 — Resolved Issues: Use "pinned volume" Instead of "persistent cache volume"

When referring to volumes that persistently cache data, use "pinned volume" instead of "persistent cache volume". Use "pinned in the cache" instead of "remain in persistent cache".

**Correct:**
- After creating a snapshot for a pinned volume, the data might fail to remain pinned in the cache. The issue has been resolved in this release.

**Incorrect:**
- After a snapshot was created for a persistent cache volume, the data might not remain in persistent cache. The issue has been resolved in this release.

---

## Rule 52 — What's New: Add "Copy-on-Write (COW)" Expansion for Acronym Clarity

When using the acronym "COW" to refer to Copy-on-Write technology, explicitly expand it as "Copy-on-Write (COW)" on first usage in an entry.

**Correct:**
- Optimizes the granularity of snapshot COW (Copy-on-Write).

**Incorrect:**
- Optimizes the granularity of snapshot COW.

---

## Rule 53 — Resolved Issues: Handle Partial Deletion Appropriately

When a resolved issue entry is deleted in its entirety, it may be removed from the release notes. Do not leave empty bullet points or placeholder text.

**Correct:**
- *(Entry removed entirely)*

**Incorrect:**
- - *(empty bullet point)*
- Fixed the issue where, after node replacement... *(retained incorrectly)*