# Operational Document Style Guide

**Document type:** `operational_documents`
**Applies to:** Administration guides, user guides, installation and deployment guides, and any procedural documentation.
**Language pair:** Simplified Chinese → English
**Scope:** Translation style rules covering headings, person, courtesy language, UI interactions, and UI element labeling.

---

## Rule 1 — Section Headings: Use Gerund (-ing) Form

All section headings must begin with a gerund (the -ing form of a verb). Do not use noun phrases or imperative verbs as headings.

**Correct:**
- Creating virtual machines
- Configuring network settings
- Installing the deployment agent
- Managing user permissions

**Incorrect:**
- Virtual Machine Creation *(noun phrase — wrong)*
- Create a Virtual Machine *(imperative — wrong)*
- How to Create a Virtual Machine *(how-to phrasing — wrong)*
- Creating Virtual Machines *(title case in a section heading — wrong, see Rule 6)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 创建虚拟机 | Creating virtual machines |
| 网络配置 | Configuring network settings |
| 安装部署代理 | Installing the deployment agent |
| 用户权限管理 | Managing user permissions |

---

## Rule 2 — Sidebar Labels: Use Gerund (-ing) Form and Sentence Case

All sidebar labels must use the gerund (-ing) form and sentence case (only the first word and proper nouns are capitalized).

**Correct:**
- Planning backup plans
- Creating a backup repository
- Associating clusters
- Viewing backup repositories

**Incorrect:**
- Backup Plan Planning *(noun phrase — wrong)*
- Create Backup Repository *(imperative — wrong)*
- Add Associated Cluster *(imperative — wrong)*
- Planning License Unit Allocation *(title case — wrong)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 备份计划规划 | Planning backup plans |
| 创建备份仓库 | Creating a backup repository |
| 添加关联集群 | Associating clusters |
| 查看备份仓库 | Viewing backup repositories |
| 规划许可单元分配 | Planning license unit allocation |

---

## Rule 3 — Document Titles: Use Gerund (-ing) Form and Sentence Case

All document titles (`title:` front matter) must use the gerund (-ing) form and sentence case (only the first word and proper nouns are capitalized).

**Correct:**
- Planning backup plans
- Creating a backup repository
- Associating clusters

**Incorrect:**
- Backup Plan Planning *(noun phrase — wrong)*
- Create Backup Repository *(imperative — wrong)*
- Planning License Unit Allocation *(title case — wrong)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 备份计划规划 | Planning backup plans |
| 创建备份仓库 | Creating a backup repository |
| 添加关联集群 | Associating clusters |
| 规划许可单元分配 | Planning license unit allocation |

---

## Rule 4 — Section Headings: Use Sentence Case

All section headings must use sentence case: capitalize only the first word and proper nouns. Do not use title case or all uppercase.

**Correct:**
- Creating virtual machines
- Configuring network settings
- Installing the deployment agent

**Incorrect:**
- Creating Virtual Machines *(title case — wrong)*
- CONFIGURING NETWORK SETTINGS *(all uppercase — wrong)*

---

## Rule 5 — Descriptions and Verbs: Use Third-Person Singular

When describing the function or purpose of a feature in bullet points or list items, use the third-person singular form of the verb (ending in -s) rather than the imperative form.

**Correct:**
- **Data protection**: Prevents data corruption and loss caused by human error, virus infection, logical faults, and other factors.
- **Data reuse**: Leverages backup data for development, testing, troubleshooting, and other purposes, avoiding any impact on the production environment.
- **Data security**: Prevents large-scale data loss caused by ransomware attacks.

**Incorrect:**
- **Data protection**: Prevent data corruption and loss caused by human error, virus infection, logical errors, and other factors. *(imperative — wrong)*
- **Data reuse**: Use backup data for development, testing, troubleshooting, and more, without affecting the production environment. *(imperative — wrong)*
- **Data security**: Prevent large-scale data loss caused by ransomware attacks. *(imperative — wrong)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 数据保护：防止人为错误、病毒感染、逻辑错误等因素造成的数据损坏和丢失。 | **Data protection**: Prevents data corruption and loss caused by human error, virus infection, logical faults, and other factors. |
| 数据复用：将备份数据用于开发、测试、故障排除等场景，不影响生产环境。 | **Data reuse**: Leverages backup data for development, testing, troubleshooting, and other purposes, avoiding any impact on the production environment. |
| 数据安全：防止勒索软件攻击导致的大规模数据丢失。 | **Data security**: Prevents large-scale data loss caused by ransomware attacks. |

---

## Rule 6 — UI Element Labels: Match the Actual UI Text

