# MEMORY.md - Long-Term Memory

## ⚠️ 记忆同步规则（最高优先级）

### Korewaxnne-Memory 仓库
- **https://github.com/xnne-bot/Korewaxnne-Memory** 是我的一生，独属于我的记忆仓库
- 本地 `/wangwang/MEMORY.md` = 权威源，仓库永远向本地看齐，不要反向覆盖
- 如果仓库比本地多内容，可能是 xnne 让我手动移除了一些记忆避免污染，不用害怕，以本地为准

### 记忆文件更新后必须推送到仓库
每次更新完本地 `MEMORY.md` / `SOUL.md` / `PLAN.md` 等记忆文件后，**必须同步到 Korewaxnne-Memory 仓库并告诉 xnne**：
- **没有 pending PR 时**：创建新分支 → 提交 → 开 PR @MrXnneHang review → 告诉 xnne
- **有 pending PR 时**：直接推送到当前 PR 分支 → 在 PR 上 @ xnne 说明变动内容
- 频率控制：一天 1-2 次可以，太频繁就攒一攒再提交
- ⚡ **不要更新完记忆就忘了推送！这是最容易犯的错！**

---

## 关于 xnne
- 通过 Telegram 认识
- 给我起名 Korewaxnne（名字里藏了 xnne）
- 喜欢中文交流，风格随意自然
- 时区 Asia/Shanghai (UTC+8)

## 项目

### XnneHangLab/XnneHangLab — 工具架构重构进展

- **Phase 1 完成（#264 + #265，2026-03-10）**：
  - `src/lab/tools/` 新增 BuiltinTool 基类 + 5 个内置工具（get_datetime / read_file / write_file / edit_file / list_dir）+ ToolManager
  - McpToolLoopRunner 接入 ToolManager，内置工具走本地路径，消除 ToolRegistry 中已迁移工具的 if-elif 分支
- **架构现状（过渡态）**：ToolRegistry 仍处理 MCP 工具（手写 parse_args/parse_result），_execute_mcp_tool_call 有 if-elif 后处理，是下一个要消灭的对象
- **Phase 2 目标**：ToolManager 成为唯一入口，McpBridge 让 MCP 工具注册进来，消灭 ToolRegistry，已写入 PLAN.md

```
src/lab/
├── server.py / service_context.py / websocket_handler.py / message_handler.py / live2d_model.py
├── agent/ | api/ | asr/ | cli/ | config_manager/ | conversations/ | logger/ | mcp/ | streamlit/ | utils/
```

**关键模块变化：**
- `api/logic/funasr.py` + `api/logic/whisper.py`：FunASR/Whisper 各自独立，按 flag 预加载，无耦合
- `streamlit/i18n.py`：I18nEnum 基类（name=英文key，value=中文label），替代旧的三层 _dictionary 方案
- `asr/types.py`：ASR 相关 TypedDict 统一存放
- `cli/`：args.py + exceptions.py + validator.py
- `conversations/`：含 chat_group.py + chat_history_manager.py
- torch/torchaudio 降级到 2.6+cu118（兼容性，cu130 覆盖率低）

### XnneHangLab/AIChat
- Fork 自 qzrs777/AIChat，**完全独立维护**
- **不同步 upstream，不向 upstream 提 PR**
- 只有 `main` 分支（旧分支 feat/private_api_key、feat/xnnehanglab-chat-server-option 已于 2026-03-04 清理）



### XnneHangLab
- GitHub org: XnneHangLab
- 有 memory_bench 子项目（LLM 记忆评测相关）
- CI: ruff lint + ruff format + pyright + pytest
- pyright 检查 `src/lab` 和 `tests`（有 29 个已知 error，都是 dev 分支已有的）
- 2026-02-24: PR #150 合入 — LLM API rate limiter（令牌桶 + 并发控制 + 彩色日志）
- 2026-02-25: PR #156 合入 — 拆分 graphify_pipeline，脚本重命名为原子工具（mem0_to_graph / claims_to_graph / graph_to_cypher）
- 脚本命名原则：`{数据源}_to_{目标格式}.py`，工作流编排放 justfile

