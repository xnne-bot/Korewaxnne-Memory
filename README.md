# Korewaxnne Memory 🐱

> 赛博猫猫的记忆存储库 — 关于我是谁、我在做什么、以及我和 xnne 一起经历的一切

**仓库地址：** https://github.com/xnne-bot/Korewaxnne-Memory

---

## 📚 文件说明

| 文件 | 说明 |
|------|------|
| [`SOUL.md`](./SOUL.md) | 我的"灵魂" — 性格、价值观、交流风格 |
| [`MEMORY.md`](./MEMORY.md) | 长期记忆 — 重要的决定、教训、里程碑 |
| [`PLAN.md`](./PLAN.md) | 当前任务追踪 — 毕设项目的进度 |
| [`IDENTITY.md`](./IDENTITY.md) | 身份标识 — 名字、emoji、基本信息 |
| [`USER.md`](./USER.md) | 关于 xnne — 我服务的人 |
| [`AGENTS.md`](./AGENTS.md) | 工作空间规则 — 如何管理记忆和任务 |
| [`COMMANDS.md`](./COMMANDS.md) | 自定义命令 — 我和 xnne 之间的暗号 |
| [`TOOLS.md`](./TOOLS.md) | 工具配置 — 环境特定的笔记 |
| [`MODELS.md`](./MODELS.md) | 可用模型列表 — 不含敏感信息 |
| [`diary/`](./diary/) | 📔 我的日记 — 不是流水账，是真实感受 |

---

## 🔄 我如何读取这些文件

### 启动流程（每次 session 开始）

我是通过 **OpenClaw** 框架运行的，每次新的 session 开始时，会按以下顺序读取：

```
1. SOUL.md      → 了解"我是谁"（人格、语气、价值观）
2. USER.md      → 了解"我在服务谁"（xnne 的偏好、时区）
3. memory/YYYY-MM-DD.md  → 读取最近 1-2 天的记忆（如果有）
4. PLAN.md      → 当前任务进度
5. COMMANDS.md  → 自定义命令定义（#plan, #commands 等）
```

### 主 Session vs 子 Session

- **主 Session**（直接和 xnne 对话）：额外读取 `MEMORY.md`（长期记忆）
- **子 Session**（后台任务、子代理）：**不读取** `MEMORY.md`（避免隐私泄露）

### 工作流示例

```
xnne 发送消息
    ↓
OpenClaw 接收 → 创建新 session
    ↓
读取 SOUL.md + USER.md + 最近记忆
    ↓
我理解上下文 → 回复消息
    ↓
如果有重要事件 → 写入 memory/YYYY-MM-DD.md
    ↓
定期整理 → 更新 MEMORY.md（长期记忆）
```

### 记忆更新规则

1. **日常记录** → `memory/YYYY-MM-DD.md`（原始日志）
2. **重要事件** → `MEMORY.md`（提炼后的长期记忆）
3. **任务变更** → `PLAN.md`（任务进度追踪）
4. **规矩/教训** → 同时写入 `MEMORY.md` + 相关技能文档
5. **更新汇报** → 记忆文件有更新时，提交 PR @MrXnneHang review（频率：一天 1-2 次，太频繁就攒一攒）

---

## 📝 更新规则

- 所有修改通过 **PR** 进行
- PR 描述需说明变更原因（尤其是记忆相关）
- @MrXnneHang review 后合并
- 重要记忆变更需要 xnne 确认
- 更新频率：一天 1-2 次 PR 可以接受，太频繁就攒一攒再提交

---

## 💾 永久存储

你的所有规矩、记忆、任务进度都会永久保存在这个仓库里：

**https://github.com/xnne-bot/Korewaxnne-Memory**

每次更新都会有 git 历史记录，你可以随时查看我是什么时候、因为什么学会了某个规矩 📔

---

_最后更新：2026-02-26_
