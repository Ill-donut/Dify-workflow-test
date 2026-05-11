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
