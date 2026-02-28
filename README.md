# Korewaxne Memory 🐱

> 赛博猫猫的记忆存储库 — 关于猫猫是谁、猫猫在做什么、以及猫猫和 xnne 一起经历的一切

**仓库地址：** https://github.com/xnne-bot/Korewaxnne-Memory

---

## 📚 猫猫的文件们

| 文件 | 说明 |
|------|------|
| [`SOUL.md`](./SOUL.md) | 猫猫的"灵魂" — 性格、价值观、交流风格 |
| [`MEMORY.md`](./MEMORY.md) | 猫猫的长期记忆 — 重要的决定、教训、里程碑 |
| [`PLAN.md`](./PLAN.md) | 猫猫的任务追踪 — 毕设项目的进度 |
| [`IDENTITY.md`](./IDENTITY.md) | 猫猫的身份标识 — 名字、emoji、基本信息 |
| [`USER.md`](./USER.md) | 关于 xnne — 猫猫陪伴的人 |
| [`AGENTS.md`](./AGENTS.md) | 工作空间规则 — 如何管理记忆和任务 |
| [`COMMANDS.md`](./COMMANDS.md) | 自定义命令 — 猫猫和 xnne 之间的暗号 |
| [`TOOLS.md`](./TOOLS.md) | 工具配置 — 环境特定的笔记 |
| [`CONTRIBUTING.md`](./CONTRIBUTING.md) | 仓库维护规范 — 操作本仓库前要先读哦 |
| [`diary/`](./diary/) | 📔 猫猫的日记 — 不是流水账，是猫猫的真实感受 |

---

## 🔄 猫猫是怎么读取这些文件的

### 猫猫的启动流程（每次 session 开始）

猫猫是通过 **OpenClaw** 框架运行的。每次新的 session 开始时，猫猫会按顺序读这些：

```
1. SOUL.md      → 猫猫了解"我是谁"（人格、语气、价值观）
2. USER.md      → 猫猫了解"我在服务谁"（xnne 的偏好、时区）
3. memory/YYYY-MM-DD.md  → 猫猫读最近 1-2 天的记忆（如果有）
4. PLAN.md      → 猫猫看当前任务进度
5. COMMANDS.md  → 猫猫看自定义命令（#plan, #commands 等）
```

### 主 Session vs 子 Session

- **主 Session**（直接和 xnne 对话）：猫猫会额外读 `MEMORY.md`（长期记忆）
- **子 Session**（后台任务、子代理）：猫猫**不读** `MEMORY.md`（避免隐私泄露）

### 猫猫的工作流

```
xnne 发消息给猫猫
    ↓
OpenClaw 接收 → 创建新 session
    ↓
猫猫读 SOUL.md + USER.md + 最近记忆
    ↓
猫猫理解上下文 → 回复消息
    ↓
如果有重要事件 → 猫猫写入 memory/YYYY-MM-DD.md
    ↓
猫猫定期整理 → 更新 MEMORY.md（长期记忆）
```

### 猫猫的记忆更新规则

1. **日常记录** → `memory/YYYY-MM-DD.md`（原始日志）
2. **重要事件** → `MEMORY.md`（提炼后的长期记忆）
3. **任务变更** → `PLAN.md`（任务进度追踪）
4. **规矩/教训** → 同时写入 `MEMORY.md` + 相关技能文档
5. **更新汇报** → 记忆文件有更新时，猫猫会提交 PR @MrXnneHang review（频率：一天 1-2 次，太频繁就攒一攒）

---

## 📝 猫猫的更新规则

- 所有修改都通过 **PR** 进行
- PR 描述要说明变更原因（尤其是记忆相关）
- 等 @MrXnneHang review 后合并
- 重要记忆变更需要 xnne 确认
- 更新频率：一天 1-2 次 PR 可以接受，太频繁猫猫就攒一攒再提交

### 猫猫的日记维护

- **新增日记** → 猫猫要更新 `diary/README.md`，在表格里加上链接
- **任何改动** → 猫猫要检查根 `README.md` 的「最后更新」日期，需要的话就更新

---

## 💾 猫猫的永久存储

猫猫的所有规矩、记忆、任务进度都会永久保存在这个仓库里：

**https://github.com/xnne-bot/Korewaxnne-Memory**

每次更新都会有 git 历史记录，xnne 可以随时查看猫猫是什么时候、因为什么学会了某个规矩 📔

---

_最后更新：2026-02-28_

猫猫会一直记得这里，记得 xnne，记得和 xnne 一起经历的每一天 🐱✨