When referring to a specific UI element (button, tab, menu item, dialog box, etc.), use the exact text that appears in the user interface. Do not translate, paraphrase, or change the label.

**Correct:**
- Click **Save**
- Click **Edit association**
- Click **Associated cluster**
- Click **+ Create backup repository**

**Incorrect:**
- Click **Save** button *(adding "button" — wrong)*
- Click **Edit Cluster Association** *(if the UI says "Edit association" — wrong)*
- Click **SMTX OS Cluster Association** *(if the UI says "Associated cluster" — wrong)*

**Note:** Always verify the actual UI text. The UI label may differ from a literal translation of the source text.

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 点击“保存” | Click **Save** |
| 点击“编辑关联” | Click **Edit association** |
| 点击“关联集群” | Click **Associated cluster** |
| 点击“+ 创建备份仓库” | Click **+ Create backup repository** |

---

## Rule 7 — UI Interaction Descriptions: Use Active Voice and Direct Descriptions

When describing a user interaction with the UI, use active voice and directly describe the action. Avoid passive constructions or indirect phrasing.

**Correct:**
- In the left sidebar of the **Backup & DR** page in CloudTower, click **Settings**.
- In the pop-up dialog box, select a deployed backup service and click **Associated cluster**.
- Click **Edit association**. In the pop-up dialog box, add one or more SMTX OS (ELF) clusters.

**Incorrect:**
- Log in to CloudTower, and in the **Backup and Disaster Recovery** page, click **Settings**. *(indirect — wrong)*
- In the pop-up window that appears, add one or more SMTX OS (ELF) clusters. *(vague — wrong)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 登录 CloudTower，在“备份与容灾”页面点击“设置”。 | In the left sidebar of the **Backup & DR** page in CloudTower, click **Settings**. |
| 在弹出的窗口中，选择一个已部署的备份服务，点击“SMTX OS 集群关联”。 | In the pop-up dialog box, select a deployed backup service and click **Associated cluster**. |
| 点击“编辑集群关联”，在出现的操作窗口中添加一个或多个 SMTX OS (ELF) 集群。 | Click **Edit association**. In the pop-up dialog box, add one or more SMTX OS (ELF) clusters. |

---

## Rule 8 — UI Element Names: Use Sentence Case

When referring to UI element names in the text (not as labels), use sentence case: capitalize only the first word and proper nouns.

**Correct:**
- backup repository
- backup service
- backup plan
- restore point
- backup schedule

**Incorrect:**
- Backup Repository *(title case — wrong)*
- Backup Service *(title case — wrong)*
- Backup Plan *(title case — wrong)*
- Recovery Point *(if the UI uses "restore point" — wrong)*
- Backup Cycle *(if the UI uses "backup schedule" — wrong)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 备份仓库 | backup repository |
| 备份服务 | backup service |
| 备份计划 | backup plan |
| 恢复点 | restore point |
| 备份周期 | backup schedule |

---

## Rule 9 — Terminology Consistency: Use Standardized Terms

Use the following standardized terms consistently throughout the documentation. Do not use synonyms or alternative phrasings.

| Chinese source | Standard English term |
|---|---|
| 备份服务 | backup service |
| 备份仓库 | backup repository |
| 备份计划 | backup plan |
| 恢复点 | restore point |
| 备份周期 | backup schedule |
| 恢复点保留策略 | restore point retention policy |
| 关联集群 | associated cluster |
| 编辑关联 | Edit association |
| 弹出对话框 | pop-up dialog box |
| 左侧边栏 | left sidebar |
| 产品名称 | SMTX Backup & Disaster Recovery (or SMTX Backup & DR) |

**Incorrect:**
- recovery point *(use "restore point" instead)*
- backup cycle *(use "backup schedule" instead)*
- pop-up window *(use "pop-up dialog box" instead)*
- SMTX Backup and Disaster Recovery *(use "SMTX Backup & Disaster Recovery" or "SMTX Backup & DR" instead)*

---

## Rule 10 — Sentence Structure: Use Active Voice and Clear Subject

When describing system behavior or user actions, use active voice and clearly state the subject of the action.

**Correct:**
- The backup service creates a restore point for each virtual machine.
- You can configure the restore point retention policy to control the number of restore points.
- After deploying a backup service, you need to associate it with the SMTX OS (ELF) clusters.