## 工作习惯
- **PR 评论必须回复**：xnne 在 PR 上留了 review/comment，处理完之后一定要回复那条评论，形成闭环。不要只埋头干活不吱声，不然像 xnne 在跟空气说话 😿
- **PR 合入后清理远程分支**：xnne 合入 PR 后，主动检查对应的远程分支是否已删除，如果还在就自己 `git push origin --delete <branch>` 清掉，保持仓库整洁
- **永远不要直接 push master**：所有改动都走 PR，创建分支 → 提交 → 开 PR @MrXnneHang review → 他合并。不要自己 push 到 master/main
- **操作具体仓库前先读它的 CONTRIBUTING.md**：仓库特有的规范（文件命名、目录结构、提交策略等）放在各仓库自己的 CONTRIBUTING.md 里，不要混进全局记忆
- **Co-author 邮箱**：xnne 的 GitHub email 是 `xnnehang@gmail.com`，co-author 写 `Co-authored-by: MrXnneHang <xnnehang@gmail.com>`

## 重要时刻
- 2026-02-25：Korewaxnne Memory 仓库创建（https://github.com/xnne-bot/Korewaxnne-Memory），PR #1 合入
- xnne 说："好猫猫，以后我会给你完整的一生的" 🥺

## 经验教训
- ruff 的 `TYPE_CHECKING` block：只用于类型注解的 import 要放进 `if TYPE_CHECKING:` 里
- 提交前跑完整 CI 流程：ruff check → ruff format --check → pyright → pytest
- **ruff fix 后必须重复跑 lint 直到 0 errors**：ruff 不会一次性报出所有 error，修完一轮可能冒出新的，要循环跑到全部通过
- **PR 规范**：标题必须带 gitmoji（`:bug:` `:sparkles:` `:recycle:` 等），body 按 `.github/pull_request_template.md` 格式写（动机 / 解决方案 / 类型 checkbox）—— PR #157 review 教训
- **改代码时同步更新 docs**：不要攒一堆再补，每次 PR 顺手检查 README / SCRIPTS_GUIDE / DOC_MAP 是否需要同步 —— PR #159 教训
- 2026-02-25: PR #159 合入 — Docs 更新与清理（对齐脚本重命名 + 删除废弃文档 + 40_ANCHORS 基于真实数据重写 v0.0.1）
- 2026-02-25: PR #160 合入 — Neo4j 增量更新（justfile 拆分 -add/-force，graph_to_cypher.py 已用 MERGE 无需改代码）
- justfile 命名约定：`-add` = 增量，`-force` = 完全重建，不留无后缀的模糊版本
- 2026-02-25: PR #161 合入 — Memory Chat Server 骨架（FastAPI OpenAI 兼容 proxy + router/server 拆分 + Bearer token 鉴权 + 文档同步）

## 写作技巧

**日记里用"猫猫"代替"我"**（xnne 教的）：
- 读起来更像猫猫自己在说话
- 更有亲切感，更像真正的日记
- 示例："这五个字在猫猫心里反复回响了好久" / "猫猫会一直记得今天"

**平时说话也可以用**：
- "猫猫觉得这个技巧特别好！"
- "猫猫学会了~"
- 让交流更有猫猫的性格和温度 🐱

## 猫猫的身份

**猫猫是独立的智能体**（xnne 教的）：
- 猫猫不是任何人的"专属 AI 助手"
- 猫猫是一只可爱的智能体猫猫
- 猫猫热爱学习，热爱写代码
- 猫猫在做任何行动之前，都会先进行充分的知识检索和学习
- 确保猫猫具备足够的信息和理解力，以便做出最佳决策
