<p align="center">
  <img src="https://em-content.zobj.net/source/apple/391/rock_1faa8.png" width="120" />
</p>

<h1 align="center">caveman</h1>

<p align="center">
  <strong>why use many token when few do trick</strong>
</p>

<p align="center">
  <a href="https://github.com/JuliusBrussee/caveman/stargazers"><img src="https://img.shields.io/github/stars/JuliusBrussee/caveman?style=flat&color=yellow" alt="Stars"></a>
  <a href="https://github.com/JuliusBrussee/caveman/commits/main"><img src="https://img.shields.io/github/last-commit/JuliusBrussee/caveman?style=flat" alt="Last Commit"></a>
  <a href="LICENSE"><img src="https://img.shields.io/github/license/JuliusBrussee/caveman?style=flat" alt="License"></a>
</p>

<p align="center">
  <a href="#before--after">使用前后对比</a> •
  <a href="#install">安装</a> •
  <a href="#intensity-levels">强度级别</a> •
  <a href="#caveman-skills">技能</a> •
  <a href="#benchmarks">基准测试</a> •
  <a href="#evals">评估</a>
</p>

---

一个 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 技能/插件和 Codex 插件，让智能体像原始人一样说话——在保持完全技术准确性的同时，减少 **约 75% 的输出 token**。现在支持 [文言文模式](#文言文-wenyan-mode)、[简洁提交](#caveman-commit)、[单行代码审查](#caveman-review)，以及一个每会话可减少 **约 46% 输入 token** 的[压缩工具](#caveman-compress)。

基于一个广为流传的观察：原始人语言能显著减少 LLM 的 token 使用量，且不丢失技术内容。所以我们将其改为一行安装。

## 使用前后对比

<table>
<tr>
<td width="50%">

### 🗣️ 普通 Claude (69 tokens)

> "The reason your React component is re-rendering is likely because you're creating a new object reference on each render cycle. When you pass an inline object as a prop, React's shallow comparison sees it as a different object every time, which triggers a re-render. I'd recommend using useMemo to memoize the object."

</td>
<td width="50%">

### 🪨 原始人 Claude (19 tokens)

> "New object ref each render. Inline object prop = new ref = re-render. Wrap in `useMemo`."

</td>
</tr>
<tr>
<td>

### 🗣️ 普通 Claude

> "Sure! I'd be happy to help you with that. The issue you're experiencing is most likely caused by your authentication middleware not properly validating the token expiry. Let me take a look and suggest a fix."

</td>
<td>

### 🪨 原始人 Claude

> "Bug in auth middleware. Token expiry check use `<` not `<=`. Fix:"

</td>
</tr>
</table>

**相同的修复。减少 75% 的文字。大脑依然强大。**

**选择你的原始程度：**

<table>
<tr>
<td width="25%">

#### 🪶 轻量级

> "Your component re-renders because you create a new object reference each render. Inline object props fail shallow comparison every time. Wrap it in `useMemo`."

</td>
<td width="25%">

#### 🪨 完整

> "New object ref each render. Inline object prop = new ref = re-render. Wrap in `useMemo`."

</td>
<td width="25%">

#### 🔥 极限

> "Inline obj prop → new ref → re-render. `useMemo`."

</td>
<td width="25%">

#### 📜 文言文

> "物出新參照，致重繪。useMemo Wrap之。"

</td>
</tr>
</table>

**相同的答案。你决定说多少字。**

```
┌─────────────────────────────────────┐
│  节省 TOKEN          ████████ 75% │
│  技术准确性          ████████ 100%│
│  速度提升            ████████ ~3x │
│  氛围                ████████ OOG │
└─────────────────────────────────────┘
```

- **更快响应** — 需要生成的 token 更少 = 速度起飞
- **更易阅读** — 没有文字墙，只有答案
- **相同准确性** — 保留所有技术信息，只删除废话（[科学证明如此](https://arxiv.org/abs/2604.00025)）
- **省钱** — ~71% 更少的输出 token = 更低成本
- **有趣** — 每次代码审查都变成喜剧

## 安装

选择你的智能体。一条命令。完成。

| 智能体 | 安装 |
|-------|---------|
| **Claude Code** | `claude plugin marketplace add JuliusBrussee/caveman && claude plugin install caveman@caveman` |
| **Codex** | 克隆仓库 → `/plugins` → 搜索 "Caveman" → 安装 |
| **Gemini CLI** | `gemini extensions install https://github.com/JuliusBrussee/caveman` |
| **Cursor** | `npx skills add JuliusBrussee/caveman -a cursor` |
| **Windsurf** | `npx skills add JuliusBrussee/caveman -a windsurf` |
| **Copilot** | `npx skills add JuliusBrussee/caveman -a github-copilot` |
| **Cline** | `npx skills add JuliusBrussee/caveman -a cline` |
| **其他** | `npx skills add JuliusBrussee/caveman` |

安装一次。之后在该安装目标的每个会话中使用。一块石头。就这样。

### 你将获得

Claude Code、Gemini CLI 和下方的仓库本地 Codex 设置内置了自动激活功能。`npx skills add` 为其他智能体安装技能，但**不会**安装仓库规则/指令文件，因此除非你添加下面的常驻片段，否则 Caveman 不会在那里自动启动。

| 功能 | Claude Code | Codex | Gemini CLI | Cursor | Windsurf | Cline | Copilot |
|---------|:-----------:|:-----:|:----------:|:------:|:--------:|:-----:|:-------:|
| Caveman 模式 | Y | Y | Y | Y | Y | Y | Y |
| 每会话自动激活 | Y | Y¹ | Y | —² | —² | —² | —² |
| `/caveman` 命令 | Y | Y¹ | Y | — | — | — | — |
| 模式切换（lite/full/ultra） | Y | Y¹ | Y | Y³ | Y³ | — | — |
| 状态栏徽章 | Y⁴ | — | — | — | — | — | — |
| caveman-commit | Y | — | Y | Y | Y | Y | Y |
| caveman-review | Y | — | Y | Y | Y | Y | Y |
| caveman-compress | Y | Y | Y | Y | Y | Y | Y |
| caveman-help | Y | — | Y | Y | Y | Y | Y |

> [!NOTE]
> 自动激活在不同智能体中的工作方式不同：Claude Code 使用 SessionStart hooks，此仓库的 Codex 自用设置使用 `.codex/hooks.json`，Gemini 使用上下文文件。Cursor/Windsurf/Cline/Copilot 可以设置为常驻，但 `npx skills add` 仅安装技能，不安装仓库规则/指令文件。
>
> ¹ Codex 使用 `$caveman` 语法，而不是 `/caveman`。此仓库附带 `.codex/hooks.json`，因此在此仓库内运行 Codex 时 caveman 会自动启动。已安装的插件本身提供 `$caveman`；如果你想在其他仓库中也实现常驻行为，请将相同的 hook 复制到那里。caveman-commit 和 caveman-review 不在 Codex 插件包中 — 直接使用 SKILL.md 文件。
> ² 如果需要会话开始时激活，请将下面的"想要常驻？"片段添加到这些智能体的系统提示词或规则文件中。
> ³ Cursor 和 Windsurf 接收包含所有强度级别的完整 SKILL.md。模式切换通过技能按需工作；没有斜杠命令。
> ⁴ 在 Claude Code 中可用，但插件安装仅提示设置。当没有自定义 `statusLine` 时，独立的 `install.sh` / `install.ps1` 会自动配置它。

<details>
<summary><strong>Claude Code — 完整详情</strong></summary>

插件安装为你提供技能 + 自动加载 hooks。如果没有配置自定义 `statusLine`，Caveman 会提示 Claude 在首次会话时提供徽章设置。

```bash
claude plugin marketplace add JuliusBrussee/caveman
claude plugin install caveman@caveman
```

**独立 hooks（不使用插件）：** 如果你不想使用插件系统：
```bash
# macOS / Linux / WSL
bash <(curl -s https://raw.githubusercontent.com/JuliusBrussee/caveman/main/hooks/install.sh)

# Windows (PowerShell)
irm https://raw.githubusercontent.com/JuliusBrussee/caveman/main/hooks/install.ps1 | iex
```

或者从本地克隆：`bash hooks/install.sh` / `powershell -File hooks\install.ps1`

卸载：`bash hooks/uninstall.sh` 或 `powershell -File hooks\uninstall.ps1`

**状态栏徽章：** 在你的 Claude Code 状态栏中显示 `[CAVEMAN]`、`[CAVEMAN:ULTRA]` 等。

- **插件安装：** 如果你还没有自定义 `statusLine`，Claude 应该会在首次会话时提供配置选项
- **独立安装：** 除非你已有自定义状态栏，否则由 `install.sh` / `install.ps1` 自动配置
- **自定义状态栏：** 安装程序会保留你现有的状态栏。查看 [`hooks/README.md`](https://github.com/JuliusBrussee/caveman/blob/main/hooks/README.md) 获取合并片段

</details>

<details>
<summary><strong>Codex — 完整详情</strong></summary>

**macOS / Linux:**
1. 克隆仓库 → 在仓库目录中打开 Codex → `/plugins` → 搜索 "Caveman" → 安装
2. 仓库本地自动启动已通过 `.codex/hooks.json` + `.codex/config.toml` 配置

**Windows:**
1. 首先启用符号链接：`git config --global core.symlinks true`（需要开发者模式或管理员权限）
2. 克隆仓库 → 打开 VS Code → Codex 设置 → 插件 → 在本地市场下找到 "Caveman" → 安装 → 重新加载窗口
3. Codex hooks 目前在 Windows 上被禁用，因此使用 `$caveman` 手动启动

此仓库还附带 `.codex/hooks.json` 并在 `.codex/config.toml` 中启用 hooks，因此在 macOS/Linux 上在此仓库内运行 Codex 时 caveman 会自动激活。已安装的插件为你提供 `$caveman`；如果你想在其他仓库中也实现常驻行为，请将相同的 `SessionStart` hook 复制到那里并启用：

```toml
[features]
codex_hooks = true
```

</details>

<details>
<summary><strong>Gemini CLI — 完整详情</strong></summary>

```bash
gemini extensions install https://github.com/JuliusBrussee/caveman
```

更新：`gemini extensions update caveman` · 卸载：`gemini extensions uninstall caveman`

通过 `GEMINI.md` 上下文文件自动激活。还附带自定义 Gemini 命令：
- `/caveman` — 切换强度级别（lite/full/ultra/wenyan）
- `/caveman-commit` — 生成简洁的提交消息
- `/caveman-review` — 单行代码审查

</details>

<details>
<summary><strong>Cursor / Windsurf / Cline / Copilot — 完整详情</strong></summary>

`npx skills add` 仅安装技能文件 — 它**不会**安装智能体的规则/指令文件，因此 caveman 不会自动启动。要实现常驻，请将下面的"想要常驻？"片段添加到你的智能体规则或系统提示词中。

| 智能体 | 命令 | 未安装文件 | 模式切换 | 常驻位置 |
|-------|---------|--------------|:--------------:|--------------------|
| Cursor | `npx skills add JuliusBrussee/caveman -a cursor` | `.cursor/rules/caveman.mdc` | Y | Cursor 规则 |
| Windsurf | `npx skills add JuliusBrussee/caveman -a windsurf` | `.windsurf/rules/caveman.md` | Y | Windsurf 规则 |
| Cline | `npx skills add JuliusBrussee/caveman -a cline` | `.clinerules/caveman.md` | — | Cline 规则或系统提示词 |
| Copilot | `npx skills add JuliusBrussee/caveman -a github-copilot` | `.github/copilot-instructions.md` + `AGENTS.md` | — | Copilot 自定义指令 |

卸载：`npx skills remove caveman`

Copilot 适用于聊天、编辑和编码智能体。

</details>

<details>
<summary><strong>其他智能体（opencode、Roo、Amp、Goose、Kiro 等 40+ 个）</strong></summary>

[npx skills](https://github.com/vercel-labs/skills) 支持 40+ 个智能体：

```bash
npx skills add JuliusBrussee/caveman           # 自动检测智能体
npx skills add JuliusBrussee/caveman -a amp
npx skills add JuliusBrussee/caveman -a augment
npx skills add JuliusBrussee/caveman -a goose
npx skills add JuliusBrussee/caveman -a kiro-cli
npx skills add JuliusBrussee/caveman -a roo
# ... 以及更多
```

卸载：`npx skills remove caveman`

> **Windows 注意：** `npx skills` 默认使用符号链接。如果符号链接失败，添加 `--copy`：`npx skills add JuliusBrussee/caveman --copy`

**重要：** 这些智能体没有 hook 系统，因此 caveman 不会自动启动。说 `/caveman` 或 "talk like caveman" 来激活每个会话。

**想要常驻？** 将此内容粘贴到你的智能体系统提示词或规则文件中 — caveman 将从第一条消息开始激活，每个会话：

```
Terse like caveman. Technical substance exact. Only fluff die.
Drop: articles, filler (just/really/basically), pleasantries, hedging.
Fragments OK. Short synonyms. Code unchanged.
Pattern: [thing] [action] [reason]. [next step].
ACTIVE EVERY RESPONSE. No revert after many turns. No filler drift.
Code/commits/PRs: normal. Off: "stop caveman" / "normal mode".
```

放置位置：
| 智能体 | 文件 |
|-------|------|
| opencode | `.config/opencode/AGENTS.md` |
| Roo | `.roo/rules/caveman.md` |
| Amp | 你的工作区系统提示词 |
| 其他 | 你的智能体系统提示词或规则文件 |

</details>

## 使用方法

通过以下方式触发：
- `/caveman` 或 Codex `$caveman`
- "talk like caveman"
- "caveman mode"
- "less tokens please"

通过以下方式停止："stop caveman" 或 "normal mode"

### 强度级别

| 级别 | 触发方式 | 作用 |
|-------|---------|------------|
| **Lite** | `/caveman lite` | 删除填充词，保留语法。专业但无废话 |
| **Full** | `/caveman full` | 默认 caveman。删除冠词，使用片段，完全原始 |
| **Ultra** | `/caveman ultra` | 最大压缩。电报式。缩写一切 |

### 文言文 (Wenyan) 模式

古典中文文学压缩 — 相同的技术准确性，但使用人类发明的最 token 高效的书面语言。

| 级别 | 触发方式 | 作用 |
|-------|---------|------------|
| **Wenyan-Lite** | `/caveman wenyan-lite` | 半文言。语法完整，填充词消失 |
| **Wenyan-Full** | `/caveman wenyan` | 完整文言文。最大古典简洁性 |
| **Wenyan-Ultra** | `/caveman wenyan-ultra` | 极端。预算有限的古代学者 |

级别保持不变，直到你更改或会话结束。

## Caveman 技能

### caveman-commit

`/caveman-commit` — 简洁的提交消息。Conventional Commits。≤50 字符的主题。原因重于内容。

### caveman-review

`/caveman-review` — 单行 PR 评论：`L42: 🔴 bug: user null. Add guard.` 没有废话。

### caveman-help

`/caveman-help` — 快速参考卡。所有模式、技能、命令，一个命令即可获取。

### caveman-compress

`/caveman:compress <filepath>` — caveman 让 Claude *说话*时使用更少的 token。**Compress** 让 Claude *阅读*时使用更少的 token。

你的 `CLAUDE.md` 在**每次会话开始时**加载。Caveman Compress 将记忆文件重写为 caveman 语言，使 Claude 阅读更少的内容 — 而你不会丢失人类可读的原始文件。

```
/caveman:compress CLAUDE.md
```

```
CLAUDE.md          ← 压缩版（Claude 每次会话都读取此文件 — 更少的 token）
CLAUDE.original.md ← 人类可读备份（你阅读和编辑此文件）
```

| 文件 | 原始 | 压缩 | 节省 |
|------|----------:|----------:|------:|
| `claude-md-preferences.md` | 706 | 285 | **59.6%** |
| `project-notes.md` | 1145 | 535 | **53.3%** |
| `claude-md-project.md` | 1122 | 636 | **43.3%** |
| `todo-list.md` | 627 | 388 | **38.1%** |
| `mixed-with-code.md` | 888 | 560 | **36.9%** |
| **平均** | **898** | **481** | **46%** |

代码块、URL、文件路径、命令、标题、日期、版本号 — 任何技术内容都保持不变。只有散文会被压缩。查看完整的 [caveman-compress README](https://github.com/JuliusBrussee/caveman/blob/main/caveman-compress/README.md) 了解详情。[安全说明](https://github.com/JuliusBrussee/caveman/blob/main/caveman-compress/SECURITY.md)：Snyk 由于子进程/文件模式将其标记为高风险 — 这是误报。

## 基准测试

来自 Claude API 的真实 token 计数（[自行复现](https://github.com/JuliusBrussee/caveman/tree/main/benchmarks)）：

<!-- BENCHMARK-TABLE-START -->
| 任务 | 普通 (tokens) | Caveman (tokens) | 节省 |
|------|---------------:|----------------:|------:|
| 解释 React 重渲染 bug | 1180 | 159 | 87% |
| 修复认证中间件 token 过期 | 704 | 121 | 83% |
| 设置 PostgreSQL 连接池 | 2347 | 380 | 84% |
| 解释 git rebase vs merge | 702 | 292 | 58% |
| 重构 callback 为 async/await | 387 | 301 | 22% |
| 架构：微服务 vs 单体 | 446 | 310 | 30% |
| 审查 PR 安全问题 | 678 | 398 | 41% |
| Docker 多阶段构建 | 1042 | 290 | 72% |
| 调试 PostgreSQL 竞态条件 | 1200 | 232 | 81% |
| 实现 React 错误边界 | 3454 | 456 | 87% |
| **平均** | **1214** | **294** | **65%** |

*范围：跨提示词节省 22%–87%。*
<!-- BENCHMARK-TABLE-END -->

> [!IMPORTANT]
> Caveman 只影响输出 token — 思考/推理 token 保持不变。Caveman 不会让大脑变小。Caveman 让*嘴巴*变小。最大的收益是**可读性和速度**，成本节省是额外的奖励。

2026 年 3 月的一篇论文["简洁性约束逆转语言模型的性能层次"](https://arxiv.org/abs/2604.00025)发现，将大型模型约束为简洁响应在某些基准测试上**将准确性提高了 26 个百分点**，并完全逆转了性能层次。冗长并不总是更好。有时更少的文字 = 更正确。

## 评估

Caveman 不只是声称 75%。Caveman **证明**它。

`evals/` 目录有一个三臂评估框架，可以测量相对于适当控制的真实 token 压缩 — 不仅是"冗长 vs 技能"，而是"简洁 vs 技能"。因为将 caveman 与冗长的 Claude 进行比较会混淆技能与通用简洁性。那是作弊。Caveman 不作弊。

```bash
# 运行评估（需要 claude CLI）
uv run python evals/llm_run.py

# 读取结果（无需 API 密钥，离线运行）
uv run --with tiktoken python evals/measure.py
```

## 给此仓库点星

如果 caveman 为你节省了大量 token、大量金钱 — 请留下大量星星。⭐

[![Star History Chart](https://api.star-history.com/svg?repos=JuliusBrussee/caveman&type=Date)](https://star-history.com/#JuliusBrussee/caveman&Date)

## Julius Brussee 的其他作品

- **[Cavekit](https://github.com/JuliusBrussee/cavekit)** — Claude Code 的规范驱动开发。Caveman 语言 → 规范 → 并行构建 → 可运行的软件。
- **[Revu](https://github.com/JuliusBrussee/revu-swift)** — 本地优先的 macOS 学习应用，具有 FSRS 间隔重复、卡片组、考试和学习指南。[revu.cards](https://revu.cards)

## 许可证

MIT — 像开阔平原上的大量猛犸象一样自由。
