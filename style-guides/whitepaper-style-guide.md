# Whitepaper style guide

**Document type:** `whitepaper`
**Applies to:** Technical whitepapers, solution briefs, architecture overviews, and any long-form analytical or persuasive technical documents.
**Language pair:** Simplified Chinese → English
**Scope:** Translation style rules covering sentence structure, logical connectors, sentence restructuring, and capitalization.

---

## Rule 1 — Sentence Structure: Full Declarative and Complex Sentences Are Expected

Whitepaper prose should read as complete, well-formed sentences. Unlike procedural documents, whitepapers allow — and often require — passive voice, conditional sentences, and causal constructions. Do not flatten complex ideas into short imperative sentences.

**Permitted structures:**

**Passive voice** — use when the subject doing the action is less important than the object or result:
- This configuration is completed by the system during initialization.
- The encryption key is generated automatically and stored in a secure vault.

**Conditional sentences** — use when describing behavior that depends on a condition:
- If the primary node becomes unavailable, the system automatically promotes the standby node.
- When resource usage exceeds the defined threshold, the scheduler redistributes workloads across available nodes.

**Causal sentences** — use when explaining why something works or happens:
- Because the architecture decouples compute from storage, each layer can scale independently.
- The system maintains low latency even under peak load, as requests are distributed evenly across all nodes.

**Examples (Chinese source → English translation):**

| Chinese source | English translation | Structure used |
|---|---|---|
| 该功能支持多节点部署。 | This feature supports multi-node deployment. | Declarative |
| 主节点故障时，系统自动切换到备用节点。 | If the primary node fails, the system automatically switches to the standby node. | Conditional |
| 采用分布式架构，系统性能大幅提升。 | Because the system adopts a distributed architecture, overall performance is significantly improved. | Causal |
| 该配置由管理员在初始化阶段完成。 | This configuration is completed by the administrator during the initialization phase. | Passive |

---

## Rule 2 — Heading and Title Capitalization: Use Sentence Case

Headings, sidebar labels, and document titles should use **sentence case** (capitalize only the first word and proper nouns), not title case (capitalizing every major word).

**Correct examples:**
- Document update history
- Virtual machine service architecture
- Job scheduling mechanism
- Job task dependency
- Virtual machine high availability
- Virtual machine auto-scheduling

**Incorrect examples:**
- Document Update Information
- Virtual Machine Service Architecture
- Job Scheduling Mechanism
- Job Task Dependencies
- Virtual Machine High Availability
- Virtual Machine Automatic Scheduling

---

## Rule 3 — UI Labels and Sidebar Labels: Use Sentence Case

UI labels, sidebar labels, and navigation elements should use **sentence case** (capitalize only the first word and proper nouns).

**Correct examples:**
- sidebar_label: Document update history
- sidebar_label: Virtual machine service architecture
- sidebar_label: Job scheduling mechanism
- sidebar_label: Job task dependency

**Incorrect examples:**
- sidebar_label: Document Update Information
- sidebar_label: Virtual Machine Service Architecture
- sidebar_label: Job Scheduling Mechanism
- sidebar_label: Job Task Dependencies

---

## Rule 4 — Terminology: Expand Abbreviations on First Use

When a technical abbreviation or acronym appears for the first time in a document, spell out the full term followed by the abbreviation in parentheses.

**Example:**
- Kernel-based Virtual Machine (KVM) — not just KVM on first use
- Virtual Machine (VM) — not just VM on first use

---

## Rule 5 — Verb Choice: Use Precise, Active Verbs

Prefer precise, active verbs over vague or overly formal constructions. Avoid redundant phrasing.

**Preferred verbs and phrases:**
- "addresses requirements" — not "implements the requirements of"
- "published with" — not "in conjunction with the release of"
- "the following examples illustrate" — not "below are examples to illustrate"
- "as follows" — not "summarized as follows"

---

## Rule 6 — Pronoun Usage: Use "You" for Direct Address

When addressing the reader or user directly, use the second-person pronoun "you" rather than the third-person "users" for a more engaging and direct tone.

**Example:**
- "You can manage the system through a simple web interface" — not "Users can manage the system through simple web interactions"

---

## Rule 7 — Bullet Points: Use Descriptive Phrases, Not Imperatives

Bullet points in whitepapers should be descriptive, well-formed phrases or sentences, not imperative commands. Use present participles or complete declarative phrases.

**Correct examples:**
- Periodically collecting static Guest OS information from virtual machines and persisting it to MongoDB.
- Providing a gRPC interface to query virtual machine information.
- Providing a file system quiescing interface to support file-system consistent snapshots.

**Incorrect examples:**
- Collect static Guest OS information from virtual machines and persist it to MongoDB.
- Provide a gRPC interface to query virtual machine information.
- Provide interfaces for silent file systems to support consistent snapshots.

---

## Rule 8 — Conciseness: Remove Unnecessary Words

Eliminate redundant or filler words in headings, bullet points, and sentences. Prefer shorter, more direct phrasing.

**Examples:**
- "Fully distributed architecture" — not "Fully distributed architecture design"
- "Successful Job" — not "Normal Successful Job"
- "Simple and intuitive Web UI" — not "Simple and easy-to-use Web UI"
- "The following two examples illustrate" — not "Below are two simple examples to illustrate"

---

## Rule 9 — Technical Terminology: Prefer Standard Industry Terms

Use standard industry terminology and phrasing for technical concepts rather than literal or awkward translations.

**Examples:**
- "supports Layer 2 VLAN network isolation" — not "supports VLAN Layer 2 network isolation"
- "covering most network use cases" — not "meeting most network usage scenarios"
- "ensuring business continuity" — not "to ensure high business availability"
- "enters read-only state" — not "enters read-only mode"

---

## Rule 10 — Prepositional Phrase Word Order: Prefer "over" for Service Dependencies

When describing a service that depends on another service or protocol, use the pattern "[Service] over [Protocol/Infrastructure]" rather than "[Protocol/Infrastructure]-based [Service]".

**Examples:**
- "The ZBS service over NFS" — not "The NFS-based ZBS service"
- "the Job Center heartbeat check over MongoDB" — not "the MongoDB-based Job Center heartbeat check"

---

## Rule 11 — Subject-Verb Agreement: Use Correct Agreement with "Any"

When "any" is used in conditional phrases like "any of the following conditions," the verb should agree with the plural noun that follows "any of."

**Example:**
- "when any of the following conditions are met" — not "when any of the following conditions is met"

---

## Rule 12 — Introductory Phrases: Use Clear, Direct Openers

Prefer clear and direct introductory phrases over wordy or indirect ones.

**Examples:**
- "The task scheduling rules are as follows:" — not "Task scheduling follows these principles:"
- "As shown in the diagram above, the concurrent execution steps are as follows:" — not "As shown in the figure above, the concurrent execution steps are summarized as follows:"
- "Currently, the main scheduled Jobs include:" — not "Currently, the scheduled Jobs mainly include:"

---

## Rule 13 — Punctuation Consistency in Bullet Points

Use consistent punctuation within bullet point lists. If one bullet point ends with a period, all bullet points in the same list should end with a period. If one uses a semicolon, all should use a semicolon. Prefer periods for complete sentences and semicolons for fragments.

---

## Rule 14 — Product and Component Name Consistency

Use consistent product and component names throughout the document. Do not vary between abbreviated and full forms, and avoid unnecessary qualifiers.

**Examples:**
- "VMTools Agent" — not "VM VMTools Agent" (avoid redundant abbreviation)
- "Periodic collection and cleanup tasks" — not "Scheduled collection and cleanup tasks" (use consistent terminology)