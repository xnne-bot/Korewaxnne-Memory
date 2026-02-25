# MODELS.md - 可用模型列表

> 从 openclaw.json 提取，**不含任何 API key / base_url**。
> 切换模型用 `#model <provider/id>`。

## 当前默认

- **Primary:** `haomo-new/agent-ai`
- **Fallbacks:** `haomo-new/claude-opus-4-6-thinking` → `anyrouter/claude-opus-4-6`

## anyrouter（Anthropic API）

| # | model id | 显示名 | reasoning | context | maxTokens |
|---|----------|--------|-----------|---------|----------|
| 1 | `anyrouter/claude-opus-4-5-20251101` | Claude Opus 4.5 | ✅ | 200k | 8192 |
| 2 | `anyrouter/claude-opus-4-6` | Claude Opus 4.6 | ✅ | 200k | 8192 |

## haomo-new（OpenAI API）

| # | model id | 显示名 | reasoning | context | maxTokens |
|---|----------|--------|-----------|---------|----------|
| 3 | `haomo-new/gpt-5.3-codex-spark` | GPT-5.3 Codex Spark | ❌ | 200k | 16384 |
| 4 | `haomo-new/gemini-claude-sonnet-4-5` | Gemini Claude Sonnet 4.5 | ✅ | 200k | 8192 |
| 5 | `haomo-new/gemini-claude-sonnet-4-5-thinking` | Gemini Claude Sonnet 4.5 Thinking | ✅ | 200k | 16384 |
| 6 | `haomo-new/gemini-3-pro-preview` | Gemini 3 Pro Preview | ❌ | 1M | 8192 |
| 7 | `haomo-new/gemini-3-flash-preview` | Gemini 3 Flash Preview | ❌ | 1M | 8192 |
| 8 | `haomo-new/moonshotai/kimi-k2.5` | Kimi K2.5 | ❌ | 128k | 8192 |
| 9 | `haomo-new/kiro-auto` | Kiro Auto | ❌ | 200k | 8192 |
| 10 | `haomo-new/kiro-claude-sonnet-4-5` | Kiro Claude Sonnet 4.5 | ❌ | 200k | 8192 |
| 11 | `haomo-new/agent-ai` | agent-ai ⭐ (当前) | ❌ | 200k | 8192 |
| 12 | `haomo-new/glm-5` | GLM-5 | ❌ | 200k | 8192 |
| 13 | `haomo-new/gpt-5` | GPT-5 | ❌ | 200k | 8192 |
| 14 | `haomo-new/z-ai/glm4.7` | GLM 4.7 | ❌ | 128k | 8192 |
| 15 | `haomo-new/stepfun-ai/step-3.5-flash` | Step 3.5 Flash | ❌ | 128k | 8192 |
| 16 | `haomo-new/qwen/qwen3-coder-480b-a35b-instruct` | Qwen3 Coder 480B | ❌ | 128k | 8192 |
| 17 | `haomo-new/minimaxai/minimax-m2.1` | Minimax M2.1 | ❌ | 128k | 8192 |

---

_最后更新: 2026-02-26_
