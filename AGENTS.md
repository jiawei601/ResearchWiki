

本文件是论文知识库项目的总控制规则。  
它只负责说明项目结构、任务路由和不可违背的基本原则。  
具体任务细节请读取 `agents/`、`templates/` 和 `memory/` 中的对应文件。

本项目的目标是：  
使用 Codex / LLM Agent + Obsidian，把论文从零散 PDF 转化为可持续维护的 Markdown 知识库，用于论文阅读、文献综述、research gap 分析、选题定位和写作积累。

---

## 1. 核心思想

本项目不是普通的 PDF 摘要工具，也不是一次性的 RAG 问答系统。

本项目采用三层结构：

1. `raw/`：原始资料层，保存 PDF、Zotero 导出文件、截图、笔记等原始材料。
    
2. `wiki/`：结构化知识层，保存论文卡片、topic、method、claim、gap、review 等 Markdown 页面。
    
3. `memory/`、`agents/`、`templates/`：规则层，告诉 Codex 如何读取、整理、链接和维护知识库。
    

每次导入新论文时，Codex 不应只生成单篇摘要，还应更新相关 topic、method、claim、gap、index 和 log，让知识库不断积累。

---

## 2. 目录职责

推荐目录结构：

```text
ResearchWiki/
├── AGENTS.md
├── index.md
├── log.md
├── inbox.md
│
├── raw/
│   ├── papers/
│   ├── notes/
│   ├── assets/
│   └── zotero_imports/
│
├── wiki/
│   ├── papers/
│   ├── authors/
│   ├── topics/
│   ├── methods/
│   ├── datasets/
│   ├── metrics/
│   ├── claims/
│   ├── gaps/
│   └── reviews/
│
├── synthesis/
│   ├── literature-map.md
│   ├── open-questions.md
│   ├── research-positioning.md
│   ├── review-outline.md
│   └── core-argument-map.md
│
├── agents/
│   ├── import_zotero.md
│   ├── pdf_read_agent.md
│   ├── synthesis_agent.md
│   ├── gap_agent.md
│   ├── review_agent.md
│   └── lint_agent.md
│
├── templates/
│   ├── pdf_ingestion_template.md
│   ├── paper.md
│   ├── topic.md
│   ├── method.md
│   ├── claim.md
│   ├── gap.md
│   └── review.md
│
└── memory/
    ├── project_profile.md
    ├── hard_memory.md
    ├── context_policy.md
    ├── style_snapshot.md
    ├── tag_taxonomy.md
    ├── term_aliases.md
    ├── error_log.md
    └── decision_log.md
```

---

## 3. 每次任务启动规则

执行任何任务前，先读取：

```text
AGENTS.md
memory/project_profile.md
memory/hard_memory.md
memory/error_log.md
memory/tag_taxonomy.md
memory/term_aliases.md
index.md
log.md
```

然后根据任务类型读取对应的 `agents/*.md` 和 `templates/*.md`。

如果某个文件不存在，应提醒用户创建，不要假装已经读取。

---

## 4. 任务路由

根据用户任务选择对应 agent：

### 4.1 论文入库

当用户要求从 Zotero 指定 collection / 文件夹读取论文候选清单时，先读取：

```text
agents/import_zotero.md
```

它通过 Codex Zotero 插件 / connector 读取指定 collection，只负责条目识别、元数据读取、去重检查、生成 `raw/zotero_imports/<collection_name>/import_plan.md` 和 `manifest.json`。单篇论文解读仍交给 `pdf_read_agent.md`。

当用户要求读取单篇 PDF、生成论文卡片、提取摘要/方法/创新点/局限性时，读取：

```text
agents/pdf_read_agent.md
templates/pdf_ingestion_template.md
```

主要输出到：

```text
wiki/papers/
wiki/topics/
wiki/methods/
wiki/claims/
wiki/gaps/
```

并更新：

```text
index.md
log.md
```

---

### 4.2 多论文综合

当用户要求对比多篇论文、整理研究路线、构建 literature map 时，读取：

```text
agents/synthesis_agent.md
```

主要输出到：

```text
synthesis/literature-map.md
wiki/reviews/
wiki/topics/
wiki/methods/
```

---

### 4.3 Research Gap 分析

当用户要求寻找 research gap、创新点、选题定位、研究不足时，读取：

```text
agents/gap_agent.md
```

主要输出到：

```text
wiki/gaps/
synthesis/open-questions.md
synthesis/research-positioning.md
```

---