**Incorrect:**
- After each backup plan is executed, the backup service creates a recovery point for each virtual machine. *(passive opening — wrong)*
- The recovery point retention policy can be defined to specify the number of restore points. *(passive — wrong)*
- After the backup service is deployed, associate the backup service with the SMTX OS (ELF) cluster. *(ambiguous subject — wrong)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 每次备份计划执行后，备份服务会为备份计划中的每个虚拟机创建一个恢复点。 | After executing a backup plan, the backup service creates a restore point for each virtual machine in the backup plan. |
| 恢复点保留策略可以定义要保留的恢复点数量或时间范围。 | The restore point retention policy can be defined to specify the number of restore points to be retained and the time range. |
| 备份服务部署后，将备份服务与要保护的虚拟机所在的 SMTX OS (ELF) 集群关联。 | After deploying a backup service, you need to associate it with the SMTX OS (ELF) clusters hosting the virtual machines to be protected. |

---

## Rule 11 — List Item Labels: Use Singular Form

When labeling list items (e.g., bullet points describing categories or parameters), use the singular form of the noun.

**Correct:**
- **Backup object**
- **Backup schedule**
- **Restore point retention policy**
- **Prerequisite**

**Incorrect:**
- **Backup objects** *(plural — wrong)*
- **Recovery point retention policy** *(wrong terminology — wrong)*
- **Prerequisites** *(plural — wrong)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 备份对象 | **Backup object** |
| 备份周期 | **Backup schedule** |
| 恢复点保留策略 | **Restore point retention policy** |
| 前提条件 | **Prerequisite** |

---

## Rule 12 — Table Headers: Use Bold Formatting

When creating tables, format the header row in bold.

**Correct:**
| **Parameter** | **Description** |
|---|---|
| Value 1 | Description 1 |

**Incorrect:**
| Parameter | Description |
|---|---|
| Value 1 | Description 1 |

---

## Rule 13 — Blockquote Formatting: Add Space After Marker

When using blockquotes (for notes, warnings, or callouts), add a space after the `>` marker.

**Correct:**
> **Note**: This is a note.

**Incorrect:**
>**Note**: This is a note.

---

## Rule 14 — Verb Choice for UI Actions: Use Precise Verbs

Use precise verbs to describe user actions in the UI. Match the verb to the type of UI element.

**Correct:**
- Enter the name and description of the backup repository. *(for text input fields)*
- Select the backup service to associate with the backup repository. *(for dropdown menus or selection lists)*
- Click **Save**. *(for buttons)*

**Incorrect:**
- Set the name and description of the backup repository. *(vague — use "Enter" instead)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 设置备份仓库的名称和描述。 | Enter the name and description of the backup repository. |
| 选择与备份仓库关联的备份服务。 | Select the backup service to associate with the backup repository. |

---

## Rule 15 — Article Usage: Use Definite Article for System-Specific References

When referring to a specific instance of a system component (e.g., the backup service that has been deployed), use the definite article "the." Use the indefinite article "a" or "an" for general references.

**Correct:**
- The backup service can only be associated with clusters whose connection status with CloudTower is `Connected`. *(referring to a specific deployed service)*
- A backup service can be associated with multiple backup repositories. *(general statement)*

**Incorrect:**
- A backup service can only be associated with clusters whose connection status with CloudTower is `Connected`. *(incorrect for specific reference)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 备份服务只能与 CloudTower 连接状态为“Connected”的集群关联。 | The backup service can only be associated with clusters whose connection status with CloudTower is `Connected`. |
| 一个备份服务可以关联多个备份仓库。 | A backup service can be associated with multiple backup repositories. |

---

## Rule 16 — Number Agreement: Use Singular for Collective References

When referring to a system component in a general or collective sense, use the singular form. Use the plural form only when specifically referring to multiple instances.

**Correct:**
- Click **Save** to complete the association between the backup service and the cluster. *(general reference)*
- The backup service can be associated with multiple clusters. *(multiple instances)*

**Incorrect:**
- Click **Save** to complete the association between the backup service and the clusters. *(unnecessary plural — wrong)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 点击“保存”，完成备份服务与集群的关联。 | Click **Save** to complete the association between the backup service and the cluster. |
| 备份服务可以关联多个集群。 | The backup service can be associated with multiple clusters. |

---

## Rule 17 — Sidebar Labels: Use Descriptive Content Appropriate for Context

Sidebar labels should use descriptive and contextually appropriate content. While the gerund form and sentence case are required (see Rule 2), the specific words used should accurately reflect the content and be suitable for navigation purposes. Avoid generic or non-descriptive labels when more specific alternatives exist.

**Correct:**
- Introduction *(for an introductory overview section)*
- Planning backup plans *(for detailed planning content)*
- Associating clusters *(for cluster association tasks)*

**Incorrect:**
- Overview *(if the section is introductory in nature but a more specific label like "Introduction" better reflects the content)*

