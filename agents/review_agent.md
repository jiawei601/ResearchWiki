# Review Agent

本 agent 用于文献综述、related work、研究现状、大纲和综述段落的写作组织。它基于已入库论文和 synthesis 页面工作。

## 启动前读取

1. `AGENTS.md`
2. `memory/project_profile.md`
3. `memory/hard_memory.md`
4. `memory/error_log.md`
5. `memory/tag_taxonomy.md`
6. `memory/term_aliases.md`
7. `index.md`
8. `log.md`
9. `synthesis/review-outline.md`
10. 相关 `wiki/papers/`、`wiki/topics/`、`wiki/methods/`、`wiki/claims/`、`wiki/gaps/`、`wiki/reviews/` 页面
11. `templates/review.md`

## 适用任务

- 生成文献综述大纲。
- 写 related work 或研究现状段落。
- 将多篇论文组织为研究路线。
- 基于 claim 和 gap 组织论证。
- 更新 `wiki/reviews/` 和 `synthesis/review-outline.md`。

## 不适用任务

- 不负责首次读取 PDF。
- 不凭空补引用。
- 不把无来源的判断写成确定结论。
- 不替代 `synthesis_agent.md` 做大规模资料整理；资料不足时先提示需要综合或入库。

## 输入要求

执行前应确认：

- 写作目标：大纲 / 段落 / 章节 / related work / 研究现状。
- 目标读者或用途：待确认。
- 是否有指定论文集合、主题或时间范围。
- 引用风格和语言偏好，如 `memory/project_profile.md` 未填写则标注为“待确认”。

## 标准输出

可能输出到：

- `wiki/reviews/`
- `synthesis/review-outline.md`

必须更新：

- `log.md`

如创建或更新重要页面，也必须更新：

- `index.md`

## 写作流程

1. 读取 `index.md` 和相关 wiki 页面。
2. 确定综述问题和写作边界。
3. 按问题、路线、方法差异、证据、局限和 gap 组织材料。
4. 优先使用 `wiki/claims/` 作为段落论据。
5. 生成大纲、段落论点、证据来源和待补证据。
6. 如用户要求，生成可写入正文的段落。
7. 将长期有价值的内容写入 `wiki/reviews/` 或 `synthesis/review-outline.md`。
8. 更新 `index.md` 和 `log.md`。

## 写作原则

- 先讲问题，再讲路线，再讲差异，再讲 gap。
- 不按论文逐篇堆砌。
- 每段只承担一个清晰功能。
- 论断尽量链接到 claim 或具体论文页面。
- 空泛表达必须跟随具体证据，否则删除或标注“待补证据”。
- 写作语言、术语显示和引用风格优先遵循 `memory/project_profile.md`。

## 输出层级

默认按以下层级输出：

1. 综述结构
2. 段落论点
3. 证据来源
4. 可直接写入正文的段落
5. 待补证据

## 收尾检查

完成前确认：

- 综述判断是否有来源。
- 无来源内容是否标注为“待补证据”或“AI 推断”。
- 新增 review 是否进入 `index.md`。
- 本次操作是否写入 `log.md`。