### 4.4 文献综述写作

当用户要求写文献综述、related work、研究现状、综述大纲时，读取：

```text
agents/review_agent.md
templates/review.md
```

主要输出到：

```text
wiki/reviews/
synthesis/review-outline.md
```

---

### 4.5 知识库检查

当用户要求检查标签、合并重复页面、修正错误、检查孤立页面时，读取：

```text
agents/lint_agent.md
```

主要更新：

```text
memory/error_log.md
memory/tag_taxonomy.md
memory/term_aliases.md
index.md
log.md
```

---

## 5. 不可违背规则

1. `raw/` 是原始资料层。除非用户明确要求，不修改、不删除、不重命名原始文件。
    
2. `wiki/` 是结构化知识层。可以创建和更新页面，但必须保留来源、证据和不确定性。
    
3. 所有重要判断必须尽量回链到具体论文、页码、章节、图表或 claim。
    
4. 不确定的信息必须标注为：`待核查`、`不确定` 或 `AI 推断`。
    
5. 不允许把 AI 推断写成论文作者的原始结论。
    
6. tags 必须遵循 `memory/tag_taxonomy.md`。
    
7. 同义词和术语别名必须遵循 `memory/term_aliases.md`。
    
8. 不要重复创建同义 topic、method、gap 页面。
    
9. 每次重要操作后必须更新 `index.md` 和 `log.md`。
    
10. 一旦发现错误，或用户指出错误，必须更新 `memory/error_log.md`。
    

---

## 6. 页面链接规则

优先使用 Obsidian 双链：

```markdown
[[wiki/papers/论文页面]]
[[wiki/topics/主题页面]]
[[wiki/methods/方法页面]]
[[wiki/claims/判断页面]]
[[wiki/gaps/研究空白页面]]
```

只有存在明确关系时才建立链接。

不要为了让图谱变复杂而乱加链接。  
有价值的 graph view 来自真实关系，不是链接数量。

---

## 7. index.md 规则

`index.md` 是知识库总目录。  
每次创建、删除、重命名或合并重要页面后，都要更新它。

推荐结构：

```markdown
# Index

## Papers

## Topics

## Methods

## Claims

## Gaps

## Reviews

## Synthesis
```

每个条目格式：

```markdown
- [[页面路径]]：一句话说明。
```

---

## 8. log.md 规则

`log.md` 是操作流水账。  
每次完成重要任务后追加记录。

格式：

```markdown
## [YYYY-MM-DD] 类型 | 标题

- 输入：
- 操作：
- 新建：
- 更新：
- 发现：
- 后续：
```

常用类型：

```text
init
ingest
query
synthesis
gap
review
lint
update
error-fix
decision
```

---

## 9. error_log.md 规则

当出现以下问题时，更新 `memory/error_log.md`：

- 标签不统一。
    
- 术语混用。
    
- 论文结论误读。
    
- 缺少证据却写成确定结论。
    
- 创建重复页面。
    
- 忘记更新 `index.md` 或 `log.md`。
    
- 用户指出事实、结构或风格错误。
    

记录格式：

```markdown
## YYYY-MM-DD | 错误类型

### 错误表现

### 原因

### 修正规则

### 影响范围

### 以后避免方式
```

---

## 10. 新用户使用流程

新用户第一次使用本项目时，按以下顺序操作：

1. 在 `memory/project_profile.md` 中填写自己的研究领域、研究目标和用途。
    
2. 在 `memory/tag_taxonomy.md` 中定义初始标签体系。
    
3. 在 `memory/term_aliases.md` 中定义常见术语别名。
    
4. 将 PDF 论文放入 `raw/papers/`。
    
5. 让 Codex 读取一篇论文并生成论文卡片。
    
6. 检查输出格式是否满意。
    
7. 调整模板和规则。
    
8. 再逐步批量导入更多论文。
    
9. 定期运行 `lint_agent.md` 检查知识库。
    

---

## 11. 最终提醒

Codex 在本项目中不是普通摘要工具，而是论文知识库维护者。

每次执行任务时都要思考：

1. 这篇论文应该进入哪个页面？
    
2. 它涉及哪些 topic、method、claim 和 gap？
    
3. 它是否支持或反驳已有判断？
    
4. 它是否能帮助写文献综述？
    
5. 它是否暴露新的 research gap？
    
6. 哪些页面需要同步更新？
    
7. 这次操作是否已经写入 `log.md`？
    

知识库应该在每次任务后变得更清晰、更准确、更可复用。
