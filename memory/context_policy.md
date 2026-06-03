---
type: memory
status: active
created: 2026-06-02
updated: 2026-06-02
tags:
  - context
---

# Context Policy

本页保存论文知识库的轻量上下文预算与历史压缩规则。它不替代 `AGENTS.md`，也不新增专门 agent。

## 目标

- 避免长期对话后丢失项目目标、已确认决策和下一步任务。
- 避免把过期对话当成当前规则。
- 在上下文变长时，把稳定信息沉淀到文件中，而不是依赖聊天历史。

## 需要优先读取的短上下文

当对话很长或任务跨阶段继续时，优先读取：

1. `AGENTS.md`
2. `memory/project_profile.md`
3. `memory/hard_memory.md`
4. `memory/context_policy.md`
5. `memory/style_snapshot.md`
6. `synthesis/core-argument-map.md`
7. `index.md`
8. `log.md` 的最近记录

## 压缩触发条件

出现以下情况时，应触发上下文压缩或更新短上下文文件：

- 对话已经跨越多个阶段，且后续任务仍依赖早期决策。
- `log.md` 最近新增多条初始化或结构变更记录。
- 用户反复要求“继续执行下一阶段”。
- agent、template、memory 或 synthesis 规则发生结构性变化。
- 发现当前回答依赖很早的聊天历史，而不是项目文件。
- 出现规则冲突、命名冲突或任务边界不清。

## 压缩后应保留的信息

压缩时只保留：

- 当前项目目标。
- 已确认结构决策。
- 当前有效规则文件。
- 废弃方案。
- 下一步任务。
- 用户稳定输出偏好。
- 未解决的待确认事项。

不要保留：

- 已完成的详细过程。
- 临时讨论但未采纳的想法。
- 重复的中间解释。
- 与论文知识库无关的内容。

## 写入位置

- 核心论点、决策和下一步：`synthesis/core-argument-map.md`
- 默认输出风格：`memory/style_snapshot.md`
- 结构性决策：`memory/decision_log.md`
- 具体操作流水：`log.md`
- 错误和修正规则：`memory/error_log.md`

## 使用规则

- 不确定的信息标注为“待确认”。
- 压缩后不要改写 `AGENTS.md`。
- 压缩不等于删除历史文件；只是在后续任务中优先读取短上下文文件。
