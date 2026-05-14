# test-case-skill

> 资深 QA 测试用例生成工作流 — Cursor Agent Skill

把一段产品需求转化成可直接交付的标准测试用例（markdown 表格，可粘贴 Excel / 飞书多维表格 / Numbers）。5 步交互式工作流，每步暂停等你确认或调整。

## Supported Agents

本 Skill 为开放格式（带 YAML frontmatter 的 markdown），多个 AI Agent 工具均可使用：

| 工具 | 安装位置 | 是否原生支持 |
|---|---|---|
| Cursor | `~/.cursor/skills/test-case-generator/` | ✅ |
| Claude Code | `~/.claude/skills/test-case-generator/` | ✅ |
| Codex CLI | `~/.codex/skills/test-case-generator/` | ✅ |

`npx skills add` 命令会自动检测你机器上的 AI 工具并装到对应位置。

## 安装

**方式一：用 `npx skills` 一键安装（推荐）**

```bash
npx skills add test111ddff-hash/test-case-skill
```

**方式二：手动安装（GitHub）**

```bash
mkdir -p ~/.cursor/skills/test-case-generator
curl -o ~/.cursor/skills/test-case-generator/SKILL.md \
  https://raw.githubusercontent.com/test111ddff-hash/test-case-skill/main/skills/test-case-generator/SKILL.md
```

**方式三：手动安装（Gitee 国内镜像）**

```bash
mkdir -p ~/.cursor/skills/test-case-generator
curl -o ~/.cursor/skills/test-case-generator/SKILL.md \
  https://gitee.com/chang-xinping/test-case-skill/raw/main/skills/test-case-generator/SKILL.md
```

安装后重启 Cursor 即可。

## 用法

在 Cursor 新对话粘贴产品需求 + 一句"帮我写测试用例"，Skill 自动按 5 步串行：

| 步骤 | 做什么 | 暂停等什么 |
|---|---|---|
| 步骤 1a | 拆解功能、识别测试对象、列歧义清单（4 列含 A/B/C 可能方向） | 你逐条回答歧义清单 |
| 步骤 1b | 基于你的歧义答案重写明确规格 | 你确认进步骤 2 |
| 步骤 2 | 9 维度爆破提取测试点（业务规则 / 数据类型 / 长度 / 格式 / 状态 / 交互 / 时序 / 环境 / 角色） | 你确认进步骤 3 |
| 步骤 3 | 输出 8 列 markdown 表格（用例编号 / 所属模块 / 优先级 / 标题 / 前置 / 数据 / 步骤 / 预期） | 你确认进步骤 4 |
| 步骤 4 | 对抗性挑刺（遗漏 / 冗余 / 不可执行 / 优先级偏差 / 致命盲点） | 你决定采纳哪些 |
| 步骤 5 | 交付清单（覆盖矩阵 / 缺口 / 主动放弃 / 一句话总结） | 流程结束 |

## 适用范围

| ✅ 适用 | ❌ 不适用 |
|---|---|
| UI 功能测试用例 | 性能压测（用 JMeter / Locust） |
| 业务流程端到端 | 接口自动化（用 Postman / HttpRunner） |
| 边界异常 / 跨端兼容 | 安全渗透（用 Burp Suite） |
| 内容安全（敏感词 / 敏感图 / 富文本注入） | 单元测试（用 Jest / Pytest） |

## 触发关键词

Skill 自动加载，触发条件：

- 消息含「测试用例 / 测试点 / 需求拆解 / QA / 用例评审 / 测试覆盖」
- 或粘贴产品需求并请求生成测试

## 设计哲学

- **QA 不替产品决策**：歧义清单的「可能方向」仅供参考，必须用户主动选择，禁止一键采纳默认
- **每步暂停**：5 步必须串行，不一次性跑完，每步可调整
- **可直接交付**：用例以 markdown 表格输出，可一键粘贴到 Excel / 飞书多维表格 / Numbers
- **明确边界**：性能 / 接口 / 渗透 / 单测均不在范围，明确告知用户用对应工具

## License

MIT — see [LICENSE](LICENSE)