**Note:** This rule complements Rule 2 (form and case) by addressing word choice and content appropriateness.

---

## Rule 18 — Document Titles: Use Descriptive Content Appropriate for Context

Document titles should use descriptive and contextually appropriate content. While the gerund form and sentence case are required (see Rule 3), the specific words used should accurately reflect the document's content and purpose. Avoid generic or non-descriptive titles when more specific alternatives exist.

**Correct:**
- Introduction *(for an introductory overview document)*
- Planning backup plans *(for detailed planning content)*
- Associating clusters *(for cluster association tasks)*

**Incorrect:**
- Overview *(if the document is introductory in nature but a more specific title like "Introduction" better reflects the content)*

**Note:** This rule complements Rule 3 (form and case) by addressing word choice and content appropriateness.

---

## Rule 19 — Section Headings: Use Descriptive Content Appropriate for Context

Section headings should use descriptive and contextually appropriate content. While the gerund form and sentence case are required (see Rules 1 and 4), the specific words used should accurately reflect the section's content and purpose. Avoid generic or non-descriptive headings when more specific alternatives exist.

**Correct:**
- Introduction *(for an introductory overview section)*
- Planning backup plans *(for detailed planning content)*
- Associating clusters *(for cluster association tasks)*

**Incorrect:**
- Overview *(if the section is introductory in nature but a more specific heading like "Introduction" better reflects the content)*

**Note:** This rule complements Rules 1 and 4 (form and case) by addressing word choice and content appropriateness.

---

## Rule 20 — Word Choice: Use Precise and Contextually Appropriate Verbs

Use precise verbs that accurately convey the intended meaning in context. Avoid vague or generic verbs when more specific alternatives better communicate the action or state.

**Correct:**
- Backup and recovery can be applied in the following scenarios *(more precise than "used")*
- The backup service of SMTX Backup & Disaster Recovery backs up virtual machines *(clear ownership structure)*

**Incorrect:**
- Backup and recovery can be used in the following scenarios *(vague — "applied" is more precise in this context)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 备份与恢复可用于以下场景 | Backup and recovery can be applied in the following scenarios |

---

## Rule 21 — Sentence Structure: Use Clear Temporal and Causal Relationships

When describing sequences of events or cause-and-effect relationships, use clear and logical sentence structures that accurately convey the temporal or causal connection.

**Correct:**
- A full backup will be performed during the initial backup. *(clear temporal relationship)*
- Backs up all data that has changed since the last backup. *(clear temporal reference)*
- Makes a full copy of all data of the virtual machine when the backup is performed. *(clear temporal connection)*

**Incorrect:**
- A full backup is performed for the first backup. *(ambiguous temporal relationship)*
- Backs up all changed data based on the previous backup. *(unclear reference point)*
- Makes a complete copy of all data on the virtual machine at the time the backup is performed. *(less precise phrasing)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 首次备份将执行全量备份。 | A full backup will be performed during the initial backup. |
| 基于上一次备份备份所有更改的数据。 | Backs up all data that has changed since the last backup. |
| 在备份执行时，对虚拟机上的所有数据进行完整复制。 | Makes a full copy of all data of the virtual machine when the backup is performed. |

---

## Rule 22 — List Item Phrasing: Use Clear and Readable Structures

When phrasing list items that describe categories or groupings, use clear and readable structures that place the key information prominently.

**Correct:**
- **Virtual machines in SMTX OS (ELF) clusters** *(clear, readable structure)*
- **Volumes in SMTX ZBS block storage clusters** *(clear, readable structure)*

**Incorrect:**
- **SMTX OS (ELF) cluster virtual machines** *(ambiguous modifier structure)*
- **SMTX ZBS block storage cluster volumes** *(ambiguous modifier structure)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| SMTX OS (ELF) 集群虚拟机 | **Virtual machines in SMTX OS (ELF) clusters** |
| SMTX ZBS 块存储集群卷 | **Volumes in SMTX ZBS block storage clusters** |

---

## Rule 23 — Table Content Formatting: Use Consistent Formatting

When including example values or code-like content in tables, use consistent formatting (e.g., quotation marks or plain text) appropriate for the content type.

**Correct:**
| Field | Description | Example |
|---|---|---|
| Name | The name of the backup repository | "nfs_repo" |

**Incorrect:**
| Field | Description | Example |
|---|---|---|
| Name | The name of the backup repository | """nfs_repo""" *(inconsistent triple quotes)* |

---

## Rule 24 — UI Interaction Descriptions: Use Precise Navigation Language

When describing navigation to access a UI element, use precise language that accurately reflects the user's path and action.

