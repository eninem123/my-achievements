# 🧙 Agent 化向导（Agent Bootstrap Wizard）

> 一键 Agent 化方法论 · 4 档配置 · 支持 GitLab / GitHub 双平台

---

## 📖 简介

Agent 化向导是一套**企业级代码仓库 Agent 化落地方法论**，通过选择题式的交互式引导，帮助团队快速完成代码仓库的 Agent 化改造。无论你是个人开发者还是大型团队，都能找到适合自己的档位。

### 核心价值
- ⚡ **快速上手**：无需阅读千行文档，回答几道选择题即可生成专属方案
- 🎯 **精准匹配**：4 档配置覆盖从个人项目到企业级合规的全部场景
- 🔒 **安全可控**：先备份、后操作，支持「只看方案不写入」模式
- 🏢 **团队友好**：支持 GitLab / GitHub 双平台，内置 CI 校验与组织模板

---

## 🎮 快速开始

### 1. 动手前（必做）
```bash
git stash                    # 或 commit 干净工作区
git pull
git checkout -b chore/agent-bootstrap
# 老库建议打备份标签：
git tag backup/pre-agent-$(date +%Y%m%d)
```

### 2. 启动向导
在 Cursor Agent 中发送：
```
@docs/ai_guides/agent_bootstrap_wizard.md 按本文件「Agent 执行说明」启动选择题向导。
```

### 3. 回答选择题 → 查看方案 → 决定是否写入
- 仓库已有 `AGENTS.md`？最后一题选 **「只要方案」**，避免覆盖
- 没弹窗？用文字回复选项 id（详见「无弹窗降级」章节）

---

## 🎚️ 四档配置

| 档位 | 名称 | 生成内容 | 适用场景 |
|------|------|----------|---------|
| A | **简单档** | 仅根 `AGENTS.md`（50-120 行） | 小项目、个人、先跑起来 |
| B | **团队轻量档** | AGENTS + 1 条 rules | 团队统一、不需要 guard |
| | **分场景向导** | AGENTS + rules + lessons 模板 + on_demand + 角色红线 | CRM/OA/DBA/数据中台 |
| C | **复杂全套档** | 完整 §0～§7 索引 + guard 可选 | 老库、企业合规、平台要求 |

> 💡 大多数项目选简单档 A 或分场景档即可，不必追求最重配置

---

## 🏗️ 完整流程

```
┌─────────────────────────────────────────────────────┐
│ 0. 备份：干净工作区 + 独立分支 +（老库）Tag        │
├─────────────────────────────────────────────────────┤
│ 1. Cursor 打开仓库根目录 → Agent 模式              │
├─────────────────────────────────────────────────────┤
│ 2. @ 向导文件 + 启动句                              │
├─────────────────────────────────────────────────────┤
│ 3. 选择题 约 4 轮                                   │
│    Q1 备份 → Q2 档位 → Q3 个人/团队 → Q4 新老库    │
│    → Q5 角色 → Q6 仓库类型 → Q7 目标               │
│    （团队另问 Q8 GitLab/GitHub）                    │
├─────────────────────────────────────────────────────┤
│ 4. AI 输出 ≤10 行「部署方案摘要」                   │
├─────────────────────────────────────────────────────┤
│ 5. 你选：只看方案 / 开始写入                        │
├─────────────────────────────────────────────────────┤
│ 6. 个人：本地 commit                                │
│    团队：push → MR/PR（GitLab/GitHub）              │
└─────────────────────────────────────────────────────┘
```

---

## 🎯 题目一览

| 轮次 | 题号 | 内容 | 备注 |
|------|------|------|------|
| 1 | Q1 | 备份了吗 | 选「尚未备份」→ 只给命令，不改仓库 |
| 1 | Q2 | 简单 / 团队轻量 / 分场景 / 复杂全套 | 最重要的一题 |
| 2 | Q3 | 个人 / 团队 | 团队 → 追问 Q8 |
| 2 | Q4 | 新仓库 / 老代码库 | 老库分阶段、不大重构 |
| 3 | Q5 | 角色（CRM/OA/DBA/数据中台…） | 简单档可跳过 |
| 3 | Q6 | 数据 / API / 前端 / 全栈 / Monorepo | |
| 4 | Q7 | 只要方案 / 写入 /（复杂档）+guard | 已有 AGENTS 建议先要方案 |
| 4 | Q8 | GitLab / GitHub / 两边都有 | 仅团队模式 |

---

## 👥 团队多角色统一方案

各岗位在本仓 wizard 里选**不同角色**，平台用组织模板仓 `agent-bootstrap` 统一：

- 同一套 **AGENTS.base**（组织铁律）+ **角色 overlay**（CRM/OA/DBA…）
- 同一 **agent-lint** CI（GitLab `include` / GitHub Actions）
- 台账 **agent-registry.yaml** 追踪全组织 Agent 化进度

GitLab / GitHub **AGENTS 文件格式相同**，只差 MR 还是 PR 流程。

---

## 📋 选项 ID 速查表

| 题目 | 选项 ID |
|------|---------|
| **Q1** | `backup_done` / `backup_partial` / `backup_no` |
| **Q2** | `tier_simple` / `tier_team_light` / `tier_scenario` / `tier_full` |
| **Q3** | `mode_solo` / `mode_team` |
| **Q4** | `proj_new` / `proj_legacy` |
| **Q5** | `role_dw` / `role_crm` / `role_oa` / `role_dba` / `role_qa` / `role_sre` / `role_pm` / `role_backend` / `role_frontend` |
| **Q6** | `type_data` / `type_api` / `type_web` / `type_fullstack` / `type_mono` / `type_tool` |
| **Q7** | `plan_only` / `write_agents` / `stage_1` / `stage_12` |
| **Q8** | `platform_gitlab` / `platform_github` / `platform_both` |

### 无弹窗降级
Cursor 没出点选题时，在对话里**逐条回复 id**：

```text
Q1 backup_done Q2 tier_simple Q3 mode_solo Q4 proj_legacy Q6 type_api Q7 plan_only
```

团队示例：
```text
Q1 backup_done Q2 tier_scenario Q3 mode_team Q8 platform_gitlab Q4 proj_legacy Q5 role_crm Q6 type_api Q7 plan_only
```

---

## ✅ 推荐自测路径

**路径 A（最常见）**：`已备份` → `简单档 A` → `个人` → `老库` → `后端 API` → `只要方案`
> 期望：方案里只有根 `AGENTS.md`，无 lessons/guard

**路径 B（CRM 团队）**：`已备份` → `分场景` → `团队` → `GitLab` → `CRM` → `API` → `只要方案`
> 期望：方案含 CRM 红线、MR 要点

**路径 C（真写入，可选）**：路径 A 最后一题改「开始写入」，在**测试分支**验证
> 期望：简单档不应出现 `ai_learning/`

---

## ❓ FAQ

### Wizard 是什么？
**向导** = AI 用选择题问清你的情况，再生成 `AGENTS.md` 等；**不是**要安装的新软件。

### 别人第一次是不是只 @ 本文件？
**是。** 不必先读一千行 export；AI 需要时会自己 Read。

### 没备份可以吗？
不可以改仓库；第一题选尚未备份则只给备份步骤。

### 和 GitHub 社区比会不会太重？
主流往往只要一个 `AGENTS.md`；本向导 Q2 可选 **简单档 A** 对齐社区。分场景/复杂档给企业多角色、老库用。

---

*向导 v2 · 推广只发本文件 · 企业级 Agent 化落地方法论*
