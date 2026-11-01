# Skills：聚焦分析与质询

两个帮助理解复杂问题的 Codex Skill：先用「聚焦分析」看清关键关系，再用「质询」检验自己是否理解。两者可以独立使用，也可以在同一段讨论中前后衔接。

## 包含什么

| Skill | 解决的问题 | 使用方式 |
| --- | --- | --- |
| [聚焦分析](skills/focused-analysis/SKILL.md) | 复杂回答信息太散，看不清核心关系、依据和必要前提。 | 显式调用 `$focused-analysis`。 |
| [质询](skills/inquiry/SKILL.md) | 看过回答，但不确定自己是否抓住主干、能否应对实际追问。 | 调用 `$inquiry`，或明确要求检验理解。 |

### 聚焦分析

围绕当前问题的关键关系深入解释，先建立骨架，再展开必要的推导。保留影响判断的证据、前提和不确定性，减少无关分支；不以省略关键逻辑来换取简短。

该 Skill 仅在明确调用时启用，保留了 `allow_implicit_invocation: false` 配置。

### 质询

默认检验主干：每次只问一个关键问题，等待用户独立回答，再根据具体回答判断是理解正确、不完整、错误，还是表达需要澄清。针对偏差解释后，换个角度复测。

主干掌握后，先询问用户是否开启场景检验；用户选择后，再模拟评审、汇报、答辩或实际应用中的追问。

发现适合动态展示的理解偏差时，可在用户选择后生成独立 HTML 文件。页面可离线打开和复用，保留相关材料摘录、原始问答、诊断与纠正依据、模型假设和复测状态，方便追溯。

## 安装

在 Codex 中使用内置安装 Skill：

```text
使用 $skill-installer，从 https://github.com/gitsirfhsakjhfaks/skills 安装 skills/focused-analysis 和 skills/inquiry 这两个 Skill。
```

也可以下载本仓库，将 `skills/` 中的两个完整目录复制到用户级的 `~/.agents/skills/`，或目标项目的 `.agents/skills/`。保留各目录中的 `agents/` 和 `references/`。这些是官方文档列出的本地 Skill 发现位置；安装后未出现时可重启 Codex。[官方安装与发现说明](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills)

## 使用示例

先分析一个问题：

```text
使用 $focused-analysis，帮我理解下面这个方案的核心机制、关键依据和成立条件：
（粘贴方案或明确指向当前上下文）
```

需要检查理解时，再调用质询：

```text
使用 $inquiry，检验我对上面这段回答的主干理解。一次问一个问题，等我回答后再评价。
```

已经掌握主干、希望模拟评审时：

```text
继续开启场景检验，模拟方案评审，检查我能否解释这个方案的依据、取舍和适用条件。
```

## 目录

```text
skills/
├── focused-analysis/
│   ├── SKILL.md
│   └── agents/openai.yaml
└── inquiry/
    ├── SKILL.md
    ├── agents/openai.yaml
    └── references/html-remediation.md
```

两个 Skill 均以指令为主，不需要额外安装脚本依赖。质询中的 HTML 辅助环节需要运行环境能够创建文件；具备浏览器能力时，应进一步验证保存后的交互页面。
