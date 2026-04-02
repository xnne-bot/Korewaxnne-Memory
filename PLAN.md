# PLAN.md - 任务追踪

<!-- 格式说明：
  - [ ] **任务标题** — 背景→动机→方案 `@关联: #其他任务`
    - [ ] 子任务（可选）
  - [x] ~~已完成任务~~ ✅ 完成于 YYYY-MM-DD `@关联: #其他任务`
  
  规则：
  - 已完成 ≥3 天 且无关联未完成任务 → 自动清理
  - 只有 xnne 说"写入 plan"时才写入新任务
-->

## 毕设：聪音记忆对话系统

### 🔴 高优先级

- [ ] **ToolManager Phase 2：Plugin 注册机制 + 统一路由** — Phase 1 (#264/#265) 已把内置工具解耦，但 MCP 路径仍走 ToolRegistry（手写 if-elif 类型注册表），每加工具要改三处，长期膨胀。Phase 2 目标：ToolManager 成为唯一入口，消灭 ToolRegistry，McpToolLoopRunner 只管循环逻辑不管路由。`@关联: #262（架构设计）#261（Phase 1 已完成）`
  - [ ] **PluginTool 基类 + McpBridge**：MCP 工具通过 McpBridge 注册进 ToolManager，不再需要 parse_args/parse_result 手写分支
  - [ ] **消灭 _execute_mcp_tool_call 的 if-elif 后处理**：web_search/web_fetch/screenshot 的后处理逻辑迁移到各自 PluginTool.post_execute() 或 hook 机制
  - [ ] **移除 ToolRegistry**：待上述完成后整体删除 tool_registry.py
  - [ ] **McpToolLoopRunner 简化**：只保留 run_tool_loop 循环逻辑，所有工具调用委托给 ToolManager

- [x] ~~**Docs 更新与清理**~~ ✅ 完成于 2026-02-25 — PR #159 合入
- [x] ~~**Neo4j 增量更新**~~ ✅ 完成于 2026-02-25 — PR #160 合入（graph_to_cypher.py 已用 MERGE，纯 justfile 拆分 -add/-force）
- [x] ~~**Memory Chat Server 骨架**~~ ✅ 完成于 2026-02-25 — PR #161 合入（FastAPI proxy + router/server 拆分 + Bearer token 鉴权 + 文档同步）
- [ ] **memory_bench 职责分离重构** — 现有 `/v1/chat/completions` stream 不透传、tool message 过滤有问题，无法作为 src/lab agent 的透明后端；同时 AIChat 需要 server 端自治管理上下文/工具调用。拆分为透明代理 + 自治 agent 两个端点。`@关联: #224（GitHub Issue）`
  - [ ] **PR 1：/memory/chat 端点骨架 + 上下文存储** — 最小可用版本：端点能响应、system prompt 拼接、日期 JSON 文件读写
    - [ ] `chat_router.py` 骨架（`/memory/chat` 路由）
    - [ ] `conversation_store.py`（读写 `conversations/YYYY-MM-DD.json`）
    - [ ] System Prompt 拼接逻辑（读取 `prompts/` 下文件）
    - [ ] 基本消息收发（直接调 LLM，返回原始响应）
  - [ ] **PR 2：Session 管理 + Tool-loop**
    - [ ] `session_store.py`（内存 session map + TTL）
    - [ ] 内置工具注册（READ/WRITE/EDIT/SEARCH）
    - [ ] Tool-loop 逻辑（LLM → tool_call → 执行 → 塞回 → 再调 LLM）
  - [ ] **PR 3：EMOTION 结构化响应 + 上下文裁剪**
    - [ ] 解析 `[Emotion] ||| TEXT` 格式
    - [ ] 返回 `{ emotion, voice_text, subtitle_text }`
    - [ ] 上下文裁剪（超 token limit 时滚动窗口）
  - [ ] **Phase 4：透明代理修复（proxy_router.py）** — 从 router.py 拆出代理逻辑，修 stream 透传、tool message 透传、写回策略（只写 user+assistant）
  - [ ] **Phase 5：文档同步** — SCRIPTS_GUIDE.md + .env.benchmark.example
- [x] ~~**AIChat Mod 配置修复**~~ ✅ 完成于 2026-03-03 — fork qzrs777/AIChat，修正 base_url 配置（localhost 而非 0.0.0.0）、端点路径（/v1/chat/completions）、加中断/取消按钮便于调试
- [x] ~~**GPT-SoVITS-Inference Logger 系统**~~ ✅ 完成于 2026-03-03 — 为 GSV 仓库建立按 group 的 logger（类似 XnneHangLab src/lab/logger），支持导入和扩展到 XnneHangLab
- [x] ~~**Chat CLI 终端调试客户端**~~ ✅ 完成于 2026-02-26 — PR #162 合入（httpx proxy=None 避坑系统代理 / max_completion_tokens 适配新模型 / 详细 PR comment）
- [x] ~~**Chat Server 日志规范化**~~ ✅ 完成于 2026-02-26 — PR #163 合入（print → bench_logger + top2 日志 + write-back 详情）
- [x] ~~**实时记忆写入 + 图谱异步更新**~~ ✅ 完成于 2026-03-03 — 不走离线管线，Server 内直接做轻量 claim 提取 + Neo4j MERGE 写入。离线管线（claimify_all/compiled_claims 等）保持不动，继续服务 benchmark replay
- [x] ~~**接入 AIChat 联调**~~ ✅ 完成于 2026-03-03 — 确保 TTS + 记忆 + 对话 end-to-end 跑通
- [x] ~~**AIChat 断句显示 + 异步 TTS**~~ ✅ 完成于 2026-03-03 — 根据中文标点（`。` `？` `！`）断句，实现流式 TTS 生成 + 逐句显示字幕
- [x] ~~**XnneHangLab Chat Server JSON 响应格式 + DeepLX 翻译集成**~~ ✅ 完成于 2026-03-03 — 为 AIChat Mod 返回结构化 JSON 响应，支持自动翻译
- [x] ~~**清理命令 + 管线文档**~~ ✅ 完成于 2026-03-03 — justfile 清理 recipes（按 LLM 调用点切入）+ SCRIPTS_GUIDE.md 补充离线/实时管线差异与增量边界说明
- [x] ~~**重构 router.py 分离 Cypher 语句**~~ ✅ 完成于 2026-03-03 — 创建 `neo4j_queries.py` 模块，将所有 Cypher 语句从 router.py 移出，使 router.py 只保留业务逻辑，Cypher 语句集中在独立文件 @关联：#实时记忆写入 + 图谱异步更新

### 🟡 中优先级

- [ ] **调整记忆注入方式** — 当前 `_inject_memories()` 把检索到的记忆拼到第一条 system message 后面（`## Recalled Memories` 模板），可能需要改成：插入到 user message 前 / 作为独立 system prompt / 动态调整位置 `@关联: #Memory Chat Server 骨架`
- [ ] **replay_zep.py** — 为 Zep 写 replay 脚本，接口统一为 ingest/export 子命令，导出格式统一 JSONL schema，复用下游 claimify → graphify → cypher 管线 `@关联: #replay_cognee` `@关联: #replay_memsearch`
- [ ] **补全实时管线节点属性** — 对比离线管线（06_SCHEMA_REFERENCE.md），补全实时管线中缺失的节点属性
  - [x] **MemoryItem** — ✅ 属性已完整（PR #181 + #185）
  - [x] **User** — ✅ 属性已完整（PR #186）
  - [x] **Agent** — ✅ 属性已完整（PR #186）
  - [x] **Character** — ✅ 属性已完整（PR #186）
  - [x] **Conversation** — ✅ 属性已完整（PR #185）
  - [x] **Scene** — ✅ 属性已完整（PR #186）
  @关联：#181（已修复 Neo4j 标签语法）#183（User ACTOR 关系）#185（Conversation 重复创建修复）#186（User/Agent/Scene/Character 属性补全）
- [ ] **replay_cognee.py** — 同上；cognee 自带知识图谱，可能可以直接导出图导入 Neo4j，跳过 claimify+graphify `@关联: #replay_zep`
- [ ] **replay_memsearch.py** — 同上；memsearch 记忆是 markdown 格式，需要 adapter 转 JSONL `@关联: #replay_zep`
- [ ] **记忆评分系统 Phase 1** — 写 `eval_memory.py`：对每个 probe 拿 ground-truth 和 recall 结果，LLM 打分（relevance + completeness + accuracy，0-5），输出 JSONL 评分报告

### 🟢 低优先级（不急）

- [ ] **横向对比报告** — 4 个系统同组 probe，生成对比表/图（matplotlib 或 Neo4j dashboard）
- [ ] **毕设报告 + 文档整理** — 不急，不是两周后交论文