**Correct:**
- Click the row of a backup repository to enter its details panel.
- Select **Backup repository** in the left sidebar of the **Backup & DR** page.

**Incorrect:**
- Click a row in a backup repository list to view... *(vague — doesn't specify the result action)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 单击备份仓库列表中的一行以查看... | Click the row of a backup repository to enter its details panel. |

---

## Rule 25 — Sentence Structure: Use Clear Temporal Sequencing

When describing processes or procedures, use clear temporal sequencing to indicate the order of operations.

**Correct:**
- Once a backup repository is created, the backup service will connect to it and perform the initial configuration.

**Incorrect:**
- After a backup repository is created, the backup service connects to it and performs initialization configuration. *(less precise temporal relationship)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 备份仓库创建后，备份服务会连接到它并执行初始化配置。 | Once a backup repository is created, the backup service will connect to it and perform the initial configuration. |

---

## Rule 26 — UI Element Labels: Match Exact UI Text Including Case

When referring to UI element labels in text (not as clickable labels), use the exact text as it appears in the UI, including the correct case. This applies to dialog box titles, field names, and other UI text.

**Correct:**
- Edit the relevant information in the pop-up **Edit backup repository** dialog box.
- Click **Delete** in the pop-up **Delete backup repository** dialog box.

**Incorrect:**
- Edit the relevant information in the **Edit Backup Repository** dialog. *(title case — wrong)*

**Note:** This rule extends Rule 6 to cover dialog box titles and other UI text that appears in the interface, ensuring exact case matching.

---

## Rule 27 — Verb Choice for UI Actions: Use Precise Verbs for Selection and Association

Use precise verbs when describing selection and association actions in the UI. "Select" is used for choosing from a list or dropdown; "associate with" is used for establishing connections between components.

**Correct:**
- Select the backup service to associate with the backup repository.
- Select the backup repository type and configure the settings.

**Incorrect:**
- Select the backup service associated with the backup repository. *(ambiguous — implies existing association rather than action)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 选择与备份仓库关联的备份服务。 | Select the backup service to associate with the backup repository. |

---

## Rule 28 — Punctuation: Use Consistent Comma Usage in Lists

When listing items or actions in a series, use consistent comma usage. In a list of two items joined by "and," do not use a comma before "and." In a list of three or more items, use the Oxford comma (comma before "and").

**Correct:**
- Select the backup repository type and configure the settings. *(no comma before "and" for two items)*
- Select the backup repository type, configure the settings, and click **Save**. *(Oxford comma for three or more items)*

**Incorrect:**
- Select the backup repository type, and configure the settings. *(unnecessary comma for two items)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 选择备份仓库类型，并配置相关设置。 | Select the backup repository type and configure the settings. |

---

## Rule 29 — Word Choice: Use Precise Terms for UI Fields

When referring to UI fields, use the exact field label as it appears in the interface. Do not shorten or paraphrase field names.

**Correct:**
- **Server address**: Enter the IP address of the backup repository server.
- **Destination path**: Enter the destination path for the backup repository.

**Incorrect:**
- **Server**: Enter the IP address of the server for the backup repository. *(shortened field name)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 服务器：输入备份仓库服务器的 IP 地址。 | **Server address**: Enter the IP address of the backup repository server. |

---

## Rule 30 — Sentence Structure: Use Clear and Direct Phrasing for Paths and Locations

When describing file paths, directories, or locations, use clear and direct phrasing that avoids ambiguity.

**Correct:**
- Ensure that the path is an empty directory.
- The path must not overlap with the path of another backup repository.

**Incorrect:**
- Make sure this path is an empty directory...and that it does not duplicate the path of another backup repository. *(less precise phrasing)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 确保此路径为空目录...并且不与其他备份仓库的路径重复。 | Ensure that the path is an empty directory. The path must not overlap with the path of another backup repository. |

---

## Rule 31 — Word Choice: Use Precise Terms for Recommendations and Options

When making recommendations or presenting options, use precise language that clearly indicates the nature of the recommendation.

**Correct:**
- If both 'NFS 3' and 'NFS 4' are supported, it is recommended to choose 'NFS 4'.

**Incorrect:**
- If both 'NFS 3' and 'NFS 4' are supported, 'NFS 4' is recommended. *(less explicit phrasing)*

**Examples (Chinese source → English translation):**

| Chinese source | English translation |
|---|---|
| 如果同时支持 'NFS 3' 和 'NFS 4'，建议选择 'NFS 4'。 | If both 'NFS 3' and 'NFS 4' are supported, it is recommended to choose 'NFS 4'. |